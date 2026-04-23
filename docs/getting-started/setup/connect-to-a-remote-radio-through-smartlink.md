# Conectarse a un radio remoto mediante SmartLink

SmartLink permite conectarse a un radio Flex que se encuentra en una ubicación diferente a la de su computadora. Utilice este procedimiento cuando el radio no esté en la misma red local que AetherSDR.

## Antes de comenzar

- El radio Flex debe estar encendido y conectado a internet en la ubicación remota, con SmartLink habilitado en la configuración del radio.
- Necesita una cuenta de FlexRadio (correo electrónico y contraseña) con acceso SmartLink para ese radio.
- AetherSDR no debe estar ya conectado a un radio. Si lo está, desconéctelo primero.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente cuando no hay ningún radio conectado. También puede acceder a ella mediante `Settings > Connect to Radio...`.
2. Haga clic en el botón de modo **Remote with SmartLink** en la parte superior del panel. El panel cambia a la página de SmartLink.
3. En el grupo **SmartLink account**, ingrese la dirección de su cuenta de FlexRadio en el campo **Email** y su contraseña en el campo **Password**.
4. Haga clic en **Sign In**. AetherSDR se autentica con SmartLink y llena la lista **Remote radios** con los radios disponibles para su cuenta.
5. Seleccione su radio en la lista **Remote radios**.
6. Haga clic en **Connect Remote Radio**. AetherSDR establece una conexión WAN al radio seleccionado.

## Función de cada control

| Control | Descripción | Ajuste persistente |
|---|---|---|
| Botón de modo **Remote with SmartLink** | Cambia el panel a la página de conexión de SmartLink. | `ConnectionMode` |
| Campo **Email** | Dirección de correo electrónico de su cuenta de FlexRadio. | `SmartLinkEmail` |
| Campo **Password** | Contraseña de su cuenta de FlexRadio. No se guarda entre sesiones. | — |
| **Sign In** | Se autentica con SmartLink y carga la lista de radios remotos. | — |
| **Sign Out** | Cierra la sesión de SmartLink y borra la lista de radios remotos. | — |
| Lista **Remote radios** | Muestra todos los radios con SmartLink habilitado disponibles para la cuenta con sesión iniciada. | — |
| **Connect Remote Radio** | Inicia la conexión WAN al radio seleccionado. | — |
| Casilla **Use low bandwidth mode** | Habilita flujos de audio y datos a tasa reducida. Úsela en conexiones a internet lentas o con cargo por consumo. | `LowBandwidthMode` |

## Consejos

- Su dirección de correo electrónico (`SmartLinkEmail`) se guarda entre sesiones. Su contraseña no se guarda: debe ingresarla cada vez.
- Si su conexión es lenta o tiene alta latencia, marque **Use low bandwidth mode** antes de hacer clic en **Connect Remote Radio**.

## Solución de problemas

- **La lista Remote radios aparece vacía después de iniciar sesión** — Es posible que el radio remoto no tenga SmartLink habilitado, o que esté fuera de línea. Confirme que el radio esté encendido y que SmartLink esté activo en la configuración del firmware del radio.
- **Sign In falla** — Verifique su correo electrónico y contraseña en su cuenta de FlexRadio. Compruebe que su computadora tenga acceso a internet.
- **La conexión se interrumpe o el audio presenta fallas** — Intente habilitar **Use low bandwidth mode** y vuelva a conectarse.

## Temas relacionados

- [Iniciar sesión en SmartLink para ver radios remotos](../../features/connection/log-in-to-smartlink-to-see-remote-radios.md)
- [Habilitar el modo de bajo ancho de banda para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Conectarse a un radio en la red local LAN](connect-to-a-local-lan-radio.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Operación remota mediante SmartLink](../../operating/remote/remote-operation-smartlink.md)
- [Desconectarse del radio actual](disconnect-from-the-current-radio.md)
