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

- **Proceso de creación del audio generativo.**
- **Decisiones técnicas y estéticas que se tomaron y por qué.**
- **Código completo de la pieza de audio.**
- **Instrucciones paso a paso para reproducir la audio.**

## Bitácora de reflexión

### Actividad 04

- Evalúa si el audio generativo que creaste logra la intención estética que planteaste en tu concepto. ¿Qué ajustarías?
- Actualiza el diagrama de sistema de tu obra incorporando los detalles reales de la implementación del audio.
- Describe los principales desafíos que enfrentaste y cómo los resolviste.
