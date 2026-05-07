# Conectarse a una radio remota a través de SmartLink

SmartLink le permite conectarse a una FLEX-8600 que se encuentra en una ubicación diferente a la de su computadora. Utilice este procedimiento cuando la radio no esté en su LAN local y tenga una cuenta de FlexRadio SmartLink.

## Antes de comenzar

- Tiene una cuenta de FlexRadio SmartLink (correo electrónico y contraseña).
- La FLEX-8600 en la estación remota está encendida y registrada en su cuenta de SmartLink.
- AetherSDR se está ejecutando y no hay ninguna radio conectada actualmente.

## Pasos

1. Abra el ConnectionPanel. Aparece automáticamente cuando no hay ninguna radio conectada. Si ya hay una radio conectada, vaya a `Settings > Connect to Radio...` para abrirlo.
2. Haga clic en **Remote with SmartLink** en la fila de botones de modo en la parte superior del panel. El panel cambia a la página de SmartLink. Esto establece `ConnectionMode` en `SmartLinkMode`.
3. En el grupo **SmartLink account**, ingrese el correo electrónico de su cuenta de FlexRadio en el campo **Email**. AetherSDR guarda este valor como `SmartLinkEmail`.
4. Ingrese su contraseña en el campo **Password**. La contraseña no se guarda después de cerrar la aplicación.
5. Haga clic en **Sign In**. AetherSDR se autentica con SmartLink. Espere a que la etiqueta de estado confirme que ha iniciado sesión.
6. En la lista **Remote radios**, haga clic en la radio a la que desea conectarse.
7. Haga clic en **Connect Remote Radio**. AetherSDR establece una conexión WAN con la radio seleccionada.

## Descripción de cada control

| Control | Descripción | Clave persistida |
|---|---|---|
| Botón de modo **Remote with SmartLink** | Cambia el panel al modo SmartLink. | `ConnectionMode` |
| Campo **Email** | La dirección de correo electrónico de su cuenta de FlexRadio SmartLink. | `SmartLinkEmail` |
| Campo **Password** | Su contraseña de SmartLink. No se guarda entre sesiones. | — |
| **Sign In** | Autentica con SmartLink y completa la lista **Remote radios**. | — |
| **Sign Out** | Cierra la sesión de SmartLink y limpia la lista de radios. | — |
| Lista **Remote radios** | Muestra todas las radios FLEX-8600 registradas en su cuenta de SmartLink que están actualmente en línea. La lista tiene una altura de visualización fija; si tiene muchas radios, desplácese dentro de la lista. | — |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en la lista **Remote radios**. Este botón aparece debajo de la lista, fuera del grupo de radios. | — |
| Casilla de verificación **Use low bandwidth mode** | Habilita flujos de audio y datos de tasa reducida. Úselo en conexiones a internet lentas o medidas. | `LowBandwidthMode` |
| Casilla de verificación **Connect to last radio on start up** | Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al inicio y en el descubrimiento por broadcast/sonda de ruta enrutada. Cuando está desmarcada, se abre el diálogo de conexión y el usuario debe elegir una radio manualmente en cada sesión. Está marcada por defecto. Añadido en v0.9.7. | `AutoConnectToLastRadio` |

## Consejos

- Si la conexión es lenta o el audio se corta, active **Use low bandwidth mode** antes de hacer clic en **Connect Remote Radio**.
- La etiqueta de estado debajo de los controles muestra el estado actual de la conexión. Si muestra un error, cierre sesión y vuelva a iniciarla para actualizar la sesión de SmartLink.
- **Connect to last radio on start up** está marcada por defecto para que los usuarios existentes mantengan su comportamiento anterior después de actualizar. Desmárquela si desea elegir una radio manualmente en cada inicio.

## Solución de problemas

- **La lista de Remote radios está vacía después de iniciar sesión** — La radio remota podría estar desconectada o no registrada en esta cuenta. Confirme que la radio en la estación remota esté encendida y que haya iniciado sesión con la cuenta correcta.
- **Sign In no responde** — Verifique su conexión a internet. Si está detrás de un firewall restrictivo, el tráfico de SmartLink podría estar bloqueado. Use `Settings > Connect to Radio...` para volver a abrir el panel e intente de nuevo.
- **La etiqueta de estado muestra un error después de hacer clic en Connect Remote Radio** — Otro cliente podría ya tener el número máximo de conexiones permitidas por la radio. Pida a otros operadores que se desconecten y luego reintente.

## Relacionados

- [Log in to SmartLink to see remote radios](../../features/connection/log-in-to-smartlink-to-see-remote-radios.md)
- [Enable low-bandwidth mode for slow links](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Connect to a local LAN radio](connect-to-a-local-lan-radio.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Operating remotely over SmartLink](../../operating/remote/remote-operation-smartlink.md)
- [Disconnect from the current radio](disconnect-from-the-current-radio.md)
