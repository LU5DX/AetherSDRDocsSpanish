# Conéctese a una radio remota mediante SmartLink

SmartLink le permite conectarse a una FLEX-8600 que se encuentra en una ubicación distinta a la de su computadora. Utilice este procedimiento cuando la radio no esté en su LAN local y usted tenga una cuenta de FlexRadio SmartLink.

## Antes de comenzar

- Usted tiene una cuenta de FlexRadio SmartLink (correo electrónico y contraseña).
- La FLEX-8600 en la estación remota está encendida y registrada en su cuenta de SmartLink.
- AetherSDR está en ejecución y no hay ninguna radio conectada actualmente.

## Pasos

1. Abra el Connection Panel. Aparece automáticamente cuando no hay ninguna radio conectada. Si ya hay una radio conectada, vaya a `Settings > Connect to a Radio...` para abrirlo.
2. Haga clic en **Remote with SmartLink** en la fila de botones de modo en la parte superior del panel. El panel cambia a la página de SmartLink. Esto establece `ConnectionMode` en `SmartLinkMode`.
3. En el grupo **SmartLink account**, ingrese el correo electrónico de su cuenta FlexRadio en el campo **Email**. AetherSDR guarda este valor como `SmartLinkEmail`.
4. Ingrese su contraseña en el campo **Password**. La contraseña no se guarda después de cerrar la aplicación.
5. Haga clic en **Sign In**. AetherSDR se autentica con SmartLink. Espere a que la etiqueta de estado confirme que ha iniciado sesión.
6. En la lista **Remote radios**, haga clic en la radio a la que desea conectarse.
7. Haga clic en **Connect Remote Radio**. AetherSDR establece una conexión WAN con la radio seleccionada.

## Qué hace cada control

| Control | Descripción | Clave persistida |
|---|---|---|
| Botones de modo **Local / SmartLink / Manual** | Cambian el panel entre los tres modos de conexión. El predeterminado es **Local**. | `ConnectionMode` |
| Botón de modo **Remote with SmartLink** | Cambia el panel al modo SmartLink. | `ConnectionMode` |
| Campo **Email** | La dirección de correo electrónico de su cuenta FlexRadio SmartLink. | `SmartLinkEmail` |
| Campo **Password** | Su contraseña de SmartLink. No se guarda entre sesiones. | — |
| **Sign In** | Autentica con SmartLink y completa la lista **Remote radios**. | — |
| **Sign Out** | Cierra la sesión de SmartLink y borra la lista de radios. | — |
| Lista **Remote radios** | Muestra todas las radios FLEX-8600 registradas en su cuenta de SmartLink que estén actualmente en línea. La lista tiene una altura de visualización fija; si tiene muchas radios, desplácese dentro de la lista. | — |
| **Connect Remote Radio** | Inicia una conexión WAN con la radio seleccionada en la lista **Remote radios**. Este botón aparece debajo de la lista, fuera del grupo de radios. | — |
| Lista **Available radios** | Enumera las radios LAN descubiertas mediante mDNS/Flex discovery. Tiene una altura limitada: use la barra de desplazamiento si se encuentran más radios de las que caben. | — |
| Indicador **No local radios found yet** | Aviso que se muestra cuando el descubrimiento está vacío. | — |
| **Retry Discovery** | Vuelve a ejecutar el descubrimiento de LAN. | — |
| **Connect Selected Radio** | Se conecta a la radio LAN resaltada. | — |
| **Connect by IP** | Atajo a la página Manual. | — |
| Campo **Radio IP address** | IP u hostname manual al que conectarse. | `ManualRadioIp` |
| Cuadro combinado **Source path** (Advanced) | Selecciona la interfaz de red local utilizada para la conexión manual. Disponible en la página Manual. | `ManualBindSource` |
| Casilla **Use low bandwidth mode** | Habilita flujos de audio y datos de tasa reducida. Úselo en conexiones a internet lentas o medidas. | `LowBandwidthMode` |
| Casilla **Connect to last radio on start up** | Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y en la sonda de descubrimiento por difusión / radio enrutada. Cuando no está marcada, se abre el diálogo de conexión y el usuario debe elegir una radio manualmente en cada sesión. Marcada por defecto. Añadido en v0.9.7. | `AutoConnectToLastRadio` |
| **Open Network Diagnostics** | Abre el diálogo Network Diagnostics para ayudar a solucionar problemas de conexión. Disponible tanto en las páginas Local como Manual. | — |
| **Network Diagnostics** | Abre NetworkDiagnosticsDialog desde la página Manual. | — |
| **Disconnect** | Desconecta de la radio actual. | — |

## Consejos

- Si la conexión es lenta o el audio se corta, active **Use low bandwidth mode** antes de hacer clic en **Connect Remote Radio**.
- La etiqueta de estado debajo de los controles muestra el estado actual de la conexión. Si muestra un error, cierre la sesión y vuelva a iniciarla para renovar la sesión de SmartLink.
- **Connect to last radio on start up** está marcada por defecto para que los usuarios existentes conserven su comportamiento anterior después de actualizar. Desmárquela si desea elegir una radio manualmente en cada inicio.
- Los campos de inicio de sesión de SmartLink ahora incluyen sugerencias de accesibilidad y nombres de objeto que ayudan a los gestores de contraseñas (macOS Passwords, Windows Authenticator, KDE Wallet) a asociar correctamente sus credenciales con el formulario de inicio de sesión de SmartLink.
- Haga clic derecho en una radio de la lista local **Available radios** para establecer un apodo personalizado para radios que no son Flex (HL2, simulador, etc.). Este apodo se guarda localmente y aparece en descubrimientos posteriores. Esta opción no está disponible para radios Flex, cuyos nombres se configuran mediante el Radio Setup propio de la radio.
- La altura de la lista de radios está limitada para garantizar que **Connect Selected Radio** y los demás controles debajo de la lista permanezcan accesibles, incluso en pantallas pequeñas (p. ej., 1024x600). Use la barra de desplazamiento vertical para ver todas las radios descubiertas.

## Solución de problemas

- **La lista de radios remotas está vacía después de iniciar sesión** — La radio remota puede estar fuera de línea o no estar registrada en esta cuenta. Confirme que la radio en la estación remota esté encendida y que haya iniciado sesión con la cuenta correcta.
- **Sign In no responde** — Verifique su conexión a internet. Si está detrás de un firewall restrictivo, el tráfico de SmartLink puede estar bloqueado. Use el botón **Open Network Diagnostics** para verificar la conectividad.
- **La etiqueta de estado muestra un error después de hacer clic en Connect Remote Radio** — Otro cliente puede estar ocupando ya el número máximo de conexiones permitidas por la radio. Pida a otros operadores que se desconecten y vuelva a intentarlo.

## Relacionado

- [Conéctese a una radio LAN local](connect-to-a-local-lan-radio.md)
- [Conéctese por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Operación remota mediante SmartLink](../../operating/remote/remote-operation-smartlink.md)
- [Desconéctese de la radio actual](disconnect-from-the-current-radio.md)
- Network Diagnostics
