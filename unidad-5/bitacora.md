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
	- **[Musica orquestal en strudel](https://youtube.com/shorts/cAUgrQALbXo?si=d5ThaOhE20_Bwnjw)**
    
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

 ```js
// ============================================================
//  C O S M O S  —  partitura Strudel  v5
//  Estilo: Hans Zimmer / Interstellar
//  Arquitectura: capas independientes activadas con constantes
//
//  CÓMO USAR:
//  · Ejecuta TODO el archivo con play global al inicio.
//  · Para activar una capa: cambia su constante de 0 a 1
//    y ejecuta SOLO esa línea con Ctrl+Enter.
//  · Para silenciarla: cambia de 1 a 0 y Ctrl+Enter.
//  · El cambio es instantáneo y sin clicks porque
//    .postgain() hace el corte limpio en el motor de audio.
//
//  GUÍA DE LA OBRA:
//  ─────────────────────────────────────────────────────────
//  FASE 1  (~2:30)  Solo PIANO_ON = 1
//  T1      (~0:40)  Activa PEDAL_ON, ECO_ON
//  FASE 2  (~2:00)  Activa STRINGS_ON, BASS_ON
//                   Silencia ECO_ON
//  T2      (~0:30)  Activa BRASS_ON
//  FASE 3  (~1:40)  Activa ORGAN_ON, PULSAR_ON
//                   Sube STRINGS_ON (ya activo, el patrón cambia solo)
//  T3      (~1:00)  Silencia en orden: PULSAR_ON → ORGAN_ON
//                   → BRASS_ON → STRINGS_ON → BASS_ON
//  FASE 1' (~1:00)  Solo PIANO_ON queda — siléncialo al final
// ============================================================

setcpm(26)

// ── INTERRUPTORES — estos son los que cambias en vivo ──────
const PIANO_ON   = 1   // arranca aquí
const ECO_ON     = 0
const PEDAL_ON   = 0
const STRINGS_ON = 0
const BASS_ON    = 0
const BRASS_ON   = 0
const ORGAN_ON   = 0
const PULSAR_ON  = 0


// ── MOTIVOS ────────────────────────────────────────────────
// El piano usa .pick() para alternar entre 3 variantes
// del mismo motif — más denso en cada nivel
const mot1 = "<[0 ~ ~ ~] [~ ~ 4 ~] [~ 7 ~ ~] [~ ~ ~ 0]>"  // F1: muy disperso
const mot2 = "<[0 ~ 4 ~] [7 ~ 4 2] [0 4 ~ 7] [~ 2 0 ~]>"  // F2: más notas
const mot3 = "<[0 2 4 7] [2 4 7 11] [4 7 11 0] [7 11 0 4]>" // F3: denso


// ── PIANO PRINCIPAL ────────────────────────────────────────
// .pick() alterna entre mot1/mot2/mot3 cada 8 ciclos
// — el patrón evoluciona solo sin necesidad de cambiar nada
piano: note(
    "<0@8 1@8 2@8>".pick([mot1, mot2, mot3])
  )
  .scale("C:lydian")
  .sound("piano")
  .octave("<4@16 5@8>")        // sube a octava 5 en F3
  .attack(0.01)
  .release(3.0)
  .room(2.5).roomsize(10)
  .cutoff("<1600@16 3000@8>")  // cutoff sube en F3
  .postgain(PIANO_ON ? 0.6 : 0)


// ── ECO DEL PIANO ──────────────────────────────────────────
// Mismo motif pero retrasado y en octava alta — T1
eco: note(mot1)
  .scale("C:lydian")
  .sound("piano")
  .octave(5)
  .attack(0.01)
  .release(4.0)
  .late(0.38)
  .room(3).roomsize(10)
  .cutoff(900)
  .pan(0.55)
  .postgain(ECO_ON ? 0.07 : 0)


// ── PEDAL DE CUERDAS ───────────────────────────────────────
// Nota larga sostenida — entra en T1 como el primer "pad"
// attack de 4s: aparece sin que se note exactamente cuándo
pedal: note("<c2 g2 e2 b2>/8")
  .sound("strings")
  .attack(4.0)
  .release(6.0)
  .room(3).roomsize(10)
  .cutoff(400)
  .postgain(PEDAL_ON ? 0.18 : 0)


// ── CUERDAS ────────────────────────────────────────────────
// Acorde que sube de complejidad: dos notas → cuatro → cinco
strings: note(
    "<[c3,g3]@8 [c3,e3,g3,b3]@8 [c3,e3,g3,b3,d4]@8>"
  )
  .sound("gm_violin")
  .attack(1.8)
  .release(3.0)
  .room(2.5).roomsize(9)
  .cutoff(sine.range(500, 2000).slow(9))
  .pan(sine.range(-0.4, 0.4).slow(11))
  .postgain(STRINGS_ON ? 0.32 : 0)


// ── BAJO ───────────────────────────────────────────────────
// Centro, sin paneo — pulso que respira
bass: note("<c1 ~ c1 ~ g0 ~ c1 ~>/2")
  .sound("sine")
  .attack(0.06)
  .release(1.2)
  .lpf(160)
  .room(1.5)
  .postgain(BASS_ON ? 0.35 : 0)


// ── METALES SUAVES (french horn) ───────────────────────────
// Notas largas en la octava media — entra en T2
brass: note("<c3 ~ g3 ~ e3 ~ b2 ~>/4")
  .sound("gm_french_horn")
  .attack(2.5)
  .release(4.0)
  .room(2.8).roomsize(10)
  .cutoff(sine.range(400, 1400).slow(13))
  .pan(sine.range(-0.35, 0.35).slow(8))
  .postgain(BRASS_ON ? 0.28 : 0)


// ── ÓRGANO ─────────────────────────────────────────────────
// La pared de sonido de Zimmer — attack 5s, aparece como niebla
organ: note("<c2 ~ g2 ~>/8")
  .sound("organ")
  .attack(5.0)
  .release(7.0)
  .cutoff(sine.range(300, 900).slow(10))
  .room(3).roomsize(10)
  .postgain(ORGAN_ON ? 0.38 : 0)


// ── PULSAR ─────────────────────────────────────────────────
// Grave profundo, lento, sin paneo — como CP 1919
pulsar: note("<c0 ~ ~ ~ ~ ~ ~ ~>/1")
  .sound("bd")
  .attack(0.08)
  .release(3.5)
  .lpf(110)
  .room(3).roomsize(10)
  .postgain(PULSAR_ON ? 0.22 : 0)


// ── SHIMMER ────────────────────────────────────────────────
// Brillo en alturas — se activa con ORGAN_ON
shimmer: note("<e5 b5 g5 d6>/2")
  .sound("sine")
  .attack(2.5)
  .release(4.0)
  .lpf(3500)
  .room(3).roomsize(10)
  .pan(sine.range(-0.7, 0.7).slow(7))
  .postgain(ORGAN_ON ? 0.12 : 0)  // ligado al órgano — sube junto

// ============================================================
//  RESUMEN DE ACCIONES EN VIVO
//  ────────────────────────────
//  0:00   PIANO_ON=1  → play global
//  ~2:30  ECO_ON=1    PEDAL_ON=1
//  ~3:10  STRINGS_ON=1  BASS_ON=1  ECO_ON=0
//  ~5:10  BRASS_ON=1
//  ~5:40  ORGAN_ON=1  PULSAR_ON=1
//         (shimmer sube automáticamente con el órgano)
//  ~7:20  PULSAR_ON=0
//  ~7:40  ORGAN_ON=0  (shimmer baja automáticamente)
//  ~8:00  BRASS_ON=0
//  ~8:20  STRINGS_ON=0  BASS_ON=0
//  ~9:00  PIANO_ON=0  → dejar morir el reverb
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
