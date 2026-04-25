# Operación remota a través de SmartLink

SmartLink le permite conectarse a un FLEX-8600 que se encuentra en una ubicación diferente a la de su computadora. Esta página explica cómo iniciar sesión en su cuenta de SmartLink y conectarse a una radio remota desde la pantalla de conexión de AetherSDR.

## Antes de comenzar

- Su FLEX-8600 debe estar encendido y conectado a internet en la ubicación remota, con SmartLink habilitado en su firmware.
- Debe tener una cuenta de FlexRadio SmartLink (correo electrónico y contraseña).
- AetherSDR no debe estar conectado a ninguna radio. Si lo está, desconéctese primero.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente cuando no hay ninguna radio conectada. También puede acceder a ella mediante `Settings > Connect to Radio...`.
2. Haga clic en **Remote with SmartLink**. Esto selecciona el modo SmartLink y muestra los controles de cuenta de SmartLink y de radio remota.
3. En el campo **SmartLink account: Email**, ingrese la dirección de correo electrónico de su cuenta de FlexRadio.
4. En el campo **SmartLink account: Password**, ingrese su contraseña. La contraseña no se guarda entre sesiones.
5. Haga clic en **Sign In**. La etiqueta de estado se actualiza para mostrar el progreso de la autenticación.
6. Una vez que haya iniciado sesión, la lista **Remote radios** se llena con las radios disponibles para su cuenta. Seleccione la radio que desea usar.
7. Si el enlace hacia el sitio remoto es lento (satélite, red celular o banda ancha congestionada), marque **Use low bandwidth mode** antes de conectarse.
8. Haga clic en **Connect Remote Radio**. La etiqueta de estado muestra el progreso de la conexión. Cuando la conexión se establezca correctamente, se abrirá la interfaz principal de AetherSDR.

## Qué hace cada control

| Control | Función | Configuración persistente |
|---|---|---|
| **Remote with SmartLink** (botón de modo) | Cambia la pantalla de conexión al modo SmartLink. | `ConnectionMode` |
| **SmartLink account: Email** | Correo electrónico de su cuenta de FlexRadio. | `SmartLinkEmail` |
| **SmartLink account: Password** | Su contraseña de SmartLink. No se guarda al finalizar la sesión. | — |
| **Sign In** | Autentica con SmartLink y llena la lista **Remote radios**. | — |
| **Sign Out** | Cierra sesión en SmartLink y borra la lista de radios remotas. | — |
| **Remote radios** | Muestra las radios WAN de SmartLink disponibles para la cuenta con sesión iniciada. | — |
| **Use low bandwidth mode** | Reduce las tasas de datos del flujo para enlaces lentos o medidos. | `LowBandwidthMode` |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en **Remote radios**. | — |

## Sugerencias

- `SmartLinkEmail` se mantiene guardado, por lo que su dirección de correo electrónico aparecerá completada automáticamente la próxima vez que abra la pantalla de conexión. Su contraseña no se guarda y debe ingresarse en cada sesión.
- Si la lista **Remote radios** está vacía después de iniciar sesión, es posible que la radio remota no tenga SmartLink habilitado o que esté sin conexión.

## Solución de problemas

- **La lista Remote radios está vacía después de Sign In** — La radio en la ubicación remota puede estar sin conexión o SmartLink puede no estar habilitado en ella. Confirme que la radio esté encendida y registrada en la misma cuenta de FlexRadio.
- **Sign In falla o la etiqueta de estado muestra un error** — Verifique que su correo electrónico y contraseña sean correctos. Compruebe que AetherSDR tenga acceso a internet de salida y que ningún cortafuegos o proxy esté bloqueando la conexión de SmartLink.
- **El audio se entrecorta o se interrumpe con frecuencia** — Habilite **Use low bandwidth mode** antes de conectarse para reducir las tasas del flujo en el enlace.

## Relacionados

- [Descripción general de Connect to a Radio](../../features/connection/overview.md)
- [Iniciar sesión en SmartLink para ver radios remotas](../../features/connection/log-in-to-smartlink-to-see-remote-radios.md)
- [Conectarse a una radio remota a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Habilitar el modo de bajo ancho de banda para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Desconectarse de la radio actual](../../getting-started/setup/disconnect-from-the-current-radio.md)
- [Conectarse por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
