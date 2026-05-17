# Habilitar el modo de ancho de banda reducido para enlaces lentos

El modo de ancho de banda reducido disminuye la tasa de flujos de audio y datos enviados desde la radio. Úselo al conectarse a través de un enlace lento o congestionado — como un punto de acceso celular, una VPN de larga distancia, o una conexión satelital — para reducir las interrupciones y mejorar la estabilidad.

## Antes de comenzar

- AetherSDR debe estar abierto y aún no conectado a una radio, o debe desconectarse primero antes de cambiar esta configuración.
- Sepa qué modo de conexión está utilizando: Local, SmartLink, o Manual. La casilla de verificación `LowBandwidthMode` está presente en el panel de conexión independientemente del modo.

## Pasos

1. Abra el panel de conexión. Aparece automáticamente antes de que una radio esté conectada. Si ya hay una radio conectada, haga clic en `Settings > Connect to Radio...` y desconéctese primero.
2. Localice la casilla **Use low bandwidth mode** cerca de la parte inferior del panel de conexión.
3. Marque **Use low bandwidth mode** para habilitar flujos de tasa reducida.
4. Proceda a conectarse usando su modo preferido — **Local**, **SmartLink**, o **Manual** — como de costumbre.

## Qué hace cada control

| Control | Tipo | Valor predeterminado |
|---|---|---|
| Local / SmartLink / Manual (botones de modo) | Botón de opción | Local |
| Radios disponibles | Lista | (no establecido) |
| Connect Selected Radio | Botón pulsador | — |
| No local radios found yet | Indicador | — |
| Retry Discovery | Botón pulsador | — |
| Remote with SmartLink | Botón pulsador | — |
| Connect by IP | Botón pulsador | — |
| Open Network Diagnostics | Botón pulsador | — |
| SmartLink account: Email | Campo de texto | (no establecido) |
| SmartLink account: Password | Campo de texto | (no establecido) |
| Sign In | Botón pulsador | — |
| Sign Out | Botón pulsador | — |
| Radios remotas | Lista | (no establecido) |
| Connect Remote Radio | Botón pulsador | — |
| Radio IP address | Campo de texto. Almacena hasta tres direcciones IP usadas recientemente. Seleccione una dirección anterior del menú desplegable o escriba una nueva. El campo reemplaza la entrada de texto simple utilizada en versiones anteriores. Se almacena como `ManualRadioIp`; las entradas recientes se almacenan como `RecentConnectByIpAddresses`. | (no establecido) |
| Network Diagnostics | Botón pulsador | — |
| Connect by IP (manual) | Botón pulsador | — |
| Advanced: Source path | Cuadro combinado | (no establecido) |
| Use low bandwidth mode | Casilla de verificación | (no establecido) |
| Connect to last radio on start up | Casilla de verificación. Cuando está marcada, AetherSDR se conecta automáticamente a la última radio usada al iniciar y en la sonda de descubrimiento por difusión / ruteo de radio. Cuando no está marcada, se abre el cuadro de diálogo de conexión y el usuario debe elegir una radio manualmente cada sesión. Se almacena como `AutoConnectToLastRadio`. | Verdadero (marcada). Nuevo en v0.9.7. Los usuarios existentes mantienen el comportamiento anterior automáticamente. |
| Disconnect | Botón pulsador | — |

## Indicadores

| Indicador | Significado |
|---|---|
| Etiqueta de estado | Estado actual de la conexión (buscando / conectando / conectado / con error). |
| Etiqueta de resultado manual | Texto de resultado después de sondear una IP manual (éxito o error). |
| Etiqueta de advertencia de origen | Advierte cuando la NIC de origen seleccionada está obsoleta o es inalcanzable. |

## Consejos

- Active **Use low bandwidth mode** antes de iniciar la conexión. El modo se negocia en el momento de la conexión.
- Si el audio aún se interrumpe después de habilitar el modo de ancho de banda reducido, verifique su ruta VPN o de enrutamiento usando `Settings > Network...`.
- El campo **Radio IP address** ahora recuerda hasta tres direcciones recientes. Si guardó previamente una IP bajo la configuración heredada `LastRoutedRadioIp`, AetherSDR la migra automáticamente la primera vez que abra el panel de conexión.
- Para evitar que AetherSDR se conecte automáticamente al iniciar — por ejemplo, cuando desee elegir una radio diferente — desmarque **Connect to last radio on start up**.
- El panel de conexión ahora utiliza una ventana sin marco con una barra de título personalizada cuando **FramelessWindow** está habilitado en la configuración (predeterminado: Verdadero). El título **Connect to Radio** aparece en la barra de título de la ventana. Para redimensionar el cuadro de diálogo, arrastre desde cualquier borde o esquina. Cuando la ventana sin marco se oculta y luego se muestra nuevamente, su geometría anterior se conserva.
- Al sondear una IP manual, AetherSDR recopila información del estado de la radio, como modelo, apodo, indicativo y estado de MultiFlex durante la negociación de la conexión. Esta información aparece en la lista de radios después de una sonda exitosa.

## Relacionado

- [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Pick the local network interface used for a manual connection](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Operating remotely over SmartLink](../../operating/remote/remote-operation-smartlink.md)
