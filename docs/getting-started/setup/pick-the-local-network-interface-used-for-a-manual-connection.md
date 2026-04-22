# Seleccionar la interfaz de red local para una conexión manual

Al conectarse por IP a través de una VPN o una red enrutada, AetherSDR necesita saber qué interfaz de red local (NIC) usar como origen del tráfico saliente. Esta página explica cómo seleccionar esa interfaz mediante el control **Advanced: Source path** en la página de conexión manual.

## Antes de comenzar

- Debe estar usando el modo de conexión **Connect by IP**. El control **Advanced: Source path** no está disponible en los modos Local ni Remote with SmartLink.
- Necesita saber qué interfaz de red de su computadora tiene acceso al radio. Si no está seguro, revise la configuración de red de su sistema operativo o use `Settings > Network...` para abrir los diagnósticos de red.
- Tenga listo el IP del radio para introducirlo en **Radio IP address**.

## Pasos

1. Abra el panel **Connect to a Radio**. Si ya hay un radio conectado, vaya a `Settings > Connect to Radio...`.
2. Haga clic en **Connect by IP** en la fila de modos en la parte superior del panel.
3. Localice el cuadro combinado **Advanced: Source path** cerca de la parte inferior de la página Manual.
4. Abra el menú desplegable **Advanced: Source path**. La lista muestra todas las interfaces de red detectadas actualmente en su computadora.
5. Seleccione la interfaz que tiene ruta hacia el radio. Para una conexión VPN, elija el adaptador VPN. Para una segunda NIC física, elija la entrada de esa NIC.
6. Revise el **Source warning label** debajo del cuadro combinado. Si muestra una advertencia como `<interface> (unavailable, last <address>)`, la interfaz guardada anteriormente ya no está disponible. Seleccione en cambio una interfaz activa de la lista.
7. Introduzca la dirección IP del radio en **Radio IP address**.
8. Haga clic en **Connect by IP** para iniciar la conexión.

## Qué hace cada control

| Control | Función | Ajuste persistente |
|---|---|---|
| **Advanced: Source path** | Selecciona la NIC local usada como dirección de origen para la conexión manual. Cuando se establece en una interfaz explícita, AetherSDR vincula el tráfico saliente a esa interfaz. | `ManualBindSource` |
| **Radio IP address** | La dirección IP o nombre de host del radio FLEX-8600 al que conectarse. | `ManualRadioIp` |
| **Use low bandwidth mode** | Habilita flujos de audio y datos a tasa reducida; útil para enlaces VPN lentos o con alta latencia. | `LowBandwidthMode` |
| **Network Diagnostics** | Abre el panel de diagnósticos de red para verificar la accesibilidad de las interfaces sin salir de la pantalla de conexión. | — |

## Consejos

- Si anteriormente se conectó exitosamente y la interfaz ha cambiado desde entonces (por ejemplo, a una VPN se le asignó un adaptador diferente), el **Source warning label** mostrará la última dirección IPv4 conocida junto al nombre de la interfaz no disponible. Seleccione la interfaz correcta antes de intentar reconectarse.
- Si ninguna de las interfaces en **Advanced: Source path** conduce al radio, verifique que su VPN o enrutamiento esté activo antes de abrir AetherSDR, ya que la detección de interfaces se ejecuta al cargar el panel.

## Solución de problemas

- **El Source warning label muestra la interfaz guardada como no disponible** — La NIC seleccionada durante una sesión anterior ya no está presente o no tiene dirección IP. Abra **Advanced: Source path** y elija la interfaz que está activa actualmente en su sistema.
- **El intento de conexión falla inmediatamente después de seleccionar una interfaz** — Es posible que la interfaz seleccionada no tenga ruta hacia la subred del radio. Confirme la tabla de enrutamiento de su computadora y vuelva a intentarlo con la interfaz correcta seleccionada.
- **Advanced: Source path está vacío o no muestra entradas útiles** — AetherSDR no encontró interfaces de red utilizables al iniciarse. Verifique que su VPN o adaptador de red esté conectado y tenga una dirección IP asignada; luego reabra `Settings > Connect to Radio...` para recargar la lista de interfaces.

## Relacionado

- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Conectarse a un radio en la LAN local](connect-to-a-local-lan-radio.md)
- [Habilitar el modo de bajo ancho de banda para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Reintentar la detección cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
