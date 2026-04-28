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

### Actividad 3

Fecha: [28 de abril de 2026]

#### 1. Proceso de Integración de Componentes

La integración del sistema se realizó de manera progresiva, organizando el flujo en tres capas principales: audio, performer y público. El objetivo fue validar cada componente de forma independiente antes de conectarlos entre sí.

##### 1.1 Capa de Audio (Strudel)

Se inició el sistema ejecutando Strudel, verificando:

- Correcta reproducción del audio.
- Envío de eventos rítmicos vía OSC al puerto 8080.

Estos eventos controlan el parpadeo de la Luna en TouchDesigner, sincronizado con el bombo.

**Captura 1: Interfaz de Strudel.**

<img width="1349" height="673" alt="Captura de pantalla 2026-04-28 a la(s) 9 57 54 a m" src="https://github.com/user-attachments/assets/dac58c5b-7659-4ec4-a018-db47215115f7" />


##### 1.2 Capa Visual (TouchDesigner)

Posteriormente, se abrió el proyecto en TouchDesigner para validar:

- Carga correcta de todas las visuales.
- Funcionamiento de la Luna como indicador principal de sincronización.

Se comprobó que:

- La Luna responde al pulso del audio (parpadeo correcto).

Luego, se verificó el sistema interno de transición:

- Uso del slider interno para cambiar entre Estrellas y Vórtice.
- Transición fluida entre ambos estados visuales.

**Captura 2:Vista general de la red de nodos.**

<img width="1352" height="796" alt="Captura de pantalla 2026-04-28 a la(s) 10 00 00 a m" src="https://github.com/user-attachments/assets/63aebfbc-af78-478f-bb2b-61ea72038cc7" />

**Captura 3:Parámetros de la Luna reaccionando al audio.**

<img width="960" height="446" alt="Captura de pantalla 2026-04-28 a la(s) 10 01 05 a m" src="https://github.com/user-attachments/assets/f2a20710-e7f3-46be-a8a7-e320f2735cce" />

**Captura 4: Transición visual entre Estrellas y Vórtice.**

<img width="730" height="368" alt="Grabación de pantalla 2026-04-28 a la(s) 10 02 36 a" src="https://github.com/user-attachments/assets/fb58b6bd-1ee3-416b-abf8-c8d00ab5bcdd" />

##### 1.3 Capa del Performer (Open Stage Control)

Se integró el control externo mediante Open Stage Control en iPad:

- Configuración del puerto 8082 en Open Stage Control.
- Verificación del nodo oscin1 en TouchDesigner en el puerto 9000.

Pruebas realizadas:

- El slider permite la transición entre Estrellas ↔ Vórtice.
- El Vórtice cambia de color progresivamente:
  - Blanco → Gris → Negro
  - El botón Reset reinicia correctamente el ciclo cromático.

**Captura 5: Interfaz del iPad (slider + botón reset).**

<img width="477" height="517" alt="Captura de pantalla 2026-04-28 a la(s) 10 04 33 a m" src="https://github.com/user-attachments/assets/ceb84c05-9fea-4f6f-8b9c-1a888a3b09c1" />

**Captura 6: Recepción de datos en oscin1.**

<img width="660" height="557" alt="Captura de pantalla 2026-04-28 a la(s) 10 05 56 a m" src="https://github.com/user-attachments/assets/6f42336c-216c-4841-ba85-153dfae5132a" />

##### 1.4 Capa del Público (Node.js + Socket.io)

Se implementó la interacción del público mediante servidor local:

- Ejecución de node server.js.
- Acceso a la interfaz desde navegador.

Configuraciones utilizadas:

- Modo local: http://localhost:3000
- Modo hotspot: http://[IP]:3000

Se utilizó hotspot móvil para evitar problemas de red.

En TouchDesigner:

- Nodo oscin2 configurado en el puerto 7000.

Funcionalidad:

- El público puede modificar el color de la Luna en tiempo real.
- Flujo de datos: Celular → Socket.io → Node.js → OSC → TouchDesigner

**Captura 7: Terminal ejecutando server.js.**

<img width="574" height="380" alt="Captura de pantalla 2026-04-28 a la(s) 10 06 56 a m" src="https://github.com/user-attachments/assets/e1721f28-8509-4a58-a050-3da372858bf6" />

**Captura 8: Interfaz del público en celular.**

<img width="640" height="636" alt="Captura de pantalla 2026-04-28 a la(s) 10 08 56 a m" src="https://github.com/user-attachments/assets/74a59305-2e67-4df0-9dda-bd4ef2429dba" />

**Captura 9: Recepción en oscin2.**

<img width="363" height="296" alt="Captura de pantalla 2026-04-28 a la(s) 10 09 26 a m" src="https://github.com/user-attachments/assets/368283da-7916-44b2-a5d5-5bf3e19f8c7c" />

##### 1.5 Arquitectura General del Sistema

El sistema final se estructura en tres capas:

- **Audio (Strudel):** OSC puerto 8080 → control rítmico.
- **Performer (iPad):** OSC puerto 9000 → control estructural.
- **Público (Celular): **Socket.io → Node.js → OSC puerto 7000 → control cromático.

**Captura 10: Diagrama del flujo completo del sistema.**

<img width="1536" height="1024" alt="ChatGPT Image Apr 28, 2026, 10_26_10 AM" src="https://github.com/user-attachments/assets/84035e1e-fdfc-4c99-b8b9-314ce1e11ee9" />

#### 2. Resultados de Pruebas con Público Simulado

Hasta el momento, no se han realizado pruebas con público real ni simulado.

Sin embargo, se validó el sistema utilizando dispositivos propios (iPhone e iPad), comprobando que:

- La interfaz es accesible desde múltiples dispositivos.
- La interacción responde correctamente en tiempo real.

Esto permite inferir que el sistema está listo para pruebas con usuarios en una siguiente fase.

#### 3. Problemas Encontrados y Soluciones

##### 3.1 Conectividad de Red

**Problema:**

Las redes institucionales presentaban restricciones de visibilidad y posibles bloqueos por firewall, dificultando la comunicación entre dispositivos.

**Solución:**

Se implementó el uso de un hotspot móvil, lo que permitió:

- Conexión directa entre dispositivos.
- Eliminación de conflictos de red.

##### 3.2 Latencia

**Problema:**

Posible retraso en la transmisión de datos entre capas.

**Resultado:**

No se detectó latencia perceptible. La señal fluye de manera continua y sincronizada entre:

- Audio
- Visuales
- Controles

##### 3.3 Usabilidad

**Problema:**

Necesidad de verificar claridad en los controles del performer.

**Resultado:**

El sistema funciona correctamente desde la primera implementación:

- El slider es intuitivo.
- El botón de reset responde adecuadamente.
- La lógica de estados del Vórtice es clara y consistente.

#### 4. Código de la Obra Integrada

<aside>
Nota: El código completo se adjunta en los archivos del proyecto debido a su extensión.
</aside>


Se incluyen:

- Script de Strudel (.osc)
- Proyecto de TouchDesigner (.toe)
- Servidor Node.js (server.js)
- Interfaz de Open Stage Control

#### 5. Instrucciones para Reproducir la Obra

Para ejecutar el sistema completo, seguir los siguientes pasos:

**Paso 1: Iniciar Strudel**

- Ejecutar Strudel.
- Verificar audio activo.
- Confirmar envío OSC (puerto 8080).

**Paso 2: Abrir TouchDesigner**

- Abrir el archivo del proyecto.
- Verificar carga de visuales.
- Confirmar que la Luna reacciona al audio.

**Paso 3: Probar visuales internas**

- Usar slider interno.
- Validar transición Estrellas ↔ Vórtice.

**Paso 4: Conectar Open Stage Control**

- Abrir interfaz en iPad.
- Verificar puerto 8082.
- Confirmar recepción en oscin1 (puerto 9000).

**Paso 5: Probar control del performer**

- Mover slider → transición visual.
- Verificar cambio de color del Vórtice.
- Probar botón reset.

**Paso 6: Iniciar servidor**

```bash
node server.js
```

**Paso 7: Conectar público**

- Conectarse al hotspot.
- **Acceder a:** http://[IP]:3000
- Interactuar con la interfaz.

**Paso 8: Verificar interacción completa**

- Cambios de color en la Luna.
- Sincronización con audio.
- Flujo continuo entre dispositivos.

#### 6. Equipos Utilizados

- MacBook Pro (TouchDesigner + servidor)
- iPad Air (control del performer)
- iPhone (interacción del público)

## Bitácora de reflexión
