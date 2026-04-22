# Conectarse por IP a través de una VPN o red enrutada

Use el modo Manual para conectarse a un FLEX-8600 cuando el descubrimiento por mDNS no puede alcanzarlo — por ejemplo, cuando la radio está en un túnel VPN o en una subred enrutada diferente y ya conoce su dirección IP.

## Antes de comenzar

- Confirme que puede hacer ping a la dirección IP de la radio desde el equipo que ejecuta AetherSDR.
- Tenga a mano la dirección IPv4 de la radio (consúltela en la pasarela VPN, la tabla DHCP del enrutador o el panel frontal de la radio).
- Si su equipo tiene varias interfaces de red (p. ej., un adaptador VPN y una NIC física), decida cuál debe transportar la conexión.

## Pasos

1. Abra la pantalla de conexión. Si no hay ninguna radio conectada, aparece automáticamente en la ventana principal. Si ya hay una radio conectada, vaya a `Settings > Connect to Radio...`.
2. Haga clic en **Connect by IP** en la fila de modos en la parte superior del panel. El panel cambia a la página del modo Manual.
3. En el campo **Radio IP address**, escriba la dirección IPv4 de la radio.
4. (Opcional) Si su equipo tiene más de una interfaz de red, abra el menú desplegable **Advanced: Source path** y seleccione la interfaz que puede alcanzar la radio. Déjelo en la entrada automática predeterminada si no está seguro.
5. (Opcional) Si su enlace es lento o tiene ancho de banda limitado, marque **Use low bandwidth mode**.
6. Haga clic en **Connect by IP**.
7. Observe el **Manual result label** debajo del botón. Indica si el intento de conexión tuvo éxito o falló.

## Qué hace cada control

| Control | Función | Configuración persistente |
|---|---|---|
| Botón de modo **Connect by IP** | Cambia el panel al modo Manual. | `ConnectionMode` |
| **Radio IP address** | La dirección IPv4 a la que AetherSDR se conecta directamente. | `ManualRadioIp` |
| **Advanced: Source path** | Selecciona la interfaz de red local (NIC) utilizada para la conexión. Déjelo en automático a menos que tenga varias interfaces. | `ManualBindSource` |
| **Use low bandwidth mode** | Reduce las tasas de datos del flujo para enlaces lentos o de alta latencia. | `LowBandwidthMode` |
| **Network Diagnostics** | Abre el cuadro de diálogo de diagnóstico de red para inspeccionar la accesibilidad. | — |
| **Connect by IP** (botón de acción) | Inicia la conexión a la dirección indicada en **Radio IP address**. | — |

## Consejos

- Si aparece el **Source warning label**, la interfaz guardada anteriormente en **Advanced: Source path** ya no está disponible. Abra el menú desplegable y elija una interfaz activa, o déjelo en automático.
- Si el descubrimiento está en ejecución y muestra **No local radios found yet**, la pantalla de estado vacío ofrece un botón de acceso directo **Connect by IP** que lo lleva directamente al modo Manual.

## Solución de problemas

- **El Manual result label muestra un error de inmediato** — La radio no es accesible en la dirección ingresada. Verifique la dirección IP, confirme que el túnel VPN esté activo y compruebe que ningún cortafuegos esté bloqueando el puerto 4992 (SmartSDR TCP) entre los dos hosts.
- **El Source warning label aparece en la página Manual** — La NIC guardada en `ManualBindSource` ha desaparecido o no tiene IP. Abra **Advanced: Source path** y elija una interfaz activa.
- **El intento de conexión se queda colgado sin resultado** — Un cortafuegos está descartando paquetes silenciosamente. Use **Network Diagnostics** para examinar la ruta, o revise las reglas del cortafuegos en la red del host de la radio.

## Relacionados

- [Conectarse a una radio en la LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse a una radio remota a través de SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Seleccionar la interfaz de red local para una conexión manual](pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Activar el modo de bajo ancho de banda para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Descripción general de Connect to a Radio](../../features/connection/overview.md)
