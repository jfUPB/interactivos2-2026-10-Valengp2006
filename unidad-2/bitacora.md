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

**Modificación: "Efecto de Reverberación Visual"**

En lugar de que cada sonido genere un solo elemento visual, generaremos múltiples partículas que explotan desde el centro, creando un efecto más dinámico y afectando la sincronización al tener múltiples elementos por cada evento de audio.

#### Código modificado:

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
#### Cómo afecta la sincronización:

**Antes (original):**

- 1 evento de audio = 1 elemento visual
- Animación simple en una posición

**Después (modificado):**

- 1 evento de audio = múltiples partículas (6-12 dependiendo del sonido)
- Cada partícula:
  - Nace en el centro en el mismo instante (sincronizada con el audio)
  - Se mueve en direcciones radiales diferentes
  - Tiene la misma duración (delta) que el evento de audio
  - Desaparece cuando termina el sonido

**Aspectos clave de sincronización modificados:**

- **Multiplicación de elemento
s visuales:** Un solo mensaje OSC genera múltiples animaciones simultáneas
- **Distribución angular:** Las partículas se distribuyen uniformemente en círculo usando (TWO_PI / particleCount) * i
- **Velocidad diferenciada**: Cada tipo de sonido tiene una velocidad de expansión diferente
- **Sincronización temporal preservada:** Todas las partículas comparten el mismo timestamp y duration

#### Evidencias:

<img width="578" height="380" alt="Captura de pantalla 2026-02-08 a la(s) 9 46 29 p m" src="https://github.com/user-attachments/assets/ae9e907a-e44d-4708-9512-096913bf9e13" />
<img width="578" height="378" alt="Captura de pantalla 2026-02-08 a la(s) 9 46 36 p m" src="https://github.com/user-attachments/assets/efd4d16e-514d-4772-b21b-b010b3f00708" />
![Grabación-de-pantalla-2026-02-08-a-la_s_-9 48 40 p m](https://github.com/user-attachments/assets/2046d05b-bb8e-42ef-978d-8cba94d7d300)

## Bitácora de aplicación 



## Bitácora de reflexión



