# Habilitar el modo de baja latencia para enlaces lentos

El modo de baja latencia reduce la velocidad de los flujos de audio y datos enviados desde la radio. Utilícelo cuando se conecte a través de un enlace lento o congestionado — como un punto de acceso celular, una VPN de larga distancia o una conexión satelital — para reducir las interrupciones y mejorar la estabilidad.

## Antes de comenzar

- AetherSDR debe estar abierto y aún no conectado a una radio, o debe desconectarse primero antes de cambiar esta configuración.
- Sepa qué modo de conexión está utilizando: Local, SmartLink o Manual. La casilla de verificación `LowBandwidthMode` está presente en el panel de conexión independientemente del modo.

## Pasos

1. Abra el panel de conexión. Aparece automáticamente antes de que se conecte una radio. Si ya hay una radio conectada, haga clic en `Settings > Connect to Radio...` y desconéctela primero.
2. Localice la casilla de verificación **Use low bandwidth mode** cerca de la parte inferior del panel de conexión.
3. Marque **Use low bandwidth mode** para habilitar flujos de velocidad reducida.
4. Proceda a conectarse usando su modo preferido — **Local**, **SmartLink** o **Manual** — como de costumbre.

## Qué hace cada control

| Control | Tipo | Valor predeterminado |
|---|---|---|
| Local / SmartLink / Manual (botones de modo) | Botón de opción | Local |
| Available radios | Lista | (no establecido) |
| Connect Selected Radio | Botón pulsador | — |
| No local radios found yet | Indicador | — |
| Retry Discovery | Botón pulsador | — |
| Remote with SmartLink | Botón pulsador | — |
| Connect by IP | Botón pulsador | — |
| Open Network Diagnostics | Botón pulsador | — |
| SmartLink account: Email | Campo de texto | (no establecido) |
| SmartLink account: Password | Campo de contraseña | (no establecido) |
| Sign In | Botón pulsador | — |
| Sign Out | Botón pulsador | — |
| Remote radios | Lista | (no establecido) |
| Connect Remote Radio | Botón pulsador | — |
| Radio IP address | Campo de texto. Almacena hasta tres direcciones IP usadas recientemente. Seleccione una dirección anterior del menú desplegable o escriba una nueva. El campo reemplaza la entrada de texto sin formato utilizada en versiones anteriores. Se almacena como `ManualRadioIp`; las entradas recientes se almacenan como `RecentConnectByIpAddresses`. | (no establecido) |
| Network Diagnostics | Botón pulsador | — |
| Connect by IP (manual) | Botón pulsador | — |
| Advanced: Source path | Cuadro combinado | (no establecido) |
| Use low bandwidth mode | Casilla de verificación | (no establecido) |
| Enable adaptive frame-rate throttle | Casilla de verificación | Falso. Cuando está marcada, AetherSDR reduce automáticamente la velocidad de fotogramas FFT/waterfall cuando la calidad de la red se degrada. Esto ayuda a mantener la estabilidad en enlaces lentos o congestionados sin requerir cambios manuales. Se almacena como `AdaptiveThrottleEnabled`. |
| Connect to last radio on start up | Casilla de verificación. Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y durante el descubrimiento por difusión/sondeo de radio enrutada. Cuando está desmarcada, el cuadro de diálogo de conexión se abre y el usuario debe elegir una radio manualmente cada sesión. Se almacena como `AutoConnectToLastRadio`. | Verdadero (marcada). Nuevo en v0.9.7. Los usuarios existentes mantienen el comportamiento anterior automáticamente. |
| Disconnect | Botón pulsador | — |

## Indicadores

| Indicador | Significado |
|---|---|
| Status label | Estado actual de la conexión (buscando / conectando / conectado / error). |
| Manual result label | Texto de resultado después de sondear una IP manual (éxito o error). |
| Source warning label | Advierte cuando la NIC de origen seleccionada está obsoleta o es inalcanzable. |

## Consejos

- Active **Use low bandwidth mode** o **Enable adaptive frame-rate throttle** antes de iniciar la conexión. Estos ajustes se negocian al momento de la conexión.
- El acelerador adaptativo funciona junto con el modo de baja latencia. Si habilita solo el acelerador adaptativo, AetherSDR reducirá la velocidad de fotogramas cuando sea necesario, pero mantendrá la velocidad de flujo completa en caso contrario.
- Si el audio aún se entrecorta después de habilitar estas opciones, verifique su VPN o ruta de enrutamiento usando `Settings > Network...`.
- El campo **Radio IP address** ahora recuerda hasta tres direcciones recientes. Si guardó previamente una IP con la configuración heredada `LastRoutedRadioIp`, AetherSDR la migra automáticamente la primera vez que abre el panel de conexión.
- Para evitar que AetherSDR se conecte automáticamente al iniciar — por ejemplo, cuando desee elegir una radio diferente — desmarque **Connect to last radio on start up**.
- El panel de conexión ahora usa una ventana sin marco con una barra de título personalizada cuando **FramelessWindow** está habilitado en la configuración (valor predeterminado: Verdadero). El título **Connect to Radio** aparece en la barra de título de la ventana. Para redimensionar el cuadro de diálogo, arrastre desde cualquier borde o esquina. Cuando la ventana sin marco se oculta y luego se muestra de nuevo, se conserva su geometría anterior.
- Al sondear una IP manual, AetherSDR recopila información de estado de la radio, como modelo, apodo, indicativo y estado de MultiFlex durante la negociación de la conexión. Esta información aparece en la lista de radios después de un sondeo exitoso.
- El formulario de inicio de sesión de SmartLink ahora incluye sugerencias de accesibilidad para administradores de contraseñas en macOS, Windows y Linux. Los administradores de contraseñas pueden reconocer y autocompletar automáticamente las credenciales para los campos de la cuenta SmartLink.

## Relacionado

- [Conectar por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Conectarse a una radio remota a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Seleccionar la interfaz de red local utilizada para una conexión manual](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Operación remota a través de SmartLink](../../operating/remote/remote-operation-smartlink.md)
