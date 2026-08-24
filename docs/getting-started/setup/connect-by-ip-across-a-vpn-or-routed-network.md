# Conectar por IP a través de una VPN o red enrutada

Use este método cuando su FLEX-8600 esté en una subred diferente a la de su computadora — por ejemplo, a través de un túnel VPN o una red de estación enrutada — y el descubrimiento mDNS no pueda alcanzarla. Usted ingresará la dirección IP de la radio directamente y AetherSDR abrirá la conexión del protocolo SmartSDR sin depender del descubrimiento.

## Antes de comenzar

- Debe conocer la dirección IPv4 o el nombre de host de la radio en la red remota o VPN.
- La radio debe ser accesible desde su computadora (haga ping primero para confirmar que el enrutamiento funciona).
- Si se conecta a través de un enlace lento o medido, decida de antemano si desea habilitar el modo de bajo ancho de banda.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente antes de que una radio esté conectada. Si ya hay una radio conectada, vaya a `Settings > Connect to Radio...` o desconéctela primero.
2. Haga clic en **Manual** en la fila de botones de modo en la parte superior del panel. El panel cambia a la página de conexión manual. (Se guarda como `ConnectionMode` = `ManualMode`).
3. Elija la familia de radio en **Advanced: Radio family**. Seleccione **FlexRadio** o **Icom** según la radio a la que se esté conectando. La selección se recuerda por dirección IP. (Se guarda como `ConnectByIpRadioFamily`).
4. En el campo **Radio IP address**, escriba la dirección IPv4 o el nombre de host de su radio, o seleccione una dirección usada recientemente de la lista desplegable. AetherSDR almacena hasta tres direcciones recientes. Este valor se guarda como `ManualRadioIp`. Los nombres de host como `ic-705.local` ahora se recuerdan en la lista de recientes.
5. Si su computadora tiene más de una interfaz de red y necesita controlar cuál se usa para la conexión, seleccione la interfaz correcta en **Advanced: Source path**. Esto se guarda como `ManualBindSource`. Si no está seguro, déjelo en la selección automática predeterminada.
6. Si el enlace es lento o medido, marque **Use low bandwidth mode** para habilitar flujos de tasa reducida. Esto se guarda como `LowBandwidthMode`.
7. Para reducir aún más el ancho de banda en enlaces muy lentos, marque **Enable adaptive frame-rate throttle**. Cuando está habilitado, AetherSDR reduce automáticamente las tasas de fotogramas de FFT y waterfall cuando la calidad de la red se degrada. Esto se guarda como `AdaptiveThrottleEnabled`. Por defecto, esta opción está desmarcada.
8. Si no desea que AetherSDR se conecte automáticamente a la última radio usada cada vez que se inicia, desmarque **Connect to last radio on start up**. Esto se guarda como `AutoConnectToLastRadio`. La casilla está habilitada por defecto.
9. Haga clic en **Connect by IP (manual)** (el botón en la parte inferior de la página manual). AetherSDR prueba la dirección y muestra el resultado en la etiqueta de resultado manual debajo del botón.
10. Observe la etiqueta de estado. Cuando muestre un estado conectado, la radio estará lista para usar.

## Qué hace cada control

| Control | Qué hace | Clave guardada |
|---|---|---|
| **Local / SmartLink / Manual** (botones de modo) | Cambia el panel entre los tres modos de conexión. | `ConnectionMode` |
| **Advanced: Radio family** | Selecciona la familia de protocolo para la conexión manual: FlexRadio o Icom. La selección se almacena por dirección IP y usa FlexRadio por defecto para perfiles antiguos. | `ConnectByIpRadioFamily` |
| **Radio IP address** | La dirección IPv4 o el nombre de host al que AetherSDR se conecta directamente. Escriba una nueva dirección o seleccione una de las últimas tres usadas de la lista desplegable. | `ManualRadioIp` |
| **Advanced: Source path** | Selecciona la interfaz de red local (NIC) utilizada para la conexión saliente. | `ManualBindSource` |
| **Use low bandwidth mode** | Reduce las tasas de datos de flujo para enlaces lentos o medidos. | `LowBandwidthMode` |
| **Enable adaptive frame-rate throttle** | Reduce automáticamente las tasas de fotogramas de FFT y waterfall cuando la calidad de la red se degrada, para enlaces muy lentos. | `AdaptiveThrottleEnabled` |
| **Connect to last radio on start up** | Cuando está marcada, AetherSDR se conecta automáticamente a la última radio usada al iniciar y al sondear por descubrimiento de difusión / radio enrutada. Cuando está desmarcada, se abre el diálogo de conexión y el usuario debe elegir una radio manualmente en cada sesión. Está marcada por defecto. | `AutoConnectToLastRadio` |
| **Connect by IP (manual)** (botón de acción) | Inicia el intento de conexión a la dirección IP ingresada. | — |
| **Network Diagnostics** | Abre el diálogo de diagnóstico de red desde la página manual. | — |
| Etiqueta de resultado manual | Muestra el resultado de la última prueba de conexión (texto de éxito o error). | — |
| Etiqueta de advertencia de fuente | Advierte cuando la interfaz seleccionada en **Advanced: Source path** ya no está disponible o su última dirección conocida ha cambiado. | — |

## Consejos

- El campo **Radio IP address** mantiene un historial desplegable de las últimas tres direcciones a las que se conectó exitosamente. Haga clic en la flecha para volver a seleccionar una dirección anterior sin volver a escribirla. Los nombres de host como `ic-705.local` ahora se recuerdan junto con las direcciones numéricas.
- La selección de **Advanced: Radio family** se recuerda independientemente para cada dirección IP. Los perfiles antiguos sin una familia explícita usan FlexRadio por defecto, lo que coincide con el comportamiento anterior.
- Si la etiqueta de advertencia de fuente muestra que su interfaz guardada no está disponible, abra **Advanced: Source path** y vuelva a seleccionar la NIC correcta para su adaptador VPN. La advertencia aparece cuando la interfaz guardada anteriormente está obsoleta o es inaccesible.
- Si llega a la página **Local** y ve "No local radios found yet", haga clic en **Connect by IP** en el aviso para saltar directamente a la página manual.
- Si se conectó anteriormente con una versión antigua de AetherSDR, su última dirección IP usada se migra automáticamente al historial de direcciones recientes en el primer inicio.

## Solución de problemas

- **La etiqueta de resultado manual muestra un error inmediatamente después de hacer clic en Connect by IP (manual)** — La radio no responde en esa dirección. Confirme que la IP o el nombre de host sean correctos, que el túnel VPN esté activo y que ningún cortafuegos en la red de la radio esté bloqueando el puerto de protocolo (4992 para FlexRadio, 50001 para Icom).
- **La etiqueta de advertencia de fuente dice que la fuente guardada no está disponible** — Su adaptador VPN ha cambiado o está caído. Restablezca la conexión VPN y luego vuelva a seleccionar el adaptador en **Advanced: Source path**.
- **La prueba de conexión tiene éxito pero la radio nunca alcanza un estado conectado** — Los flujos de datos UDP pueden estar bloqueados. Verifique que su VPN o enrutador permita tráfico UDP bidireccional entre su computadora y la radio.
- **La ventana de conexión se abre en modo sin marco y la geometría no se restaura correctamente cuando la ventana se muestra nuevamente** — Este problema se ha resuelto. La geometría de la ventana ahora se restaura correctamente solo cuando la ventana estuvo visible anteriormente.

## Relacionado

- [Conectar a una radio LAN local](connect-to-a-local-lan-radio.md)
- [Conectar a una radio remota a través de SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Elegir la interfaz de red local usada para una conexión manual](pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Habilitar el modo de bajo ancho de banda para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- Habilitar el limitador adaptativo de tasa de fotogramas para enlaces muy lentos
- [Resumen de conexión a una radio](../../features/connection/overview.md)
