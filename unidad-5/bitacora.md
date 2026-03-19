# Unidad 5
## Bitácora de proceso de aprendizaje

### Actividad 01 - 17/03/2026

#### Preguntas:
- **¿Qué quieres comunicar o provocar con tu obra? (intención artística/estética):**
  Busco representar una experiencia inspirada en el espacio exterior, que comience de manera calmada y vaya aumentando progresivamente en intensidad. A medida que avanza, se revelan más elementos, generando una sensación de descubrimiento y expansión.
- ¿**En qué contexto se presentará? (sala oscura, espacio abierto, escenario, etc.):**
  La obra se presentará en un salón de clase compartido con otros compañeros, adaptando el espacio para favorecer la experiencia.
- **¿Cuál es la experiencia que deseas para el público? (contemplativa, participativa, inmersiva, etc.):**
  La experiencia será principalmente inmersiva, buscando que el público se sienta dentro del entorno y conectado con la obra.
- **¿Qué rol tendrá el público? (observador, participante activo, co-creador, etc.):**
  El público tendrá un rol principalmente de observador, aunque se está considerando la posibilidad de incluir interacción mediante sus propios dispositivos.

#### Diagrama:
  
  <img width="689" height="337" alt="Captura de pantalla 2026-03-17 a la(s) 9 06 27 a m" src="https://github.com/user-attachments/assets/eb3e4f8e-4cc1-48e6-97dd-4743b89c4f30" />

### Actividad 02

#### Referentes encontrados y por qué son relevantes para la obra:
  - **[Interestellar](https://www.youtube.com/watch?v=UDVtMYqUAyw):** Este proyecto toma como uno de sus principales referentes la banda sonora y estética visual de Interstellar. La obra de Hans Zimmer construye una sensación de intensidad a través de la acumulación progresiva de capas sonoras, partiendo de elementos casi imperceptibles hasta alcanzar momentos de gran densidad. Asimismo, la película presenta el espacio como un entorno orgánico y dinámico, donde fenómenos como nebulosas o agujeros negros poseen una cualidad casi tangible. De este referente se retoma especialmente la idea de una evolución gradual y respiración del espacio, alineada con la intención de representar una nebulosa en formación.
  - **[Space](https://www.youtube.com/watch?v=ztVV54sPOns):** Como referente visual y sonoro, se toma contenido de Space, el cual combina imágenes reales del espacio con música ambiental diseñada para transmitir calma y favorecer la concentración. Este tipo de contenido resalta una visión del espacio como un entorno tranquilo, contemplativo y expansivo, lo cual influye directamente en el inicio de la obra. De aquí se retoma la atmósfera inicial de serenidad y la relación entre imagen y sonido como generadores de una experiencia envolvente.
  - **[Sound space Strudel](https://www.youtube.com/watch?v=dyIkHQbxJFc):** El uso de Strudel como herramienta de live coding también se apoya en referentes existentes dentro de esta plataforma, especialmente en la construcción de “espacios sonoros” mediante ciclos que se superponen y evolucionan con el tiempo. Este enfoque se relaciona directamente con la estructura de la obra, organizada en fases que aumentan progresivamente en complejidad. De este referente se toma la forma de construir el sonido como un entorno dinámico, donde la síntesis y la repetición generan profundidad y transformación.
  - **[Visuales](https://pin.it/6z44seCAb):** Adicionalmente, se cuenta con un tablero de referencias visuales en Pinterest que reúne imágenes relacionadas con la estética del espacio y la formación de estructuras como nebulosas. Estas imágenes funcionan como guía para definir las distintas etapas visuales de la obra, permitiendo establecer una evolución coherente en términos de color, densidad y movimiento.
    <img width="1280" height="555" alt="Captura de pantalla 2026-03-17 a la(s) 9 11 55 a m" src="https://github.com/user-attachments/assets/44eeec71-1f14-4867-8d00-54610ec5f4cd" />
    
#### Técnicas de audio generativo que se planea usar y por qué se ajustan al concepto:

La obra se estructura en tres fases progresivas —vacío, pulso e ignición— que desarrollan una intensidad creciente tanto a nivel sonoro como visual.

En la **Fase 1 (vacío)**, se construye una atmósfera basada en drones y síntesis FM con ondas senoidales, utilizando modulaciones lentas para generar un espacio sonoro estable y contemplativo. No hay pulso definido, sino eventos esporádicos, mientras que visualmente comienzan a aparecer partículas de forma gradual. La afinación se basa en just intonation, reforzando la pureza y sensación etérea del espacio.

En la **Fase 2 (pulso)**, emerge una estructura rítmica progresiva donde el kick activa el desarrollo sonoro y visual, dando paso a capas que se suman mediante síntesis aditiva. Este pulso también se traduce en eventos visuales a través de OSC, generando expansión de partículas. La afinación evoluciona hacia escalas modales, aportando mayor dirección musical.

Finalmente, en la **Fase 3 (ignición)**, se alcanza la máxima densidad mediante el uso de ruido, filtros y múltiples capas rítmicas (polirritmia). El sonido se vuelve más complejo y texturizado, mientras que los parámetros visuales como color e intensidad aumentan dinámicamente. La afinación incorpora clusters, generando tensión y complejidad armónica.

A nivel interactivo, la obra integra tres tipos de control:
	1.	Eventos discretos (como el kick) que generan cambios visuales directos.
	2.	Parámetros continuos (amplitud, LFOs) que modulan aspectos como color y movimiento.
	3.	Evolución espacial del sonido, especialmente mediante reverberación variable, que refuerza la sensación de expansión del entorno.

En conjunto, estos elementos permiten construir una experiencia en la que el sonido no solo acompaña la imagen, sino que la genera y transforma, creando una narrativa audiovisual coherente y en constante evolución.

La siguiente figura resume la estructura general de la obra, organizada en tres fases de intensidad creciente y sus respectivas capas sonoras, rítmicas, visuales y de afinación:

<img width="631" height="431" alt="Captura de pantalla 2026-03-17 a la(s) 9 28 02 a m" src="https://github.com/user-attachments/assets/49079d63-7df5-4fee-8f42-88f4eaeca218" />

Esta estructura guía tanto el desarrollo compositivo como la relación entre sonido e imagen a lo largo de la experiencia.

## Bitácora de aplicación 

### Actividad 03

**Versión 1 audio:**

```js
// ============================================================
//  C O S M O S  —  partitura Strudel
//  Estructura: Fase 1 → T1 → Fase 2 → T2 → Fase 3 → T3 → Fase 1'
//  Duración total aprox: 9–10 minutos
//  Escala base: C lydian (el cuarto grado elevado medio tono
//               da sensación de vastedad, nunca resuelve)
// ============================================================
//
//  CÓMO USAR ESTE ARCHIVO
//  ─────────────────────
//  1. Pega TODO el archivo en Strudel al inicio.
//  2. Solo ejecuta los bloques de la fase activa
//     (Ctrl+Enter en cada bloque que quieras activar).
//  3. Para silenciar un bloque: Ctrl+. con el cursor en ese bloque.
//  4. Sigue la guía de ACCIONES en cada sección.
//  5. Los tiempos son orientativos — confía en tu oído.
//
// ============================================================




// ============================================================
//  FASE 1  —  "El vacío respira"
//  Duración: ~2 min 45 s  (20 ciclos a 28 cpm)
//  Sensación: inmensidad, silencio habitado, expectativa
//
//  ACCIÓN: Ejecuta estos 2 bloques al comenzar.
//          Deja correr ~20 ciclos antes de pasar a T1.
//          Observa al público — si están muy quietos y
//          absorbidos, espera unos ciclos más.
// ============================================================

setcpm(28)

const motif = "<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>"

// Piano principal — notas dispersas, mucho silencio entre ellas
$: s("piano")
  .n(motif)
  .scale("C:lydian")
  .octave(4)
  .adsr("0.01 2.0 0.3 3.0")
  .gain(0.55)
  .room(2.5).roomsize(10)
  .cutoff(1800)
  .pan(sine.range(-0.3, 0.3).slow(8))

// Eco lejano — llega tarde, casi inaudible, como una memoria
$: s("piano")
  .n(motif)
  .scale("C:lydian")
  .octave(5)
  .adsr("0.01 1.5 0.1 4.0")
  .gain(0.08)
  .late(0.35)
  .room(3).roomsize(10)
  .cutoff(900)
  .pan(0.6)




// ============================================================
//  TRANSICIÓN 1  —  "Algo despierta"
//  Duración: ~35 s
//  Sensación: el espacio se llena sin que sepas cuándo empezó
//
//  ACCIÓN: Ejecuta los 2 bloques nuevos de abajo.
//          NO apagues todavía el piano de Fase 1.
//          Las cuerdas tardan 3 s en aparecer — son invisibles
//          al principio. El bajo aparece suave por debajo.
//          Espera ~4 ciclos. Cuando las cuerdas sean audibles,
//          silencia el eco de piano (el segundo bloque de F1).
// ============================================================

// Cuerdas — entran como niebla, attack de 3 segundos
$: note("<c3 g3>/4")
  .s("strings")
  .adsr("3.0 0 1 5.0")
  .gain(0.2)
  .cutoff(sine.range(200, 600).slow(12))
  .room(3).roomsize(10)
  .pan(0.4)

// Bajo — primera respiración rítmica de la obra
$: note("<c1 ~ c1 ~>/2")
  .s("sine")
  .adsr("0.05 0.8 0 0.5")
  .gain(0.28)
  .room(1.5)
  .lpf(180)




// ============================================================
//  FASE 2  —  "La materia se organiza"
//  Duración: ~2 min  (15 ciclos a 32 cpm)
//  Sensación: pulso, gravedad, algo tomando forma
//
//  ACCIÓN: Cambia setcpm a 32 (ejecútalo solo).
//          Ejecuta el nuevo piano denso.
//          Silencia el piano original de Fase 1 cuando
//          el nuevo piano ya esté sonando con fuerza.
//          Las cuerdas y el bajo siguen corriendo.
// ============================================================

setcpm(32)

// Piano más denso — el motif se llena, sube densidad
$: s("piano")
  .n("<[0 2 4 ~] [7 ~ 4 2] [0 4 7 11] [~ 2 ~ 0]>")
  .scale("C:lydian")
  .octave(4)
  .adsr("0.01 1.2 0.4 2.0")
  .gain(0.6)
  .density(1.4)
  .room(2).roomsize(9)
  .cutoff(sine.range(600, 2200).slow(6))
  .pan(sine.range(-0.4, 0.4).slow(5))

// Cuerdas más activas — reemplaza las cuerdas de T1
$: note("<c3 e3 g3 b3>/2")
  .s("strings")
  .adsr("1.5 0 1 3.0")
  .gain(0.3)
  .cutoff(sine.range(400, 1200).slow(7))
  .room(2.5).roomsize(9)
  .pan(-0.4)

// Piano eco en octava alta — reaparece más brillante
$: s("piano")
  .n("<[0 2 4 ~] [7 ~ 4 2] [0 4 7 11] [~ 2 ~ 0]>")
  .scale("C:lydian")
  .octave(5)
  .adsr("0.01 1.0 0.2 2.5")
  .gain(0.12)
  .late(0.28)
  .room(2.5).roomsize(9)
  .cutoff(1200)
  .pan(-0.5)




// ============================================================
//  TRANSICIÓN 2  —  "La ignición comienza"
//  Duración: ~30 s
//  Sensación: el techo sube, algo irreversible ocurre
//
//  ACCIÓN: Ejecuta el órgano y la percusión.
//          El órgano tiene attack de 4 s — tarda en aparecer.
//          Cuando lo sientas presente, estás en Fase 3.
//          No hace falta silenciar nada aún.
// ============================================================

// Órgano — la pared de sonido, entra como una ola lenta
$: note("<c2 g2>/8")
  .s("organ")
  .adsr("4.0 0 1 6.0")
  .gain(sine.range(0.15, 0.45).slow(16))
  .cutoff(sine.range(300, 1000).slow(8))
  .room(3).roomsize(10)

// Percusión cósmica — metal resonante, no drum kit
$: s("metal")
  .n("<0 ~ 3 ~>")
  .adsr("0.001 2.0 0 1.5")
  .gain(0.18)
  .room(3).roomsize(10)
  .cutoff(sine.range(200, 700).slow(3))
  .pan(rand.range(-0.7, 0.7))




// ============================================================
//  FASE 3  —  "Ignición"
//  Duración: ~1 min 40 s  (clímax — no lo extiendas demasiado)
//  Sensación: expansión total, todo presente, abrumador
//
//  ACCIÓN: Cambia setcpm a 38.
//          Ejecuta el piano de clímax y el shimmer.
//          Silencia el piano de Fase 2 cuando el nuevo esté activo.
//          Aquí todos los bloques corren juntos:
//          piano clímax + cuerdas F2 + bajo + órgano + percusión + shimmer.
//          Deja correr ~10–12 ciclos. Siente el punto de saturación
//          — ese es el momento de empezar T3.
// ============================================================

setcpm(38)

// Piano clímax — sube una octava, más urgente
$: s("piano")
  .n("<[0 2 4 7] [2 4 7 11] [4 7 11 14] [7 11 14 16]>")
  .scale("C:lydian")
  .octave(5)
  .adsr("0.01 0.8 0.5 1.5")
  .gain(0.7)
  .density(2)
  .room(1.8).roomsize(8)
  .cutoff(sine.range(1000, 4000).fast(0.8))
  .pan(sine.range(-0.6, 0.6).slow(3))

// Shimmer — brillo extremo en las alturas
$: note("<e5 b5 g5 d6>/2")
  .s("sine")
  .adsr("2.0 0 1 4.0")
  .gain(sine.range(0.06, 0.22).slow(5))
  .room(3).roomsize(10)
  .lpf(3000)
  .pan(sine.range(-0.8, 0.8).slow(7))




// ============================================================
//  TRANSICIÓN 3  —  "El cosmos exhala"
//  Duración: ~45 s – 1 min
//  Sensación: la energía no colapsa — se disuelve hacia afuera
//
//  ACCIÓN: Silencia en este orden, con ~10 s entre cada uno:
//          1. Percusión (metal)
//          2. Piano clímax y shimmer
//          3. Cuerdas (o baja su gain gradualmente)
//          4. Órgano (tiene release de 6 s — su cola es parte del silencio)
//          5. Bajo
//          Queda solo el piano de Fase 1' corriendo.
// ============================================================




// ============================================================
//  FASE 1'  —  "El vacío que recuerda"
//  Duración: ~1 min – 1 min 30 s hasta silencio total
//  Sensación: el mismo inicio, pero el público ya no es el mismo
//
//  ACCIÓN: Mientras silencias T3, ya ejecuta estos 2 bloques.
//          Son casi idénticos a Fase 1, pero el gain es más bajo
//          y el cutoff más oscuro — como un recuerdo del inicio.
//          Deja correr 6–8 ciclos.
//          Al final, silencia el eco primero, luego el piano.
//          El reverb tiene release de 5 s — el último sonido
//          tarda en desaparecer. Ese fade es el final de la obra.
// ============================================================

setcpm(28)

// Piano — igual que Fase 1 pero más tenue, más oscuro
$: s("piano")
  .n(motif)
  .scale("C:lydian")
  .octave(4)
  .adsr("0.01 2.0 0.3 3.0")
  .gain(0.38)
  .room(2.5).roomsize(10)
  .cutoff(1100)
  .pan(sine.range(-0.3, 0.3).slow(8))

// Eco — más suave aún que al inicio, casi inaudible
$: s("piano")
  .n(motif)
  .scale("C:lydian")
  .octave(5)
  .adsr("0.01 1.5 0.1 5.0")
  .gain(0.04)
  .late(0.4)
  .room(3).roomsize(10)
  .cutoff(700)
  .pan(-0.5)


// ============================================================
//  FIN
//  Duración total aproximada: 9 min 30 s
//
//  RESUMEN DE ACCIONES EN VIVO:
//  0:00        Ejecuta Fase 1 (2 bloques)
//  ~2:45       Ejecuta T1 (2 bloques nuevos)
//  ~3:20       setcpm(32) + ejecuta Fase 2, silencia eco F1
//  ~5:20       Ejecuta T2 (órgano + percusión)
//  ~5:50       setcpm(38) + ejecuta Fase 3, silencia piano F2
//  ~7:30       Inicia T3: silencia bloques en orden (ver arriba)
//  ~8:15       Ejecuta Fase 1' (2 bloques)
//  ~9:30       Silencia eco, luego piano. Deja morir el reverb.
// ============================================================
```
**Código strudel versión 2:**
```js
// ============================================================
//  C O S M O S  —  partitura Strudel  v3
//  Cambios respecto a v2:
//  · Crossfades entre todas las transiciones (sin cortes)
//  · Percusión metálica reemplazada por pulsar grave
//  · Estructura: un solo $ con stack + arrange
//  · Ejecutar con play global — corre solo ~9 min
// ============================================================
//
//  Tabla de ciclos (cpm base = 28):
//  Fase 1   : 20 ciclos  (~2:45)
//  T1       :  4 ciclos  (~35s)   crossfade incluido
//  Fase 2   : 15 ciclos  (~2:00)
//  T2       :  4 ciclos  (~35s)   crossfade incluido
//  Fase 3   : 12 ciclos  (~1:40)
//  T3       :  6 ciclos  (~50s)   fade out gradual
//  Fase 1'  :  8 ciclos  (~1:05)
//  TOTAL    : 69 ciclos  (~9:30)
// ============================================================

$: stack(

  // ── PIANO ──────────────────────────────────────────────
  arrange(
    // F1: disperso, mucho silencio
    [20, s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>")
         .scale("C:lydian").octave(4)
         .adsr("0.01 2.0 0.3 3.0").gain(0.55)
         .room(2.5).roomsize(10).cutoff(1800)
         .pan(sine.range(-0.3, 0.3).slow(8))],

    // T1: mismo piano, fade suave hacia F2
    [2,  s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>")
         .scale("C:lydian").octave(4)
         .adsr("0.01 2.0 0.3 3.0").gain(0.55)
         .room(2.5).roomsize(10).cutoff(1800)],
    [2,  s("piano").n("<[0 2 4 ~] [7 ~ 4 2] [0 4 7 11] [~ 2 ~ 0]>")
         .scale("C:lydian").octave(4)
         .adsr("0.01 1.5 0.4 2.5")
         .gain(sine.range(0.55, 0.6).slow(2))
         .room(2.5).roomsize(10).cutoff(1600)],

    // F2: denso, cutoff animado
    [15, s("piano").n("<[0 2 4 ~] [7 ~ 4 2] [0 4 7 11] [~ 2 ~ 0]>")
         .scale("C:lydian").octave(4)
         .adsr("0.01 1.2 0.4 2.0").gain(0.6).density(1.4)
         .room(2).roomsize(9)
         .cutoff(sine.range(600, 2200).slow(6))
         .pan(sine.range(-0.4, 0.4).slow(5))],

    // T2: crossfade hacia F3 — sube octava gradualmente
    [2,  s("piano").n("<[0 2 4 ~] [7 ~ 4 2] [0 4 7 11] [~ 2 ~ 0]>")
         .scale("C:lydian").octave(4)
         .gain(sine.range(0.6, 0.3).slow(2))
         .room(2).roomsize(9).cutoff(1800)],
    [2,  s("piano").n("<[0 2 4 7] [2 4 7 11] [4 7 11 14] [7 11 14 16]>")
         .scale("C:lydian").octave(5)
         .gain(sine.range(0.3, 0.7).slow(2)).density(1.5)
         .room(2).roomsize(9).cutoff(2000)],

    // F3: clímax — octava alta, máxima densidad
    [12, s("piano").n("<[0 2 4 7] [2 4 7 11] [4 7 11 14] [7 11 14 16]>")
         .scale("C:lydian").octave(5)
         .adsr("0.01 0.8 0.5 1.5").gain(0.7).density(2)
         .room(1.8).roomsize(8)
         .cutoff(sine.range(1000, 4000).fast(0.8))
         .pan(sine.range(-0.6, 0.6).slow(3))],

    // T3: fade out hacia F1'
    [3,  s("piano").n("<[0 2 4 7] [2 4 7 11]>")
         .scale("C:lydian").octave(5)
         .gain(sine.range(0.7, 0.4).slow(3))
         .room(2).roomsize(9).cutoff(2000)],
    [3,  s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>")
         .scale("C:lydian").octave(4)
         .gain(sine.range(0.4, 0.38).slow(3))
         .room(2.5).roomsize(10).cutoff(1300)],

    // F1': igual que F1 pero más tenue y oscuro
    [8,  s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>")
         .scale("C:lydian").octave(4)
         .adsr("0.01 2.0 0.3 3.0")
         .gain(sine.range(0.38, 0.0).slow(8))
         .room(2.5).roomsize(10).cutoff(1100)
         .pan(sine.range(-0.3, 0.3).slow(8))]
  ),


  // ── ECO DE PIANO ───────────────────────────────────────
  arrange(
    // F1: eco lejano
    [20, s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>")
         .scale("C:lydian").octave(5)
         .adsr("0.01 1.5 0.1 4.0").gain(0.08).late(0.35)
         .room(3).roomsize(10).cutoff(900).pan(0.6)],

    // T1 + F2: eco se apaga
    [4,  s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~]>")
         .scale("C:lydian").octave(5)
         .gain(sine.range(0.08, 0.0).slow(4)).late(0.35)
         .room(3).roomsize(10).cutoff(800)],

    // F2, T2, F3, T3: silencio
    [33, s("piano").n("0").gain(0)],

    // F1': eco reaparece, más suave que al inicio
    [8,  s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>")
         .scale("C:lydian").octave(5)
         .adsr("0.01 1.5 0.1 5.0")
         .gain(sine.range(0.04, 0.0).slow(8)).late(0.4)
         .room(3).roomsize(10).cutoff(700).pan(-0.5)]
  ),


  // ── CUERDAS ────────────────────────────────────────────
  arrange(
    // F1: silencio
    [20, s("strings").note("c3").gain(0)],

    // T1: entran como niebla — attack 3s hace que sean invisibles al principio
    [4,  s("strings").note("<c3 g3>/4")
         .adsr("3.0 0 1 5.0")
         .gain(sine.range(0.0, 0.2).slow(4))
         .cutoff(sine.range(200, 600).slow(12))
         .room(3).roomsize(10).pan(0.4)],

    // F2: más activas
    [15, s("strings").note("<c3 e3 g3 b3>/2")
         .adsr("1.5 0 1 3.0").gain(0.3)
         .cutoff(sine.range(400, 1200).slow(7))
         .room(2.5).roomsize(9).pan(-0.4)],

    // T2: crecen hacia F3
    [4,  s("strings").note("<c3 e3 g3 b3>/2")
         .adsr("1.5 0 1 3.0")
         .gain(sine.range(0.3, 0.42).slow(4))
         .cutoff(sine.range(600, 2000).slow(5))
         .room(2.5).roomsize(9)],

    // F3: máxima presencia
    [12, s("strings").note("<c3 e3 g3 b3 d4>/2")
         .adsr("1.5 0 1 3.0").gain(0.42)
         .cutoff(sine.range(800, 3000).slow(4))
         .room(2.5).roomsize(9)],

    // T3: fade out gradual
    [6,  s("strings").note("<c3 e3 g3>/2")
         .gain(sine.range(0.42, 0.0).slow(6))
         .room(3).roomsize(10)],

    // F1': silencio
    [8,  s("strings").note("c3").gain(0)]
  ),


  // ── BAJO ───────────────────────────────────────────────
  arrange(
    // F1: silencio
    [20, s("sine").note("c1").gain(0)],

    // T1: aparece suave
    [4,  s("sine").note("<c1 ~ c1 ~>/2")
         .adsr("0.05 0.8 0 0.5")
         .gain(sine.range(0.0, 0.28).slow(4))
         .room(1.5).lpf(180)],

    // F2: estable
    [15, s("sine").note("<c1 ~ c1 ~>/2")
         .adsr("0.05 0.8 0 0.5").gain(0.3)
         .room(1.5).lpf(180)],

    // T2: crece
    [4,  s("sine").note("<c1 ~ c1 ~>/2")
         .adsr("0.05 0.8 0 0.5")
         .gain(sine.range(0.3, 0.45).slow(4))
         .room(1.5).lpf(200)],

    // F3: más denso
    [12, s("sine").note("<c1 c1 g0 c1>/1")
         .adsr("0.02 0.6 0 0.4").gain(0.45)
         .room(1.5).lpf(200)],

    // T3: fade out
    [6,  s("sine").note("<c1 ~ c1 ~>/2")
         .gain(sine.range(0.45, 0.0).slow(6))
         .room(1.5).lpf(180)],

    // F1': silencio
    [8,  s("sine").note("c1").gain(0)]
  ),


  // ── ÓRGANO ─────────────────────────────────────────────
  arrange(
    // F1 + T1 + F2: silencio
    [39, s("organ").note("c2").gain(0)],

    // T2: entra como ola — attack 4s, completamente invisible al principio
    [4,  s("organ").note("<c2 g2>/8")
         .adsr("4.0 0 1 6.0")
         .gain(sine.range(0.0, 0.35).slow(4))
         .cutoff(sine.range(300, 1000).slow(8))
         .room(3).roomsize(10)],

    // F3: plena presencia
    [12, s("organ").note("<c2 g2>/8")
         .adsr("4.0 0 1 6.0")
         .gain(sine.range(0.25, 0.5).slow(16))
         .cutoff(sine.range(300, 1000).slow(8))
         .room(3).roomsize(10)],

    // T3: fade muy lento — el release de 6s hace que la cola
    //     se escuche incluso después de que el gain llegue a 0
    [6,  s("organ").note("<c2 g2>/8")
         .adsr("4.0 0 1 6.0")
         .gain(sine.range(0.4, 0.0).slow(6))
         .room(3).roomsize(10)],

    // F1': silencio (pero la cola del órgano sigue resonando)
    [8,  s("organ").note("c2").gain(0)]
  ),


  // ── PULSAR  (reemplaza percusión metálica) ─────────────
  // Inspirado en CP 1919 — el primer púlsar descubierto.
  // Graves lentos con decay largo, como una estrella que respira.
  arrange(
    // F1 + T1 + F2: silencio
    [39, s("bd").n("0").gain(0)],

    // T2: aparece suave, casi imperceptible
    [4,  s("bd").n("<0 ~ ~ ~ ~ ~ ~ ~>")
         .adsr("0.001 3.5 0 2.0")
         .gain(sine.range(0.0, 0.18).slow(4))
         .room(3).roomsize(10).lpf(100)],

    // F3: pulsar pleno — lento, profundo, inexorable
    [12, s("bd").n("<0 ~ ~ ~ ~ ~ ~ ~>")
         .adsr("0.001 3.5 0 2.0").gain(0.22)
         .room(3).roomsize(10).lpf(120)
         .pan(sine.range(-0.25, 0.25).slow(13))],

    // T3: se aleja lentamente
    [6,  s("bd").n("<0 ~ ~ ~ ~ ~ ~ ~>")
         .adsr("0.001 3.5 0 2.0")
         .gain(sine.range(0.22, 0.0).slow(6))
         .room(3).roomsize(10).lpf(100)],

    // F1': silencio
    [8,  s("bd").n("0").gain(0)]
  ),


  // ── SHIMMER (brillo en alturas, solo F3) ───────────────
  arrange(
    // F1 + T1 + F2 + T2: silencio
    [43, s("sine").note("e5").gain(0)],

    // F3: brillo pulsante en las alturas
    [12, s("sine").note("<e5 b5 g5 d6>/2")
         .adsr("2.0 0 1 4.0")
         .gain(sine.range(0.05, 0.2).slow(5))
         .room(3).roomsize(10).lpf(3000)
         .pan(sine.range(-0.8, 0.8).slow(7))],

    // T3 + F1': fade y silencio
    [6,  s("sine").note("<e5 b5>/2")
         .gain(sine.range(0.15, 0.0).slow(6))
         .room(3).roomsize(10).lpf(3000)],

    [8,  s("sine").note("e5").gain(0)]
  )

).cpm(28)
// ============================================================
//  FIN  —  ~9 min 30 s
//  Presiona play una vez y deja correr.
// ============================================================
```
**Verisón 3 código strudel:**
```js
// ============================================================
//  C O S M O S  —  partitura Strudel  v4
//  Cambios respecto a v3:
//  · Clicks eliminados — crossfades con .gain().fadein/fadeout
//    reemplazados por .legato() y ataques más suaves
//  · Bajo y pulsar fijados al centro (sin pan)
//  · Ataque del pulsar subido de 0.001 a 0.08 para evitar pop
// ============================================================
//
//  Ciclos totales: 69  (~9 min 30 s a 28 cpm)
//  Ejecutar: botón play global, una sola vez.
// ============================================================

$: stack(

  // ── PIANO ──────────────────────────────────────────────
  arrange(
    // F1
    [20, s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>")
         .scale("C:lydian").octave(4)
         .adsr("0.01 2.0 0.3 3.0").gain(0.55)
         .room(2.5).roomsize(10).cutoff(1800)
         .pan(sine.range(-0.3, 0.3).slow(8))],

    // T1a: mismo patrón F1, gain estable — sin sine.range para evitar clicks
    [2,  s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>")
         .scale("C:lydian").octave(4)
         .adsr("0.01 2.0 0.3 3.0").gain(0.55)
         .room(2.5).roomsize(10).cutoff(1800)],

    // T1b: patrón F2 entra suave con gain bajo, sube en F2
    [2,  s("piano").n("<[0 2 4 ~] [7 ~ 4 2] [0 4 7 11] [~ 2 ~ 0]>")
         .scale("C:lydian").octave(4)
         .adsr("0.01 1.8 0.4 2.5").gain(0.3)
         .room(2.2).roomsize(10).cutoff(1500)],

    // F2
    [15, s("piano").n("<[0 2 4 ~] [7 ~ 4 2] [0 4 7 11] [~ 2 ~ 0]>")
         .scale("C:lydian").octave(4)
         .adsr("0.01 1.2 0.4 2.0").gain(0.6).density(1.4)
         .room(2).roomsize(9)
         .cutoff(sine.range(600, 2200).slow(6))
         .pan(sine.range(-0.4, 0.4).slow(5))],

    // T2a: F2 baja gain
    [2,  s("piano").n("<[0 2 4 ~] [7 ~ 4 2] [0 4 7 11] [~ 2 ~ 0]>")
         .scale("C:lydian").octave(4)
         .adsr("0.01 1.5 0.4 2.5").gain(0.35)
         .room(2.2).roomsize(9).cutoff(1800)],

    // T2b: F3 entra en octava 5 con gain bajo
    [2,  s("piano").n("<[0 2 4 7] [2 4 7 11] [4 7 11 14] [7 11 14 16]>")
         .scale("C:lydian").octave(5)
         .adsr("0.01 1.2 0.5 2.0").gain(0.35).density(1.5)
         .room(2).roomsize(9).cutoff(2000)],

    // F3
    [12, s("piano").n("<[0 2 4 7] [2 4 7 11] [4 7 11 14] [7 11 14 16]>")
         .scale("C:lydian").octave(5)
         .adsr("0.01 0.8 0.5 1.5").gain(0.7).density(2)
         .room(1.8).roomsize(8)
         .cutoff(sine.range(1000, 4000).fast(0.8))
         .pan(sine.range(-0.6, 0.6).slow(3))],

    // T3a: baja octava gradualmente
    [3,  s("piano").n("<[0 2 4 7] [2 4 7 11]>")
         .scale("C:lydian").octave(5)
         .adsr("0.01 1.5 0.4 2.5").gain(0.45)
         .room(2.2).roomsize(9).cutoff(2000)],

    // T3b: vuelve a patrón F1 en octava 4
    [3,  s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>")
         .scale("C:lydian").octave(4)
         .adsr("0.01 2.0 0.3 3.0").gain(0.4)
         .room(2.5).roomsize(10).cutoff(1300)],

    // F1': igual a F1 pero más oscuro, gain baja progresivamente
    [8,  s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>")
         .scale("C:lydian").octave(4)
         .adsr("0.01 2.5 0.2 4.0").gain(0.32)
         .room(2.5).roomsize(10).cutoff(1000)
         .pan(sine.range(-0.2, 0.2).slow(10))]
  ),


  // ── ECO DE PIANO ───────────────────────────────────────
  arrange(
    // F1
    [20, s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>")
         .scale("C:lydian").octave(5)
         .adsr("0.01 1.5 0.1 4.0").gain(0.08).late(0.35)
         .room(3).roomsize(10).cutoff(900).pan(0.6)],

    // T1: eco se desvanece — gain fijo bajo, no sine.range
    [4,  s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~]>")
         .scale("C:lydian").octave(5)
         .adsr("0.01 1.5 0.1 4.0").gain(0.03).late(0.35)
         .room(3).roomsize(10).cutoff(800)],

    // F2 + T2 + F3 + T3: silencio
    [33, s("piano").n("0").gain(0)],

    // F1': eco reaparece muy suave
    [8,  s("piano").n("<[0 ~ ~ 4] [~ 7 ~ ~] [11 ~ 4 ~] [~ ~ 0 ~]>")
         .scale("C:lydian").octave(5)
         .adsr("0.01 2.0 0.1 5.0").gain(0.04).late(0.4)
         .room(3).roomsize(10).cutoff(700).pan(-0.4)]
  ),


  // ── CUERDAS ────────────────────────────────────────────
  arrange(
    // F1: silencio
    [20, s("strings").note("c3").gain(0)],

    // T1: entran con attack 3s — el gain bajo hace que sean casi inaudibles
    //     al principio, sin necesidad de sine.range
    [4,  s("strings").note("<c3 g3>/4")
         .adsr("3.0 0 1 5.0").gain(0.15)
         .cutoff(sine.range(200, 600).slow(12))
         .room(3).roomsize(10).pan(0.35)],

    // F2: gain sube al valor pleno
    [15, s("strings").note("<c3 e3 g3 b3>/2")
         .adsr("1.5 0 1 3.0").gain(0.3)
         .cutoff(sine.range(400, 1200).slow(7))
         .room(2.5).roomsize(9).pan(-0.35)],

    // T2: gain sube un poco más
    [4,  s("strings").note("<c3 e3 g3 b3>/2")
         .adsr("1.5 0 1 3.0").gain(0.38)
         .cutoff(sine.range(600, 2000).slow(5))
         .room(2.5).roomsize(9)],

    // F3
    [12, s("strings").note("<c3 e3 g3 b3 d4>/2")
         .adsr("1.5 0 1 3.0").gain(0.42)
         .cutoff(sine.range(800, 3000).slow(4))
         .room(2.5).roomsize(9)],

    // T3a: reducen notas y gain
    [3,  s("strings").note("<c3 e3 g3>/2")
         .adsr("2.0 0 1 4.0").gain(0.25)
         .room(3).roomsize(10)],

    // T3b: dos notas, casi desaparecen
    [3,  s("strings").note("<c3 g3>/4")
         .adsr("3.0 0 1 5.0").gain(0.1)
         .room(3).roomsize(10)],

    // F1': silencio
    [8,  s("strings").note("c3").gain(0)]
  ),


  // ── BAJO — SIEMPRE EN EL CENTRO ────────────────────────
  arrange(
    // F1: silencio
    [20, s("sine").note("c1").gain(0)],

    // T1: aparece suave, gain fijo bajo
    [4,  s("sine").note("<c1 ~ c1 ~>/2")
         .adsr("0.05 0.8 0 0.5").gain(0.18)
         .room(1.5).lpf(180)],

    // F2: sube a gain pleno
    [15, s("sine").note("<c1 ~ c1 ~>/2")
         .adsr("0.05 0.8 0 0.5").gain(0.3)
         .room(1.5).lpf(180)],

    // T2: sube un poco
    [4,  s("sine").note("<c1 ~ c1 ~>/2")
         .adsr("0.05 0.8 0 0.5").gain(0.38)
         .room(1.5).lpf(200)],

    // F3: más denso
    [12, s("sine").note("<c1 c1 g0 c1>/1")
         .adsr("0.05 0.6 0 0.5").gain(0.45)
         .room(1.5).lpf(200)],

    // T3: baja en dos pasos
    [3,  s("sine").note("<c1 ~ c1 ~>/2")
         .adsr("0.05 0.8 0 0.5").gain(0.25)
         .room(1.5).lpf(180)],
    [3,  s("sine").note("<c1 ~ ~ ~>/2")
         .adsr("0.05 1.0 0 0.8").gain(0.12)
         .room(2).lpf(160)],

    // F1': silencio
    [8,  s("sine").note("c1").gain(0)]
  ),


  // ── ÓRGANO ─────────────────────────────────────────────
  arrange(
    // F1 + T1 + F2: silencio
    [39, s("organ").note("c2").gain(0)],

    // T2: entra con attack 4s — el gain bajo hace el trabajo
    //     sin necesidad de sine.range en el gain
    [4,  s("organ").note("<c2 g2>/8")
         .adsr("4.0 0 1 6.0").gain(0.2)
         .cutoff(sine.range(300, 1000).slow(8))
         .room(3).roomsize(10)],

    // F3: sube a gain pleno
    [12, s("organ").note("<c2 g2>/8")
         .adsr("4.0 0 1 6.0").gain(0.42)
         .cutoff(sine.range(300, 1000).slow(8))
         .room(3).roomsize(10)],

    // T3: baja gain en dos pasos
    [3,  s("organ").note("<c2 g2>/8")
         .adsr("4.0 0 1 6.0").gain(0.22)
         .room(3).roomsize(10)],
    [3,  s("organ").note("c2")
         .adsr("4.0 0 1 6.0").gain(0.08)
         .room(3).roomsize(10)],

    // F1': silencio (la cola de release suena igual)
    [8,  s("organ").note("c2").gain(0)]
  ),


  // ── PULSAR — CENTRO, SIN PANEO ─────────────────────────
  // Ataque subido a 0.08 para eliminar el pop de 0.001
  arrange(
    // F1 + T1 + F2: silencio
    [39, s("bd").n("0").gain(0)],

    // T2: aparece muy suave, sin paneo
    [4,  s("bd").n("<0 ~ ~ ~ ~ ~ ~ ~>")
         .adsr("0.08 3.5 0 2.0").gain(0.14)
         .room(3).roomsize(10).lpf(100)],

    // F3: pleno — lento, profundo, sin paneo
    [12, s("bd").n("<0 ~ ~ ~ ~ ~ ~ ~>")
         .adsr("0.08 3.5 0 2.0").gain(0.22)
         .room(3).roomsize(10).lpf(120)],

    // T3: baja en dos pasos
    [3,  s("bd").n("<0 ~ ~ ~ ~ ~ ~ ~>")
         .adsr("0.08 3.5 0 2.0").gain(0.12)
         .room(3).roomsize(10).lpf(110)],
    [3,  s("bd").n("<0 ~ ~ ~ ~ ~ ~ ~>")
         .adsr("0.08 3.5 0 2.0").gain(0.05)
         .room(3).roomsize(10).lpf(100)],

    // F1': silencio
    [8,  s("bd").n("0").gain(0)]
  ),


  // ── SHIMMER ────────────────────────────────────────────
  arrange(
    // F1 + T1 + F2 + T2: silencio
    [43, s("sine").note("e5").gain(0)],

    // F3: gain fijo bajo — el adsr con attack 2s hace la entrada suave
    [12, s("sine").note("<e5 b5 g5 d6>/2")
         .adsr("2.0 0 1 4.0").gain(0.15)
         .room(3).roomsize(10).lpf(3000)
         .pan(sine.range(-0.7, 0.7).slow(7))],

    // T3: baja gain
    [4,  s("sine").note("<e5 b5>/2")
         .adsr("2.0 0 1 4.0").gain(0.06)
         .room(3).roomsize(10).lpf(3000)],

    // F1': silencio
    [10, s("sine").note("e5").gain(0)]
  )

).cpm(28)
// ============================================================
//  FIN  —  ~9 min 30 s
// ============================================================
```
- **Proceso de creación del audio generativo.**
- **Decisiones técnicas y estéticas que se tomaron y por qué.**
- **Código completo de la pieza de audio.**
- **Instrucciones paso a paso para reproducir la audio.**

## Bitácora de reflexión

### Actividad 04

- Evalúa si el audio generativo que creaste logra la intención estética que planteaste en tu concepto. ¿Qué ajustarías?
- Actualiza el diagrama de sistema de tu obra incorporando los detalles reales de la implementación del audio.
- Describe los principales desafíos que enfrentaste y cómo los resolviste.
