# Unidad 1

## Bitácora de proceso de aprendizaje

### Actividad 01  22/01/2026

<img width="1352" height="787" alt="Captura de pantalla 2026-01-22 a la(s) 9 19 29 a m" src="https://github.com/user-attachments/assets/2ad9c2a9-0601-47c3-a452-923da527e2a7" />
<img width="583" height="385" alt="Captura de pantalla 2026-01-22 a la(s) 9 19 46 a m" src="https://github.com/user-attachments/assets/ead762d5-3219-4b0e-8668-a22449bf5218" />
<img width="579" height="382" alt="Captura de pantalla 2026-01-22 a la(s) 9 35 18 a m" src="https://github.com/user-attachments/assets/bb4bb7c9-e579-4c94-bb4c-433a310c20a0" />
<img width="1350" height="777" alt="Captura de pantalla 2026-01-22 a la(s) 9 43 48 a m" src="https://github.com/user-attachments/assets/3e600dd3-8bb2-429b-925b-441ad9b18937" />
<img width="1352" height="788" alt="Captura de pantalla 2026-01-22 a la(s) 9 44 49 a m" src="https://github.com/user-attachments/assets/13e279e0-2b02-4315-bb80-118443611ade" />
<img width="1352" height="789" alt="Captura de pantalla 2026-01-22 a la(s) 9 45 08 a m" src="https://github.com/user-attachments/assets/060fb382-bada-4f52-9aa4-486536c77560" />

### Actividad 02

**1. Sistema Físico Interactivo del Caso de Estudio**

El caso de estudio implementa un sistema de visualización sonora en Strudel que combina audio y gráficos de manera sincronizada.

**Componentes del sistema:**

1. **Tempo**: `setcps(0.5)` establece 0.5 ciclos por segundo (aproximadamente 30 BPM), controlando la velocidad de reproducción del patrón.

2. **Patrón rítmico**: `s("[bd*2 sd hh oh]")` define una secuencia de batería electrónica:
   - `bd*2`: Bass drum (bombo) se repite 2 veces
   - `sd`: Snare drum (redoblante)
   - `hh`: Hi-hat cerrado
   - `oh`: Open hi-hat (hi-hat abierto)
   - Los corchetes `[]` agrupan estos elementos en un ciclo

3. **Banco de sonidos**: `.bank("tr909")` utiliza samples de la legendaria caja de ritmos Roland TR-909.

4. **Interacción audiovisual**: El sistema utiliza `stack()` para superponer dos capas:
   - **Capa de audio**: `pat.gain('0.05')` reproduce el patrón con volumen reducido al 5%
   - **Capa visual**: `pat.osc()` genera un osciloscopio que visualiza la forma de onda en tiempo real

**Funcionamiento**

El patrón se reproduce continuamente, y cada golpe de percusión se refleja simultáneamente tanto en el audio como en la representación visual, creando una experiencia multisensorial sincronizada.

**2. Variación Propuesta e Implementación**

**Cambios implementados**

1. **Duplicación del patrón base**: Mantuve el patrón original de batería TR-909 pero lo dupliqué en dos capas con diferentes velocidades.

2. **Variación de velocidad**: 
   - Primera capa: velocidad normal (ritmo base)
   - Segunda capa: velocidad aumentada 1.5x (crea contrapunto rítmico)

3. **Efecto de reverberación**: Añadí `.room(0.8)` para crear un efecto de espacio amplio, dando profundidad al sonido.

4. **Ajuste de ganancia**: Modifiqué los niveles de volumen para balancear las capas:
   - Capa normal: 0.06 (ligeramente más alta que el original)
   - Capa rápida: 0.03 (más sutil para no saturar)

5. **Visualización mejorada**: La visualización ahora refleja la complejidad de ambas capas superpuestas.


**3. Código y Reproducción Paso a Paso**

**Código completo**

```javascript
setcps(0.5)

const pat = s("[bd*2 sd hh oh]").bank("tr909")

$: stack(
  pat.gain('0.06').room(0.8),
  pat.fast(1.5).gain('0.03').room(0.8),
  pat.osc()
)
```

**Pasos para reproducir**

**Paso 1 - Configurar el tempo**

```javascript
setcps(0.5)
```

Establece la velocidad base de 0.5 ciclos por segundo, manteniendo el tempo del caso de estudio original.

**Paso 2 - Definir el patrón base**

```javascript
const pat = s("[bd*2 sd hh oh]").bank("tr909")
```

Crea el patrón de batería usando samples de la TR-909. Este patrón se almacena en la constante `pat` para reutilizarlo en múltiples capas.

**Paso 3 - Construir la estructura de capas**

```javascript
$: stack(
  pat.gain('0.06').room(0.8),
  pat.fast(1.5).gain('0.03').room(0.8),
  pat.osc()
)
```

**Desglose de cada capa:**

- **Capa 1** - `pat.gain('0.06').room(0.8)`:
  - Reproduce el patrón a velocidad normal
  - `gain('0.06')`: volumen al 6% (ligeramente más alto que el original 5%)
  - `room(0.8)`: añade reverberación espacial al 80%

- **Capa 2** - `pat.fast(1.5).gain('0.03').room(0.8)`:
  - `.fast(1.5)`: acelera el patrón 1.5 veces (50% más rápido)
  - `gain('0.03')`: volumen al 3% (más sutil para evitar saturación)
  - `room(0.8)`: misma reverberación para coherencia espacial
  - Esta capa crea un contrapunto rítmico sobre el patrón base

- **Capa 3** - `pat.osc()`:
  - Visualización del patrón original mediante osciloscopio
  - Muestra la forma de onda combinada de ambas capas de audio

**Resultado**

Un patrón rítmico más complejo que combina el ritmo original con una versión acelerada, creando una textura polirrítmica con profundidad espacial gracias a la reverberación. La visualización muestra la suma de ambas capas, revelando la complejidad del resultado final.

### Actividad 03

**Código del experimento**

```javascript
setcps(0.4)
//set cicles per seconds

let drum = stack (
  s("oh").beat("0, 2, 5, 7, 9, 13, 15", 16),
  s("cr").beat("1, 4, 6, 8, 10, 12, 14", 16),
  s("cp").beat("4, 12", 16),
  s("bd").beat("0, 5, 7, 10, 15", 16)
)

$drum: drum
```

**Explicación detallada del código**

**Línea 1: `setcps(0.4)`**
- **Función**: Establece la velocidad de reproducción
- **Parámetro**: `0.4` ciclos por segundo (aproximadamente 24 BPM)
- **Efecto**: Controla qué tan rápido se reproduce el patrón completo
- **Nota**: Un valor más bajo hace el ritmo más lento, un valor más alto lo acelera

**Línea 4: `let drum = stack (`**
- **`let drum`**: Crea una variable llamada `drum` que almacena todo el patrón
- **`stack(`**: Función que superpone múltiples capas de sonido para que suenen simultáneamente
- **Propósito**: Permite combinar diferentes instrumentos de percusión en un solo patrón

**Línea 5: `s("oh").beat("0, 2, 5, 7, 9, 13, 15", 16)`**
- **`s("oh")`**: Selecciona el sonido "oh" (open hi-hat - platillo abierto)
- **`.beat("0, 2, 5, 7, 9, 13, 15", 16)`**: Define en qué posiciones del ciclo suena
  - Primer argumento: `"0, 2, 5, 7, 9, 13, 15"` son las posiciones donde suena el hi-hat
  - Segundo argumento: `16` es la división total del ciclo (16 partes)
- **Resultado**: El open hi-hat suena en las posiciones 0, 2, 5, 7, 9, 13 y 15 de un ciclo dividido en 16 partes

**Línea 6: `s("cr").beat("1, 4, 6, 8, 10, 12, 14", 16)`**
- **`s("cr")`**: Selecciona el sonido "cr" (crash cymbal - platillo crash)
- **`.beat("1, 4, 6, 8, 10, 12, 14", 16)`**: El crash suena en las posiciones 1, 4, 6, 8, 10, 12 y 14
- **Efecto**: Crea un patrón complementario al open hi-hat, llenando diferentes espacios rítmicos

**Línea 7: `s("cp").beat("4, 12", 16)`**
- **`s("cp")`**: Selecciona el sonido "cp" (clap - palmada)
- **`.beat("4, 12", 16)`**: La palmada suena solo en las posiciones 4 y 12
- **Función**: Actúa como el tiempo fuerte del patrón, similar al redoblante en música tradicional

**Línea 8: `s("bd").beat("0, 5, 7, 10, 15", 16)`**
- **`s("bd")`**: Selecciona el sonido "bd" (bass drum - bombo)
- **`.beat("0, 5, 7, 10, 15", 16)`**: El bombo suena en las posiciones 0, 5, 7, 10 y 15
- **Propósito**: Proporciona la base grave y el pulso fundamental del ritmo

**Línea 11: `$drum: drum`**
- **`$drum:`**: Crea un canal de salida llamado "drum"
- **`drum`**: Envía el contenido de la variable `drum` a ese canal
- **Función**: Hace que el patrón se reproduzca y sea audible
- **Nota**: Sin esta línea, el patrón no sonaría

**Concepto del método `.beat()`**

El método `.beat()` permite especificar exactamente en qué momentos de un ciclo debe sonar un instrumento:

- **Sintaxis**: `.beat("posiciones", divisiones_totales)`
- **Ventaja**: Control preciso sobre el ritmo sin usar notación de patrones complejos
- **Ejemplo**: `.beat("0, 4, 8, 12", 16)` hace que el sonido suene cada 4 pasos en un ciclo de 16

**Representación visual del patrón (ciclo de 16 partes)**

```
Posición: 0  1  2  3  4  5  6  7  8  9  10 11 12 13 14 15
---------------------------------------------------------------
oh:       X     X        X     X     X           X     X
cr:          X        X     X     X     X     X     X     X
cp:                   X                          X
bd:       X              X     X           X              X
```

**Resultado sonoro**

Este patrón crea un ritmo complejo de batería electrónica donde:
- Los hi-hats (oh y cr) crean una textura continua alternada
- Los claps (cp) marcan los acentos principales
- El bombo (bd) proporciona el pulso de baja frecuencia
- La combinación genera un groove polirrítmico interesante

<img width="538" height="352" alt="Captura de pantalla 2026-01-27 a la(s) 8 11 02 a m" src="https://github.com/user-attachments/assets/e7474ea5-88cb-4904-8d0f-c312bff9b01e" />

## Bitácora de aplicación 

### Actividad 03 27/01/2026

```javascript
setcps(0.7);

p1: n("0 2 4 6 7 6 4 2")
  .scale("<c3:major>")
  .distort(0.9)
  .superimpose((x) => x.detune("<0.5>"))
  .lpenv(perlin.slow(3).range(1, 4))
  .lpf(perlin.slow(2).range(100, 2000))
  .gain(0.3);

p2: "<a1>/8".clip(0.8).struct("x*8").note();

p3: n("0@3 2 4 <[6,8] [7,9]>")
.scale("C:minor").sound("piano")

p4: sound("[bd*4,~ rim ~ cp]*<1 [2 4]>")
```

<img width="520" height="409" alt="Captura de pantalla 2026-01-27 a la(s) 9 25 59 a m" src="https://github.com/user-attachments/assets/bc844247-53f2-48d2-8939-276ccdcfb84c" />

## Bitácora de reflexión







