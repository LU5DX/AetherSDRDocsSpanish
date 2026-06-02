# Conectarse a una Radio Remota a Través de SmartLink

SmartLink le permite conectarse a una FLEX-8600 que se encuentra en una ubicación diferente a la de su computadora. Use este procedimiento cuando la radio no esté en su LAN local y tenga una cuenta de FlexRadio SmartLink.

## Antes de empezar

- Tiene una cuenta de FlexRadio SmartLink (correo electrónico y contraseña).
- La FLEX-8600 en la estación remota está encendida y registrada en su cuenta de SmartLink.
- AetherSDR está ejecutándose y ninguna radio está conectada actualmente.

## Pasos

1. Abra el Panel de Conexión. Aparece automáticamente cuando no hay ninguna radio conectada. Si ya hay una radio conectada, vaya a `Settings > Connect to a Radio...` para abrirlo.
2. Haga clic en **Remote with SmartLink** en la fila de botones de modo en la parte superior del panel. El panel cambia a la página de SmartLink. Esto establece `ConnectionMode` en `SmartLinkMode`.
3. En el grupo **SmartLink account**, ingrese el correo electrónico de su cuenta de FlexRadio en el campo **Email**. AetherSDR guarda este valor como `SmartLinkEmail`.
4. Ingrese su contraseña en el campo **Password**. La contraseña no se guarda después de cerrar la aplicación.
5. Haga clic en **Sign In**. AetherSDR se autentica con SmartLink. Espere a que la etiqueta de estado confirme que ha iniciado sesión.
6. En la lista **Remote radios**, haga clic en la radio a la que desea conectarse.
7. Haga clic en **Connect Remote Radio**. AetherSDR establece una conexión WAN con la radio seleccionada.

## Función de cada control

| Control | Descripción | Clave persistida |
|---|---|---|
| Botón de modo **Remote with SmartLink** | Cambia el panel al modo SmartLink. | `ConnectionMode` |
| Campo **Email** | La dirección de correo electrónico de su cuenta de FlexRadio SmartLink. | `SmartLinkEmail` |
| Campo **Password** | Su contraseña de SmartLink. No se guarda entre sesiones. | — |
| **Sign In** | Autentica con SmartLink y completa la lista de **Remote radios**. | — |
| **Sign Out** | Cierra la sesión de SmartLink y limpia la lista de radios. | — |
| Lista **Remote radios** | Muestra todas las radios FLEX-8600 registradas en su cuenta de SmartLink que están actualmente en línea. La lista tiene una altura de visualización fija; si tiene muchas radios, desplácese dentro de la lista. | — |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en la lista **Remote radios**. Este botón aparece debajo de la lista, fuera del grupo de radios. | — |
| Casilla **Use low bandwidth mode** | Habilita flujos de audio y datos de tasa reducida. Úselo en conexiones a internet lentas o con límite de datos. | `LowBandwidthMode` |
| Casilla **Enable adaptive frame-rate throttle** | Reduce automáticamente la tasa de cuadros FFT/waterfall cuando la calidad de la red se degrada. Esto ayuda a mantener el rendimiento en enlaces de velocidad variable. | `AdaptiveThrottleEnabled` |
| Casilla **Connect to last radio on start up** | Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y durante el descubrimiento por difusión / sondeo de radio enrutada. Cuando no está marcada, se abre el diálogo de conexión y el usuario debe elegir una radio manualmente cada sesión. Por defecto está marcada. Añadida en v0.9.7. | `AutoConnectToLastRadio` |
| **Open Network Diagnostics** | Abre el diálogo de Diagnóstico de Red para ayudar a solucionar problemas de conexión. | — |
| Cuadro combinado **Source path** (Avanzado) | Elige la interfaz de red local utilizada para la conexión manual. Disponible en la página Manual. | `ManualBindSource` |
| **Connect by IP (manual)** | Inicia una conexión manual o VPN a la dirección IP ingresada en el campo **Radio IP address**. | — |

## Consejos

- Si la conexión es lenta o el audio se entrecorta, active **Use low bandwidth mode** antes de hacer clic en **Connect Remote Radio**.
- Para enlaces de red de velocidad variable (por ejemplo, celular), active **Enable adaptive frame-rate throttle** para permitir que AetherSDR ajuste automáticamente las tasas de cuadros FFT/waterfall cuando la calidad de la red cambie.
- La etiqueta de estado debajo de los controles muestra el estado actual de la conexión. Si muestra un error, cierre la sesión y vuelva a iniciarla para renovar la sesión de SmartLink.
- **Connect to last radio on start up** está marcada por defecto para que los usuarios existentes mantengan su comportamiento anterior después de actualizar. Desmárquela si desea elegir una radio manualmente en cada inicio.
- Los campos de inicio de sesión de SmartLink ahora incluyen sugerencias de accesibilidad y nombres de objeto que ayudan a los gestores de contraseñas (macOS Passwords, Windows Authenticator, KDE Wallet) a asociar correctamente sus credenciales con el formulario de inicio de sesión de SmartLink.

## Solución de problemas

- **La lista de Remote radios está vacía después de iniciar sesión** — La radio remota puede estar fuera de línea o no registrada en esta cuenta. Confirme que la radio en la estación remota esté encendida y que haya iniciado sesión con la cuenta correcta.
- **Sign In no responde** — Verifique su conexión a internet. Si está detrás de un firewall restrictivo, el tráfico de SmartLink puede estar bloqueado. Use el botón **Open Network Diagnostics** para verificar la conectividad.
- **La etiqueta de estado muestra un error después de hacer clic en Connect Remote Radio** — Otro cliente puede estar usando ya el número máximo de conexiones permitidas por la radio. Pida a otros operadores que se desconecten y luego vuelva a intentarlo.

## Relacionado

- [Connect to a local LAN radio](connect-to-a-local-lan-radio.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Operating remotely over SmartLink](../../operating/remote/remote-operation-smartlink.md)
- [Disconnect from the current radio](disconnect-from-the-current-radio.md)
- Network Diagnostics
