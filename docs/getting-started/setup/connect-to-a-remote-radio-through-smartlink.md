# Conectarse a una Radio Remota a Través de SmartLink

SmartLink le permite conectarse a una FLEX-8600 que se encuentra en una ubicación distinta a la de su computadora. Utilice este procedimiento cuando la radio no esté en su LAN local y usted tenga una cuenta de FlexRadio SmartLink.

## Antes de comenzar

- Debe tener una cuenta de FlexRadio SmartLink (correo electrónico y contraseña).
- La FLEX-8600 en la estación remota debe estar encendida y registrada en su cuenta de SmartLink.
- AetherSDR debe estar ejecutándose y no debe haber ninguna radio conectada actualmente.

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
| Botones de modo **Local / SmartLink / Manual** | Cambian el panel entre los tres modos de conexión. El valor predeterminado es **Local**. | `ConnectionMode` |
| Botón de modo **Remote with SmartLink** | Cambia el panel al modo SmartLink. | `ConnectionMode` |
| Campo **Email** | Dirección de correo electrónico de su cuenta de FlexRadio SmartLink. | `SmartLinkEmail` |
| Campo **Password** | Contraseña de su SmartLink. No se guarda entre sesiones. | — |
| **Sign In** | Se autentica con SmartLink y llena la lista **Remote radios**. | — |
| **Sign Out** | Cierra la sesión de SmartLink y borra la lista de radios. | — |
| Lista **Remote radios** | Muestra todas las radios FLEX-8600 registradas en su cuenta de SmartLink que están actualmente en línea. La lista tiene una altura de visualización fija; si tiene muchas radios, desplácese dentro de la lista. | — |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en la lista **Remote radios**. Este botón aparece debajo de la lista, fuera del grupo de radios. | — |
| Lista **Available radios** | Enumera las radios LAN descubiertas mediante mDNS/detección de Flex. Tiene una altura limitada; use la barra de desplazamiento si se encuentran más radios de las que caben. | — |
| Indicador **No local radios found yet** | Mensaje que se muestra cuando la detección está vacía. | — |
| **Retry Discovery** | Vuelve a ejecutar la detección LAN. | — |
| **Connect Selected Radio** | Se conecta a la radio LAN resaltada. | — |
| **Connect by IP** | Acceso directo a la página Manual. | — |
| Campo **Radio IP address** | IP manual a la que conectarse. | `ManualRadioIp` |
| **Connect by IP (manual)** | Inicia la conexión manual/VPN. | — |
| Cuadro combinado **Source path** (Avanzado) | Selecciona la interfaz de red local utilizada para la conexión manual. Disponible en la página Manual. | `ManualBindSource` |
| Casilla de verificación **Use low bandwidth mode** | Habilita flujos de audio y datos de velocidad reducida. Úselo en conexiones a internet lentas o medidas. | `LowBandwidthMode` |
| Casilla de verificación **Connect to last radio on start up** | Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y al sondear detección por difusión/radio enrutada. Cuando no está marcada, se abre el diálogo de conexión y el usuario debe seleccionar una radio manualmente en cada sesión. Marcada por defecto. Añadido en v0.9.7. | `AutoConnectToLastRadio` |
| **Open Network Diagnostics** | Abre el diálogo de Diagnóstico de Red para ayudar a solucionar problemas de conexión. Disponible tanto en las páginas Local como Manual. | — |
| **Network Diagnostics** | Abre NetworkDiagnosticsDialog desde la página Manual. | — |
| **Disconnect** | Desconecta la radio actual. | — |

## Consejos

- Si la conexión es lenta o el audio se entrecorta, active **Use low bandwidth mode** antes de hacer clic en **Connect Remote Radio**.
- La etiqueta de estado debajo de los controles muestra el estado actual de la conexión. Si muestra un error, cierre sesión y vuelva a iniciarla para actualizar la sesión de SmartLink.
- **Connect to last radio on start up** está marcada por defecto para que los usuarios existentes mantengan su comportamiento anterior después de actualizar. Desmárquela si desea elegir una radio manualmente en cada inicio.
- Los campos de inicio de sesión de SmartLink ahora incluyen sugerencias de accesibilidad y nombres de objeto que ayudan a los gestores de contraseñas (macOS Passwords, Windows Authenticator, KDE Wallet) a asociar correctamente sus credenciales con el formulario de inicio de sesión de SmartLink.
- Haga clic derecho en una radio de la lista local **Available radios** para establecer un apodo personalizado para radios que no son Flex (HL2, simulador, etc.). Este apodo se guarda localmente y aparece en detecciones posteriores. Esta opción no está disponible para radios Flex, cuyos nombres se configuran mediante la propia Configuración de Radio de la radio.
- La altura de la lista de radios está limitada para garantizar que el botón **Connect Selected Radio** y otros controles debajo de la lista permanezcan accesibles, incluso en pantallas pequeñas (p. ej., 1024x600). Use la barra de desplazamiento vertical para ver todas las radios descubiertas.

## Solución de problemas

- **La lista de radios remotas está vacía después de iniciar sesión** — La radio remota podría estar fuera de línea o no estar registrada en esta cuenta. Confirme que la radio en la estación remota esté encendida y que haya iniciado sesión con la cuenta correcta.
- **Sign In no responde** — Verifique su conexión a internet. Si está detrás de un firewall restrictivo, el tráfico de SmartLink podría estar bloqueado. Use el botón **Open Network Diagnostics** para verificar la conectividad.
- **La etiqueta de estado muestra un error después de hacer clic en Connect Remote Radio** — Es posible que otro cliente ya tenga el número máximo de conexiones permitidas por la radio. Pida a cualquier otro operador que se desconecte y vuelva a intentarlo.

## Relacionados

- [Conectarse a una radio LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Operación remota a través de SmartLink](../../operating/remote/remote-operation-smartlink.md)
- [Desconectarse de la radio actual](disconnect-from-the-current-radio.md)
- Diagnóstico de Red
