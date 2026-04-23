# Unidad 7

## Bitácora de proceso de aprendizaje
### Actividad 01

#### 1. ¿Qué parámetros de tu obra se van a controlar en tiempo real?

La interacción se centrará exclusivamente en **parámetros visuales** dentro de TouchDesigner. El objetivo es manipular la morfología y la estética del entorno espacial sin intervenir directamente en la composición generativa de audio de Strudel en esta etapa.

#### 2. ¿Quién controla qué?

Se establece una jerarquía de control dividida entre la narrativa de la obra y el detalle estético:
-  **Performer:** Maneja la transición estructural de la atmósfera mediante un *slider* maestro. Este controla el paso gradual entre un **fondo de estrellas estático/profundo** y un **vórtice dinámico**.
-  **Público:** Posee un control sobre un elemento focal de la composición, teniendo la capacidad de **cambiar el color de la luna** en tiempo real.

#### 3. ¿Cómo participará el público?

La participación será remota y directa a través de sus **dispositivos móviles**. Los usuarios enviarán **datos de color** (RGB/Hex) interactuando con un controlador visual (color picker) alojado en una interfaz web.

#### 4. ¿Qué dispositivos se usarán?

-  **Open Stage Control:** Como servidor de control central y plataforma para la interfaz del performer.
-  **Smartphone (Público):** Conexión vía **Socket.io** para garantizar una comunicación bidireccional de baja latencia entre la web y el sistema de control.

### Diagrama de Sistema 

<img width="1920" height="1080" alt="Diseño sin título" src="https://github.com/user-attachments/assets/4cdb43a1-7ef2-4401-aa93-a2dcbd995e07" />

### Plan de Implementación

| Orden | Fase | Acción Técnica |
| :--- | :--- | :--- |
| **01** | **Infraestructura de Red** | Configurar el servidor de **Open Stage Control** y habilitar el puente de **Socket.io** para la recepción de datos externos. |
| **02** | **Desarrollo de Interfaces** | Diseñar el slider para el performer y el controlador de color para el público en el editor de Open Stage Control. |
| **03** | **Lógica en TouchDesigner** | Mapear los mensajes OSC entrantes a los operadores correspondientes (ej. un `Cross TOP` para el vórtice y un `Constant CHOP` para el color de la luna). |
| **04** | **Sincronización y Test** | Realizar pruebas de estrés conectando varios celulares para verificar que el cambio de color de la luna sea fluido y no interfiera con el slider del performer. |

### Actividad 02

#### 1. Superficie de Control (Performer)

Este subsistema centraliza la manipulación de la narrativa visual de la obra.

- **Implementación:** Se ha configurado un servidor local mediante Open Stage Control. Se diseñó una interfaz personalizada que incluye un slider maestro encargado de la transición entre los dos estados visuales de la obra (Estrellas $\leftrightarrow$ Vórtice). El diseño se ha pensado para ser operado desde un iPad, permitiendo una interacción táctil independiente mientras la computadora principal procesa el renderizado de TouchDesigner y el audio de Strudel.
- **Mapeo Técnico:** La señal del slider se envía vía protocolo OSC al puerto de entrada de TouchDesigner, donde un nodo OSC In CHOP recibe los valores normalizados ($0.0$ a $1.0$) para controlar el mix de los operadores visuales.

#### 2. Participación del Público (Socket.io + Celular)

Este subsistema permite la interacción colectiva mediante la modificación cromática de la luna.

- **Implementación:** Se está desarrollando una página web minimalista alojada en un servidor local. Esta interfaz presenta un slider interactivo diseñado para ser visualmente atractivo y coherente con la temática espacial. La comunicación se realiza mediante Socket.io, lo que permite que el envío de datos desde el navegador del celular del usuario sea casi instantáneo.
- **Mapeo Técnico:** El servidor recibe el valor del color/posición del slider y lo reenvía a TouchDesigner (o vía Open Stage Control) para actualizar el color del objeto "Luna" en tiempo real.

#### Proceso de implementación por subsistemas y pruebas de funcionamiento

El desarrollo se ha ejecutado de forma modular siguiendo este orden cronológico:

- **Motor de Audio**: Programación de la partitura y grupos instrumentales en Strudel.
- **Motor Visual:** Creación de los sistemas de partículas y lógica de renderizado en TouchDesigner.
- **Puente Audio-Visual:** Sincronización de señales de Strudel hacia TouchDesigner.
- **Control Performer:** Integración del slider OSC para el cambio de escenas.
- **Control Público:** Desarrollo de la capa de Socket.io (en ejecución).

**Pruebas de funcionamiento independiente**

Para garantizar la estabilidad del sistema, se realizaron las siguientes validaciones:

- **Validación de Visuales:** Se utilizó el pre-render dentro de TouchDesigner para simular cómo se comportarían los materiales y partículas ante cambios de valores, asegurando que la transición fuera fluida antes de conectar el hardware externo.
- **Prueba de Recepción de Datos:** Se emplearon nodos OSC In CHOP y DAT para verificar que las señales provenientes de Open Stage Control llegaran con la precisión necesaria y sin pérdida de paquetes en la red local.

#### Problemas Encontrados y SolucionesEstado: 

Hasta el momento, la implementación ha avanzado sin problemas técnicos críticos.Estrategia de Resolución: 

- Se ha mantenido una arquitectura limpia y modular.
- Al probar cada subsistema por separado (primero audio, luego visual, luego control), se ha evitado la acumulación de errores en la fase de integración.
- El siguiente paso crítico será la configuración de red para asegurar que el iPad y los celulares del público se comuniquen sin restricciones de Firewall o latencia.

## Bitácora de aplicación 


## Bitácora de reflexión
