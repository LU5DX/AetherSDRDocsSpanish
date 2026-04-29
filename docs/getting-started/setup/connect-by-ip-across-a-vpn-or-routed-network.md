# Conectar por IP a través de una VPN o red enrutada

Use este método cuando su FLEX-8600 se encuentra en una subred diferente a la de su computadora — por ejemplo, a través de un túnel VPN o una red de estación enrutada — y la detección por mDNS no puede alcanzarlo. Deberá ingresar la dirección IP del radio directamente y AetherSDR abrirá la conexión de protocolo SmartSDR sin depender de la detección automática.

## Antes de comenzar

- Debe conocer la dirección IPv4 del radio en la red remota o VPN.
- El radio debe ser accesible desde su computadora (haga ping primero para confirmar que el enrutamiento funciona).
- Si se conecta a través de un enlace lento o con datos medidos, decida con anticipación si desea habilitar el modo de bajo ancho de banda.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente antes de que se conecte un radio. Si ya hay un radio conectado, vaya a `Settings > Connect to Radio...` o desconéctelo primero.
2. Haga clic en **Connect by IP** en la fila de botones de modo en la parte superior del panel. El panel cambia a la página de conexión manual. (Se guarda como `ConnectionMode` = `ManualMode`.)
3. En el campo **Radio IP address**, escriba la dirección IPv4 de su FLEX-8600. Este valor se guarda como `ManualRadioIp`.
4. Si su computadora tiene más de una interfaz de red y necesita controlar cuál se usa para la conexión, seleccione la interfaz correcta en **Advanced: Source path**. Esto se guarda como `ManualBindSource`. Si no está seguro, déjelo en la selección automática predeterminada.
5. Si el enlace es lento o con datos medidos, marque **Use low bandwidth mode** para habilitar flujos de datos a tasa reducida. Esto se guarda como `LowBandwidthMode`.
6. Haga clic en **Connect by IP** (el botón en la parte inferior de la página manual). AetherSDR sondea la dirección y muestra el resultado en la etiqueta de resultado manual debajo del botón.
7. Observe la etiqueta de estado. Cuando muestre un estado conectado, el radio está listo para usar.

## Qué hace cada control

| Control | Qué hace | Clave guardada |
|---|---|---|
| **Connect by IP** (botón de modo) | Cambia el panel a la página de conexión manual. | `ConnectionMode` |
| **Radio IP address** | La dirección IPv4 que AetherSDR marca directamente. | `ManualRadioIp` |
| **Advanced: Source path** | Selecciona la interfaz de red local (NIC) utilizada para la conexión saliente. | `ManualBindSource` |
| **Use low bandwidth mode** | Reduce las tasas de datos del flujo para enlaces lentos o con datos medidos. | `LowBandwidthMode` |
| **Connect by IP** (botón de acción) | Inicia el intento de conexión a la dirección IP ingresada. | — |
| **Network Diagnostics** | Abre el diálogo de diagnóstico de red desde la página manual. | — |
| Etiqueta de resultado manual | Muestra el resultado del último sondeo de conexión (texto de éxito o error). | — |
| Etiqueta de advertencia de origen | Advierte cuando la interfaz seleccionada en **Advanced: Source path** ya no está disponible o su última dirección conocida ha cambiado. | — |

## Consejos

- Si la etiqueta de advertencia de origen indica que la interfaz guardada no está disponible, abra **Advanced: Source path** y vuelva a seleccionar la NIC correcta para su adaptador VPN. La advertencia aparece cuando la interfaz guardada anteriormente está desactualizada o es inaccesible.
- Si llega a la página **On This Network** y ve "No local radios found yet", haga clic en **Connect by IP** en el aviso para ir directamente a la página manual.

## Solución de problemas

- **La etiqueta de resultado manual muestra un error inmediatamente después de hacer clic en Connect by IP** — El radio no responde en esa dirección. Confirme que la IP es correcta, que el túnel VPN está activo y que ningún firewall en la red del radio está bloqueando el puerto TCP 4992 (el puerto de comandos SmartSDR).
- **La etiqueta de advertencia de origen indica que el origen guardado no está disponible** — Su adaptador VPN ha cambiado o está inactivo. Restablezca la conexión VPN y luego vuelva a seleccionar el adaptador en **Advanced: Source path**.
- **El sondeo de conexión tiene éxito pero el radio nunca alcanza un estado conectado** — Es posible que los flujos de datos UDP estén bloqueados. Verifique que su VPN o enrutador permita tráfico UDP bidireccional entre su computadora y el radio.

## Relacionados

- [Conectar a un radio en la LAN local](connect-to-a-local-lan-radio.md)
- [Conectar a un radio remoto a través de SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Seleccionar la interfaz de red local para una conexión manual](pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Habilitar el modo de bajo ancho de banda para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Descripción general de Connect to a Radio](../../features/connection/overview.md)
