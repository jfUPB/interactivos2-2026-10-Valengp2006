# Unidad 2

## Bitácora de proceso de aprendizaje

### Actividad 01: 03-02-2026

<img width="1350" height="797" alt="Captura de pantalla 2026-02-03 a la(s) 9 35 34 a m" src="https://github.com/user-attachments/assets/4a42f784-7873-470b-8da0-29c75e56b232" />
<img width="1350" height="791" alt="Captura de pantalla 2026-02-03 a la(s) 9 35 46 a m" src="https://github.com/user-attachments/assets/fc29847d-d447-43c5-bd58-53f460db3e59" />
<img width="1345" height="780" alt="Captura de pantalla 2026-02-03 a la(s) 9 36 06 a m" src="https://github.com/user-attachments/assets/f6babe9f-bb8e-4338-b73b-acbf67c12821" />
<img width="1350" height="764" alt="Captura de pantalla 2026-02-03 a la(s) 9 41 28 a m" src="https://github.com/user-attachments/assets/a7cdce4f-77cd-4389-8ae7-a21ea2e311ce" />

### Actividad 02: 

#### Aspectos clave de la sincronización:

1. **Comunicación OSC via WebSocket**
```javascript
const socket = new WebSocket('ws://localhost:8081');
```
- El puente OSC (OSC Bridge) recibe mensajes de Strudel en el puerto 8081
- Los mensajes incluyen información sobre qué sonido se reproduce y cuándo

2. **Sistema de Cola de Eventos (Event Queue)**
```javascript
let eventQueue = [];
```
- Los eventos OSC se almacenan con su **timestamp** exacto
- Se ordenan cronológicamente: `eventQueue.sort((a, b) => a.timestamp - b.timestamp)`
- Esto permite reproducir los eventos visuales en el momento preciso

3. **Sincronización Temporal**
```javascript
let now = Date.now() + LATENCY_CORRECTION;
while (eventQueue.length > 0 && now >= eventQueue[0].timestamp) {
```
- Compara el tiempo actual con el timestamp de cada evento
- Ejecuta las animaciones cuando llega su momento exacto
- Incluye corrección de latencia ajustable

4. **Duración Rítmica (Delta)**
```javascript
duration: ev.delta * 1000, // Convertimos delta a milisegundos
```
- Cada evento tiene un parámetro `delta` que define su duración
- Las animaciones duran exactamente lo que dura el sonido

5. **Mapeo Sonido → Visual**
```javascript
function getColorForSound(s) {
  const colors = {
    'tr909bd': [255, 0, 80],    // Bombo → Rosa/Rojo
    'tr909sd': [0, 200, 255],   // Caja → Azul
    'tr909hh': [255, 255, 0],   // Hi-hat → Amarillo
    'tr909oh': [255, 150, 0]    // Open hat → Naranja
  };
}
```

6. **Progreso de Animación**
```javascript
let progress = elapsed / anim.duration; // 0.0 → 1.0
```
- Calcula qué tan avanzada está cada animación
- Se usa para interpolar tamaño, opacidad, rotación, etc.

### Actividad 03:

<img width="578" height="380" alt="Captura de pantalla 2026-02-08 a la(s) 9 46 29 p m" src="https://github.com/user-attachments/assets/ae9e907a-e44d-4708-9512-096913bf9e13" />
<img width="578" height="378" alt="Captura de pantalla 2026-02-08 a la(s) 9 46 36 p m" src="https://github.com/user-attachments/assets/efd4d16e-514d-4772-b21b-b010b3f00708" />
![Grabación-de-pantalla-2026-02-08-a-la_s_-9 48 40 p m](https://github.com/user-attachments/assets/e83b981b-ada8-4b9c-a3b7-e0914cbbcc2c)

## Bitácora de aplicación 

### Actividad 04: 10/02/2026

#### Pieza de Audio Original:

##### Código Strudel:
```javascript
setcps(0.7);

// P1: Melodía sintética con distorsión
p1: n("0 2 4 6 7 6 4 2")
  .scale("<c3:major>")
  .distort(0.9)
  .superimpose((x) => x.detune("<0.5>"))
  .lpenv(perlin.slow(3).range(1, 4))
  .lpf(perlin.slow(2).range(100, 2000))
  .gain(0.3);

// P2: Bajo agresivo con clip
p2: "<a1>/8".clip(0.8).struct("x*8").note();

// P3: Piano melódico
p3: n("0@3 2 4 <[6,8] [7,9]>")
  .scale("C:minor")
  .sound("piano")

// P4: Patrón rítmico de percusión
p4: sound("[bd*4,~ rim ~ cp]*<1 [2 4]>")
```
Esta pieza combina cuatro capas sonoras:

1. **Melodía principal** (p1): Un sintetizador con distorsión pesada y filtro automático
2. **Bajo rítmico** (p2): Notas graves con clipping para textura agresiva
3. **Armonía de piano** (p3): Acordes menores que aportan melancolía
4. **Percusión** (p4): Patrón de bombo, rim y clap con variaciones rítmicas

#### Implementación de Visuales Reactivas

##### 1. Configuración del Sistema de Sincronización

**Sistema de Cola de Eventos:**

```javascript
let eventQueue = [];
let activeAnimations = [];
const LATENCY_CORRECTION = 0;
```

**Función**: 

- `eventQueue`: Almacena los eventos OSC ordenados cronológicamente
- `activeAnimations`: Contiene las animaciones actualmente dibujándose
- `LATENCY_CORRECTION`: Permite ajustar la sincronización si hay desfase

**Conexión WebSocket**

```javascript
const socket = new WebSocket('ws://localhost:8081');

socket.onmessage = (event) => {
    const msg = JSON.parse(event.data);
    let params = {};
    
    for (let i = 0; i < msg.args.length; i += 2) {
        params[msg.args[i]] = msg.args[i+1];
    }
    
    eventQueue.push({ 
      timestamp: msg.timestamp, 
      sound: params.s,
      note: params.note || params.n || 0,
      delta: params.delta || 0.25,
      gain: params.gain || 0.5,
      params: params 
    });

    eventQueue.sort((a, b) => a.timestamp - b.timestamp);
};
```

**Cómo funciona la sincronización**:

1. Strudel envía mensajes OSC con datos de cada evento de audio
2. Los mensajes incluyen: `timestamp` (cuándo debe sonar), `sound` (qué sonido), `note`, `delta` (duración)
3. Los eventos se ordenan por timestamp para reproducirse en orden cronológico

##### 2. Mapeo Audio → Visual

| Sonido (Strudel) | Tipo Visual | Características |
|------------------|-------------|-----------------|
| `sawtooth` (p1) | Ondas vibrantes | Posición vertical según nota, vibración por distorsión |
| `clip` (p2) | Fragmentos explosivos | 8 fragmentos que rotan desde el centro |
| `piano` (p3) | Teclas que caen | Rebote 3 veces, altura según nota musical |
| `bd` | Pulso central | Círculo que expande desde el centro |
| `rim` | Destellos verticales | Líneas en bordes superior/inferior |
| `cp` | Ondas de choque | 4 ondas concéntricas escalonadas |

##### 3. Funciones Visuales Específicas

**P1 - Synth con Distorsión:**

```javascript
function dibujarSawtoothDistort(anim, p, c) {
    // Posición basada en la nota (más agudo = más arriba)
    let yPos = map(anim.note, 0, 12, height * 0.7, height * 0.3);
    let xPos = width / 2;
    
    // Efecto de distorsión: el tamaño vibra
    let distortion = sin(p * TWO_PI * 8) * 10;
    let size = lerp(150, 50, p) + distortion;
    
    let alpha = lerp(200, 0, p);
    
    noFill();
    stroke(c[0], c[1], c[2], alpha);
    strokeWeight(3);
    
    // Múltiples círculos concéntricos (efecto superimpose/detune)
    for (let i = 0; i < 3; i++) {
      let offset = i * 15;
      circle(xPos + offset, yPos, size + offset);
    }
}
```
**Sincronización implementada**:

- La altura de la nota musical (`anim.note`) controla la posición vertical
- La vibración simula el efecto de distorsión del audio
- Los 3 círculos representan el `superimpose` con `detune`

**P3 - Piano Melódico:**

```javascript
function dibujarPiano(anim, p, c) {
    // Altura basada en la nota musical
    let noteHeight = map(anim.note, 0, 12, height * 0.8, height * 0.2);
    
    // Animación de "caída" y rebote
    let bounce = abs(sin(p * PI * 3)) * 20;
    let yPos = noteHeight + bounce;
    
    // Tamaño basado en el gain
    let size = anim.gain * 150;
    let currentSize = lerp(size, size * 0.3, p);
    let alpha = lerp(220, 0, p);
    
    fill(c[0], c[1], c[2], alpha);
    
    // Forma de tecla de piano
    rectMode(CORNER);
    rect(anim.x - currentSize/2, yPos, currentSize, currentSize * 0.3, 5);
    rectMode(CENTER);
    
    // Onda de sonido expandiéndose
    noFill();
    stroke(c[0], c[1], c[2], alpha * 0.5);
    strokeWeight(2);
    let waveSize = lerp(0, 300, p);
    circle(anim.x, yPos, waveSize);
}
```

**Sincronización implementada**:

- `noteHeight`: La nota musical determina la altura
- `bounce`: Rebote 3 veces durante la duración del sonido
- `size`: El volumen (`gain`) afecta el tamaño inicial
- `waveSize`: Onda que se expande durante el `delta`

##### 4. Sistema de Colores Dinámico

```javascript
function getColorForSound(s, note = 0) {
    const colors = {
      // P1: Synth - Colores cálidos que varían con la nota
      'sawtooth': [255 - note * 10, 100 + note * 5, 180],
      
      // P2: Clip - Rojo agresivo
      'clip': [255, 50, 50],
      
      // P3: Piano - Azul/Púrpura melódico que varía con la nota
      'piano': [100 + note * 12, 150, 255 - note * 8],
      
      // P4: Percusión
      'bd': [255, 0, 80],      // Bombo - Rosa fuerte
      'rim': [0, 255, 200],    // Rim - Cyan
      'cp': [255, 200, 0]      // Clap - Amarillo
    };

    if (colors[s]) return colors[s];

    // Fallback para sonidos no mapeados
    let charCode = s.charCodeAt(0) || 0;
    let r = (charCode * 123) % 255;
    let g = (charCode * 456) % 255;
    let b = (charCode * 789) % 255;
    return [r, g, b];
}
```

**Variación cromática por nota**: 

- Los sintetizadores (sawtooth, piano) cambian de color según la altura de la nota
- Notas más agudas → colores más brillantes
- Notas más graves → colores más oscuros

#### Proceso de Mejora

**Primero: Visuales básicas**

- Implementé formas simples (círculos) para cada sonido
- Problema: Todas las capas se veían similares, difícil distinguir

**Segundo: Diferenciación por tipo**

- Creé formas únicas para cada instrumento
- Bombo = pulso central
- Piano = teclas que caen
- Resultado: Mucho más legible visualmente

**Tercero: Sincronización con parámetros musicales**

- Agregué mapeo de notas a posiciones
- Incorporé el `gain` al tamaño de elementos
- Resultado: Las visuales "cantan" con la música

**Cuarto: Efectos avanzados**

- Vibración para simular distorsión
- Rebotes para elementos percusivos
- Ondas concéntricas para resonancia

#### Aspectos Técnicos de la Sincronización

**Timing Preciso**

```javascript
let now = Date.now() + LATENCY_CORRECTION;

while (eventQueue.length > 0 && now >= eventQueue[0].timestamp) {
    let ev = eventQueue.shift();
    // Crear animación exactamente cuando debe sonar
}
```

**Progreso de Animación**

```javascript
let elapsed = now - anim.startTime;
let progress = elapsed / anim.duration; // 0.0 → 1.0

if (progress <= 1.0) {
    dibujarElemento(anim, progress);
} else {
    activeAnimations.splice(i, 1); // Eliminar cuando termina
}
```

**El parámetro `progress`**:
- 0.0 = inicio de la nota
- 0.5 = mitad de la duración
- 1.0 = final de la nota
- Se usa para interpolar tamaño, opacidad, posición

#### Resultados

- Sincronización precisa entre audio y visuales
- Identidad visual única para cada capa
- Parámetros musicales (nota, gain) afectan las visuales
- Animaciones que respetan la duración (`delta`) de cada sonido  

#### Capturas de Pantalla



#### Código Completo

##### Archivo HTML (visuales_reactivas.html)

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Visuales Reactivas - Pieza de Audio Interactivo</title>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.11/lib/p5.min.js"></script>
  <style> 
    body { 
      margin: 0; 
      overflow: hidden; 
      background: black; 
    } 
  </style>
</head>
<body>

<script>
  let eventQueue = [];
  let activeAnimations = [];
  const LATENCY_CORRECTION = 0;

  function setup() {
    createCanvas(windowWidth, windowHeight);
    rectMode(CENTER);
    noStroke();

    const socket = new WebSocket('ws://localhost:8081');

    socket.onopen = () => {
      console.log('✅ WebSocket conectado');
    };

    socket.onerror = (error) => {
      console.error('❌ Error WebSocket:', error);
    };

    socket.onmessage = (event) => {
        const msg = JSON.parse(event.data);
        
        let params = {};
        
        // Parsear argumentos OSC
        for (let i = 0; i < msg.args.length; i += 2) {
            params[msg.args[i]] = msg.args[i+1];
        }
        
        // Log simplificado
        console.log('🎵', params.s || 'unknown', '| note:', params.n || params.note);
        
        // Crear evento
        eventQueue.push({ 
          timestamp: msg.timestamp, 
          sound: params.s || 'unknown',
          note: params.note || params.n || 0,
          delta: params.delta || 0.25,
          gain: params.gain || 0.5,
          params: params 
        });

        eventQueue.sort((a, b) => a.timestamp - b.timestamp);
    };
  }

  function draw() {
    background(0, 40); // Trail suave

    let now = Date.now() + LATENCY_CORRECTION;

    // Procesar eventos
    while (eventQueue.length > 0 && now >= eventQueue[0].timestamp) {
        let ev = eventQueue.shift();

        activeAnimations.push({
          startTime: ev.timestamp,
          duration: ev.delta * 1000,
          type: ev.sound,
          note: ev.note,
          gain: ev.gain,
          x: random(width * 0.2, width * 0.8), 
          y: random(height * 0.2, height * 0.8),
          color: getColorForSound(ev.sound, ev.note)
        });
    }
    
    // Dibujar animaciones
    for (let i = activeAnimations.length - 1; i >= 0; i--) {
      let anim = activeAnimations[i];
      let elapsed = now - anim.startTime;
      let progress = elapsed / anim.duration;

      if (progress <= 1.0) {
        dibujarElemento(anim, progress);
      } else {
        activeAnimations.splice(i, 1);
      }
    }
  }

  function dibujarElemento(anim, p) {
    push();
    const color = anim.color;
    
    // Mapear sonidos específicos
    switch (anim.type) {
      case 'sawtooth':
        dibujarSawtoothDistort(anim, p, color);
        break;

      case 'square':
      case 'clip':
        dibujarClip(anim, p, color);
        break;

      case 'piano':
        dibujarPiano(anim, p, color);
        break;

      case 'bd':
      case '909bd':
        dibujarBombo(p, color);
        break;

      case 'rim':
      case '909rim':
        dibujarRim(anim, p, color);
        break;

      case 'cp':
      case '909cp':
        dibujarClap(anim, p, color);
        break;

      case 'hh':
      case '909hh':
        dibujarHat(anim, p, color);
        break;

      case 'sd':
      case '909sd':
        dibujarCaja(p, color);
        break;

      default:
        dibujarDefault(anim, p, color);
        break;
    }
    pop();
  }

  // ========================================
  // FUNCIONES VISUALES ESPECÍFICAS
  // ========================================

  function dibujarSawtoothDistort(anim, p, c) {
    let yPos = map(anim.note, 0, 12, height * 0.7, height * 0.3);
    let xPos = width / 2;
    
    // Vibración por distorsión
    let distortion = sin(p * TWO_PI * 8) * 10;
    let size = lerp(150, 50, p) + distortion;
    let alpha = lerp(200, 0, p);
    
    noFill();
    stroke(c[0], c[1], c[2], alpha);
    strokeWeight(3);
    
    // Múltiples círculos (superimpose)
    for (let i = 0; i < 3; i++) {
      let offset = i * 15;
      circle(xPos + offset, yPos, size + offset);
    }
  }

  function dibujarClip(anim, p, c) {
    let alpha = lerp(255, 0, p);
    fill(c[0], c[1], c[2], alpha);
    
    // Fragmentos que explotan
    let fragments = 8;
    for (let i = 0; i < fragments; i++) {
      let angle = (TWO_PI / fragments) * i;
      let distance = lerp(0, 200, p);
      let x = width / 2 + cos(angle) * distance;
      let y = height / 2 + sin(angle) * distance;
      let size = lerp(30, 5, p);
      
      push();
      translate(x, y);
      rotate(angle + p * PI);
      rect(0, 0, size, size * 2);
      pop();
    }
  }

  function dibujarPiano(anim, p, c) {
    let noteHeight = map(anim.note, 0, 12, height * 0.8, height * 0.2);
    let bounce = abs(sin(p * PI * 3)) * 20;
    let yPos = noteHeight + bounce;
    
    let size = anim.gain * 150;
    let currentSize = lerp(size, size * 0.3, p);
    let alpha = lerp(220, 0, p);
    
    fill(c[0], c[1], c[2], alpha);
    
    // Tecla de piano
    rectMode(CORNER);
    rect(anim.x - currentSize/2, yPos, currentSize, currentSize * 0.3, 5);
    rectMode(CENTER);
    
    // Onda expandiéndose
    noFill();
    stroke(c[0], c[1], c[2], alpha * 0.5);
    strokeWeight(2);
    let waveSize = lerp(0, 300, p);
    circle(anim.x, yPos, waveSize);
  }

  function dibujarBombo(p, c) {
    let d = lerp(100, 700, p);
    let alpha = lerp(255, 0, p);
    
    // Doble círculo
    fill(c[0], c[1], c[2], alpha * 0.3);
    circle(width / 2, height / 2, d * 1.2);
    
    fill(c[0], c[1], c[2], alpha);
    circle(width / 2, height / 2, d);
  }

  function dibujarCaja(p, c) {
    let w = lerp(width, 0, p);
    let alpha = lerp(255, 0, p);
    fill(c[0], c[1], c[2], alpha);
    rect(width / 2, height / 2, w, 50);
  }

  function dibujarRim(anim, p, c) {
    let alpha = lerp(255, 0, p);
    strokeWeight(lerp(10, 2, p));
    stroke(c[0], c[1], c[2], alpha);
    
    let margin = 50;
    let len = lerp(0, 200, p);
    
    // Líneas en bordes
    line(anim.x, margin, anim.x, margin + len);
    line(anim.x, height - margin, anim.x, height - margin - len);
  }

  function dibujarClap(anim, p, c) {
    noFill();
    
    // Ondas concéntricas
    for (let i = 0; i < 4; i++) {
      let delay = i * 0.15;
      let adjustedP = constrain(p - delay, 0, 1);
      
      if (adjustedP > 0) {
        let size = lerp(50, 400, adjustedP);
        let alpha = lerp(200, 0, adjustedP);
        
        stroke(c[0], c[1], c[2], alpha);
        strokeWeight(3);
        circle(anim.x, anim.y, size);
      }
    }
  }

  function dibujarHat(anim, p, c) {
    let sz = lerp(40, 0, p);
    let alpha = lerp(255, 0, p);
    fill(c[0], c[1], c[2], alpha);
    rect(anim.x, anim.y, sz, sz);
  }

  function dibujarDefault(anim, p, c) {
    // Círculo simple para sonidos no mapeados
    let size = lerp(150, 0, p);
    let alpha = lerp(200, 0, p);
    fill(c[0], c[1], c[2], alpha);
    circle(anim.x, anim.y, size);
  }

  // ========================================
  // SISTEMA DE COLORES
  // ========================================

  function getColorForSound(s, note = 0) {
    if (!s) return [150, 150, 150];

    const colors = {
      'sawtooth': [255 - note * 10, 100 + note * 5, 180],
      'square': [255, 50, 50],
      'clip': [255, 50, 50],
      'piano': [100 + note * 12, 150, 255 - note * 8],
      'bd': [255, 0, 80],
      '909bd': [255, 0, 80],
      'sd': [0, 200, 255],
      '909sd': [0, 200, 255],
      'rim': [0, 255, 200],
      '909rim': [0, 255, 200],
      'cp': [255, 200, 0],
      '909cp': [255, 200, 0],
      'hh': [255, 255, 100],
      '909hh': [255, 255, 100],
      'unknown': [150, 100, 150]
    };

    if (colors[s]) return colors[s];

    // Color basado en hash del nombre
    let hash = 0;
    for (let i = 0; i < s.length; i++) {
      hash = s.charCodeAt(i) + ((hash << 5) - hash);
    }
    let r = Math.abs(hash % 255);
    let g = Math.abs((hash * 123) % 255);
    let b = Math.abs((hash * 456) % 255);
    return [r, g, b];
  }

  function windowResized() { 
    resizeCanvas(windowWidth, windowHeight); 
  }

</script>
</body>
</html>
```

##### Archivo Strudel (audio_interactivo.js)
```javascript
setcps(0.7);

p1: n("0 2 4 6 7 6 4 2")
  .scale("<c3:major>")
  .distort(0.9)
  .superimpose((x) => x.detune("<0.5>"))
  .lpenv(perlin.slow(3).range(1, 4))
  .lpf(perlin.slow(2).range(100, 2000))
  .gain(0.3)
  .osc(); 

p2: "<a1>/8".clip(0.8).struct("x*8").note()
  .osc();

p3: n("0@3 2 4 <[6,8] [7,9]>")
  .scale("C:minor")
  .sound("piano")
  .osc();

p4: sound("[bd*4,~ rim ~ cp]*<1 [2 4]>")
  .osc();
```

## Bitácora de reflexión

<img width="877" height="458" alt="Captura de pantalla 2026-02-12 a la(s) 8 37 25 a m" src="https://github.com/user-attachments/assets/fe8d6724-7153-485b-aec9-a6420a3c2404" />

A través del puerto 4321, el servidor envía información a Reepl  (Strudel) para el audio, y a las Visuales (p5.js). Luego, el Node Bridge.js a través del puerto 8080, recibe la información de strudel en websockets, y la envía por el puerto 8081 a las visuales.A través del puerto 4321, el servidor envía información a Reepl  (Strudel) para el audio, y a las Visuales (p5.js). Luego, el Node Bridge.js a través del puerto 8080, recibe la información de strudel en websockets, y la envía por el puerto 8081 a las visuales.








