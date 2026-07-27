# Descripción general de Conectar a una Radio

El panel Conectar a una Radio es el punto de partida para cada sesión de AetherSDR. Permite elegir cómo llegar a su FLEX-8600 — en su red local, a través de FlexRadio SmartLink, o ingresando una dirección IP directamente — y luego iniciar la conexión.

## Antes de comenzar

- Su FLEX-8600 debe estar encendido y ejecutando el firmware 4.2.
- Para conexiones SmartLink, necesita una cuenta de FlexRadio y acceso a internet en ambos extremos.
- Para conexiones manuales/VPN, necesita la dirección IP de la radio.

## Cómo funciona

El panel se abre como una ventana separada cuando no hay ninguna radio conectada. Cuenta con una barra de título personalizada con el texto "Connect to Radio". Puede arrastrar la ventana por su barra de título. El panel aparece en la ventana principal cuando no hay ninguna radio conectada. También puede abrirlo en cualquier momento a través de `Settings > Connect to Radio...`.

El panel utiliza un estilo de ventana sin marco de forma predeterminada, controlado por el ajuste `FramelessWindow` (valor predeterminado: True). Cuando el modo sin marco está activo, la barra de título personalizada permite arrastrar la ventana. El panel restaura su geometría anterior cuando se vuelve visible después de haber estado oculto. Cerrar esta ventana cerrará el panel de conexión.

Tres botones de modo en la parte superior determinan qué método de conexión está activo. Al seleccionar un modo, el panel inferior cambia para mostrar los controles relevantes. AetherSDR conserva el último modo utilizado en `ConnectionMode`.

### En Esta Red (Modo Local)

Use este modo cuando la radio y su computadora estén en la misma LAN. AetherSDR ejecuta la detección mDNS/Flex automáticamente y lista cualquier radio que encuentre bajo **Available radios**. Seleccione una radio de la lista y haga clic en **Connect Selected Radio** para conectarse.

Si la detección no encuentra nada, el panel cambia a una vista de estado vacío que muestra **No local radios found yet**. Desde allí puede:

- Hacer clic en **Retry Discovery** para ejecutar la detección nuevamente.
- Hacer clic en **Connect by IP** para cambiar a la página Manual.
- Hacer clic en **Remote with SmartLink** para cambiar a la página SmartLink.
- Hacer clic en **Open Network Diagnostics** para investigar problemas de red.

Las razones comunes por las que la detección no devuelve nada incluyen el aislamiento de AP en Wi-Fi de invitados, software VPN ejecutándose en el host y reglas de firewall que bloquean los paquetes de detección.

La lista **Available radios** tiene una altura limitada (mínimo 120 px, máximo 240 px), por lo que se desplaza internamente cuando se descubren más radios de las que caben en el área visible. Esto evita que la lista crezca más allá del diálogo en pantallas pequeñas. La lista incluye una barra de desplazamiento vertical con estilo personalizado y controles redondeados.

Puede hacer clic derecho en cualquier radio de la lista **Available radios** para abrir un menú contextual. Elija **Set custom nickname** para asignar un apodo del lado del cliente que persiste entre barridos de detección. Esto está pensado para radios que no son Flex (como HL2 o radios simuladas) que no almacenan un nombre en la propia radio. Para radios Flex, el apodo se gestiona a través de Radio Setup mientras está conectado, por lo que el menú contextual no se ofrece para las radios Flex para evitar fuentes de información contradictorias.

### Remoto con SmartLink

Use este modo cuando la radio esté en una ubicación diferente. Ingrese su correo electrónico de cuenta FlexRadio en **SmartLink account: Email** (guardado como `SmartLinkEmail`) y su contraseña en **SmartLink account: Password** (no guardada), luego haga clic en **Sign In**. Después de la autenticación, AetherSDR llena la lista **Remote radios** con las radios WAN disponibles para su cuenta. La lista tiene una altura fija; si tiene muchas radios remotas, desplácese dentro de la lista para encontrar la deseada. Seleccione una radio y haga clic en **Connect Remote Radio**. Para finalizar la sesión, haga clic en **Sign Out**.

Los campos de correo electrónico y contraseña incluyen metadatos de accesibilidad para ayudar a los gestores de contraseñas (macOS Passwords, Windows Authenticator, KDE Wallet) a asociar el par de credenciales con el formulario de inicio de sesión de SmartLink.

### Conectar por IP (Modo Manual)

Use este modo para conexiones VPN o de red enrutada donde ya conoce la dirección IP de la radio. Ingrese la dirección en **Radio IP address** (guardada como `ManualRadioIp`), luego haga clic en **Connect by IP**.

El campo **Radio IP address** es un menú desplegable editable. AetherSDR almacena hasta tres direcciones usadas recientemente (guardadas como `RecentConnectByIpAddresses`) y completa el menú desplegable con ellas cuando se abre el panel. Haga clic en la flecha del menú desplegable para seleccionar una dirección anterior, o escriba una nueva directamente. Las direcciones se normalizan antes de guardarlas; no se almacenan duplicados. Si existe un valor `LastRoutedRadioIp` heredado de una versión anterior, se importa automáticamente la primera vez que se abre el panel.

Hay tres controles adicionales disponibles en esta página:

- **Advanced: Source path** — selecciona qué interfaz de red local (NIC) se utiliza para la conexión. La interfaz elegida se guarda como `ManualBindSource`. Aparece una **Source warning label** si la interfaz guardada no está disponible o está obsoleta.
- **Use low bandwidth mode** — reduce las tasas de datos de la transmisión para enlaces lentos o congestionados. Se guarda como `LowBandwidthMode`.
- **Enable adaptive frame-rate throttle** — cuando está activado, reduce automáticamente la tasa de fotogramas FFT/waterfall cuando la calidad de la red se degrada. Se guarda como `AdaptiveThrottleEnabled`. Valor predeterminado: desactivado.
- **Network Diagnostics** — abre la herramienta de diagnóstico de red si la conexión falla.

Al sondear una dirección IP manual, AetherSDR recopila información detallada del estado de la radio. Captura el modelo de la radio, apodo, indicativo, soporte multiFlex y datos de conexión del cliente durante una ventana de 400 milisegundos después del protocolo de enlace inicial. Esta información se utiliza para completar los campos de identidad de la radio y verificar la conexión.

### Comportamiento de inicio

La casilla de verificación **Connect to last radio on start up** controla si AetherSDR se conecta automáticamente cuando se inicia. Cuando está marcada (valor predeterminado), AetherSDR intenta reconectarse a la última radio utilizada al iniciar y cada vez que sondea direcciones de difusión-detección o radio enrutada. Cuando no está marcada, el panel de conexión se abre al inicio y debe seleccionar una radio manualmente cada sesión. Esta preferencia se guarda como `AutoConnectToLastRadio`.

### Indicadores de estado

Independientemente del modo, una **Status label** muestra el estado actual de la conexión (buscando, conectando, conectado o un mensaje de error). Después de sondear una IP manual, una **Manual result label** muestra si el sondeo tuvo éxito o falló.

### Desconexión

Una vez conectado, haga clic en **Disconnect** para volver al panel de conexión. También puede acceder al panel nuevamente a través de `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Modo | Comportamiento |
|---|---|---|
| **Local** | — | Cambia al modo de detección LAN local. |
| **SmartLink** | — | Cambia al modo remoto SmartLink. |
| **Manual** | — | Cambia al modo de ingreso manual de IP. |
| **Available radios** | Local | Lista las radios encontradas por detección LAN. Altura limitada (120–240 px) con desplazamiento interno. Clic derecho para establecer un apodo personalizado para radios que no son Flex. |
| **Connect Selected Radio** | Local | Se conecta a la radio resaltada. |
| **No local radios found yet** | Local | Indicador que se muestra cuando la detección está vacía. |
| **Retry Discovery** | Local | Vuelve a ejecutar la detección LAN. |
| **Remote with SmartLink** (acceso directo) | Local | Cambia a la página SmartLink. |
| **Connect by IP** (acceso directo) | Local | Cambia a la página Manual. |
| **Open Network Diagnostics** | Local | Abre la herramienta de diagnóstico de red. |
| **SmartLink account: Email** | SmartLink | Dirección de correo electrónico de la cuenta FlexRadio. Se guarda como `SmartLinkEmail`. Incluye metadatos de accesibilidad para la integración con el gestor de contraseñas. |
| **SmartLink account: Password** | SmartLink | Contraseña de la cuenta (no se guarda entre sesiones). Incluye metadatos de accesibilidad para la integración con el gestor de contraseñas. |
| **Sign In** | SmartLink | Autentica con SmartLink. |
| **Sign Out** | SmartLink | Cierra la sesión de SmartLink. |
| **Remote radios** | SmartLink | Lista las radios WAN disponibles para la cuenta. Desplazable; altura de visualización fija. |
| **Connect Remote Radio** | SmartLink | Inicia una conexión WAN con la radio seleccionada. |
| **Radio IP address** | Manual | Menú desplegable editable que muestra hasta tres direcciones recientes (guardadas como `RecentConnectByIpAddresses`). Escriba una nueva dirección o seleccione una anterior. Se guarda como `ManualRadioIp`. |
| **Advanced: Source path** | Manual | Selecciona la NIC local para la conexión. Se guarda como `ManualBindSource`. |
| **Use low bandwidth mode** | Manual | Activa transmisiones de tasa reducida para enlaces lentos. Se guarda como `LowBandwidthMode`. |
| **Enable adaptive frame-rate throttle** | Manual | Reduce automáticamente la tasa de fotogramas FFT/waterfall cuando la calidad de la red se degrada. Se guarda como `AdaptiveThrottleEnabled`. Valor predeterminado: desactivado. |
| **Network Diagnostics** | Manual | Abre la herramienta de diagnóstico de red. |
| **Connect by IP** (manual) | Manual | Inicia la conexión manual/VPN. |
| **Connect to last radio on start up** | Todos | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y al sondear difusión-detección / radio enrutada. Cuando no está marcado, el panel de conexión se abre y el usuario debe elegir una radio manualmente cada sesión. Valor predeterminado: marcado. Se guarda como `AutoConnectToLastRadio`. |
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
- [Set a custom nickname for a discovered radio](set-a-custom-nickname-for-a-discovered-radio.md)
