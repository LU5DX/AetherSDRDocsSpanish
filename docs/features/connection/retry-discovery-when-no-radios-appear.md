# Reintentar la detección cuando no aparecen equipos

Cuando la detección local de AetherSDR no encuentra ningún equipo, el aviso "No local radios found yet" aparece en lugar de la lista de equipos. Esta página explica cómo iniciar un nuevo escaneo de detección y qué hacer si la lista continúa vacía.

## Antes de comenzar

- AetherSDR está abierto y muestra el panel "Connect to a Radio". Si no está visible, vaya a `Settings > Connect to Radio...`.
- Su FLEX-8600 está encendido y conectado a la misma LAN que su computadora.

## Pasos

1. En el panel "Connect to a Radio", confirme que **Local** sea el modo seleccionado. Si no lo es, haga clic en **Local**.
2. Si el aviso "No local radios found yet" está visible, haga clic en **Retry Discovery**.
3. Espere unos segundos para que AetherSDR escuche los paquetes de detección. Si su equipo es encontrado, aparecerá en la lista **Available radios**.
4. Seleccione su equipo en la lista **Available radios** y luego haga clic en **Connect Selected Radio**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Local** | Botón de modo | Cambia al modo de detección en LAN local. | `ConnectionMode` |
| **SmartLink** | Botón de modo | Cambia al modo de conexión remota mediante SmartLink. | `ConnectionMode` |
| **Manual** | Botón de modo | Cambia al modo de conexión por IP manual. | `ConnectionMode` |
| **No local radios found yet** | Indicador | Se muestra cuando la detección no arroja resultados. Reemplaza la lista de equipos. | — |
| **Retry Discovery** | Botón | Vuelve a ejecutar el escaneo de detección en la LAN de forma inmediata. | — |
| **Connect Selected Radio** | Botón | Conecta al equipo resaltado en la lista **Available radios**. | — |
| **Connect by IP** | Botón | Acceso directo al modo de conexión Manual. | `ConnectionMode` |
| **Remote with SmartLink** | Botón | Acceso directo al modo de conexión SmartLink. | `ConnectionMode` |
| **Open Network Diagnostics** | Botón | Abre la pantalla de diagnóstico de red para inspeccionar la conectividad. | — |

## Sugerencias

- El aviso "No local radios found yet" también se muestra mientras la detección aún está en curso inmediatamente después del inicio. Espere unos segundos antes de concluir que el equipo no es accesible.
- Si el equipo y la computadora están en subredes diferentes o si utiliza una VPN, los paquetes de detección mDNS no cruzarán el límite de red. Haga clic en **Connect by IP** e ingrese directamente la dirección IP del equipo.
- Las redes Wi-Fi de invitados suelen bloquear el tráfico entre dispositivos. Si está conectado por Wi-Fi, verifique si su punto de acceso aplica aislamiento de clientes.

## Solución de problemas

- **Retry Discovery no hace nada y la lista permanece vacía** — El equipo puede estar en una subred diferente, detrás de una VPN o bloqueado por un firewall del host. Haga clic en **Connect by IP** e ingrese la dirección IP del equipo manualmente, o haga clic en **Open Network Diagnostics** para obtener más detalles.
- **El equipo aparece brevemente y luego desaparece** — Inestabilidad de red o un firewall que interrumpe el tráfico mDNS de forma intermitente. Revise las reglas de su firewall y vuelva a intentarlo. Si el problema persiste, use **Connect by IP** para una conexión estable.
- **Open Network Diagnostics no muestra información útil** — Vaya a `Settings > Network...` para abrir la pantalla completa de diagnóstico de red.

## Relacionados

- [Conectarse a un equipo en LAN local](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Conectarse por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Iniciar sesión en SmartLink para ver equipos remotos](log-in-to-smartlink-to-see-remote-radios.md)
- [Conectarse a un equipo remoto a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
