# Descripción general de Connect to a Radio

El panel **Connect to a Radio** es el punto de partida de cada sesión de AetherSDR. Le permite elegir cómo llegar a su FLEX-8600 — en su red local, a través de FlexRadio SmartLink, o ingresando una dirección IP directamente — y luego iniciar la conexión.

## Antes de comenzar

- Su FLEX-8600 debe estar encendido y ejecutando el firmware 4.2.
- Para conexiones SmartLink, necesita una cuenta de FlexRadio y acceso a internet en ambos extremos.
- Para conexiones manuales/VPN, necesita la dirección IP o el nombre de host de la radio.

## Cómo funciona

El panel se abre como una ventana separada siempre que no haya ninguna radio conectada. Cuenta con una barra de título personalizada con el texto "Connect to Radio". Puede arrastrar la ventana por su barra de título. El panel aparece en la ventana principal siempre que no haya ninguna radio conectada. También puede abrirlo en cualquier momento a través de `Settings > Connect to Radio...`.

El panel utiliza un estilo de ventana sin marco por defecto, controlado por la configuración `FramelessWindow` (valor predeterminado: True). Cuando el modo sin marco está activado, la barra de título personalizada permite arrastrar la ventana. El panel restaura su geometría anterior cuando vuelve a ser visible después de haberse ocultado. Al cerrar esta ventana se cierra el panel de conexión.

Tres botones de modo en la parte superior determinan qué método de conexión está activo. Seleccionar un modo cambia el panel inferior para mostrar los controles correspondientes. AetherSDR conserva el último modo utilizado en `ConnectionMode`.

### On This Network (modo Local)

Use este modo cuando la radio y su computadora estén en la misma LAN. AetherSDR ejecuta la detección mDNS/Flex automáticamente y enumera cualquier radio que encuentre en **Available radios**. Seleccione una radio de la lista y haga clic en **Connect Selected Radio** para conectarse.

Si la detección no encuentra nada, el panel cambia a una vista de estado vacío que muestra **No local radios found yet**. Desde allí puede:

- Hacer clic en **Retry Discovery** para volver a ejecutar la detección.
- Hacer clic en **Connect by IP** para cambiar a la página Manual.
- Hacer clic en **Remote with SmartLink** para cambiar a la página SmartLink.
- Hacer clic en **Open Network Diagnostics** para investigar problemas de red.

Las razones comunes por las que la detección no devuelve nada incluyen el aislamiento de AP en redes Wi-Fi de invitados, software VPN ejecutándose en el host y reglas de firewall que bloquean los paquetes de detección.

La lista **Available radios** tiene una altura limitada (mínimo 120px, máximo 240px), por lo que se desplaza internamente cuando se detectan más radios de las que caben en el área visible. Esto evita que la lista crezca más allá del diálogo en pantallas pequeñas. La lista incluye una barra de desplazamiento vertical de estilo personalizado con controles redondeados.

Puede hacer clic derecho en cualquier radio de la lista **Available radios** para abrir un menú contextual. Elija **Set custom nickname** para asignar un apodo del lado del cliente que persiste entre barridos de detección. Esto está pensado para radios que no son Flex (como HL2 o radios simuladas) que no almacenan un nombre en la propia radio. Para radios Flex, el apodo se gestiona a través de Radio Setup mientras está conectado, por lo que el menú contextual no se ofrece para radios Flex para evitar fuentes de verdad conflictivas.

### Remote with SmartLink

Use este modo cuando la radio esté en una ubicación diferente. Ingrese el correo electrónico de su cuenta FlexRadio en **SmartLink account: Email** (conservado como `SmartLinkEmail`) y su contraseña en **SmartLink account: Password** (no conservada), y luego haga clic en **Sign In**. Después de la autenticación, AetherSDR llena la lista **Remote radios** con las radios WAN disponibles para su cuenta. La lista tiene una altura fija; si tiene muchas radios remotas, desplácese dentro de la lista para encontrar la que desea. Seleccione una radio y haga clic en **Connect Remote Radio**. Para finalizar la sesión, haga clic en **Sign Out**.

Los campos de correo electrónico y contraseña incluyen metadatos de accesibilidad para ayudar a los gestores de contraseñas (macOS Passwords, Windows Authenticator, KDE Wallet) a asociar el par de credenciales con el formulario de inicio de sesión de SmartLink.

### Connect by IP (modo Manual)

Use este modo para conexiones VPN o de red enrutada donde ya conoce la dirección IP o el nombre de host de la radio. Ingrese la dirección en **Radio IP address** (conservada como `ManualRadioIp`) y luego haga clic en **Connect by IP**.

El campo **Radio IP address** es una lista desplegable editable. AetherSDR almacena hasta tres direcciones utilizadas recientemente (conservadas como `RecentConnectByIpAddresses`) y llena la lista desplegable con ellas cuando se abre el panel. Haga clic en la flecha de la lista desplegable para seleccionar una dirección anterior, o escriba una nueva directamente. Las direcciones y nombres de host se normalizan antes de guardarse; no se almacenan duplicados. Las direcciones numéricas se canonizan (por lo que `192.168.001.5` y `192.168.1.5` se tratan como una sola entrada), y los nombres de host como `ic-705.local` ahora se recuerdan. Si existe un valor heredado de `LastRoutedRadioIp` de una versión anterior, se importa automáticamente la primera vez que se abre el panel.

El campo **Radio IP address** acepta tanto direcciones IP numéricas como nombres de host. Los nombres de host se validan con un conjunto de caracteres conservador (letras, dígitos, punto, guion, guion bajo, con extremos alfanuméricos) y una longitud máxima de 253 caracteres. Esto permite que las radios VPN alcanzadas por nombre DNS aparezcan en la lista reciente; anteriormente se descartaban silenciosamente.

Hay tres controles adicionales disponibles en esta página:

- **Advanced: Source path** — selecciona qué interfaz de red local (NIC) se utiliza para la conexión. La interfaz elegida se conserva como `ManualBindSource`. Una **Source warning label** aparece si la interfaz guardada no está disponible o está obsoleta.
- **Use low bandwidth mode** — reduce las tasas de datos de transmisión para enlaces lentos o congestionados. Se conserva como `LowBandwidthMode`.
- **Enable adaptive frame-rate throttle** — cuando está habilitado, reduce automáticamente la tasa de fotogramas FFT/waterfall cuando la calidad de la red se degrada. Se conserva como `AdaptiveThrottleEnabled`. Valor predeterminado: desactivado.
- **Network Diagnostics** — abre la herramienta de diagnóstico de red si la conexión falla.

Al sondear una dirección IP manual, AetherSDR recopila información de estado detallada de la radio. Captura el modelo de la radio, el apodo, el indicativo, la compatibilidad con multiFlex y los datos de conexión del cliente durante una ventana de observación de 400 milisegundos después del protocolo de enlace inicial. Esta información se utiliza para llenar los campos de identidad de la radio y verificar la conexión.

### Comportamiento de inicio

La casilla **Connect to last radio on start up** controla si AetherSDR se conecta automáticamente al iniciarse. Cuando está marcada (valor predeterminado), AetherSDR intenta reconectarse a la última radio utilizada al inicio y siempre que sondea direcciones de detección por difusión o de radio enrutada. Cuando está desmarcada, el panel de conexión se abre al inicio y debe seleccionar una radio manualmente en cada sesión. Esta preferencia se conserva como `AutoConnectToLastRadio`.

### Indicadores de estado

Independientemente del modo, una **Status label** muestra el estado actual de la conexión (buscando, conectando, conectado o un mensaje de error). Después de sondear una IP manual, una **Manual result label** muestra si el sondeo tuvo éxito o falló.

### Desconexión

Una vez conectado, haga clic en **Disconnect** para volver al panel de conexión. También puede llegar al panel nuevamente a través de `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Modo | Comportamiento |
|---|---|---|
| **Local** | — | Cambia al modo de detección LAN local. |
| **SmartLink** | — | Cambia al modo remoto SmartLink. |
| **Manual** | — | Cambia al modo de ingreso manual de IP. |
| **Available radios** | Local | Enumera las radios encontradas por detección LAN. Altura limitada (120–240px) con desplazamiento interno. Haga clic derecho para establecer un apodo personalizado para radios que no son Flex. |
| **Connect Selected Radio** | Local | Se conecta a la radio resaltada. |
| **No local radios found yet** | Local | Indicador mostrado cuando la detección está vacía. |
| **Retry Discovery** | Local | Vuelve a ejecutar la detección LAN. |
| **Remote with SmartLink** (acceso directo) | Local | Cambia a la página SmartLink. |
| **Connect by IP** (acceso directo) | Local | Cambia a la página Manual. |
| **Open Network Diagnostics** | Local | Abre la herramienta de diagnóstico de red. |
| **SmartLink account: Email** | SmartLink | Dirección de correo electrónico de la cuenta FlexRadio. Se conserva como `SmartLinkEmail`. Incluye metadatos de accesibilidad para la integración con gestores de contraseñas. |
| **SmartLink account: Password** | SmartLink | Contraseña de la cuenta (no se guarda entre sesiones). Incluye metadatos de accesibilidad para la integración con gestores de contraseñas. |
| **Sign In** | SmartLink | Autentica con SmartLink. |
| **Sign Out** | SmartLink | Cierra la sesión de SmartLink. |
| **Remote radios** | SmartLink | Enumera las radios WAN disponibles para la cuenta. Desplazable; altura de visualización fija. |
| **Connect Remote Radio** | SmartLink | Inicia una conexión WAN a la radio seleccionada. |
| **Radio IP address** | Manual | Lista desplegable editable que muestra hasta tres direcciones recientes (conservadas como `RecentConnectByIpAddresses`). Acepta direcciones IP numéricas y nombres de host (hasta 253 caracteres, validados con un conjunto de caracteres conservador). Escriba una nueva dirección o seleccione una anterior. Se conserva como `ManualRadioIp`. |
| **Advanced: Source path** | Manual | Selecciona la NIC local para la conexión. Se conserva como `ManualBindSource`. |
| **Use low bandwidth mode** | Manual | Habilita flujos de tasa reducida para enlaces lentos. Se conserva como `LowBandwidthMode`. |
| **Enable adaptive frame-rate throttle** | Manual | Reduce automáticamente la tasa de fotogramas FFT/waterfall cuando la calidad de la red se degrada. Se conserva como `AdaptiveThrottleEnabled`. Valor predeterminado: desactivado. |
| **Network Diagnostics** | Manual | Abre la herramienta de diagnóstico de red. |
| **Connect by IP** (manual) | Manual | Inicia la conexión manual/VPN. |
| **Connect to last radio on start up** | Todos | Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al inicio y en el sondeo de detección por difusión / radio enrutada. Cuando está desmarcada, el panel de conexión se abre y el usuario debe elegir una radio manualmente en cada sesión. Valor predeterminado: marcada. Se conserva como `AutoConnectToLastRadio`. |
| **Disconnect** | Todos | Desconecta de la radio actual. |

## Relacionado

- [Connect to a local LAN radio](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Retry discovery when no radios appear](retry-discovery-when-no-radios-appear.md)
- [Log in to SmartLink to see remote radios](log-in-to-smartlink-to-see-remote-radios.md)
- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Pick the local network interface used for a manual connection](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Enable low-bandwidth mode for slow links](enable-low-bandwidth-mode-for-slow-links.md)
- [Disconnect from the current radio](../../getting-started/setup/disconnect-from-the-current-radio.md)
- Establecer un apodo personalizado para una radio detectada
