# Descripción general de Connect to a Radio

El panel Connect to a Radio es el punto de partida de cada sesión de AetherSDR. Permite elegir cómo conectarse al FLEX-8600 — en la red local, a través de FlexRadio SmartLink, o ingresando una dirección IP directamente — y luego iniciar la conexión.

## Antes de comenzar

- El FLEX-8600 debe estar encendido y ejecutando el firmware 4.1.5.
- Para conexiones SmartLink, se necesita una cuenta de FlexRadio y acceso a internet en ambos extremos.
- Para conexiones manuales o por VPN, se necesita la dirección IP del equipo.

## Cómo funciona

El panel aparece en la ventana principal cuando no hay ningún equipo conectado. También puede abrirse en cualquier momento mediante `Settings > Connect to Radio...`.

Tres botones de modo en la parte superior determinan qué método de conexión está activo. Al seleccionar un modo, el panel inferior cambia para mostrar los controles correspondientes. AetherSDR guarda el último modo utilizado en `ConnectionMode`.

### On This Network (modo local)

Use este modo cuando el equipo y la computadora están en la misma LAN. AetherSDR ejecuta el descubrimiento mDNS/Flex automáticamente y lista los equipos encontrados bajo **Available radios**. Seleccione un equipo de la lista y haga clic en **Connect Selected Radio** para conectarse.

Si el descubrimiento no encuentra nada, el panel cambia a una vista de estado vacío que muestra **No local radios found yet**. Desde allí puede:

- Hacer clic en **Retry Discovery** para ejecutar el descubrimiento nuevamente.
- Hacer clic en **Connect by IP** para cambiar a la página Manual.
- Hacer clic en **Remote with SmartLink** para cambiar a la página de SmartLink.
- Hacer clic en **Open Network Diagnostics** para investigar problemas de red.

Las razones más comunes por las que el descubrimiento no encuentra nada incluyen el aislamiento de AP en redes Wi-Fi de invitados, software VPN en ejecución en el equipo anfitrión y reglas de firewall que bloquean los paquetes de descubrimiento.

### Remote with SmartLink

Use este modo cuando el equipo se encuentra en una ubicación diferente. Ingrese el correo electrónico de su cuenta de FlexRadio en **SmartLink account: Email** (guardado como `SmartLinkEmail`) y su contraseña en **SmartLink account: Password** (no se guarda), luego haga clic en **Sign In**. Tras la autenticación, AetherSDR llena la lista **Remote radios** con los equipos WAN disponibles para su cuenta. La lista tiene una altura fija; si tiene muchos equipos remotos, desplácese dentro de la lista para encontrar el deseado. Seleccione un equipo y haga clic en **Connect Remote Radio**. Para finalizar la sesión, haga clic en **Sign Out**.

### Connect by IP (modo manual)

Use este modo para conexiones VPN o redes enrutadas cuando ya conoce la dirección IP del equipo. Ingrese la dirección en **Radio IP address** (guardada como `ManualRadioIp`), luego haga clic en **Connect by IP**.

Hay dos controles adicionales disponibles en esta página:

- **Advanced: Source path** — selecciona qué interfaz de red local (NIC) se usa para la conexión. La interfaz elegida se guarda como `ManualBindSource`. Aparece un **Source warning label** si la interfaz guardada no está disponible o está desactualizada.
- **Use low bandwidth mode** — reduce las tasas de datos del flujo para enlaces lentos o congestionados. Se guarda como `LowBandwidthMode`.

Haga clic en **Network Diagnostics** en esta página para abrir la herramienta de diagnóstico de red si la conexión falla.

### Indicadores de estado

Independientemente del modo, un **Status label** muestra el estado de conexión actual (buscando, conectando, conectado o un mensaje de error). Tras sondear una IP manual, un **Manual result label** indica si el sondeo fue exitoso o falló.

### Desconexión

Una vez conectado, haga clic en **Disconnect** para volver al panel de conexión. También puede acceder al panel nuevamente mediante `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Modo | Comportamiento | Clave guardada | Valor predeterminado |
|---|---|---|---|---|
| **On This Network** | — | Cambia al modo de descubrimiento en LAN local. | `ConnectionMode` | Local |
| **Remote with SmartLink** | — | Cambia al modo remoto SmartLink. | `ConnectionMode` | — |
| **Connect by IP** | — | Cambia al modo de ingreso manual de IP. | `ConnectionMode` | — |
| **Available radios** | Local | Lista los equipos encontrados por el descubrimiento en LAN. | — | — |
| **Connect Selected Radio** | Local | Se conecta al equipo resaltado. | — | — |
| **No local radios found yet** | Local | Indicador mostrado cuando el descubrimiento no encuentra nada. | — | — |
| **Retry Discovery** | Local | Vuelve a ejecutar el descubrimiento en LAN. | — | — |
| **Remote with SmartLink** (acceso directo) | Local | Cambia a la página de SmartLink. | — | — |
| **Connect by IP** (acceso directo) | Local | Cambia a la página Manual. | — | — |
| **Open Network Diagnostics** | Local | Abre la herramienta de diagnóstico de red. | — | — |
| **SmartLink account: Email** | SmartLink | Correo electrónico de la cuenta de FlexRadio. | `SmartLinkEmail` | — |
| **SmartLink account: Password** | SmartLink | Contraseña de la cuenta (no se guarda entre sesiones). | — | — |
| **Sign In** | SmartLink | Se autentica con SmartLink. | — | — |
| **Sign Out** | SmartLink | Cierra sesión en SmartLink. | — | — |
| **Remote radios** | SmartLink | Lista los equipos WAN disponibles para la cuenta. Desplazable; altura de visualización fija. | — | — |
| **Connect Remote Radio** | SmartLink | Inicia una conexión WAN al equipo seleccionado. | — | — |
| **Radio IP address** | Manual | Dirección IP del equipo al que conectarse. | `ManualRadioIp` | — |
| **Advanced: Source path** | Manual | Selecciona la NIC local para la conexión. | `ManualBindSource` | — |
| **Use low bandwidth mode** | Manual | Habilita flujos de datos reducidos para enlaces lentos. | `LowBandwidthMode` | — |
| **Network Diagnostics** | Manual | Abre la herramienta de diagnóstico de red. | — | — |
| **Connect by IP** (manual) | Manual | Inicia la conexión manual o por VPN. | — | — |
| **Disconnect** | Todos | Desconecta del equipo actual. | — | — |

## Temas relacionados

- [Conectarse a un equipo en LAN local](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Reintentar el descubrimiento cuando no aparecen equipos](retry-discovery-when-no-radios-appear.md)
- [Iniciar sesión en SmartLink para ver equipos remotos](log-in-to-smartlink-to-see-remote-radios.md)
- [Conectarse a un equipo remoto a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Seleccionar la interfaz de red local para una conexión manual](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Habilitar el modo de bajo ancho de banda para enlaces lentos](enable-low-bandwidth-mode-for-slow-links.md)
- [Desconectarse del equipo actual](../../getting-started/setup/disconnect-from-the-current-radio.md)
