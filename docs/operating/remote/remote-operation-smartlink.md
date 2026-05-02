# Operar en remoto mediante SmartLink

SmartLink le permite conectarse a un FLEX-8600 que se encuentra en una ubicación diferente a la de su computadora. Esta página explica cómo iniciar sesión en su cuenta de SmartLink y conectarse a un radio remoto desde la pantalla de conexión de AetherSDR.

## Antes de comenzar

- Su FLEX-8600 debe estar encendido y conectado a internet en la ubicación remota, con SmartLink habilitado en su firmware.
- Debe tener una cuenta de FlexRadio SmartLink (correo electrónico y contraseña).
- AetherSDR no debe estar ya conectado a un radio. Si lo está, desconéctelo primero.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente cuando no hay ningún radio conectado. También puede acceder a ella mediante `Settings > Connect to Radio...`.
2. Haga clic en **Remote with SmartLink**. Esto selecciona el modo SmartLink y muestra los controles de cuenta SmartLink y de radio remoto.
3. En el campo **SmartLink account: Email**, introduzca la dirección de correo electrónico de su cuenta de FlexRadio.
4. En el campo **SmartLink account: Password**, introduzca su contraseña. La contraseña no se guarda entre sesiones.
5. Haga clic en **Sign In**. La etiqueta de estado se actualiza para mostrar el progreso de la autenticación.
6. Una vez que haya iniciado sesión, la lista **Remote radios** se rellena con los radios disponibles para su cuenta. Seleccione el radio que desea utilizar.
7. Si su enlace al sitio remoto es lento (satelital, celular o banda ancha congestionada), active **Use low bandwidth mode** antes de conectarse.
8. Haga clic en **Connect Remote Radio**. La etiqueta de estado muestra el progreso de la conexión. Cuando la conexión se establece correctamente, se abre la interfaz principal de AetherSDR.

## Qué hace cada control

| Control | Qué hace | Ajuste persistente |
|---|---|---|
| **Remote with SmartLink** (botón de modo) | Cambia la pantalla de conexión al modo SmartLink. | `ConnectionMode` |
| **SmartLink account: Email** | Su correo electrónico de cuenta FlexRadio. | `SmartLinkEmail` |
| **SmartLink account: Password** | Su contraseña de SmartLink. No se guarda al finalizar la sesión. | — |
| **Sign In** | Se autentica con SmartLink y rellena la lista **Remote radios**. | — |
| **Sign Out** | Cierra sesión en SmartLink y borra la lista de radios remotos. | — |
| **Remote radios** | Muestra los radios WAN de SmartLink disponibles para la cuenta con sesión iniciada. La lista tiene una altura de visualización fija; si tiene muchos radios remotos, desplácese dentro de la lista para verlos todos. | — |
| **Use low bandwidth mode** | Reduce las tasas de datos del flujo para enlaces lentos o con consumo medido. | `LowBandwidthMode` |
| **Connect Remote Radio** | Inicia una conexión WAN al radio seleccionado en **Remote radios**. | — |

## Consejos

- `SmartLinkEmail` es persistente, por lo que su dirección de correo electrónico aparece precompletada la próxima vez que abra la pantalla de conexión. Su contraseña no es persistente y debe introducirse en cada sesión.
- Si la lista **Remote radios** aparece vacía después de iniciar sesión, es posible que el radio remoto no tenga SmartLink habilitado o que esté fuera de línea.

## Resolución de problemas

- **La lista Remote radios aparece vacía después de Sign In** — El radio en la ubicación remota puede estar fuera de línea o SmartLink puede no estar habilitado en él. Confirme que el radio está encendido y registrado en la misma cuenta de FlexRadio.
- **Sign In falla o la etiqueta de estado muestra un error** — Verifique que su correo electrónico y contraseña sean correctos. Compruebe que AetherSDR tenga acceso saliente a internet y que ningún cortafuegos o proxy esté bloqueando la conexión SmartLink.
- **El audio está entrecortado o se interrumpe con frecuencia** — Active **Use low bandwidth mode** antes de conectarse para reducir las tasas del flujo en el enlace.

## Relacionado

- [Descripción general de Connect to a Radio](../../features/connection/overview.md)
- [Iniciar sesión en SmartLink para ver radios remotos](../../features/connection/log-in-to-smartlink-to-see-remote-radios.md)
- [Conectarse a un radio remoto mediante SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Habilitar el modo de bajo ancho de banda para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Desconectarse del radio actual](../../getting-started/setup/disconnect-from-the-current-radio.md)
- [Conectarse por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
