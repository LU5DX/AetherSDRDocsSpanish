# Conectarse a una radio remota a través de SmartLink

SmartLink le permite conectarse a una FLEX-8600 que se encuentra en una ubicación diferente a la de su computadora. Utilice este procedimiento cuando la radio no esté en su LAN local y tenga una cuenta de FlexRadio SmartLink.

## Antes de comenzar

- Tiene una cuenta de FlexRadio SmartLink (correo electrónico y contraseña).
- La FLEX-8600 en la estación remota está encendida y registrada en su cuenta de SmartLink.
- AetherSDR se está ejecutando y no hay ninguna radio conectada actualmente.

## Pasos

1. Abra el Panel de conexión. Aparece automáticamente cuando no hay ninguna radio conectada. Si ya hay una radio conectada, vaya a `Settings > Connect to a Radio...` para abrirlo.
2. Haga clic en **Remote with SmartLink** en la fila de botones de modo en la parte superior del panel. El panel cambia a la página SmartLink. Esto establece `ConnectionMode` en `SmartLinkMode`.
3. En el grupo **SmartLink account**, ingrese su correo electrónico de la cuenta de FlexRadio en el campo **Email**. AetherSDR guarda este valor como `SmartLinkEmail`.
4. Ingrese su contraseña en el campo **Password**. La contraseña no se guarda después de cerrar la aplicación.
5. Haga clic en **Sign In**. AetherSDR se autentica con SmartLink. Espere a que la etiqueta de estado confirme que ha iniciado sesión.
6. En la lista **Remote radios**, haga clic en la radio a la que desea conectarse.
7. Haga clic en **Connect Remote Radio**. AetherSDR establece una conexión WAN con la radio seleccionada.

## Qué hace cada control

| Control | Descripción | Clave persistida |
|---|---|---|
| Botón de modo **Remote with SmartLink** | Cambia el panel al modo SmartLink. | `ConnectionMode` |
| Campo **Email** | Su dirección de correo electrónico de la cuenta de FlexRadio SmartLink. | `SmartLinkEmail` |
| Campo **Password** | Su contraseña de SmartLink. No se guarda entre sesiones. | — |
| **Sign In** | Autentica con SmartLink y completa la lista **Remote radios**. | — |
| **Sign Out** | Cierra la sesión de SmartLink y borra la lista de radios. | — |
| Lista **Remote radios** | Muestra todas las radios FLEX-8600 registradas en su cuenta de SmartLink que están actualmente en línea. La lista tiene una altura de visualización fija; si tiene muchas radios, desplácese dentro de la lista. | — |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en la lista **Remote radios**. Este botón aparece debajo de la lista, fuera del grupo de radios. | — |
| Casilla **Use low bandwidth mode** | Habilita transmisiones de audio y datos de velocidad reducida. Úselo en conexiones a internet lentas o medidas. | `LowBandwidthMode` |
| Casilla **Connect to last radio on start up** | Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al inicio y durante el descubrimiento por difusión / sonda de radio enrutada. Cuando no está marcada, se abre el diálogo de conexión y el usuario debe elegir una radio manualmente cada sesión. Valor predeterminado: marcada. Añadido en v0.9.7. | `AutoConnectToLastRadio` |
| **Open Network Diagnostics** | Abre el diálogo de Diagnóstico de red para ayudar a solucionar problemas de conexión. | — |
| Cuadro combinado **Source path** (Avanzado) | Selecciona la interfaz de red local utilizada para la conexión manual. Disponible en la página Manual. | `ManualBindSource` |
| **Connect by IP (manual)** | Inicia una conexión manual o VPN a la dirección IP ingresada en el campo **Radio IP address**. | — |

## Consejos

- Si la conexión es lenta o el audio se entrecorta, active **Use low bandwidth mode** antes de hacer clic en **Connect Remote Radio**.
- La etiqueta de estado debajo de los controles muestra el estado actual de la conexión. Si muestra un error, cierre la sesión y vuelva a iniciarla para renovar la sesión de SmartLink.
- **Connect to last radio on start up** está marcada por defecto para que los usuarios existentes mantengan su comportamiento anterior después de actualizar. Desmárquela si desea elegir una radio manualmente en cada inicio.

## Solución de problemas

- **La lista de radios remotas está vacía después de iniciar sesión** — La radio remota puede estar desconectada o no estar registrada en esta cuenta. Confirme que la radio en la estación remota esté encendida y que haya iniciado sesión con la cuenta correcta.
- **Sign In no responde** — Verifique su conexión a internet. Si está detrás de un firewall restrictivo, el tráfico de SmartLink puede estar bloqueado. Use el botón **Open Network Diagnostics** para verificar la conectividad.
- **La etiqueta de estado muestra un error después de hacer clic en Connect Remote Radio** — Es posible que otro cliente ya tenga el número máximo de conexiones permitidas por la radio. Pida a otros operadores que se desconecten y vuelva a intentarlo.

## Relacionado

- [Conectarse a una radio LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Operar de forma remota a través de SmartLink](../../operating/remote/remote-operation-smartlink.md)
- [Desconectarse de la radio actual](disconnect-from-the-current-radio.md)
- [Diagnóstico de red](../../tools/network-diagnostics.md)
