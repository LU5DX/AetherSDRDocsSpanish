# Reintentar el descubrimiento cuando no aparecen radios

Cuando el descubrimiento local de AetherSDR no encuentra ninguna radio, el aviso "No local radios found yet" aparece en lugar de la lista de radios. Esta página explica cómo iniciar un nuevo escaneo de descubrimiento y qué intentar si la lista permanece vacía.

## Antes de comenzar

- AetherSDR está abierto y muestra el panel "Connect to a Radio". Si no está visible, vaya a `Settings > Connect to Radio...`.
- Su FLEX-8600 está encendido y conectado a la misma LAN que su computadora.

## Pasos

1. En el panel "Connect to a Radio", confirme que **Local** es el modo seleccionado. Si no lo es, haga clic en **Local**.
2. Si el aviso "No local radios found yet" está visible, haga clic en **Retry Discovery**.
3. Espere unos segundos para que AetherSDR escuche los paquetes de descubrimiento. Si su radio es encontrada, aparece en la lista **Available radios**.
4. Seleccione su radio en la lista **Available radios** y luego haga clic en **Connect Selected Radio**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Local** | Botón de modo | Cambia al modo de descubrimiento en LAN local. | `ConnectionMode` |
| **SmartLink** | Botón de modo | Cambia al modo de conexión remota SmartLink. | `ConnectionMode` |
| **Manual** | Botón de modo | Cambia al modo de conexión por IP manual. | `ConnectionMode` |
| **No local radios found yet** | Indicador | Se muestra cuando el descubrimiento no devuelve resultados. Reemplaza la lista de radios. | — |
| **Retry Discovery** | Botón | Vuelve a ejecutar el escaneo de descubrimiento en LAN de inmediato. | — |
| **Connect Selected Radio** | Botón | Conecta a la radio resaltada en la lista **Available radios**. | — |
| **Connect by IP** | Botón | Acceso directo al modo de conexión Manual. | `ConnectionMode` |
| **Remote with SmartLink** | Botón | Acceso directo al modo de conexión SmartLink. | `ConnectionMode` |
| **Open Network Diagnostics** | Botón | Abre la pantalla de diagnóstico de red para inspeccionar la conectividad. | — |

## Consejos

- El aviso "No local radios found yet" también se muestra mientras el descubrimiento aún está en curso justo después del inicio. Espere unos segundos antes de concluir que la radio es inalcanzable.
- Si la radio y la computadora están en subredes diferentes o está usando una VPN, los paquetes de descubrimiento mDNS no cruzarán el límite de la red. Haga clic en **Connect by IP** e ingrese la dirección IP de la radio directamente.
- Las redes Wi-Fi para invitados suelen bloquear el tráfico entre dispositivos. Si está en Wi-Fi, verifique si su punto de acceso aplica aislamiento de clientes.

## Solución de problemas

- **Retry Discovery no hace nada y la lista permanece vacía** — La radio puede estar en una subred diferente, detrás de una VPN o bloqueada por un firewall del host. Haga clic en **Connect by IP** e ingrese la dirección IP de la radio manualmente, o haga clic en **Open Network Diagnostics** para obtener más detalles.
- **La radio aparece brevemente y luego desaparece** — Inestabilidad de red o un firewall que descarta el tráfico mDNS de forma intermitente. Revise las reglas de su firewall y reintente. Si el problema persiste, use **Connect by IP** para una conexión estable.
- **Open Network Diagnostics no muestra información útil** — Vaya a `Settings > Network...` para abrir la pantalla completa de diagnóstico de red.

## Relacionados

- [Conectarse a una radio en LAN local](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Conectarse por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Iniciar sesión en SmartLink para ver radios remotas](log-in-to-smartlink-to-see-remote-radios.md)
- [Conectarse a una radio remota a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
