# Unidad 6

## Bitácora de proceso de aprendizaje

### Actividad 01

#### Preguntas

- **¿Qué tipo de visuales van a acompañar tu audio? (formas geométricas, partículas, texturas orgánicas, arte generativo abstracto, representaciones figurativas, etc.)**

  Las visuales que van a acompañar mi audio son particulas y algunas texturas organicas que representen diferentes cosas. El proyecto esta dividido en 3 fases, comenzando en la fase 1 con un fondo unicolor que asemeje al espacio y particulas dispersas que representen las estrellas; continuando con la fase 2, tendriamos la aparecion de formas abstractas similares nubes que representan nebulosas espaciales, comenzando a darle algo de peso a las visuales mientras el audio tambien sube la intensidad; finalmente, en la fase 3 aparecerian figuras un poco mas circulares que asemejen planetas, agujeros negros y demas cuerpos celestes para dar una sensacion de asombro al usuario a medida que la musica se vuelve mas epica y por tanto las visuales tambien.
  
- **¿Qué paleta de colores usarás y por qué?**

  Usaré paletas de colores alrededor del morado, rosado y naranja, ya que estos colores son los que se visualizan comunmente en las imagenes que tenemos del espacio. 
  
- **¿Cómo reaccionarán las visuales al audio? (¿Qué parámetros del audio controlarán qué aspectos visuales?)**

  ##### Fase 1 — El vacío respira

  **Piano (`PIANO_ON`, motivos mot1 → mot3)**
  - **Tipo de vínculo:** ON/OFF + reactivo
  - **Elemento visual:** Partículas de polvo estelar muy dispersas, casi estáticas. Cada nota dispara un destello puntual de luz.
  - **Parámetro reactivo:** Amplitud del piano → tamaño del destello. A medida que evoluciona mot1 → mot3, la densidad de partículas sube   automáticamente.

  **Eco (`ECO_ON`, delay 0.38s)**
  - **Tipo de vínculo:** ON/OFF
  - **Elemento visual:** Un segundo anillo de destellos más tenue, desplazado en el espacio. El eco visual de cada nota del piano.
  - **Parámetro reactivo:** Sin reactividad continua — la aparición ya es el efecto. El delay de 0.38s crea una separación espacial natural entre nota y eco visual.

  **Pedal (`PEDAL_ON`, attack 4s)**
  - **Tipo de vínculo:** ON/OFF
  - **Elemento visual:** Una nébula de fondo muy tenue — un velo morado casi imperceptible que llena el espacio gradualmente.
  - **Parámetro reactivo:** El attack de 4s se traduce directo: el velo hace un fade-in de 4 segundos, igual que el audio. Sin reactividad rítmica.

  ##### Fase 2 — La materia se organiza

  **Strings (`STRINGS_ON`, cutoff con sine 500→2000Hz, ciclo 9s)**
  - **Tipo de vínculo:** ON/OFF + reactivo
  - **Elemento visual:** Las partículas comienzan a orbitar — aparecen centros de gravedad y las partículas se agrupan formando filamentos.
  - **Parámetro reactivo:** El sine que mueve el cutoff controla el radio de las órbitas. Cutoff alto = órbitas más abiertas y rápidas.

  **Bajo (`BASS_ON`, notas c1/g0, sine puro)**
  - **Tipo de vínculo:** ON/OFF + reactivo
  - **Elemento visual:** Pulso de expansión radial — cada nota genera una onda circular que se propaga desde el centro hacia afuera.
  - **Parámetro reactivo:** Amplitud del bajo → radio máximo de la onda. Es el vínculo más físico y directo: lo que se escucha se ve al instante.

  ##### Transición Fase 2 → 3

  **Metales / Brass (`BRASS_ON`, french horn, attack 2.5s, cutoff sine 400→1400Hz ciclo 13s)**
  - **Tipo de vínculo:** ON/OFF + reactivo
  - **Elemento visual:** Arcos de luz que atraviesan la nébula, como chorros de gas ionizado. Aparecen lentamente (2.5s) igual que el audio.
  - **Parámetro reactivo:** El sine del cutoff + el paneo (ciclo 8s) mueven la dirección y el color de los arcos: de rosa a naranja.

  ##### Fase 3 — Ignición

  **Órgano (`ORGAN_ON`, attack 5s, "pared de sonido")**
  - **Tipo de vínculo:** ON/OFF + reactivo
  - **Elemento visual:** La nébula entera se ilumina — el fondo pasa de morado oscuro a naranja/rosa profundo, como una nebulosa del Hubble en plena formación.
  - **Parámetro reactivo:** El cutoff (300→900Hz, ciclo 10s) controla la saturación del color: cutoff bajo = morado frío, cutoff alto = naranja cálido.

  **Pulsar (`PULSAR_ON`, c0, cada 8 tiempos)**
  - **Tipo de vínculo:** ON/OFF + reactivo
  - **Elemento visual:** Flash blanco total — un destello que ilumina toda la pantalla por un instante, como una estrella de neutrones pulsando.
  - **Parámetro reactivo:** Completamente rítmico: cada golpe del pulsar = un flash. Sin reactividad de amplitud — el ritmo lento ya es el efecto.

  **Shimmer (ligado a `ORGAN_ON`, notas e5/b5/g5/d6)**
  - **Tipo de vínculo:** Reactivo (sube y baja junto con el órgano)
  - **Elemento visual:** Destellos de alta frecuencia en los bordes de la nébula — chispas en las puntas de los filamentos de gas.
  - **Parámetro reactivo:** El paneo lento (ciclo 7s) mueve los destellos de izquierda a derecha. Al apagar el órgano, el shimmer desaparece junto con él.
  
- **¿Por qué estas decisiones estéticas sirven al concepto de tu obra?**

  Porque el concepto principal de mi obra esta alrdedor del espacio, ya que esta fue mi inspiracion inicial, y este tipo de texturas y colores son comunmente en las imagenes que conoces del espacio exterior.

#### Bocetos o mockups de cómo imaginas las visuales.

##### Fase 1:
<img width="129" height="281" alt="Captura de pantalla 2026-04-09 a la(s) 8 35 39 a m" src="https://github.com/user-attachments/assets/e5b4abdd-f7c8-4561-9ec2-236eb00c6a2f" />
<img width="133" height="233" alt="Captura de pantalla 2026-04-09 a la(s) 8 35 57 a m" src="https://github.com/user-attachments/assets/4d7ce362-f634-4fa1-bd23-e5c35c85be78" />
<img width="125" height="280" alt="Captura de pantalla 2026-04-09 a la(s) 8 36 16 a m" src="https://github.com/user-attachments/assets/5adddcb4-50d3-4584-9026-0ca955f6510d" />

##### Fase 2:
<img width="131" height="232" alt="Captura de pantalla 2026-04-09 a la(s) 8 36 48 a m" src="https://github.com/user-attachments/assets/ce0373a7-b757-4253-a829-b1c2c6dfcc12" />
<img width="127" height="283" alt="Captura de pantalla 2026-04-09 a la(s) 8 37 00 a m" src="https://github.com/user-attachments/assets/abc8a38f-18f3-4dfb-b62f-5c2e541747d1" />
<img width="131" height="232" alt="Captura de pantalla 2026-04-09 a la(s) 8 37 14 a m" src="https://github.com/user-attachments/assets/ce43fb7c-6a5c-43eb-8bec-963e980c8c7c" />

##### Fase 3:
<img width="413" height="404" alt="Captura de pantalla 2026-04-09 a la(s) 8 31 39 a m" src="https://github.com/user-attachments/assets/6f43e5ef-db2c-44e3-9410-23dae345d581" />
<img width="130" height="226" alt="Captura de pantalla 2026-04-09 a la(s) 8 37 40 a m" src="https://github.com/user-attachments/assets/95e66f17-6f38-41fc-a85f-87715a4bdc3b" />
<img width="131" height="213" alt="Captura de pantalla 2026-04-09 a la(s) 8 37 51 a m" src="https://github.com/user-attachments/assets/362c898f-9c8d-4ce8-b6c8-f07bfa1c103f" />

#### Mapeo entre parámetros de audio y parámetros visuales (por ejemplo: frecuencia → color, amplitud → tamaño, etc.).

| Mensaje OSC       | Fuente en Strudel         | Efecto en TouchDesigner                        |
|-------------------|---------------------------|------------------------------------------------|
| `/piano/amp`      | Amplitud del piano        | Tamaño de destellos de partículas              |
| `/piano/density`  | Índice de motivo (0/1/2)  | Densidad del sistema de partículas             |
| `/bass/amp`       | Amplitud del bajo         | Radio de onda de expansión radial              |
| `/strings/cutoff` | Sine cutoff (500→2000Hz)  | Radio de órbita de partículas                  |
| `/brass/cutoff`   | Sine cutoff (400→1400Hz)  | Color y dirección de arcos de luz              |
| `/brass/pan`      | Sine paneo (ciclo 8s)     | Posición espacial de los arcos                 |
| `/organ/cutoff`   | Sine cutoff (300→900Hz)   | Saturación de color de la nébula               |
| `/pulsar/trigger` | Evento rítmico del pulsar | Flash blanco total                             |
| `/shimmer/pan`    | Sine paneo (ciclo 7s)     | Posición de destellos en bordes de filamentos  |
| `/phase`          | Constantes ON/OFF         | Cambio de modo visual completo (1 / 2 / 3)    |

#### Referentes:

- [Luna en TouchDesigner](https://youtu.be/rLuFBhFJhVU?si=RkDOio56kWYmA5yY)
- [Estrella grande](https://youtu.be/WS2Ww6zYgJw?si=cYvuc4DIO2Bl3VUJ)
- [Nube de particulas](https://youtu.be/Jz-irdEYUZM?si=nubdSfaiuVqoo2ni)
- [Nebulosas](https://youtu.be/SlVoPnsQlbU?si=_75DR91a-v6VKFyQ)

### Actividad 02

#### Exploración de técnicas y prototipos

Durante esta etapa exploré diferentes técnicas dentro de TouchDesigner, comenzando con procesamiento de imagen en tiempo real mediante el uso de TOPs, y posteriormente avanzando hacia sistemas de partículas (POPs) para lograr resultados más complejos.

Inicialmente realicé pruebas básicas guiadas por una IA, con el objetivo de comprender el funcionamiento general del software, especialmente en la manipulación de texturas y flujos visuales.

A partir de estas bases, pasé a seguir tutoriales más avanzados de YouTube enfocados en el uso de partículas.

Como resultado, logré desarrollar un prototipo visual compuesto por:
	•	Una luna generada con partículas
	•	Un vórtice dinámico
	•	Un cúmulo de estrellas

**Evidencia – Prototipo Luna**

<img width="702" height="384" alt="Grabación de pantalla 2026-04-16 a la(s) 9 58 41 a" src="https://github.com/user-attachments/assets/287fbdde-ab30-4e64-92bd-cf3bc2123f46" />

**Evidencia – Vórtice y estrellas**

<img width="694" height="388" alt="Grabación de pantalla 2026-04-16 a la(s) 10 05 51 a" src="https://github.com/user-attachments/assets/15a66504-33f7-4173-bd61-0da642c416c7" />

#### Resultados y ajustes

Durante el proceso surgieron varios problemas técnicos. Uno de los principales fue que los elementos visuales no se renderizaban de forma independiente: la textura de la luna se estaba aplicando también al vórtice.

Para solucionar esto, opté por organizar el proyecto en containers separados, dejando la luna en uno y el vórtice junto con las estrellas en otro. Esta decisión permitió aislar correctamente cada sistema visual y controlar mejor los renders.

**Evidencia – Solución con containers**

En cuanto a la integración de audio y visuales, enfrenté múltiples dificultades. Aunque lograba recibir mensajes desde el websocket, no estaba capturando correctamente los eventos enviados desde Strudel.

Intenté reiniciar el proceso desde cero utilizando el ejemplo proporcionado por el profesor y apoyándome nuevamente en IA, pero el problema persistió. Finalmente, con ayuda del profesor en clase, logré establecer correctamente la conexión.

#### Técnica seleccionada y justificación

La técnica principal elegida para mi obra es la combinación de sistemas de partículas (POPs) con procesamiento de imagen en tiempo real, integrada con reactividad al audio.

Esta combinación me permite:
- Generar visuales más orgánicos y dinámicos (partículas)
- Mantener control sobre la estética visual (TOPs)
- Crear una relación directa entre sonido e imagen (audio-reactividad)

Como resultado final del prototipo, logré que la luna reaccionara al audio: específicamente, cada vez que se activa un bombo, la luna parpadea, estableciendo una conexión clara entre lo sonoro y lo visual.

## Bitácora de aplicación 


## Bitácora de reflexión
