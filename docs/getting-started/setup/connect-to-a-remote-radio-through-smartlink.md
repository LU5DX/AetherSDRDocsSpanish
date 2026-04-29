# Conectarse a una Radio Remota a Través de SmartLink

SmartLink permite conectarse a un FLEX-8600 que se encuentra en una ubicación diferente a la de su computadora. Use este procedimiento cuando la radio no esté en su LAN local y disponga de una cuenta FlexRadio SmartLink.

## Antes de comenzar

- Tiene una cuenta FlexRadio SmartLink (correo electrónico y contraseña).
- El FLEX-8600 en la estación remota está encendido y registrado en su cuenta SmartLink.
- AetherSDR está en ejecución y no hay ninguna radio conectada en este momento.

## Pasos

1. Abra el ConnectionPanel. Aparece automáticamente cuando no hay ninguna radio conectada. Si ya hay una radio conectada, vaya a `Settings > Connect to Radio...` para abrirlo.
2. Haga clic en **Remote with SmartLink** en la fila de botones de modo situada en la parte superior del panel. El panel cambia a la página de SmartLink. Esto establece `ConnectionMode` en `SmartLinkMode`.
3. En el grupo **SmartLink account**, ingrese el correo electrónico de su cuenta FlexRadio en el campo **Email**. AetherSDR guarda este valor como `SmartLinkEmail`.
4. Ingrese su contraseña en el campo **Password**. La contraseña no se guarda al cerrar la aplicación.
5. Haga clic en **Sign In**. AetherSDR se autentica con SmartLink. Espere a que la etiqueta de estado confirme que ha iniciado sesión.
6. En la lista **Remote radios**, haga clic en la radio a la que desea conectarse.
7. Haga clic en **Connect Remote Radio**. AetherSDR establece una conexión WAN con la radio seleccionada.

## Qué hace cada control

| Control | Descripción | Clave persistida |
|---|---|---|
| Botón de modo **Remote with SmartLink** | Cambia el panel al modo SmartLink. | `ConnectionMode` |
| Campo **Email** | La dirección de correo electrónico de su cuenta FlexRadio SmartLink. | `SmartLinkEmail` |
| Campo **Password** | Su contraseña de SmartLink. No se guarda entre sesiones. | — |
| **Sign In** | Se autentica con SmartLink y rellena la lista **Remote radios**. | — |
| **Sign Out** | Cierra la sesión de SmartLink y borra la lista de radios. | — |
| Lista **Remote radios** | Muestra todas las radios FLEX-8600 registradas en su cuenta SmartLink que están en línea en este momento. La lista tiene una altura de visualización fija; si tiene muchas radios, desplácese dentro de la lista. | — |
| **Connect Remote Radio** | Inicia una conexión WAN con la radio seleccionada en la lista **Remote radios**. Este botón aparece debajo de la lista, fuera del grupo de radios. | — |
| Casilla **Use low bandwidth mode** | Habilita flujos de audio y datos a tasa reducida. Úsela en conexiones a internet lentas o con datos limitados. | `LowBandwidthMode` |

## Consejos

- Si la conexión es lenta o el audio se interrumpe, habilite **Use low bandwidth mode** antes de hacer clic en **Connect Remote Radio**.
- La etiqueta de estado situada debajo de los controles muestra el estado de conexión actual. Si indica un error, cierre la sesión e iníciela de nuevo para actualizar la sesión SmartLink.

## Solución de problemas

- **La lista Remote radios está vacía después de iniciar sesión** — Es posible que la radio remota esté sin conexión o no esté registrada en esta cuenta. Confirme que la radio en la estación remota esté encendida y que haya iniciado sesión con la cuenta correcta.
- **Sign In no responde** — Verifique su conexión a internet. Si está detrás de un cortafuegos restrictivo, el tráfico de SmartLink puede estar bloqueado. Use `Settings > Connect to Radio...` para volver a abrir el panel e inténtelo de nuevo.
- **La etiqueta de estado muestra un error al hacer clic en Connect Remote Radio** — Es posible que otro cliente ya ocupe el número máximo de conexiones permitidas por la radio. Solicite a los demás operadores que se desconecten y vuelva a intentarlo.

## Relacionado

- [Iniciar sesión en SmartLink para ver radios remotas](../../features/connection/log-in-to-smartlink-to-see-remote-radios.md)
- [Habilitar el modo de bajo ancho de banda para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Conectarse a una radio en la LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Operación remota a través de SmartLink](../../operating/remote/remote-operation-smartlink.md)
- [Desconectarse de la radio actual](disconnect-from-the-current-radio.md)
