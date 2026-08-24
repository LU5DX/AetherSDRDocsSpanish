# Reintentar la detección cuando no aparecen radios

Cuando la detección local de AetherSDR no encuentra radios, aparece el aviso "No local radios found yet" en lugar de la lista de radios. Esta página explica cómo activar un nuevo escaneo de detección y qué probar si la lista sigue vacía.

## Antes de comenzar

- AetherSDR está abierto y muestra el panel "Connect to a Radio". Si no está visible, vaya a `Settings > Connect to Radio...`.
- Su FLEX-8600 está encendido y conectado a la misma LAN que su computadora.

## Pasos

1. En el panel "Connect to a Radio", confirme que **Local** es el modo seleccionado. Si no lo es, haga clic en **Local**.
2. Si el aviso "No local radios found yet" es visible, haga clic en **Retry Discovery**.
3. Espere unos segundos mientras AetherSDR escucha los paquetes de detección. Si se encuentra su radio, aparecerá en la lista **Available radios**.
4. Seleccione su radio en la lista **Available radios** y luego haga clic en **Connect Selected Radio**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Local** | Botón de modo | Cambia al modo de detección de LAN local. |
| **SmartLink** | Botón de modo | Cambia al modo de conexión remota SmartLink. |
| **Manual** | Botón de modo | Cambia al modo de conexión manual por IP. |
| **No local radios found yet** | Indicador | Se muestra cuando la detección no devuelve resultados. Reemplaza la lista de radios. |
| **Retry Discovery** | Botón | Vuelve a ejecutar el escaneo de detección LAN inmediatamente. |
| **Connect Selected Radio** | Botón | Conecta a la radio resaltada en la lista **Available radios**. |
| **Connect by IP** | Botón | Acceso directo al modo de conexión Manual. |
| **Remote with SmartLink** | Botón | Acceso directo al modo de conexión SmartLink. |
| **Open Network Diagnostics** | Botón | Abre la pantalla de diagnóstico de red para inspeccionar la conectividad. |
| **Radio IP address** | Campo de texto | Ingrese la dirección IP o el nombre de host (por ejemplo, `ic-705.local`) para una conexión manual. Se guarda como `ManualRadioIp`. |
| **Advanced: Source path** | Cuadro combinado | Selecciona la interfaz de red local utilizada para la conexión manual. Se guarda como `ManualBindSource`. |
| **Use low bandwidth mode** | Casilla de verificación | Habilita flujos de tasa reducida para enlaces lentos. Se guarda como `LowBandwidthMode`. |
| **Enable adaptive frame-rate throttle** | Casilla de verificación | Cuando está marcada, reduce automáticamente la tasa de fotogramas de FFT/waterfall cuando la calidad de la red se degrada. Se guarda como `AdaptiveThrottleEnabled`. Por defecto está desmarcada. |
| **Connect to last radio on start up** | Casilla de verificación | Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y durante la detección por difusión / sondeo de radio enrutado. Cuando está desmarcada, se abre el diálogo de conexión y el usuario debe elegir una radio manualmente en cada sesión. Se guarda como `AutoConnectToLastRadio`. Por defecto está marcada. |
| **Disconnect** | Botón | Desconecta de la radio actual. |

## Indicadores

| Indicador | Significado |
|---|---|
| **Status label** | Muestra el estado actual de la conexión: buscando, conectando, conectado o con error. |
| **Manual result label** | Muestra el texto de resultado después de sondear una IP manual (éxito o error). |
| **Source warning label** | Advierte cuando la interfaz de red de origen seleccionada está obsoleta o es inaccesible. |

## Conexión SmartLink

| Control | Tipo | Comportamiento |
|---|---|---|
| **SmartLink account: Email** | Campo de texto | La dirección de correo electrónico de su cuenta SmartLink. Se guarda como `SmartLinkEmail`. |
| **SmartLink account: Password** | Campo de texto | La contraseña de su cuenta SmartLink (no se guarda). |
| **Sign In** | Botón | Autentica con SmartLink. |
| **Sign Out** | Botón | Cierra la sesión de SmartLink. |
| **Remote radios** | Lista | Enumera las radios WAN SmartLink disponibles para su cuenta. |
| **Connect Remote Radio** | Botón | Inicia una conexión WAN con la radio remota seleccionada. |

## Menú contextual de la lista de radios

Haga clic derecho en una radio de la lista **Available radios** para mostrar un menú contextual. La acción disponible depende del tipo de radio:

| Acción | Comportamiento |
|---|---|
| **Set Nickname...** | Abre un diálogo para asignar un apodo personalizado a la radio. El apodo se almacena en el lado del cliente y se muestra en la lista de radios en los escaneos de detección posteriores. Esta opción solo está disponible para radios sin un almacén de nombres integrado (como HL2 o radios simuladas). Para radios FlexRadio, configure el nombre de la radio desde Radio Setup mientras está conectado. |

## Consejos

- El aviso "No local radios found yet" también se muestra mientras la detección aún está en progreso inmediatamente después del inicio. Espere unos segundos antes de concluir que la radio es inalcanzable.
- Si la radio y la computadora están en subredes diferentes o está usando una VPN, los paquetes de detección mDNS no cruzarán el límite de la red. Haga clic en **Connect by IP** e ingrese la dirección IP o el nombre de host de la radio directamente.
- Las redes Wi-Fi para invitados suelen bloquear el tráfico entre dispositivos. Si está en Wi-Fi, verifique si su punto de acceso aplica aislamiento de clientes.
- Si comparte la computadora con otros operadores o prefiere elegir una radio explícitamente en cada sesión, desmarque **Connect to last radio on start up**. AetherSDR abrirá el diálogo de conexión en cada inicio en lugar de conectarse automáticamente.
- El control **Advanced: Source path** le permite elegir qué interfaz de red local usar para conexiones manuales/VPN. Seleccione la NIC que tenga la mejor ruta hacia su radio.
- Habilite **Use low bandwidth mode** al conectarse a través de un enlace lento o poco confiable para reducir las tasas de flujo de audio y datos.
- Habilite **Enable adaptive frame-rate throttle** para que AetherSDR reduzca automáticamente la tasa de fotogramas de FFT/waterfall cuando la calidad de la red se degrada. Esto ayuda a mantener una conexión estable en enlaces intermitentes. El limitador restablece la tasa completa de fotogramas cuando la calidad de la red mejora.
- Haga clic derecho en una radio que no sea Flex en la lista **Available radios** y seleccione **Set Nickname...** para asignarle un nombre personalizado que persista entre reinicios.

## Solución de problemas

- **Retry Discovery no hace nada y la lista sigue vacía** — La radio puede estar en una subred diferente, detrás de una VPN o bloqueada por un firewall del host. Haga clic en **Connect by IP** e ingrese la dirección IP o el nombre de host de la radio manualmente, o haga clic en **Open Network Diagnostics** para obtener más detalles.
- **La radio aparece brevemente y luego desaparece** — Inestabilidad de la red o un firewall que descarta el tráfico mDNS de forma intermitente. Verifique las reglas de su firewall y reintente. Si el problema persiste, use **Connect by IP** para una conexión estable.
- **Open Network Diagnostics no muestra información útil** — Vaya a `Settings > Network...` para abrir la pantalla completa de diagnóstico de red.
- **AetherSDR se conecta a la radio incorrecta al iniciar** — Desmarque **Connect to last radio on start up** para que el diálogo de conexión se abra al inicio y luego seleccione la radio deseada manualmente.
- **La conexión manual falla** — Verifique que **Advanced: Source path** esté configurado con una interfaz de red válida. Si el **Source warning label** es visible, seleccione una NIC diferente o reconecte su red.
- **El inicio de sesión de SmartLink falla** — Verifique que su correo electrónico y contraseña sean correctos. Si ha cambiado su contraseña de SmartLink recientemente, cierre la sesión e inicie sesión nuevamente con las nuevas credenciales.

## Relacionado

- [Connect to a local LAN radio](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Log in to SmartLink to see remote radios](log-in-to-smartlink-to-see-remote-radios.md)
- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
