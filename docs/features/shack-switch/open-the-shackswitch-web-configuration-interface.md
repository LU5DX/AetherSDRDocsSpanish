# Abrir la interfaz de configuración web de ShackSwitch

El dispositivo ShackSwitch incluye una interfaz web integrada para la configuración a nivel de firmware. Esta página explica cómo abrir esa interfaz desde AetherSDR usando el botón "Settings ⚙" en el applet de ShackSwitch.

## Antes de comenzar

- El applet de ShackSwitch debe estar visible en el Panel de Applets. Aparece automáticamente cuando se descubre un dispositivo ShackSwitch en la LAN, o después de conectarse a través de la pestaña Peripherals en Radio Setup.
- Si el dispositivo no está conectado actualmente, AetherSDR utiliza como respaldo la dirección IP almacenada en `SS_ManualIp`. Configure ese valor antes de continuar si planea abrir la interfaz web mientras está desconectado.
- Su navegador del sistema debe poder alcanzar el dispositivo ShackSwitch en la red.

## Pasos

1. Localice el applet de ShackSwitch en el Panel de Applets, en el lado derecho de la ventana principal. Si no está visible, haga clic en el botón de la bandeja SS en la barra lateral derecha para mostrarlo.
2. Haga clic en "Settings ⚙" en la parte inferior del applet.
3. AetherSDR construye una URL a partir de la IP del dispositivo y el puerto web, y luego la abre en su navegador del sistema.

## Función de cada control

| Control | Comportamiento | Configuración persistente |
|---|---|---|
| Botón "Settings ⚙" | Abre la interfaz de configuración web del dispositivo ShackSwitch en el navegador del sistema. Usa la dirección del par activo cuando está conectado; utiliza `SS_ManualIp` como respaldo cuando está desconectado. El puerto se toma del webPort de la baliza del dispositivo cuando ese valor es superior a 1024; de lo contrario, se toma de `SS_WebPort`, con un valor de respaldo final de 5000. | — |
| `SS_ManualIp` | Dirección IP utilizada cuando no hay una conexión activa con el dispositivo. | `SS_ManualIp` |
| `SS_WebPort` | Puerto de la interfaz web utilizado cuando la baliza no anuncia un puerto válido (superior a 1024). Valor predeterminado: `5000`. | `SS_WebPort` |
| `SS_DummyLoadAnt` | Almacena el ID de la antena configurada como carga falsa. Se establece en `-1` cuando no hay ninguna carga falsa configurada. | `SS_DummyLoadAnt` |

## Controles de fila de antena

Cada antena en ShackSwitch aparece en su propia fila con los siguientes controles:

| Control | Comportamiento | Notas |
|---|---|---|
| Botón [A] (por fila de antena) | Selecciona esta antena para la Entrada A. La deselecciona si ya está seleccionada. | Parpadea en ámbar cuando el Puerto A y el Puerto B están asignados a la misma antena (conflicto). |
| Botón [B] (por fila de antena) | Selecciona esta antena para la Entrada B. La deselecciona si ya está seleccionada. | Parpadea en ámbar cuando hay conflicto. Cuando hay una carga falsa configurada y B se enruta automáticamente allí, el botón B de la fila prevista parpadea en ámbar y la fila de la carga falsa parpadea en naranja. |
| Selector de carga falsa | Selecciona o deselecciona una antena como carga falsa. Cuando está configurada, el Puerto B se enruta automáticamente a la carga falsa para proteger la antena durante la transmisión. | Se almacena como ID de antena entero. `-1` significa que no hay carga falsa configurada. |

## Indicadores de estado

| Indicador | Visualización | Significado |
|---|---|---|
| Etiqueta de estado | Muestra la dirección IP del dispositivo conectado y la versión del firmware, o un mensaje de desconexión. | Indica el estado de la conexión. |
| Tarjeta INPUT A | Muestra la banda actual y el nombre de la antena seleccionada en el Puerto A. Resaltada en cian. | Muestra `—` cuando no hay antena seleccionada. |
| Tarjeta INPUT B | Muestra la banda actual y el nombre de la antena seleccionada en el Puerto B. Resaltada en naranja. | Oculta en dispositivos de un solo puerto (R4). Muestra `—` cuando no hay antena seleccionada. |

## Consejos

- Si el dispositivo está conectado, AetherSDR usa automáticamente la dirección del par activo. No necesita configurar `SS_ManualIp` para la operación normal con conexión.
- El webPort de la baliza solo se considera válido cuando es superior a 1024. Si el firmware del dispositivo transmite el puerto 80 como marcador de posición, AetherSDR lo ignora y usa `SS_WebPort` o el valor predeterminado de 5000.
- Para abrir la interfaz web mientras la radio está fuera de línea, configure `SS_ManualIp` con la dirección IP estática del dispositivo con anticipación.
- Cuando hay una carga falsa configurada, AetherSDR enruta automáticamente la Entrada B a la carga falsa para proteger su antena principal durante la transmisión.

## Solución de problemas

- **El navegador se abre pero la página no carga** — El dispositivo puede estar en una subred diferente o detrás de un cortafuegos. Confirme que la IP mostrada en la etiqueta de estado del applet de ShackSwitch sea accesible desde su máquina. Verifique que el puerto (predeterminado `5000`) no esté bloqueado.
- **No sucede nada al hacer clic en "Settings ⚙"** — AetherSDR no abrirá una URL si no hay una dirección IP disponible. Conéctese al dispositivo para que se use la dirección activa, o configure `SS_ManualIp` con la dirección IP del dispositivo.
- **Se usa el puerto incorrecto** — Si el dispositivo sirve su interfaz web en un puerto no predeterminado y la baliza no lo está anunciando correctamente, configure `SS_WebPort` con el número de puerto correcto.
- **No aparecen antenas en el applet** — Es posible que el dispositivo no haya terminado de descubrir sus antenas. Espere unos segundos para que la baliza transmita la lista de antenas.

## Relacionado

- [Descripción general de ShackSwitch](overview.md)
- [Seleccionar una antena para la Entrada A de ShackSwitch](select-an-antenna-for-shackswitch-input-a.md)
- [Configurar una antena de carga falsa para proteger la ruta de transmisión](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
