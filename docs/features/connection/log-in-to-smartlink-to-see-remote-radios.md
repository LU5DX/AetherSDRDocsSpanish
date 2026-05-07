# Iniciar sesión en SmartLink para ver radios remotas

SmartLink le permite acceder a un FLEX-8600 en una ubicación remota a través de internet. Esta página cubre cómo iniciar sesión en su cuenta de FlexRadio SmartLink para que AetherSDR pueda listar las radios disponibles.

## Antes de comenzar

- Debe tener una cuenta de FlexRadio con acceso a SmartLink. Si no tiene una, créela en el sitio web de FlexRadio antes de continuar.
- La radio remota ya debe estar registrada en SmartLink y encendida.
- AetherSDR no debe estar ya conectado a una radio. El panel de conexión aparece automáticamente cuando no hay ninguna radio conectada.

## Pasos

1. Abra el panel de conexión. Si AetherSDR ya muestra la interfaz principal, vaya a `Settings > Connect to Radio...`.
2. Haga clic en `Remote with SmartLink`. El panel cambia a la página de SmartLink.
3. En **SmartLink account**, ingrese su correo electrónico de la cuenta FlexRadio en el campo `SmartLink account: Email`.
4. Ingrese su contraseña en el campo `SmartLink account: Password`. La contraseña no se guarda entre sesiones.
5. Haga clic en `Sign In`. AetherSDR se autentica con SmartLink y, si es exitoso, completa la lista `Remote radios` con las radios disponibles para su cuenta.

## Descripción de cada control

| Control | Qué hace | Configuración persistida |
|---|---|---|
| Botón de modo `Remote with SmartLink` | Cambia el panel a la página de SmartLink. | `ConnectionMode` |
| `SmartLink account: Email` | Su dirección de correo electrónico de la cuenta FlexRadio. | `SmartLinkEmail` |
| `SmartLink account: Password` | Su contraseña de SmartLink. No se guarda después de que finaliza la sesión. | — |
| `Sign In` | Autentica con SmartLink y recupera la lista de radios remotas. | — |
| `Remote radios` | Lista las radios WAN disponibles para su cuenta después de iniciar sesión. La lista tiene una altura de visualización fija; si tiene muchas radios remotas, desplácese dentro de la lista para verlas todas. | — |
| `Connect Remote Radio` | Inicia una conexión WAN a la radio seleccionada en la lista `Remote radios`. | — |
| `Sign Out` | Finaliza la sesión actual de SmartLink. | — |
| `Radio IP address` | La dirección IP o nombre de host al que conectarse cuando se usa el modo Manual. El campo es un cuadro combinado editable que recuerda las últimas tres direcciones a las que se conectó exitosamente. Seleccione una dirección anterior del menú desplegable o escriba una nueva. | `ManualRadioIp` |
| `Connect to last radio on start up` | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y durante la detección por difusión / sonda de radio enrutada. Cuando no está marcado, se abre el diálogo de conexión y el usuario debe elegir una radio manualmente cada sesión. Marcado por defecto. | `AutoConnectToLastRadio` |

## Consejos

- `SmartLinkEmail` se persiste, por lo que su dirección de correo electrónico se rellena automáticamente en el próximo inicio. Su contraseña nunca se almacena.
- Después de iniciar sesión, la etiqueta de estado debajo del grupo de cuenta muestra su nombre, indicativo o una confirmación de que ha iniciado sesión, dependiendo de lo que contenga su perfil de cuenta.
- La lista `Remote radios` tiene un tamaño para mostrar una vista compacta de las radios disponibles. Desplácese dentro de la lista si la entrada que desea no es visible de inmediato.
- El campo `Radio IP address` en la página Manual ahora almacena hasta tres direcciones recientes en `RecentConnectByIpAddresses`. Si usó anteriormente la configuración `LastRoutedRadioIp`, AetherSDR la importa automáticamente la primera vez que abre la página Manual después de actualizar a la versión v0.9.7.

## Solución de problemas

- **La lista `Remote radios` está vacía después de iniciar sesión** — La radio remota puede estar apagada, no registrada en SmartLink o asociada con una cuenta de FlexRadio diferente. Confirme que la radio esté encendida y registrada bajo la misma cuenta que usó para iniciar sesión.
- **`Sign In` produce un error** — Verifique que su correo electrónico y contraseña sean correctos. Un error tipográfico en el campo de correo electrónico es una causa común porque el campo no tiene autocorrección. Verifique sus credenciales en el sitio web de FlexRadio.
- **La página de SmartLink no es accesible** — El software de cortafuegos o VPN en esta máquina puede estar bloqueando el tráfico saliente de SmartLink. Use `Open Network Diagnostics` (disponible en la página Local) para verificar la conectividad, o consulte [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md) si su configuración requiere una ruta IP directa en su lugar.
- **AetherSDR se conecta a la radio incorrecta al iniciar** — Si `Connect to last radio on start up` está marcado, AetherSDR intentará reconectarse a la radio que se usó en la sesión anterior. Desmarque esta opción si desea elegir una radio manualmente cada vez que inicie la aplicación.

## Relacionado

- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Connect to a local LAN radio](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Enable low-bandwidth mode for slow links](enable-low-bandwidth-mode-for-slow-links.md)
- [Operating remotely over SmartLink](../../operating/remote/remote-operation-smartlink.md)
