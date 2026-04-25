# Reintentar el descubrimiento cuando no aparecen radios

Cuando el descubrimiento local de AetherSDR no encuentra radios, el aviso "No local radios found yet" aparece en lugar de la lista de radios. Esta página explica cómo activar un nuevo escaneo de descubrimiento y qué intentar si la lista permanece vacía.

## Antes de comenzar

- AetherSDR está abierto y muestra el panel "Connect to a Radio". Si no está visible, vaya a `Settings > Connect to Radio...`.
- Su FLEX-8600 está encendido y conectado a la misma LAN que su computadora.

## Pasos

1. En el panel "Connect to a Radio", confirme que **On This Network** sea el modo seleccionado. Si no lo es, haga clic en **On This Network**.
2. Si el aviso "No local radios found yet" está visible, haga clic en **Retry Discovery**.
3. Espere unos segundos para que AetherSDR escuche los paquetes de descubrimiento. Si su radio es encontrada, aparece en la lista **Available radios**.
4. Seleccione su radio en la lista **Available radios** y luego haga clic en **Connect Selected Radio**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **On This Network** | Botón de modo | Cambia al modo de descubrimiento en la LAN local. | `ConnectionMode` |
| **No local radios found yet** | Indicador | Se muestra cuando el descubrimiento no devuelve resultados. Reemplaza la lista de radios. | — |
| **Retry Discovery** | Botón | Vuelve a ejecutar el escaneo de descubrimiento en la LAN de inmediato. | — |
| **Connect Selected Radio** | Botón | Conecta a la radio resaltada en la lista **Available radios**. | — |
| **Connect by IP** | Botón | Acceso directo al modo de conexión manual por dirección IP. | `ConnectionMode` |
| **Remote with SmartLink** | Botón | Acceso directo al modo de conexión mediante SmartLink. | `ConnectionMode` |
| **Open Network Diagnostics** | Botón | Abre la pantalla de diagnóstico de red para inspeccionar la conectividad. | — |

## Consejos

- El aviso "No local radios found yet" también se muestra mientras el descubrimiento aún está en curso inmediatamente después del inicio. Espere unos segundos antes de concluir que la radio no es alcanzable.
- Si la radio y la computadora están en subredes diferentes o está usando una VPN, los paquetes de descubrimiento mDNS no cruzarán el límite de la red. Haga clic en **Connect by IP** en su lugar e ingrese la dirección IP de la radio directamente.
- Las redes Wi-Fi de invitados comúnmente bloquean el tráfico entre dispositivos. Si está en Wi-Fi, verifique si su punto de acceso aplica aislamiento de clientes.

## Solución de problemas

- **Retry Discovery no hace nada y la lista permanece vacía** — Es posible que la radio esté en una subred diferente, detrás de una VPN o bloqueada por un firewall del host. Haga clic en **Connect by IP** e ingrese la dirección IP de la radio manualmente, o haga clic en **Open Network Diagnostics** para obtener más detalles.
- **La radio aparece brevemente y luego desaparece** — Inestabilidad de red o un firewall que interrumpe el tráfico mDNS de forma intermitente. Revise las reglas de su firewall y reintente. Si el problema persiste, use **Connect by IP** para una conexión estable.
- **Open Network Diagnostics no muestra información útil** — Vaya a `Settings > Network...` para abrir la pantalla completa de diagnóstico de red.

## Relacionados

- [Conectar a una radio en la LAN local](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Conectar por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Iniciar sesión en SmartLink para ver radios remotas](log-in-to-smartlink-to-see-remote-radios.md)
- [Conectar a una radio remota mediante SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
