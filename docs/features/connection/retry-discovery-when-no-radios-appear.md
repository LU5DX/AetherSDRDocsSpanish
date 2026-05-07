# Reintento de descubrimiento cuando no aparecen radios

Cuando el descubrimiento local de AetherSDR no encuentra radios, aparece el aviso "No local radios found yet" en lugar de la lista de radios. Esta página explica cómo iniciar un nuevo escaneo de descubrimiento y qué probar si la lista sigue vacía.

## Antes de comenzar

- AetherSDR está abierto y muestra el panel "Connect to a Radio". Si no está visible, vaya a `Settings > Connect to Radio...`.
- Su FLEX-8600 está encendido y conectado a la misma LAN que su computadora.

## Pasos

1. En el panel "Connect to a Radio", confirme que **Local** sea el modo seleccionado. Si no lo es, haga clic en **Local**.
2. Si el aviso "No local radios found yet" está visible, haga clic en **Retry Discovery**.
3. Espere unos segundos mientras AetherSDR escucha paquetes de descubrimiento. Si su radio es encontrada, aparece en la lista **Available radios**.
4. Seleccione su radio en la lista **Available radios** y luego haga clic en **Connect Selected Radio**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Local** | Botón de modo | Cambia al modo de descubrimiento por LAN local. |
| **SmartLink** | Botón de modo | Cambia al modo de conexión remota SmartLink. |
| **Manual** | Botón de modo | Cambia al modo de conexión manual por IP. |
| **No local radios found yet** | Indicador | Se muestra cuando el descubrimiento no obtiene resultados. Reemplaza la lista de radios. |
| **Retry Discovery** | Botón | Vuelve a ejecutar el escaneo de descubrimiento LAN inmediatamente. |
| **Connect Selected Radio** | Botón | Conecta a la radio resaltada en la lista **Available radios**. |
| **Connect by IP** | Botón | Acceso directo al modo de conexión Manual. |
| **Remote with SmartLink** | Botón | Acceso directo al modo de conexión SmartLink. |
| **Open Network Diagnostics** | Botón | Abre la pantalla de diagnóstico de red para inspeccionar la conectividad. |
| **Radio IP address** | Cuadro combinado (editable) | Ingrese o seleccione la dirección IP para usar en una conexión manual. La lista desplegable muestra hasta tres direcciones usadas recientemente. Se guarda como `ManualRadioIp`; las entradas recientes se almacenan bajo `RecentConnectByIpAddresses`. |
| **Connect to last radio on start up** | Casilla de verificación | Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y al sondear descubrimiento por difusión/radio enrutada. Cuando está desmarcada, el diálogo de conexión se abre y el usuario debe elegir una radio manualmente en cada sesión. Se guarda como `AutoConnectToLastRadio`. Por defecto está marcada. |

## Consejos

- El aviso "No local radios found yet" también se muestra mientras el descubrimiento aún está en progreso inmediatamente después del inicio. Espere unos segundos antes de concluir que la radio es inalcanzable.
- Si la radio y la computadora están en diferentes subredes o está usando una VPN, los paquetes de descubrimiento mDNS no cruzarán el límite de la red. En su lugar, haga clic en **Connect by IP** e ingrese la dirección IP de la radio directamente.
- Las redes Wi-Fi para invitados comúnmente bloquean el tráfico entre dispositivos. Si está en Wi-Fi, verifique si su punto de acceso aplica aislamiento de clientes.
- El campo **Radio IP address** retiene hasta tres direcciones usadas recientemente. Abra la lista desplegable para reutilizar una dirección anterior sin volver a escribirla.
- Si comparte la computadora con otros operadores o prefiere elegir una radio explícitamente en cada sesión, desmarque **Connect to last radio on start up**. AetherSDR abrirá el diálogo de conexión en cada inicio en lugar de conectarse automáticamente.

## Solución de problemas

- **Retry Discovery no hace nada y la lista sigue vacía** — La radio puede estar en una subred diferente, detrás de una VPN o bloqueada por un firewall del equipo. Haga clic en **Connect by IP** e ingrese la dirección IP de la radio manualmente, o haga clic en **Open Network Diagnostics** para más detalle.
- **La radio aparece brevemente y luego desaparece** — Inestabilidad de red o un firewall que descarta tráfico mDNS intermitentemente. Verifique sus reglas de firewall y reintente. Si el problema persiste, use **Connect by IP** para una conexión estable.
- **Open Network Diagnostics no muestra información útil** — Vaya a `Settings > Network...` para abrir la pantalla completa de diagnóstico de red.
- **AetherSDR se conecta a la radio incorrecta al iniciar** — Desmarque **Connect to last radio on start up** para que el diálogo de conexión se abra al iniciar, luego seleccione la radio deseada manualmente.

## Relacionado

- [Connect to a local LAN radio](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Log in to SmartLink to see remote radios](log-in-to-smartlink-to-see-remote-radios.md)
- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
