# Resumen de Conexión a una Radio

El panel **Connect to a Radio** es el punto de partida para cada sesión de AetherSDR. Permite elegir cómo llegar a su FLEX-8600 — en su red local, a través de FlexRadio SmartLink, o ingresando una dirección IP directamente — y luego iniciar la conexión.

## Antes de comenzar

- Su FLEX-8600 debe estar encendido y ejecutando firmware 4.2.
- Para conexiones SmartLink, necesita una cuenta FlexRadio y acceso a internet en ambos extremos.
- Para conexiones manuales/VPN, necesita la dirección IP de la radio.

## Cómo funciona

El panel se abre como una ventana separada cuando no hay ninguna radio conectada. Cuenta con una barra de título personalizada con el texto "Connect to Radio". Puede arrastrar la ventana por su barra de título. El panel aparece en la ventana principal cuando no hay ninguna radio conectada. También puede abrirlo en cualquier momento a través de `Settings > Connect to Radio...`.

El panel utiliza un estilo de ventana sin bordes por defecto, controlado por la configuración `FramelessWindow` (valor predeterminado: True). Cuando el modo sin bordes está activo, la barra de título personalizada permite arrastrar la ventana. Cerrar esta ventana cerrará el panel de conexión.

Tres botones de modo en la parte superior determinan qué método de conexión está activo. Al seleccionar un modo, el panel cambia para mostrar los controles correspondientes. AetherSDR guarda su último modo usado en `ConnectionMode`.

### En Esta Red (Modo Local)

Use este modo cuando la radio y su computadora estén en la misma LAN. AetherSDR ejecuta la detección mDNS/Flex automáticamente y lista cualquier radio que encuentre bajo **Available radios**. Seleccione una radio de la lista y haga clic en **Connect Selected Radio** para conectarse.

Si la detección no encuentra nada, el panel cambia a una vista de estado vacío que muestra **No local radios found yet**. Desde allí puede:

- Hacer clic en **Retry Discovery** para ejecutar la detección nuevamente.
- Hacer clic en **Connect by IP** para cambiar a la página Manual.
- Hacer clic en **Remote with SmartLink** para cambiar a la página SmartLink.
- Hacer clic en **Open Network Diagnostics** para investigar problemas de red.

Las razones comunes por las que la detección no devuelve nada incluyen el aislamiento de AP en Wi-Fi de invitados, software VPN ejecutándose en el host y reglas de firewall que bloquean los paquetes de detección.

### Remoto con SmartLink

Use este modo cuando la radio esté en una ubicación diferente. Ingrese el correo electrónico de su cuenta FlexRadio en **SmartLink account: Email** (guardado como `SmartLinkEmail`) y su contraseña en **SmartLink account: Password** (no guardada), luego haga clic en **Sign In**. Después de la autenticación, AetherSDR llena la lista **Remote radios** con las radios WAN disponibles para su cuenta. La lista tiene una altura fija; si tiene muchas radios remotas, desplácese dentro de la lista para encontrar la que desea. Seleccione una radio y haga clic en **Connect Remote Radio**. Para finalizar la sesión, haga clic en **Sign Out**.

### Conectar por IP (Modo Manual)

Use este modo para conexiones VPN o de red enrutada donde ya conoce la dirección IP de la radio. Ingrese la dirección en **Radio IP address** (guardada como `ManualRadioIp`), luego haga clic en **Connect by IP**.

El campo **Radio IP address** es un menú desplegable editable. AetherSDR almacena hasta tres direcciones usadas recientemente (guardadas como `RecentConnectByIpAddresses`) y las muestra en el menú desplegable cuando se abre el panel. Haga clic en la flecha del menú desplegable para seleccionar una dirección anterior, o escriba una nueva directamente. Las direcciones se normalizan antes de guardarse; no se almacenan duplicados. Si existe un valor `LastRoutedRadioIp` heredado de una versión anterior, se importa automáticamente la primera vez que se abre el panel.

Tres controles adicionales están disponibles en esta página:

- **Advanced: Source path** — selecciona qué interfaz de red local (NIC) se utiliza para la conexión. La interfaz elegida se guarda como `ManualBindSource`. Aparece una **Source warning label** si la interfaz guardada no está disponible o está desactualizada.
- **Use low bandwidth mode** — reduce las tasas de datos de transmisión para enlaces lentos o congestionados. Se guarda como `LowBandwidthMode`.
- **Network Diagnostics** — abre la herramienta de diagnóstico de red si la conexión falla.

Al sondear una dirección IP manual, AetherSDR recopila información de estado detallada de la radio. Captura el modelo de radio, apodo, indicativo, soporte multiFlex y datos de conexión del cliente durante una ventana de observación de 400 milisegundos después del saludo inicial. Esta información se utiliza para llenar los campos de identidad de la radio y verificar la conexión.

### Comportamiento de inicio

La casilla de verificación **Connect to last radio on start up** controla si AetherSDR se conecta automáticamente al iniciar. Cuando está marcada (valor predeterminado), AetherSDR intenta reconectarse a la última radio usada al inicio y cada vez que sondea direcciones de radiodifusión-detección o de radio enrutada. Cuando no está marcada, el panel de conexión se abre al inicio y debe seleccionar una radio manualmente cada sesión. Esta preferencia se guarda como `AutoConnectToLastRadio`.

### Indicadores de estado

Independientemente del modo, una **Status label** muestra el estado actual de la conexión (buscando, conectando, conectado, o un mensaje de error). Después de sondear una IP manual, una **Manual result label** muestra si la sonda tuvo éxito o falló.

### Desconexión

Una vez conectado, haga clic en **Disconnect** para regresar al panel de conexión. También puede acceder al panel nuevamente a través de `Settings > Connect to Radio...`.

## Función de cada control

| Control | Modo | Comportamiento |
|---|---|---|
| **Local** | — | Cambia al modo de detección de LAN local. |
| **SmartLink** | — | Cambia al modo remoto SmartLink. |
| **Manual** | — | Cambia al modo de ingreso manual de IP. |
| **Available radios** | Local | Lista las radios encontradas por detección de LAN. |
| **Connect Selected Radio** | Local | Se conecta a la radio resaltada. |
| **No local radios found yet** | Local | Indicador mostrado cuando la detección está vacía. |
| **Retry Discovery** | Local | Vuelve a ejecutar la detección de LAN. |
| **Remote with SmartLink** (acceso directo) | Local | Cambia a la página SmartLink. |
| **Connect by IP** (acceso directo) | Local | Cambia a la página Manual. |
| **Open Network Diagnostics** | Local | Abre la herramienta de diagnóstico de red. |
| **SmartLink account: Email** | SmartLink | Dirección de correo electrónico de la cuenta FlexRadio. Guardada como `SmartLinkEmail`. |
| **SmartLink account: Password** | SmartLink | Contraseña de la cuenta (no guardada entre sesiones). |
| **Sign In** | SmartLink | Autentica con SmartLink. |
| **Sign Out** | SmartLink | Cierra la sesión de SmartLink. |
| **Remote radios** | SmartLink | Lista las radios WAN disponibles para la cuenta. Desplazable; altura de visualización fija. |
| **Connect Remote Radio** | SmartLink | Inicia una conexión WAN a la radio seleccionada. |
| **Radio IP address** | Manual | Menú desplegable editable que muestra hasta tres direcciones recientes (guardadas como `RecentConnectByIpAddresses`). Escriba una nueva dirección o seleccione una anterior. Guardada como `ManualRadioIp`. |
| **Advanced: Source path** | Manual | Selecciona la NIC local para la conexión. Guardada como `ManualBindSource`. |
| **Use low bandwidth mode** | Manual | Habilita transmisiones de tasa reducida para enlaces lentos. Guardada como `LowBandwidthMode`. |
| **Network Diagnostics** | Manual | Abre la herramienta de diagnóstico de red. |
| **Connect by IP** (manual) | Manual | Inicia la conexión manual/VPN. |
| **Connect to last radio on start up** | Todas | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio usada al inicio y al sondear radiodifusión-detección / radio enrutada. Cuando no está marcado, se abre el panel de conexión y el usuario debe elegir una radio manualmente cada sesión. Marcado por defecto. Guardado como `AutoConnectToLastRadio`. |
| **Disconnect** | Todas | Desconecta la radio actual. |

## Relacionados

- [Conectar a una radio LAN local](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Reintentar detección cuando no aparecen radios](retry-discovery-when-no-radios-appear.md)
- [Iniciar sesión en SmartLink para ver radios remotas](log-in-to-smartlink-to-see-remote-radios.md)
- [Conectar a una radio remota a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Conectar por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Elegir la interfaz de red local utilizada para una conexión manual](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Habilitar el modo de ancho de banda bajo para enlaces lentos](enable-low-bandwidth-mode-for-slow-links.md)
- [Desconectar la radio actual](../../getting-started/setup/disconnect-from-the-current-radio.md)
