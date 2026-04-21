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

### Diagrama de Sistema (Propuesta de flujo)
El sistema opera bajo una arquitectura de red local para el performer y una capa web para el público:

1.  **Capa de Usuario (Público):** Navegador móvil → Socket.io → Servidor de Control.
2.  **Capa de Control (Performer):** Interfaz Open Stage Control (OSC) → TouchDesigner.
3.  **Capa de Salida:** TouchDesigner recibe los valores del *slider* (vórtice) y del *color picker* (luna) para renderizar los cambios visuales, mientras mantiene la sincronía con el audio de Strudel.

### Plan de Implementación

| Orden | Fase | Acción Técnica |
| :--- | :--- | :--- |
| **01** | **Infraestructura de Red** | Configurar el servidor de **Open Stage Control** y habilitar el puente de **Socket.io** para la recepción de datos externos. |
| **02** | **Desarrollo de Interfaces** | Diseñar el slider para el performer y el controlador de color para el público en el editor de Open Stage Control. |
| **03** | **Lógica en TouchDesigner** | Mapear los mensajes OSC entrantes a los operadores correspondientes (ej. un `Cross TOP` para el vórtice y un `Constant CHOP` para el color de la luna). |
| **04** | **Sincronización y Test** | Realizar pruebas de estrés conectando varios celulares para verificar que el cambio de color de la luna sea fluido y no interfiera con el slider del performer. |

## Bitácora de aplicación 


## Bitácora de reflexión
