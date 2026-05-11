# Conectar a una Radio

El Panel de Conexión es la pantalla principal para descubrir y conectarse a una radio FLEX-8600. Ofrece tres modos de conexión: Local (descubrimiento en LAN), SmartLink (remoto a través de internet) y Manual (IP directa o VPN). El panel aparece automáticamente cuando AetherSDR se inicia y no hay ninguna radio conectada, o puede abrirlo en cualquier momento desde `Settings > Connect to Radio...`.

## Antes de empezar

- AetherSDR no debe estar ya conectado a una radio.
- El panel ahora se abre como un diálogo sin marco. Puede arrastrarlo por la barra de título en la parte superior.

## Pasos

### Conectarse a una radio local en LAN

1. Abra el panel de conexión. De forma predeterminada, la pestaña Local está activa.
2. Espere a que AetherSDR descubra radios en la red local. La lista `Available radios` se llena automáticamente.
3. Seleccione una radio de la lista.
4. Haga clic en `Connect Selected Radio`.

### Conectarse a una radio remota a través de SmartLink

1. Abra el panel de conexión.
2. Haga clic en `Remote with SmartLink`. El panel cambia a la página SmartLink.
3. En **SmartLink account**, introduzca el correo electrónico de su cuenta FlexRadio en el campo `SmartLink account: Email`.
4. Introduzca su contraseña en el campo `SmartLink account: Password`. La contraseña no se guarda entre sesiones.
5. Haga clic en `Sign In`. AetherSDR se autentica con SmartLink y, si tiene éxito, llena la lista `Remote radios` con las radios disponibles para su cuenta.
6. Seleccione una radio de la lista `Remote radios`.
7. Haga clic en `Connect Remote Radio`.

### Conectarse por dirección IP (manual o VPN)

1. Abra el panel de conexión.
2. Haga clic en `Connect by IP` (desde la página Local) o seleccione la página Manual directamente.
3. En el campo `Radio IP address`, introduzca la dirección IP o el nombre de host de la radio.
4. (Opcional) Seleccione una interfaz de red del menú desplegable `Advanced: Source path` para vincular la conexión a una NIC específica.
5. (Opcional) Marque `Use low bandwidth mode` para flujos de tasa reducida en enlaces lentos.
6. Haga clic en `Connect by IP (manual)`.

### Controles adicionales

- `Open Network Diagnostics` — Abre un diálogo de diagnóstico para solucionar problemas de conectividad de red.
- `Retry Discovery` — Vuelve a ejecutar el descubrimiento en LAN en la página Local.
- `Disconnect` — Desconecta la radio actual y regresa al panel de conexión.
- `Connect to last radio on start up` — Cuando está marcado (por defecto), AetherSDR se reconecta automáticamente a la última radio utilizada al iniciar. Cuando no está marcado, el panel de conexión se abre en cada sesión.

## Qué hace cada control

| Control | Qué hace | Configuración persistida |
|---|---|---|
| Botones de modo Local / SmartLink / Manual | Cambian el panel entre los tres modos de conexión. | `ConnectionMode` |
| `Available radios` | Muestra las radios LAN descubiertas mediante mDNS/Flex discovery. | — |
| `Connect Selected Radio` | Se conecta a la radio LAN resaltada. | — |
| `No local radios found yet` | Aviso que se muestra cuando el descubrimiento está vacío. | — |
| `Retry Discovery` | Vuelve a ejecutar el descubrimiento en LAN. | — |
| `Remote with SmartLink` | Acceso directo a la página SmartLink. | — |
| `Connect by IP` | Acceso directo a la página Manual. | — |
| `Open Network Diagnostics` | Abre el diálogo de diagnóstico de red. | — |
| `SmartLink account: Email` | Su dirección de correo electrónico de la cuenta FlexRadio. | `SmartLinkEmail` |
| `SmartLink account: Password` | Su contraseña de SmartLink. No se guarda después de que finaliza la sesión. | — |
| `Sign In` | Se autentica con SmartLink y recupera la lista de radios remotas. | — |
| `Sign Out` | Finaliza la sesión actual de SmartLink. | — |
| `Remote radios` | Muestra las radios WAN disponibles para su cuenta después de iniciar sesión. | — |
| `Connect Remote Radio` | Inicia una conexión WAN con la radio remota seleccionada. | — |
| `Radio IP address` | La dirección IP o nombre de host para conectarse en modo Manual. Cuadro combinado editable que recuerda las últimas tres direcciones a las que se conectó correctamente. | `ManualRadioIp` |
| `Advanced: Source path` | Selecciona la interfaz de red local utilizada para la conexión manual. | `ManualBindSource` |
| `Use low bandwidth mode` | Habilita flujos de tasa reducida para enlaces lentos. | `LowBandwidthMode` |
| `Connect by IP (manual)` | Inicia la conexión manual/VPN. | — |
| `Connect to last radio on start up` | Cuando está marcado, se conecta automáticamente a la última radio utilizada al iniciar. Marcado por defecto. | `AutoConnectToLastRadio` |
| `Disconnect` | Desconecta la radio actual. | — |

## Indicadores de estado

| Indicador | Significado |
|---|---|
| Etiqueta de estado | Estado actual de la conexión: buscando, conectando, conectado o con error. |
| Etiqueta de resultado manual | Texto de resultado después de sondear una IP manual (éxito o error). |
| Etiqueta de advertencia de origen | Advierte cuando la NIC de origen seleccionada está desactualizada o es inalcanzable. |

## Consejos

- El panel de conexión ahora aparece como un diálogo sin marco. Arrástrelo por la barra de título en la parte superior.
- `SmartLinkEmail` se persiste, por lo que su dirección de correo electrónico se rellena previamente en el siguiente inicio. Su contraseña nunca se almacena.
- Después de iniciar sesión en SmartLink, la etiqueta de estado muestra su nombre, indicativo o una confirmación de que ha iniciado sesión.
- La lista `Remote radios` tiene un tamaño para una visualización compacta; desplace la lista si la radio que desea no es visible de inmediato.
- El campo `Radio IP address` almacena hasta tres direcciones recientes. Si utilizó anteriormente la configuración `LastRoutedRadioIp`, AetherSDR la importa automáticamente la primera vez que abre la página Manual después de una actualización.
- En la página Local, puede cambiar rápidamente al modo SmartLink o Manual usando los botones de acceso directo.

## Solución de problemas

- **La lista `Available radios` está vacía** — Asegúrese de que la radio esté encendida y en la misma red local. Haga clic en `Retry Discovery` para actualizar la lista.
- **La lista `Remote radios` está vacía después de iniciar sesión** — La radio remota puede estar apagada, no registrada en SmartLink o asociada con una cuenta FlexRadio diferente.
- **`Sign In` produce un error** — Verifique que su correo electrónico y contraseña sean correctos. Compruebe sus credenciales en el sitio web de FlexRadio.
- **No se puede conectar por IP** — Asegúrese de que la radio sea accesible en la red. Use `Open Network Diagnostics` para verificar la conectividad.
- **AetherSDR se conecta a la radio incorrecta al iniciar** — Desmarque `Connect to last radio on start up` si desea elegir una radio manualmente cada sesión.

## Relacionado

- [Conectarse a una radio remota a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse a una radio local en LAN](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Habilitar el modo de ancho de banda bajo para enlaces lentos](enable-low-bandwidth-mode-for-slow-links.md)
- [Operación remota a través de SmartLink](../../operating/remote/remote-operation-smartlink.md)
