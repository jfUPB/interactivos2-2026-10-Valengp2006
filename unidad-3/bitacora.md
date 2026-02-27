# Unidad 3

## Bitácora de proceso de aprendizaje

### Actividad 01

**Paso 1 – Clonar el repositorio**

```bash
git clone https://github.com/juanferfranco/OpenStageControlUITest.git
cd OpenStageControlUITest
```

**Paso 2 – Instalar dependencias**

El proyecto usa Node.js. Instala las dependencias con:

```bash
npm install
```

Esto leerá el `package.json` e instalará lo necesario (probablemente un servidor local y la librería OSC para Node).

**Paso 3 – Ejecutar la aplicación**

```bash
npm start
```

Esto levantará un servidor local. Abre el navegador en `http://localhost` (el puerto dependerá de la configuración en `package.json`).

**Paso 4 – Configurar Open Stage Control**

Al abrir Open Stage Control, se configura los siguientes campos antes de hacer clic en **Play**:

| Campo | Valor |
|---|---|
| **send** | `127.0.0.1:puerto_que_escucha_la_app` |
| **receive** | Puerto donde OSC recibirá feedback (opcional) |
| **load** | Archivo `.json` de sesión (si hay uno disponible) |

El puerto exacto se encuentra en `bridgeUI.js` o `package.json` del repositorio.

**Paso 5 – Verificar la comunicación**

Una vez que ambos estén corriendo, se manipula un control en Open Stage Control (un slider, un botón, un knob). Si la integración funciona correctamente, el sketch de p5.js en el navegador debe reaccionar visualmente en tiempo real a esos mensajes.

### Actividad 02:

El sketch recibe mensajes desde un WebSocket en `ws://localhost:8081` (el oscBridge). Cada mensaje contiene un `timestamp`, un sonido (`s`), y parámetros adicionales. Los eventos se encolan, ordenan por tiempo, y se disparan en el `draw()` creando animaciones en `activeAnimations`.

#### Parámetros visuales actuales (hardcodeados)

Revisando el código línea por línea, estos son los valores fijos que actualmente no se pueden controlar externamente:

| Variable | Ubicación | Valor actual | Qué hace |
|---|---|---|---|
| `background(0, 30)` | `draw()` | Alpha = **30** | Desvanecimiento del fondo |
| `lerp(100, 600, p)` | `dibujarBombo()` | min=100, max=**600** | Tamaño máximo del bombo |
| `lerp(width, 0, p)` | `dibujarCaja()` | Ancho inicial = **width** | Ancho de la caja (snare) |
| `lerp(40, 0, p)` | `dibujarHat()` | Tamaño inicial = **40** | Tamaño del hi-hat |
| `x: random(0.2, 0.8)` | `draw()` | Fijo | Zona de aparición en X |
| Colores en `getColorForSound` | función | Fijos por sonido | Color de cada instrumento |

#### Parámetro seleccionado: `bgAlpha` — la opacidad del fondo

##### Línea de código objetivo

```javascript
background(0, 30); // ← el 30 es el alpha del fondo
```

##### ¿Por qué este parámetro?

Este valor de `30` controla qué tan rápido se "borra" el canvas en cada frame. Es el parámetro con mayor impacto expresivo global porque afecta toda la escena simultáneamente:

- **Alpha bajo (ej. 5–15)** → las animaciones dejan rastros largos, efecto de motion blur acumulado, sensación etérea y densa.
- **Alpha medio (ej. 30)** → el valor actual, balance entre persistencia y limpieza.
- **Alpha alto (ej. 100–255)** → el canvas se limpia casi instantáneamente, figuras contundentes y secas, percusión muy marcada.

Controlarlo en vivo desde Open Stage Control permite jugar con la densidad visual de la escena en tiempo real, algo especialmente potente durante una performance de live coding.

#### Plan de implementación

##### Paso 1 — Declarar variable global en `visualesMin.html`

Agregar al inicio del script, junto a las otras variables globales:

```javascript
let bgAlpha = 30; // valor por defecto, idéntico al actual
```

##### Paso 2 — Usar la variable en `draw()`

Cambiar esta línea:
```javascript
background(0, 30);
```
Por:
```javascript
background(0, bgAlpha);
```

##### Paso 3 — Recibir el valor desde el WebSocket

Dentro del `socket.onmessage`, agregar una bifurcación para distinguir mensajes de Strudel de mensajes de Open Stage Control:

```javascript
socket.onmessage = (event) => {
  const msg = JSON.parse(event.data);

  // Mensajes de control desde Open Stage Control
  if (msg.address === '/bgAlpha') {
    bgAlpha = msg.args[0] * 255; // OSC envía 0–1, mapeamos a 0–255
    return;
  }

  // Mensajes de audio desde Strudel (comportamiento existente)
  let params = {};
  for (let i = 0; i < msg.args.length; i += 2) {
    params[msg.args[i]] = msg.args[i + 1];
  }
  eventQueue.push({
    timestamp: msg.timestamp,
    sound: params.s,
    delta: params.delta || 0.25,
    params: params
  });
  eventQueue.sort((a, b) => a.timestamp - b.timestamp);
};
```

##### Paso 4 — Configurar Open Stage Control

Crear un slider en la interfaz de Open Stage Control con estas propiedades:

| Propiedad | Valor |
|---|---|
| **address** | `/bgAlpha` |
| **range mínimo** | `0` |
| **range máximo** | `1` |
| **valor inicial** | `0.12` (equivale al alpha 30 actual) |
| **send** | `127.0.0.1:puerto_del_bridge` |

##### Paso 5 — Adaptar el bridge (`bridge.js`)

El bridge necesita reenviar los mensajes de Open Stage Control al WebSocket del navegador. La lógica a agregar sería:

```javascript
// Al recibir un mensaje OSC desde Open Stage Control
oscServer.on('message', (msg) => {
  // Reenviar al navegador tal cual, con address y args
  broadcast(JSON.stringify({ address: msg.address, args: msg.args }));
});
```

## Bitácora de aplicación 

### Actividad 03

#### ¿Qué hice?

Agregué controles para cambiar los colores de las visuales en tiempo real usando Open Stage Control.

Ahora puedo cambiar el color de cada instrumento (bombo, piano, synth, etc.) individualmente mientras la música está sonando.

#### Decisión: ¿Qué controlar?

Decidí controlar **los colores de cada instrumento por separado**.

**¿Por qué? Porque así puedo:**
- Darle un color diferente a cada instrumento
- Cambiar el mood de la pieza sin tocar el código
- Experimentar con diferentes paletas de colores en vivo

#### Cómo lo hice

##### 1. Cambié las variables de color

En lugar de tener colores fijos, creé variables que puedo cambiar:

```javascript
// Antes: colores fijos
'piano': [100, 150, 255]

// Después: variables que puedo controlar
let pianoRed = 100;
let pianoGreen = 150;
let pianoBlue = 255;
```

Hice esto para cada instrumento: piano, bombo, synth, clap, etc.

##### 2. Agregué un segundo WebSocket

Mi código ahora tiene dos conexiones:
- **Puerto 8081**: Recibe el audio de Strudel
- **Puerto 8083**: Recibe los controles de Open Stage Control

```javascript
// Para el audio (Strudel)
const socket = new WebSocket('ws://localhost:8081');

// Para los controles (Open Stage Control)
const socketControl = new WebSocket('ws://localhost:8083');
```

##### 3. Programé cómo recibir los cambios de color

Cuando muevo un control en Open Stage Control, el código actualiza las variables:

```javascript
socketControl.onmessage = (event) => {
  const data = JSON.parse(event.data);

  // Si cambian el color del piano
  if (data.address == "/rgb_1") {
    pianoRed   = Number(data.args[0]);
    pianoGreen = Number(data.args[1]);
    pianoBlue  = Number(data.args[2]);
  }
  
  // Y así para cada instrumento...
}
```

##### 4. Hice un control especial para el bombo

Para el bombo usé un **XY pad** en lugar de 3 sliders:
- Mover a la izquierda/derecha = cambia el color (rojo→verde→azul)
- Mover arriba/abajo = cambia el brillo (oscuro→brillante)

Para esto necesité convertir de HSB a RGB con una función.

#### Controles que creé en Open Stage Control

1. **Control RGB para Sawtooth** - 3 colores (rojo, verde, azul)
2. **Control RGB para Square** - 3 colores
3. **Control RGB para Piano** - 3 colores
4. **XY Pad para Bombo** - mueves en 2 dimensiones
5. **Controles RGB para SD, Rim, CP, HH** - 3 colores cada uno

Cada control envía a una dirección diferente:
- Piano: `/rgb_1`
- Bombo: `/xy_1`
- Sawtooth: `/sawtooth_rgb`
- etc.

#### Lo que aprendí

- Cómo usar dos WebSockets al mismo tiempo
- Cómo funciona la conversión entre RGB y HSB
- Que el XY pad es más fácil de usar que 3 sliders separados
- Que puedo cambiar completamente el ambiente visual sin tocar el código

#### Conclusión

Ahora tengo control total sobre los colores de mi pieza. Puedo cambiar el mood visual en tiempo real mientras la música suena.

El sistema funciona bien y es fácil de usar durante una presentación.

## Bitácora de reflexión

### Actividad 05

<img width="836" height="441" alt="Captura de pantalla 2026-02-26 a la(s) 8 37 50 p m" src="https://github.com/user-attachments/assets/573a3321-253e-4487-9de8-e45e58ae05b1" />

El sistema ahora tiene dos flujos: uno para los eventos de audio y otro para los parámetros de control. Strudel envía el audio a través de bridge.js, mientras que Open Stage Control envía los parámetros a bridgeUI.js. Ambos llegan al navegador por diferentes puertos, lo que permite controlar el sonido en tiempo real de forma organizada y modular.


