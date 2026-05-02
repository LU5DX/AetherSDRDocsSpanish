# Abrir la interfaz de configuración web de ShackSwitch

El dispositivo ShackSwitch incluye una interfaz web integrada para la configuración a nivel de firmware. Esta página explica cómo abrir dicha interfaz desde AetherSDR utilizando el botón "Settings ⚙" del applet de ShackSwitch.

## Antes de comenzar

- El applet de ShackSwitch debe estar visible en el Panel de Applets. Aparece automáticamente cuando se detecta un dispositivo ShackSwitch en la LAN, o después de conectarse mediante la pestaña Peripherals en Radio Setup.
- Si el dispositivo no está conectado en ese momento, AetherSDR utiliza como alternativa la dirección IP almacenada en `SS_ManualIp`. Establezca ese valor antes de continuar si desea abrir la interfaz web estando desconectado.
- El navegador del sistema debe poder alcanzar el dispositivo ShackSwitch en la red.

## Pasos

1. Localice el applet de ShackSwitch en el Panel de Applets, en el lado derecho de la ventana principal. Si no está visible, haga clic en el botón SS de la barra lateral derecha para mostrarlo.
2. Haga clic en "Settings ⚙" en la parte inferior del applet.
3. AetherSDR construye una URL a partir de la IP del dispositivo y el puerto web, y la abre en el navegador del sistema.

## Qué hace cada control

| Control | Comportamiento | Ajuste persistido |
|---|---|---|
| Botón "Settings ⚙" | Abre la interfaz de configuración web del dispositivo ShackSwitch en el navegador del sistema. Usa la dirección del par activo cuando está conectado; recurre a `SS_ManualIp` cuando está desconectado. El puerto se toma del puerto web anunciado en el beacon del dispositivo si ese valor es superior a 1024; de lo contrario, se usa `SS_WebPort`, con un valor de reserva final de 5000. | — |
| `SS_ManualIp` | Dirección IP utilizada cuando no hay ninguna conexión activa con el dispositivo. | `SS_ManualIp` |
| `SS_WebPort` | Puerto de la interfaz web utilizado cuando el beacon no anuncia un puerto válido (superior a 1024). Valor predeterminado: `5000`. | `SS_WebPort` |

## Consejos

- Si el dispositivo está conectado, AetherSDR usa automáticamente la dirección del par activo. No es necesario establecer `SS_ManualIp` para el funcionamiento normal en modo conectado.
- El puerto web del beacon solo se considera válido cuando es superior a 1024. Si el firmware del dispositivo difunde el puerto 80 como marcador de posición, AetherSDR lo ignora y utiliza `SS_WebPort` o el valor predeterminado de 5000.
- Para abrir la interfaz web mientras la radio está desconectada, establezca `SS_ManualIp` con la dirección IP estática del dispositivo con antelación.

## Solución de problemas

- **El navegador se abre pero la página no carga** — El dispositivo puede estar en una subred diferente o detrás de un cortafuegos. Confirme que la IP mostrada en la etiqueta de estado del applet de ShackSwitch es accesible desde su equipo. Verifique que el puerto (predeterminado `5000`) no esté bloqueado.
- **No ocurre nada al hacer clic en "Settings ⚙"** — AetherSDR no abrirá una URL si no hay ninguna dirección IP disponible. Conecte el dispositivo para que se use la dirección activa, o establezca `SS_ManualIp` con la dirección IP del dispositivo.
- **Se utiliza un puerto incorrecto** — Si el dispositivo sirve su interfaz web en un puerto no predeterminado y el beacon no lo anuncia correctamente, establezca `SS_WebPort` con el número de puerto correcto.

## Temas relacionados

- [Descripción general de ShackSwitch](overview.md)
- [Seleccionar una antena para la entrada A de ShackSwitch](select-an-antenna-for-shackswitch-input-a.md)
- [Configurar una carga dummy como antena para proteger la ruta de transmisión](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
