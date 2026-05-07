# Resumen de Conectar a una Radio

El panel Conectar a una Radio es el punto de partida para cada sesión de AetherSDR. Permite elegir cómo acceder a su FLEX-8600 — en su red local, a través de FlexRadio SmartLink, o ingresando una dirección IP directamente — y luego iniciar la conexión.

## Antes de empezar

- Su FLEX-8600 debe estar encendido y ejecutando firmware 4.1.5.
- Para conexiones SmartLink, necesita una cuenta de FlexRadio y acceso a internet en ambos extremos.
- Para conexiones manuales/VPN, necesita la dirección IP de la radio.

## Cómo funciona

El panel aparece en la ventana principal cuando no hay ninguna radio conectada. También puede abrirlo en cualquier momento a través de `Settings > Connect to Radio...`.

Tres botones de modo en la parte superior determinan qué método de conexión está activo. Al seleccionar un modo, el panel inferior cambia para mostrar los controles correspondientes. AetherSDR conserva el último modo utilizado en `ConnectionMode`.

### En esta red (Modo local)

Use este modo cuando la radio y su computadora estén en la misma LAN. AetherSDR ejecuta la detección mDNS/Flex automáticamente y lista las radios que encuentre bajo **Available radios**. Seleccione una radio de la lista y haga clic en **Connect Selected Radio** para conectarse.

Si la detección no encuentra nada, el panel cambia a una vista de estado vacío que muestra **No local radios found yet**. Desde allí puede:

- Haga clic en **Retry Discovery** para ejecutar la detección nuevamente.
- Haga clic en **Connect by IP** para cambiar a la página Manual.
- Haga clic en **Remote with SmartLink** para cambiar a la página SmartLink.
- Haga clic en **Open Network Diagnostics** para investigar problemas de red.

Las razones comunes por las que la detección no devuelve nada incluyen el aislamiento AP de Wi-Fi para invitados, software VPN ejecutándose en el anfitrión y reglas de firewall que bloquean los paquetes de descubrimiento.

### Remoto con SmartLink

Use este modo cuando la radio esté en una ubicación diferente. Ingrese su correo electrónico de cuenta FlexRadio en **SmartLink account: Email** (conservado como `SmartLinkEmail`) y su contraseña en **SmartLink account: Password** (no se conserva), luego haga clic en **Sign In**. Después de la autenticación, AetherSDR completa la lista **Remote radios** con las radios WAN disponibles para su cuenta. La lista tiene una altura fija; si tiene muchas radios remotas, desplácese dentro de la lista para encontrar la que desee. Seleccione una radio y haga clic en **Connect Remote Radio**. Para finalizar la sesión, haga clic en **Sign Out**.

### Conectar por IP (Modo manual)

Use este modo para conexiones VPN o de red enrutada donde ya conozca la dirección IP de la radio. Ingrese la dirección en **Radio IP address** (conservada como `ManualRadioIp`), luego haga clic en **Connect by IP**.

El campo **Radio IP address** es un menú desplegable editable. AetherSDR almacena hasta tres direcciones utilizadas recientemente (conservadas como `RecentConnectByIpAddresses`) y completa el menú desplegable con ellas cuando se abre el panel. Haga clic en la flecha del menú desplegable para seleccionar una dirección anterior, o escriba una nueva directamente. Las direcciones se normalizan antes de guardarse; no se almacenan direcciones duplicadas. Si existe un valor heredado `LastRoutedRadioIp` de una versión anterior, se importa automáticamente la primera vez que se abre el panel.

Tres controles adicionales están disponibles en esta página:

- **Advanced: Source path** — selecciona qué interfaz de red local (NIC) se utiliza para la conexión. La interfaz elegida se conserva como `ManualBindSource`. Aparece una **Source warning label** si la interfaz guardada no está disponible o está obsoleta.
- **Use low bandwidth mode** — reduce las tasas de datos del flujo para enlaces lentos o congestionados. Se conserva como `LowBandwidthMode`.
- **Network Diagnostics** — abre la herramienta de diagnóstico de red si la conexión falla.

### Comportamiento al inicio

La casilla de verificación **Connect to last radio on start up** controla si AetherSDR se conecta automáticamente al iniciarse. Cuando está marcada (por defecto), AetherSDR intenta reconectarse a la última radio utilizada al inicio y cada vez que sondea direcciones de difusión-descubrimiento o de radio enrutada. Cuando no está marcada, el panel de conexión se abre al inicio y usted debe seleccionar una radio manualmente cada sesión. Esta preferencia se conserva como `AutoConnectToLastRadio`.

### Indicadores de estado

Independientemente del modo, una **Status label** muestra el estado actual de la conexión (buscando, conectando, conectado o un mensaje de error). Después de sondear una IP manual, una **Manual result label** muestra si la sonda tuvo éxito o falló.

### Desconexión

Una vez conectado, haga clic en **Disconnect** para regresar al panel de conexión. También puede acceder al panel nuevamente a través de `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Modo | Comportamiento |
|---|---|---|
| **Local** | — | Cambia al modo de detección LAN local. |
| **SmartLink** | — | Cambia al modo remoto SmartLink. |
| **Manual** | — | Cambia al modo de ingreso manual de IP. |
| **Available radios** | Local | Lista las radios encontradas por detección LAN. |
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
| **Remote radios** | SmartLink | Lista las radios WAN disponibles para la cuenta. Desplazable; altura de visualización fija. |
| **Connect Remote Radio** | SmartLink | Inicia una conexión WAN a la radio seleccionada. |
| **Radio IP address** | Manual | Menú desplegable editable que muestra hasta tres direcciones recientes (conservadas como `RecentConnectByIpAddresses`). Escriba una nueva dirección o seleccione una anterior. Se conserva como `ManualRadioIp`. |
| **Advanced: Source path** | Manual | Selecciona la NIC local para la conexión. Se conserva como `ManualBindSource`. |
| **Use low bandwidth mode** | Manual | Habilita flujos de tasa reducida para enlaces lentos. Se conserva como `LowBandwidthMode`. |
| **Network Diagnostics** | Manual | Abre la herramienta de diagnóstico de red. |
| **Connect by IP** (manual) | Manual | Inicia la conexión manual/VPN. |
| **Connect to last radio on start up** | Todos | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al inicio y al sondear difusión-descubrimiento / radio enrutada. Cuando no está marcado, el panel de conexión se abre y el usuario debe elegir una radio manualmente cada sesión. Marcado por defecto. Se conserva como `AutoConnectToLastRadio`. |
| **Disconnect** | Todos | Desconecta la radio actual. |

## Relacionado

- [Connect to a local LAN radio](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Retry discovery when no radios appear](retry-discovery-when-no-radios-appear.md)
- [Log in to SmartLink to see remote radios](log-in-to-smartlink-to-see-remote-radios.md)
- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Pick the local network interface used for a manual connection](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Enable low-bandwidth mode for slow links](enable-low-bandwidth-mode-for-slow-links.md)
- [Disconnect from the current radio](../../getting-started/setup/disconnect-from-the-current-radio.md)
