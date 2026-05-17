# Conectar por IP a través de una VPN o red enrutada

Utilice este método cuando su FLEX-8600 esté en una subred diferente a la de su computadora, por ejemplo, a través de un túnel VPN o una red de estación enrutada, y la detección mDNS no pueda alcanzarlo. Ingresará la dirección IP de la radio directamente y AetherSDR abrirá la conexión del protocolo SmartSDR sin depender de la detección.

## Antes de comenzar

- Debe conocer la dirección IPv4 de la radio en la red remota o VPN.
- La radio debe ser accesible desde su computadora (verifique primero con un ping para confirmar que el enrutamiento funcione).
- Si se conecta a través de un enlace lento o medido, decida de antemano si desea habilitar el modo de ancho de banda reducido.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente antes de que una radio esté conectada. Si ya hay una radio conectada, vaya a `Settings > Connect to Radio...` o desconéctela primero.
2. Haga clic en **Connect by IP** en la fila de botones de modo en la parte superior del panel. El panel cambia a la página de conexión manual. (Se conserva como `ConnectionMode` = `ManualMode`).
3. En el campo **Radio IP address**, escriba la dirección IPv4 de su FLEX-8600, o seleccione una dirección usada recientemente de la lista desplegable. AetherSDR almacena hasta tres direcciones recientes. Este valor se guarda como `ManualRadioIp`.
4. Si su computadora tiene más de una interfaz de red y necesita controlar cuál se utiliza para la conexión, seleccione la interfaz correcta en **Advanced: Source path**. Esto se guarda como `ManualBindSource`. Si no está seguro, déjelo en la selección automática predeterminada.
5. Si el enlace es lento o medido, marque **Use low bandwidth mode** para habilitar flujos de datos de tasa reducida. Esto se guarda como `LowBandwidthMode`.
6. Si no desea que AetherSDR se conecte automáticamente a la última radio utilizada cada vez que se inicie, desmarque **Connect to last radio on start up**. Esto se guarda como `AutoConnectToLastRadio`. La casilla de verificación está habilitada por defecto.
7. Haga clic en **Connect by IP** (el botón en la parte inferior de la página manual). AetherSDR sondea la dirección y muestra el resultado en la etiqueta de resultado manual debajo del botón.
8. Observe la etiqueta de estado. Cuando muestre un estado conectado, la radio estará lista para usar.

## Qué hace cada control

| Control | Qué hace | Clave persistida |
|---|---|---|
| **Connect by IP** (botón de modo) | Cambia el panel a la página de conexión manual. | `ConnectionMode` |
| **Radio IP address** | La dirección IPv4 a la que AetherSDR se conecta directamente. Escriba una nueva dirección o seleccione una de las últimas tres direcciones usadas de la lista desplegable. | `ManualRadioIp` |
| **Advanced: Source path** | Selecciona la interfaz de red local (NIC) utilizada para la conexión saliente. | `ManualBindSource` |
| **Use low bandwidth mode** | Reduce las tasas de datos del flujo para enlaces lentos o medidos. | `LowBandwidthMode` |
| **Connect to last radio on start up** | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al inicio y durante la detección por difusión / sonda de radio enrutada. Cuando no está marcado, se abre el diálogo de conexión y el usuario debe seleccionar una radio manualmente cada sesión. Por defecto está marcado. | `AutoConnectToLastRadio` |
| **Connect by IP** (botón de acción) | Inicia el intento de conexión a la dirección IP ingresada. | — |
| **Network Diagnostics** | Abre el diálogo de diagnóstico de red desde la página manual. | — |
| Etiqueta de resultado manual | Muestra el resultado del último sondeo de conexión (texto de éxito o error). | — |
| Etiqueta de advertencia de origen | Advierte cuando la interfaz seleccionada en **Advanced: Source path** ya no está disponible o su última dirección conocida ha cambiado. | — |

## Consejos

- El campo **Radio IP address** mantiene un historial desplegable de las últimas tres direcciones a las que se conectó exitosamente. Haga clic en la flecha para volver a seleccionar una dirección anterior sin tener que escribirla de nuevo.
- Si la etiqueta de advertencia de origen muestra que su interfaz guardada no está disponible, abra **Advanced: Source path** y vuelva a seleccionar la NIC correcta para su adaptador VPN. La advertencia aparece cuando la interfaz guardada previamente está obsoleta o es inaccesible.
- Si llega a la página **On This Network** y ve "No local radios found yet", haga clic en **Connect by IP** en el aviso para saltar directamente a la página manual.
- Si se conectó anteriormente usando una versión anterior de AetherSDR, su última dirección IP utilizada se migra automáticamente al historial de direcciones recientes en el primer inicio.

## Solución de problemas

- **La etiqueta de resultado manual muestra un error inmediatamente después de hacer clic en Connect by IP** — La radio no responde en esa dirección. Confirme que la IP sea correcta, que el túnel VPN esté activo y que ningún cortafuegos en la red de la radio esté bloqueando el puerto TCP 4992 (el puerto de comando de SmartSDR).
- **La etiqueta de advertencia de origen indica que el origen guardado no está disponible** — Su adaptador VPN ha cambiado o está caído. Restablezca la conexión VPN y luego vuelva a seleccionar el adaptador en **Advanced: Source path**.
- **El sondeo de conexión tiene éxito pero la radio nunca alcanza un estado conectado** — Los flujos de datos UDP pueden estar bloqueados. Verifique que su VPN o enrutador permita el tráfico UDP bidireccional entre su computadora y la radio.
- **La ventana de conexión se abre en modo sin marco y la geometría no se restaura correctamente cuando la ventana se muestra de nuevo** — Este problema se ha resuelto. La geometría de la ventana ahora se restaura correctamente solo cuando la ventana estaba visible anteriormente.

## Relacionados

- [Connect to a local LAN radio](connect-to-a-local-lan-radio.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Pick the local network interface used for a manual connection](pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Enable low-bandwidth mode for slow links](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Connect to a Radio overview](../../features/connection/overview.md)
