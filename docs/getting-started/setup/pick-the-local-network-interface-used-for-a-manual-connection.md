# Seleccione la interfaz de red local para una conexión manual

Al conectarse mediante IP a través de una VPN o una red enrutada, AetherSDR le permite elegir qué interfaz de red local (NIC) utiliza su computadora para llegar a la radio. Esto es importante cuando su máquina tiene varias interfaces de red y la ruta predeterminada no conduce a la radio.

## Antes de comenzar

- Debe conocer la dirección IP de la radio. Consulte [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md).
- El ConnectionPanel debe estar visible. Aparece automáticamente antes de conectar una radio, o puede abrirlo mediante `Settings > Connect to Radio...`.

## Pasos

1. En el ConnectionPanel, haga clic en `Connect by IP` para cambiar a la página de modo manual.
2. Ingrese la dirección IP de la radio en el campo `Radio IP address`. Este valor se guarda como `ManualRadioIp`. Si se ha conectado a esta radio antes, puede abrir la lista desplegable `Radio IP address` y seleccionarla de la lista de direcciones recientes en lugar de volver a escribirla.
3. Localice el cuadro combinado `Advanced: Source path` debajo del campo de dirección IP.
4. Abra el cuadro combinado y seleccione la interfaz de red local que desea usar para esta conexión. La interfaz seleccionada se guarda como `ManualBindSource`.
5. Si la interfaz que guardó anteriormente ya no está disponible, aparece una `Source warning label` debajo del cuadro combinado indicando que la fuente guardada está obsoleta o es inalcanzable. Seleccione una interfaz actualmente disponible antes de continuar.
6. Haga clic en `Connect by IP` para iniciar la conexión.

## Función de cada control

| Control | Función | Clave persistida |
|---|---|---|
| `Radio IP address` | La dirección IP o nombre de host de la radio a la que conectarse. Se muestra como un cuadro combinado editable; la lista desplegable muestra hasta tres direcciones usadas recientemente. | `ManualRadioIp` |
| `Advanced: Source path` | Selecciona la NIC local a la que AetherSDR se vincula al abrir la conexión. Déjelo en la entrada automática predeterminada a menos que necesite forzar una interfaz específica. | `ManualBindSource` |
| `Use low bandwidth mode` | Reduce las tasas de datos de transmisión para enlaces lentos o congestionados. | `LowBandwidthMode` |
| `Enable adaptive frame-rate throttle` | Reduce automáticamente la velocidad de fotogramas de FFT/waterfall cuando la calidad de la red se degrada. Útil para enlaces lentos o intermitentes. Sin marcar por defecto. | `AdaptiveThrottleEnabled` |
| `Connect to last radio on start up` | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio usada al iniciar y durante la detección por difusión / sonda de radio enrutada. Cuando no está marcado, se abre el diálogo de conexión y el usuario debe seleccionar una radio manualmente en cada sesión. Por defecto está marcado. | `AutoConnectToLastRadio` |
| `Connect by IP` (botón) | Inicia la conexión manual usando la IP y la fuente de ruta configuradas arriba. | — |
| `Network Diagnostics` (botón) | Abre el diálogo de Diagnósticos de Red para ayudar a solucionar problemas de conectividad. | — |
| `Source warning label` (indicador) | Advierte cuando la NIC fuente seleccionada está obsoleta o es inalcanzable. | — |
| `Manual result label` (indicador) | Muestra el texto de resultado después de sondear una IP manual (éxito o error). | — |

## Consejos

- Si la interfaz guardada anteriormente no está disponible, la `Source warning label` muestra el nombre (o ID) de la interfaz guardada y la última dirección IPv4 conocida. Elija una interfaz diferente de `Advanced: Source path` antes de conectar.
- En una máquina con una sola interfaz de red, la selección de `Advanced: Source path` no tiene efecto práctico. Es más útil en máquinas con interfaces separadas de red cableada, inalámbrica y VPN.
- Si está en un enlace lento como una conexión celular o satelital, active `Use low bandwidth mode` en la misma página antes de hacer clic en `Connect by IP`.
- Para enlaces con latencia variable, active `Enable adaptive frame-rate throttle`. Esto reduce la velocidad de fotogramas de FFT y waterfall cuando la calidad de la red disminuye, manteniendo la conexión utilizable.
- El campo `Radio IP address` conserva las tres direcciones más recientemente usadas. Seleccione una dirección anterior de la lista desplegable para evitar volver a escribirla.
- Si desmarca `Connect to last radio on start up`, AetherSDR abre el diálogo de conexión en cada inicio y espera a que usted seleccione una radio manualmente.
- Las listas de radios locales y remotas tienen ahora una altura máxima de 240 píxeles y se desplazan internamente. Si tiene muchas radios descubiertas, desplace dentro de la lista para llegar a las entradas que no son visibles inmediatamente. Esto evita que la lista crezca más allá del diálogo en pantallas pequeñas (por ejemplo, un panel de 1024×600).
- Haga clic derecho en una radio local descubierta para establecer un apodo personalizado sin conectarse primero. Esto está disponible para radios que no son Flex (como HL2 o radios simuladas). Los nombres de las radios Flex se configuran desde Radio Setup mientras está conectado.
- El ConnectionPanel conserva su geometría de ventana al alternar el modo sin marco.

## Solución de problemas

- **`Source warning label` aparece después de seleccionar una interfaz** — La interfaz guardada en `ManualBindSource` ya no está presente o no tiene una dirección activa. Abra `Advanced: Source path` y seleccione una interfaz actualmente disponible.
- **La conexión falla inmediatamente después de hacer clic en `Connect by IP`** — El `Manual result label` debajo del botón muestra el error. Verifique que la IP en `Radio IP address` sea alcanzable desde la interfaz seleccionada en `Advanced: Source path`. Use `Network Diagnostics` en la misma página para verificar la accesibilidad.

## Relacionado

- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Enable low-bandwidth mode for slow links](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Connect to a local LAN radio](connect-to-a-local-lan-radio.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
