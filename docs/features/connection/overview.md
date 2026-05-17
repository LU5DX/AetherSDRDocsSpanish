# Resumen de Conectar a una Radio

El panel Conectar a una Radio es el punto de partida para cada sesión de AetherSDR. Le permite elegir cómo acceder a su FLEX-8600 — en su red local, a través de FlexRadio SmartLink, o ingresando una dirección IP directamente — y luego iniciar la conexión.

## Antes de comenzar

- Su FLEX-8600 debe estar encendido y ejecutando el firmware 4.2.
- Para conexiones SmartLink, necesita una cuenta de FlexRadio y acceso a internet en ambos extremos.
- Para conexiones manuales/VPN, necesita la dirección IP de la radio.

## Cómo funciona

El panel se abre como una ventana separada cuando no hay ninguna radio conectada. Cuenta con una barra de título personalizada con el texto "Connect to Radio". Puede arrastrar la ventana por su barra de título. El panel aparece en la ventana principal cuando no hay ninguna radio conectada. También puede abrirlo en cualquier momento mediante `Settings > Connect to Radio...`.

El panel usa un estilo de ventana sin bordes de forma predeterminada, controlado por el ajuste `FramelessWindow` (valor predeterminado: True). Cuando el modo sin bordes está activo, la barra de título personalizada permite arrastrar la ventana. El panel restaura su geometría anterior cuando vuelve a ser visible después de ocultarse. Cerrar esta ventana cerrará el panel de conexión.

Tres botones de modo en la parte superior determinan qué método de conexión está activo. Seleccionar un modo cambia el panel inferior para mostrar los controles correspondientes. AetherSDR conserva el último modo utilizado en `ConnectionMode`.

### En Esta Red (modo Local)

Use este modo cuando la radio y su computadora estén en la misma LAN. AetherSDR ejecuta la detección mDNS/Flex automáticamente y enumera las radios que encuentre bajo **Available radios**. Seleccione una radio de la lista y haga clic en **Connect Selected Radio** para conectarse.

Si la detección no encuentra nada, el panel cambia a una vista de estado vacío que muestra **No local radios found yet**. Desde allí puede:

- Haga clic en **Retry Discovery** para ejecutar la detección nuevamente.
- Haga clic en **Connect by IP** para cambiar a la página Manual.
- Haga clic en **Remote with SmartLink** para cambiar a la página SmartLink.
- Haga clic en **Open Network Diagnostics** para investigar problemas de red.

Las razones comunes por las que la detección no devuelve nada incluyen el aislamiento de AP en redes Wi-Fi de invitados, software VPN ejecutándose en el equipo anfitrión y reglas de firewall que bloquean los paquetes de detección.

### Remoto con SmartLink

Use este modo cuando la radio esté en una ubicación diferente. Ingrese su correo electrónico de la cuenta FlexRadio en **SmartLink account: Email** (conservado como `SmartLinkEmail`) y su contraseña en **SmartLink account: Password** (no se conserva), luego haga clic en **Sign In**. Después de la autenticación, AetherSDR llena la lista **Remote radios** con las radios WAN disponibles para su cuenta. La lista tiene una altura fija; si tiene muchas radios remotas, desplácese dentro de la lista para encontrar la que desea. Seleccione una radio y haga clic en **Connect Remote Radio**. Para finalizar la sesión, haga clic en **Sign Out**.

### Conectar por IP (modo Manual)

Use este modo para conexiones VPN o de red enrutada donde ya conoce la dirección IP de la radio. Ingrese la dirección en **Radio IP address** (conservada como `ManualRadioIp`), luego haga clic en **Connect by IP**.

El campo **Radio IP address** es un desplegable editable. AetherSDR almacena hasta tres direcciones utilizadas recientemente (conservadas como `RecentConnectByIpAddresses`) y las muestra en el desplegable cuando se abre el panel. Haga clic en la flecha del desplegable para seleccionar una dirección anterior, o escriba una nueva directamente. Las direcciones se normalizan antes de guardarse; no se almacenan duplicados. Si existe un valor `LastRoutedRadioIp` heredado de una versión anterior, se importa automáticamente la primera vez que se abre el panel.

Tres controles adicionales están disponibles en esta página:

- **Advanced: Source path** — selecciona qué interfaz de red local (NIC) se usa para la conexión. La interfaz elegida se conserva como `ManualBindSource`. Aparece una **Source warning label** si la interfaz guardada no está disponible o está desactualizada.
- **Use low bandwidth mode** — reduce las tasas de datos del flujo para enlaces lentos o congestionados. Se conserva como `LowBandwidthMode`.
- **Network Diagnostics** — abre la herramienta de diagnóstico de red si la conexión falla.

Al sondear una dirección IP manual, AetherSDR recopila información de estado detallada de la radio. Captura el modelo de la radio, el apodo, el indicativo, la compatibilidad con multiFlex y los datos de conexión del cliente durante una ventana de 400 milisegundos después del protocolo de enlace inicial. Esta información se usa para llenar los campos de identidad de la radio y verificar la conexión.

### Comportamiento al inicio

La casilla de verificación **Connect to last radio on start up** controla si AetherSDR se conecta automáticamente al iniciarse. Cuando está marcada (valor predeterminado), AetherSDR intenta reconectarse a la última radio utilizada al inicio y cada vez que sondea direcciones de descubrimiento por difusión o de radio enrutada. Cuando no está marcada, el panel de conexión se abre al inicio y debe seleccionar una radio manualmente cada sesión. Esta preferencia se conserva como `AutoConnectToLastRadio`.

### Indicadores de estado

Independientemente del modo, una **Status label** muestra el estado actual de la conexión (buscando, conectando, conectado, o un mensaje de error). Después de sondear una IP manual, una **Manual result label** muestra si la sonda tuvo éxito o falló.

### Desconexión

Una vez conectado, haga clic en **Disconnect** para volver al panel de conexión. También puede acceder al panel nuevamente a través de `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Modo | Comportamiento |
|---|---|---|
| **Local** | — | Cambia al modo de detección LAN local. |
| **SmartLink** | — | Cambia al modo remoto SmartLink. |
| **Manual** | — | Cambia al modo de ingreso manual de IP. |
| **Available radios** | Local | Enumera las radios encontradas por detección LAN. |
| **Connect Selected Radio** | Local | Se conecta a la radio resaltada. |
| **No local radios found yet** | Local | Indicador mostrado cuando la detección está vacía. |
| **Retry Discovery** | Local | Vuelve a ejecutar la detección LAN. |
| **Remote with SmartLink** (acceso directo) | Local | Cambia a la página SmartLink. |
| **Connect by IP** (acceso directo) | Local | Cambia a la página Manual. |
| **Open Network Diagnostics** | Local | Abre la herramienta de diagnóstico de red. |
| **SmartLink account: Email** | SmartLink | Dirección de correo electrónico de la cuenta FlexRadio. Se conserva como `SmartLinkEmail`. |
| **SmartLink account: Password** | SmartLink | Contraseña de la cuenta (no se guarda entre sesiones). |
| **Sign In** | SmartLink | Autentica con SmartLink. |
| **Sign Out** | SmartLink | Cierra la sesión de SmartLink. |
| **Remote radios** | SmartLink | Enumera las radios WAN disponibles para la cuenta. Desplazable; altura de visualización fija. |
| **Connect Remote Radio** | SmartLink | Inicia una conexión WAN a la radio seleccionada. |
| **Radio IP address** | Manual | Desplegable editable que muestra hasta tres direcciones recientes (conservadas como `RecentConnectByIpAddresses`). Escriba una dirección nueva o seleccione una anterior. Se conserva como `ManualRadioIp`. |
| **Advanced: Source path** | Manual | Selecciona la NIC local para la conexión. Se conserva como `ManualBindSource`. |
| **Use low bandwidth mode** | Manual | Activa flujos de tasa reducida para enlaces lentos. Se conserva como `LowBandwidthMode`. |
| **Network Diagnostics** | Manual | Abre la herramienta de diagnóstico de red. |
| **Connect by IP** (manual) | Manual | Inicia la conexión manual/VPN. |
| **Connect to last radio on start up** | Todos | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al inicio y en la sonda de descubrimiento por difusión / radio enrutada. Cuando no está marcado, el panel de conexión se abre y el usuario debe elegir una radio manualmente cada sesión. Valor predeterminado: marcado. Se conserva como `AutoConnectToLastRadio`. |
| **Disconnect** | Todos | Desconecta la radio actual. |

## Relacionados

- [Connect to a local LAN radio](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Retry discovery when no radios appear](retry-discovery-when-no-radios-appear.md)
- [Log in to SmartLink to see remote radios](log-in-to-smartlink-to-see-remote-radios.md)
- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Pick the local network interface used for a manual connection](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Enable low-bandwidth mode for slow links](enable-low-bandwidth-mode-for-slow-links.md)
- [Disconnect from the current radio](../../getting-started/setup/disconnect-from-the-current-radio.md)
