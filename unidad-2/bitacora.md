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

<img width="578" height="380" alt="Captura de pantalla 2026-02-08 a la(s) 9 46 29 p m" src="https://github.com/user-attachments/assets/ae9e907a-e44d-4708-9512-096913bf9e13" />
<img width="578" height="378" alt="Captura de pantalla 2026-02-08 a la(s) 9 46 36 p m" src="https://github.com/user-attachments/assets/efd4d16e-514d-4772-b21b-b010b3f00708" />

![Grabación-de-pantalla-2026-02-08-a-la_s_-9 48 40 p m](https://github.com/user-attachments/assets/e83b981b-ada8-4b9c-a3b7-e0914cbbcc2c)

#### Código Completo

##### Archivo HTML (visuales_reactivas.html)

```html
<!DOCTYPE html>
<html>
<head>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.11/lib/p5.min.js"></script>
  <style> body { margin: 0; overflow: hidden; background: black; } </style>
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

    socket.onmessage = (event) => {
        const msg = JSON.parse(event.data);
        console.log('Mensaje OSC recibido:', msg);
        
        let params = {};
        for (let i = 0; i < msg.args.length; i += 2) {
            params[msg.args[i]] = msg.args[i+1];
        }
        
        eventQueue.push({ 
          timestamp: msg.timestamp, 
          sound: params.s,
          delta: params.delta || 0.25,
          params: params 
        });

        eventQueue.sort((a, b) => a.timestamp - b.timestamp);
    };
  }

  function draw() {
    background(0, 30); 

    let now = Date.now() + LATENCY_CORRECTION;

    while (eventQueue.length > 0 && now >= eventQueue[0].timestamp) {
        let ev = eventQueue.shift();

        // MODIFICACIÓN: Generamos múltiples partículas por evento
        let particleCount = getParticleCount(ev.sound);
        
        for (let i = 0; i < particleCount; i++) {
          let angle = (TWO_PI / particleCount) * i; // Distribuir en círculo
          
          activeAnimations.push({
            startTime: ev.timestamp,
            duration: ev.delta * 1000,
            type: ev.sound,
            // Posición inicial en el centro
            startX: width / 2,
            startY: height / 2,
            // Dirección de movimiento
            angle: angle,
            speed: getSpeed(ev.sound),
            color: getColorForSound(ev.sound),
            particleIndex: i // Para variaciones
          });
        }
    }
    
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

  // FUNCIÓN: Define cuántas partículas genera cada sonido
  function getParticleCount(sound) {
    const counts = {
      'tr909bd': 8,   // Bombo: 8 partículas
      'tr909sd': 12,  // Caja: 12 partículas
      'tr909hh': 6,   // Hi-hat cerrado: 6 partículas
      'tr909oh': 10   // Hi-hat abierto: 10 partículas
    };
    return counts[sound] || 8;
  }

  // FUNCIÓN: Define la velocidad de expansión
  function getSpeed(sound) {
    const speeds = {
      'tr909bd': 200,  // Bombo: expansión lenta y pesada
      'tr909sd': 350,  // Caja: expansión rápida
      'tr909hh': 150,  // Hi-hat: expansión corta
      'tr909oh': 180   // Open hat: expansión media
    };
    return speeds[sound] || 200;
  }

  function dibujarElemento(anim, p) {
    push();
    
    // CALCULAR POSICIÓN ACTUAL basada en el ángulo y progreso
    let distance = anim.speed * p; // La distancia aumenta con el tiempo
    let x = anim.startX + cos(anim.angle) * distance;
    let y = anim.startY + sin(anim.angle) * distance;
    
    const color = anim.color;
    
    switch (anim.type) {
      case 'tr909bd':
        dibujarParticulaBombo(x, y, p, color);
        break;

      case 'tr909sd':
        dibujarParticulaCaja(x, y, p, color);
        break;

      case 'tr909hh':
      case 'tr909oh':
        dibujarParticulaHat(x, y, p, color, anim.particleIndex);
        break;

      default:
        dibujarParticulaDefault(x, y, p, color);
        break;
    }
    pop();
  }

  // FUNCIONES DE DIBUJO MODIFICADAS
  function dibujarParticulaBombo(x, y, p, c) {
    // Círculos que se expanden y desvanecen
    let size = lerp(30, 60, p);
    let alpha = lerp(255, 0, p);
    fill(c[0], c[1], c[2], alpha);
    circle(x, y, size);
  }

  function dibujarParticulaCaja(x, y, p, c) {
    // Cuadrados que rotan mientras se expanden
    let size = lerp(20, 5, p);
    let alpha = lerp(255, 0, p);
    let rotation = p * TWO_PI * 2; // Rotación doble
    
    translate(x, y);
    rotate(rotation);
    fill(c[0], c[1], c[2], alpha);
    rect(0, 0, size, size);
  }

  function dibujarParticulaHat(x, y, p, c, index) {
    // Líneas que se alargan
    let len = lerp(5, 30, p);
    let alpha = lerp(255, 0, p);
    
    stroke(c[0], c[1], c[2], alpha);
    strokeWeight(2);
    line(x - len/2, y, x + len/2, y);
  }

  function dibujarParticulaDefault(x, y, p, c) {
    let size = lerp(25, 0, p);
    let alpha = lerp(200, 0, p);
    fill(c[0], c[1], c[2], alpha);
    circle(x, y, size);
  }

  function getColorForSound(s) {
    const colors = {
      'tr909bd': [255, 0, 80],
      'tr909sd': [0, 200, 255],
      'tr909hh': [255, 255, 0],
      'tr909oh': [255, 150, 0]
    };
    if (colors[s]) return colors[s];
    let charCode = s.charCodeAt(0) || 0;
    let r = (charCode * 123) % 255;
    let g = (charCode * 456) % 255;
    let b = (charCode * 789) % 255;
    return [r, g, b];
  }  

  function windowResized() { resizeCanvas(windowWidth, windowHeight); }

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






