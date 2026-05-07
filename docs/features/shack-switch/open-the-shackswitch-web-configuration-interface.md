# Abrir la interfaz de configuración web de ShackSwitch

El dispositivo ShackSwitch incluye una interfaz web integrada para la configuración a nivel de firmware. Esta página explica cómo abrir esa interfaz desde AetherSDR usando el botón "Settings ⚙" en el applet de ShackSwitch.

## Antes de comenzar

- El applet de ShackSwitch debe estar visible en el Panel de Applets. Aparece automáticamente cuando se descubre un dispositivo ShackSwitch en la LAN, o después de conectarse a través de la pestaña Peripherals en Radio Setup.
- Si el dispositivo no está conectado actualmente, AetherSDR recurre a la dirección IP almacenada en `SS_ManualIp`. Establezca ese valor antes de continuar si tiene la intención de abrir la interfaz web mientras está desconectado.
- Su navegador del sistema debe poder alcanzar el dispositivo ShackSwitch en la red.

## Pasos

1. Localice el applet de ShackSwitch en el Panel de Applets, en el lado derecho de la ventana principal. Si no está visible, haga clic en el botón de la bandeja SS en la barra lateral derecha para mostrarlo.
2. Haga clic en "Settings ⚙" en la parte inferior del applet.
3. AetherSDR construye una URL a partir de la IP del dispositivo y el puerto web, y la abre en su navegador del sistema.

## Qué hace cada control

| Control | Comportamiento | Ajuste persistente |
|---|---|---|
| Botón "Settings ⚙" | Abre la interfaz de configuración web del dispositivo ShackSwitch en el navegador del sistema. Utiliza la dirección del par activo cuando está conectado; recurre a `SS_ManualIp` cuando está desconectado. El puerto se toma del puerto web de la baliza del dispositivo cuando ese valor es superior a 1024; de lo contrario, se toma de `SS_WebPort`, con un valor de respaldo final de 5000. | — |
| `SS_ManualIp` | Dirección IP utilizada cuando no hay una conexión activa con el dispositivo. | `SS_ManualIp` |
| `SS_WebPort` | Puerto de la interfaz web utilizado cuando la baliza no anuncia un puerto válido (superior a 1024). Valor predeterminado: `5000`. | `SS_WebPort` |

## Consejos

- Si el dispositivo está conectado, AetherSDR utiliza la dirección del par activo automáticamente. No necesita establecer `SS_ManualIp` para la operación normal con conexión.
- El puerto web de la baliza solo se considera confiable cuando es superior a 1024. Si el firmware del dispositivo transmite el puerto 80 como un marcador de posición, AetherSDR lo ignora y utiliza `SS_WebPort` o el valor predeterminado de 5000 en su lugar.
- Para abrir la interfaz web mientras el radio está fuera de línea, establezca `SS_ManualIp` con la dirección IP estática del dispositivo con antelación.

## Solución de problemas

- **El navegador se abre pero la página no carga** — El dispositivo puede estar en una subred diferente o detrás de un cortafuegos. Confirme que la IP mostrada en la etiqueta de estado del applet de ShackSwitch sea accesible desde su máquina. Verifique que el puerto (predeterminado `5000`) no esté bloqueado.
- **No sucede nada al hacer clic en "Settings ⚙"** — AetherSDR no abrirá una URL si no hay una dirección IP disponible. Conéctese al dispositivo para que se utilice la dirección activa, o establezca `SS_ManualIp` con la dirección IP del dispositivo.
- **Se utiliza el puerto incorrecto** — Si el dispositivo sirve su interfaz web en un puerto no predeterminado y la baliza no lo está anunciando correctamente, establezca `SS_WebPort` con el número de puerto correcto.

## Relacionados

- [ShackSwitch overview](overview.md)
- [Select an antenna for ShackSwitch Input A](select-an-antenna-for-shackswitch-input-a.md)
- [Configure a dummy load antenna to protect the transmit path](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
