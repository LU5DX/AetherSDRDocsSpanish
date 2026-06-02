# Conectar a una Radio

El Panel de Conexión es la pantalla principal para descubrir y conectarse a una radio FLEX-8600. Proporciona tres modos de conexión: Local (descubrimiento LAN), SmartLink (remoto a través de internet) y Manual (IP directa o VPN). El panel aparece automáticamente cuando AetherSDR se inicia y no hay ninguna radio conectada, o puede abrirlo en cualquier momento desde `Settings > Connect to Radio...`.

## Antes de comenzar

- AetherSDR no debe estar ya conectado a una radio.
- El panel ahora se abre como un diálogo sin bordes. Puede arrastrarlo por la barra de título en la parte superior.

## Pasos

### Conectar a una radio LAN local

1. Abra el panel de conexión. De forma predeterminada, la pestaña Local está activa.
2. Espere a que AetherSDR descubra radios en la red local. La lista `Available radios` se completa automáticamente.
3. Seleccione una radio de la lista.
4. Haga clic en `Connect Selected Radio`.

### Conectar a una radio remota a través de SmartLink

1. Abra el panel de conexión.
2. Haga clic en `Remote with SmartLink`. El panel cambia a la página SmartLink.
3. En **SmartLink account**, ingrese su correo electrónico de cuenta FlexRadio en el campo `SmartLink account: Email`.
4. Ingrese su contraseña en el campo `SmartLink account: Password`. La contraseña no se guarda entre sesiones.
5. Haga clic en `Sign In`. AetherSDR se autentica con SmartLink y, si tiene éxito, completa la lista `Remote radios` con las radios disponibles para su cuenta.
6. Seleccione una radio de la lista `Remote radios`.
7. Haga clic en `Connect Remote Radio`.

### Conectar por dirección IP (manual o VPN)

1. Abra el panel de conexión.
2. Haga clic en `Connect by IP` (desde la página Local) o seleccione la página Manual directamente.
3. En el campo `Radio IP address`, ingrese la dirección IP o el nombre de host de la radio.
4. (Opcional) Seleccione una interfaz de red del menú desplegable `Advanced: Source path` para vincular la conexión a una NIC específica.
5. (Opcional) Marque `Use low bandwidth mode` para flujos de tasa reducida en enlaces lentos.
6. Haga clic en `Connect by IP (manual)`.

### Controles adicionales

- `Open Network Diagnostics` — Abre un diálogo de diagnóstico para solucionar problemas de conectividad de red.
- `Retry Discovery` — Vuelve a ejecutar el descubrimiento LAN en la página Local.
- `Disconnect` — Desconecta la radio actual y vuelve al panel de conexión.
- `Connect to last radio on start up` — Cuando está marcado (predeterminado), AetherSDR se reconecta automáticamente a la última radio utilizada al iniciar. Cuando no está marcado, el panel de conexión se abre en cada sesión.
- `Enable adaptive frame-rate throttle` — Cuando está marcado, AetherSDR reduce automáticamente las tasas de cuadros FFT y waterfall cuando la calidad de la red se degrada, lo que ayuda a mantener una conexión estable en enlaces más lentos o congestionados.

## Qué hace cada control

| Control | Qué hace | Configuración persistente |
|---|---|---|
| Botones de modo Local / SmartLink / Manual | Cambian el panel entre los tres modos de conexión. | `ConnectionMode` |
| `Available radios` | Enumera las radios LAN descubiertas a través de mDNS/Flex discovery. | — |
| `Connect Selected Radio` | Se conecta a la radio LAN resaltada. | — |
| `No local radios found yet` | Aviso que se muestra cuando el descubrimiento está vacío. | — |
| `Retry Discovery` | Vuelve a ejecutar el descubrimiento LAN. | — |
| `Remote with SmartLink` | Acceso directo a la página SmartLink. | — |
| `Connect by IP` | Acceso directo a la página Manual. | — |
| `Open Network Diagnostics` | Abre el diálogo de diagnóstico de red. | — |
| `SmartLink account: Email` | Su dirección de correo electrónico de la cuenta FlexRadio. | `SmartLinkEmail` |
| `SmartLink account: Password` | Su contraseña de SmartLink. No se guarda después de que finaliza la sesión. | — |
| `Sign In` | Se autentica con SmartLink y recupera la lista de radios remotas. | — |
| `Sign Out` | Finaliza la sesión actual de SmartLink. | — |
| `Remote radios` | Enumera las radios WAN disponibles para su cuenta después de iniciar sesión. | — |
| `Connect Remote Radio` | Inicia una conexión WAN a la radio remota seleccionada. | — |
| `Radio IP address` | La dirección IP o nombre de host al que conectarse en modo Manual. Cuadro combinado editable que recuerda las últimas tres direcciones a las que se conectó correctamente. | `ManualRadioIp` |
| `Advanced: Source path` | Selecciona la interfaz de red local utilizada para la conexión manual. | `ManualBindSource` |
| `Use low bandwidth mode` | Habilita flujos de tasa reducida para enlaces lentos. | `LowBandwidthMode` |
| `Connect by IP (manual)` | Inicia la conexión manual/VPN. | — |
| `Connect to last radio on start up` | Cuando está marcado, se conecta automáticamente a la última radio utilizada al iniciar. Marcado por defecto. | `AutoConnectToLastRadio` |
| `Enable adaptive frame-rate throttle` | Reduce automáticamente la tasa de cuadros FFT/waterfall cuando la calidad de la red se degrada. | `AdaptiveThrottleEnabled` |
| `Disconnect` | Desconecta la radio actual. | — |

## Indicadores de estado

| Indicador | Significado |
|---|---|
| Etiqueta de estado | Estado actual de la conexión: buscando, conectando, conectado o con error. |
| Etiqueta de resultado manual | Texto de resultado después de probar una IP manual (éxito o error). |
| Etiqueta de advertencia de origen | Advierte cuando la NIC de origen seleccionada está obsoleta o es inalcanzable. |

## Consejos

- El panel de conexión ahora aparece como un diálogo sin bordes. Arrástrelo por la barra de título en la parte superior.
- `SmartLinkEmail` se conserva, por lo que su dirección de correo electrónico se rellena previamente en el siguiente inicio. Su contraseña nunca se almacena.
- Después de iniciar sesión en SmartLink, la etiqueta de estado muestra su nombre, indicativo o confirmación de que ha iniciado sesión.
- La lista `Remote radios` está diseñada para una visualización compacta; desplácese dentro de la lista si la radio que desea no es visible de inmediato.
- El campo `Radio IP address` almacena hasta tres direcciones recientes. Si usó anteriormente la configuración `LastRoutedRadioIp`, AetherSDR la importa automáticamente la primera vez que abre la página Manual después de la actualización.
- En la página Local, puede cambiar rápidamente al modo SmartLink o Manual usando los botones de acceso directo.
- Al cambiar al modo sin bordes o desde él, AetherSDR conserva la geometría del diálogo solo si el diálogo era visible en el momento del cambio.
- El formulario de inicio de sesión de SmartLink ahora incluye sugerencias de accesibilidad para administradores de contraseñas (macOS Passwords, Windows Authenticator, KDE Wallet). Los campos de correo electrónico y contraseña están etiquetados como un "formulario de inicio de sesión de SmartLink" para que los administradores de credenciales puedan definir correctamente el alcance del par de cuentas.

## Solución de problemas

- **La lista `Available radios` está vacía** — Asegúrese de que la radio esté encendida y en la misma red local. Haga clic en `Retry Discovery` para actualizar la lista.
- **La lista `Remote radios` está vacía después de iniciar sesión** — La radio remota puede estar apagada, no registrada en SmartLink o asociada con una cuenta de FlexRadio diferente.
- **`Sign In` produce un error** — Verifique que su correo electrónico y contraseña sean correctos. Verifique sus credenciales en el sitio web de FlexRadio.
- **No se puede conectar por IP** — Asegúrese de que la radio sea accesible en la red. Use `Open Network Diagnostics` para verificar la conectividad.
- **AetherSDR se conecta a la radio incorrecta al iniciar** — Desmarque `Connect to last radio on start up` si desea elegir una radio manualmente cada sesión.

## Relacionado

- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Connect to a local LAN radio](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Enable low-bandwidth mode for slow links](enable-low-bandwidth-mode-for-slow-links.md)
- [Operating remotely over SmartLink](../../operating/remote/remote-operation-smartlink.md)
