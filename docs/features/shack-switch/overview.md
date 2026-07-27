# Descripción general de ShackSwitch

El applet ShackSwitch le permite controlar un conmutador de antena ShackSwitch directamente desde AetherSDR. Úselo para asignar antenas a uno o dos puertos de entrada, configurar una carga fantasma para protección en transmisión y abrir la interfaz web del dispositivo, todo sin salir de la aplicación.

## Antes de comenzar

- Debe haber un dispositivo ShackSwitch presente en su LAN o agregado a través de la pestaña Periféricos en `Settings > Radio Setup...`. AetherSDR descubre dispositivos ShackSwitch automáticamente mediante el protocolo AG UDP.
- El panel del applet debe estar visible. Si no lo está, verifique `View > Applet Panel`.

## Cómo funciona

AetherSDR escucha en la LAN un dispositivo que se identifique como ShackSwitch. Cuando se encuentra uno, el applet ShackSwitch aparece automáticamente en el Panel de applets. Alterne su visibilidad usando el botón de bandeja ShackSwitch en la barra lateral derecha.

El applet presenta cada antena que el dispositivo informa como una fila en una lista. Cada fila tiene un botón [A] y, en dispositivos de dos puertos, un botón [B]. Al hacer clic en [A] o [B] se enruta esa antena al puerto de entrada correspondiente. La tarjeta INPUT A (resaltada en cian) y la tarjeta INPUT B (resaltada en naranja) siempre muestran la banda y el nombre de la antena actuales para cada puerto.

Si ambos puertos están asignados a la misma antena, los botones [A] y [B] afectados parpadean en ámbar para señalar el conflicto. Cuando se configura una carga fantasma, el Puerto B se enruta automáticamente a la carga fantasma en lugar de a la antena seleccionada mientras esa condición esté activa; el botón [B] de la fila prevista parpadea en ámbar y el botón [B] de la fila de la carga fantasma parpadea en naranja para indicar el re-enrutamiento automático.

En dispositivos de un solo puerto (R4), la tarjeta INPUT B y la columna B están ocultas por completo.

## Qué hace cada control

| Control | Comportamiento | Configuración persistente |
|---|---|---|
| Etiqueta de estado | Muestra la dirección IP del dispositivo conectado y la versión de firmware, o un mensaje de desconexión. | — |
| Tarjeta INPUT A | Muestra la banda y el nombre de la antena actualmente asignados al Puerto A. Resaltada en cian. Muestra — cuando no hay antena seleccionada. | — |
| Tarjeta INPUT B | Muestra la banda y el nombre de la antena actualmente asignados al Puerto B. Resaltada en naranja. Muestra — cuando no hay antena seleccionada. Oculta en dispositivos de un solo puerto (R4). | — |
| Botón [A] (por fila de antena) | Selecciona esa antena para la Entrada A. Haga clic de nuevo para anular la selección. Parpadea en ámbar cuando el Puerto A y el Puerto B están ambos asignados a la misma antena. | — |
| Botón [B] (por fila de antena) | Selecciona esa antena para la Entrada B. Haga clic de nuevo para anular la selección. Parpadea en ámbar en caso de conflicto. Parpadea en naranja en la fila de la carga fantasma cuando el Puerto B se enruta automáticamente allí. | — |
| Selector de carga fantasma | Selecciona o anula la selección de una antena como carga fantasma. Cuando está configurada, el Puerto B se enruta automáticamente a la carga fantasma para proteger la antena al transmitir. Se almacena como ID de antena entero. -1 significa que no hay carga fantasma configurada. | `SS_DummyLoadAnt` |
| Configuración ⚙ | Abre la interfaz de configuración web del dispositivo ShackSwitch en el navegador del sistema. Usa la dirección del par activo cuando está conectado; en caso contrario, usa `SS_ManualIp`. El puerto se determina mediante `SS_WebPort`, el puerto web de la baliza o el valor predeterminado 5000. | `SS_ManualIp`, `SS_WebPort` |

`SS_ControlPort` establece el puerto de control UDP utilizado para comunicarse con el dispositivo.

## Relacionados

- [Seleccionar una antena para la Entrada A de ShackSwitch](select-an-antenna-for-shackswitch-input-a.md)
- [Seleccionar una antena para la Entrada B de ShackSwitch](select-an-antenna-for-shackswitch-input-b.md)
- [Configurar una antena de carga fantasma para proteger la ruta de transmisión](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
- [Resolver un conflicto entre antenas de Entrada A y Entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md)
- [Abrir la interfaz de configuración web de ShackSwitch](open-the-shackswitch-web-configuration-interface.md)
