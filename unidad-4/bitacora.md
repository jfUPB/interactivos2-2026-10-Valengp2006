# Unidad 4

## Bitácora de proceso de aprendizaje

### Actividad 02

En esta actividad he diseñado e implementado un sistema que permite al público participar activamente en mi pieza audiovisual interactiva. Los participantes pueden controlar en tiempo real los colores de diferentes instrumentos musicales, convirtiéndose en co-creadores de la experiencia visual.

#### Sistema elegido: Control grupal por instrumentos

He decidido implementar un sistema donde **grupos de personas controlan colaborativamente el color de un instrumento específico**. Cada grupo tiene acceso exclusivo a los controles de su instrumento asignado, evitando conflictos entre diferentes elementos visuales.

#### Justificación

Esta aproximación ofrece varios beneficios:

**Participación significativa:** Cada grupo tiene un impacto claro y visible en la pieza, lo que aumenta el sentido de agencia y conexión con la obra.

**Organización clara:** Al asignar instrumentos específicos a cada grupo, se evita el caos que podría surgir si todos controlaran todos los elementos simultáneamente.

**Colaboración interna:** Dentro de cada grupo, los participantes deben negociar y decidir colectivamente los cambios visuales, fomentando la interacción social.

**Escalabilidad:** El sistema funciona igualmente bien con 5 participantes individuales o con 5 grupos de varias personas cada uno.

**Sencillez técnica:** No requiere programación adicional, solo configuración de la interfaz existente.

#### Flujo de datos

El flujo de información en el sistema es el siguiente:

1. **Strudel** genera eventos de audio (notas, ritmos, timbres)
2. Estos eventos se envían vía OSC al puerto 8081
3. **Las visuales** reciben estos eventos y generan animaciones sincronizadas
4. **El público** mueve controles en sus dispositivos
5. **Open Stage Control** recibe estos cambios en el puerto 8083
6. **Las visuales** actualizan los colores según los controles del público
7. El resultado final es una pieza donde el audio está preprogramado pero las visuales son co-creadas en tiempo real

#### Implementación Técnica

##### Cambios necesarios en el código

**Importante:** No es necesario modificar el código HTML de las visuales. El sistema funciona con el código existente que ya recibe mensajes OSC en el puerto 8083.

##### Configuración de Open Stage Control

La única modificación necesaria es en la forma de iniciar Open Stage Control.

**Comando anterior (solo local):**
```bash
open-stage-control -s localhost:8083 -t localhost:8081
```

**Comando nuevo (accesible en red):**
```bash
open-stage-control -s 0.0.0.0:8083 -t localhost:8081
```

**Explicación del cambio:**
- `localhost` solo permite conexiones desde la misma computadora
- `0.0.0.0` permite conexiones desde cualquier dispositivo en la misma red WiFi
- El resto de los parámetros permanecen iguales

#### Obtener la dirección IP

Para que el público pueda conectarse, necesitan conocer la dirección IP de mi computadora en la red local.

**En Mac:**
```bash
ifconfig | grep "inet "
```
#### Sistema de Acceso mediante Códigos QR

Escribir URLs largas en dispositivos móviles es propenso a errores y consume tiempo. Los códigos QR simplifican este proceso significativamente.

#### Funcionamiento

1. Abro el archivo en mi navegador
2. Si es necesario, ajusto la dirección IP en la línea 88 del código
3. Proyecto la página en pantalla
4. Hago clic en el instrumento deseado (ej: "Piano")
5. Aparece el código QR correspondiente
6. El grupo asignado escanea el QR con sus celulares
7. Acceden automáticamente a su interfaz específica

## Bitácora de aplicación 



## Bitácora de reflexión
