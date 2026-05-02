# Descripción general de ShackSwitch

El applet ShackSwitch permite controlar un conmutador de antenas ShackSwitch directamente desde AetherSDR. Úselo para asignar antenas a uno o dos puertos de entrada, configurar una carga ficticia para protección en transmisión y abrir la interfaz web del dispositivo, todo sin salir de la aplicación.

## Antes de comenzar

- El dispositivo ShackSwitch debe estar presente en su red LAN o agregado a través de la pestaña Peripherals en `Settings > Radio Setup...`. AetherSDR descubre los dispositivos ShackSwitch automáticamente mediante el protocolo AG UDP.
- El panel del applet debe estar visible. Si no lo está, active `View > Applet Panel`.

## Cómo funciona

AetherSDR escucha en la red LAN un dispositivo que se identifique como ShackSwitch. Cuando se encuentra uno, el applet ShackSwitch aparece automáticamente en el Applet Panel. Alterne su visibilidad usando el botón de bandeja ShackSwitch en la barra lateral derecha.

El applet muestra cada antena que el dispositivo reporta como una fila en una lista. Cada fila tiene un botón [A] y, en dispositivos de doble puerto, un botón [B]. Al hacer clic en [A] o [B] se enruta esa antena al puerto de entrada correspondiente. La tarjeta INPUT A (resaltada en cian) y la tarjeta INPUT B (resaltada en naranja) muestran siempre la banda y el nombre de antena actuales para cada puerto.

Si ambos puertos están asignados a la misma antena, los botones [A] y [B] afectados parpadean en ámbar para señalar el conflicto. Cuando se configura una carga ficticia, el Puerto B se enruta automáticamente a la carga ficticia en lugar de a la antena seleccionada mientras esa condición esté activa; el botón [B] de la fila prevista parpadea en ámbar y el botón [B] de la fila de carga ficticia parpadea en naranja para indicar el redireccionamiento automático.

En dispositivos de un solo puerto (R4), la tarjeta INPUT B y la columna B se ocultan por completo.

## Qué hace cada control

| Control | Comportamiento | Ajuste persistente |
|---|---|---|
| Etiqueta de estado | Muestra la dirección IP del dispositivo conectado y la versión de firmware, o un mensaje de desconexión. | — |
| Tarjeta INPUT A | Muestra la banda y el nombre de antena asignados actualmente al Puerto A. Resaltada en cian. Muestra — cuando no hay antena seleccionada. | — |
| Tarjeta INPUT B | Muestra la banda y el nombre de antena asignados actualmente al Puerto B. Resaltada en naranja. Muestra — cuando no hay antena seleccionada. Oculta en dispositivos de un solo puerto (R4). | — |
| Botón [A] (por fila de antena) | Selecciona esa antena para el Input A. Haga clic de nuevo para deseleccionar. Parpadea en ámbar cuando el Puerto A y el Puerto B están asignados a la misma antena. | — |
| Botón [B] (por fila de antena) | Selecciona esa antena para el Input B. Haga clic de nuevo para deseleccionar. Parpadea en ámbar en caso de conflicto. Parpadea en naranja en la fila de carga ficticia cuando el Puerto B se enruta automáticamente allí. | — |
| Selector de carga ficticia | Abre un menú para asignar una antena como carga ficticia o borrar la asignación. Cuando está configurado, el Puerto B se enruta automáticamente a esa antena para proteger la ruta de transmisión. Se almacena como un ID de antena entero; -1 significa que no hay carga ficticia configurada. | `SS_DummyLoadAnt` |
| Settings ⚙ | Abre la interfaz de configuración web del dispositivo ShackSwitch en el navegador del sistema. Usa la IP del dispositivo activo cuando está conectado; si no, recurre a `SS_ManualIp`. El puerto proviene de la baliza del dispositivo, `SS_WebPort`, o toma el valor predeterminado 5000. | `SS_ManualIp`, `SS_WebPort` |

`SS_ControlPort` establece el puerto de control UDP utilizado para comunicarse con el dispositivo.

## Relacionado

- [Seleccionar una antena para ShackSwitch Input A](select-an-antenna-for-shackswitch-input-a.md)
- [Seleccionar una antena para ShackSwitch Input B](select-an-antenna-for-shackswitch-input-b.md)
- [Configurar una antena de carga ficticia para proteger la ruta de transmisión](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
- [Resolver un conflicto de antena entre Input A e Input B](resolve-an-input-a-and-input-b-antenna-conflict.md)
- [Abrir la interfaz de configuración web de ShackSwitch](open-the-shackswitch-web-configuration-interface.md)
