# Reintento de descubrimiento cuando no aparecen radios

Cuando el descubrimiento local de AetherSDR no encuentra ninguna radio, aparece el aviso "No local radios found yet" en lugar de la lista de radios. Esta página explica cómo activar un nuevo escaneo de descubrimiento y qué probar si la lista sigue vacía.

## Antes de comenzar

- AetherSDR está abierto y muestra el panel "Connect to a Radio". Si no está visible, vaya a `Settings > Connect to Radio...`.
- Su FLEX-8600 está encendido y conectado a la misma LAN que su computadora.

## Pasos

1. En el panel "Connect to a Radio", confirme que **Local** sea el modo seleccionado. Si no lo es, haga clic en **Local**.
2. Si el aviso "No local radios found yet" está visible, haga clic en **Retry Discovery**.
3. Espere unos segundos mientras AetherSDR escucha paquetes de descubrimiento. Si se encuentra su radio, aparecerá en la lista **Available radios**.
4. Seleccione su radio en la lista **Available radios**, luego haga clic en **Connect Selected Radio**.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Local** | Botón de modo | Cambia al modo de descubrimiento de LAN local. |
| **SmartLink** | Botón de modo | Cambia al modo de conexión remota SmartLink. |
| **Manual** | Botón de modo | Cambia al modo de conexión IP manual. |
| **No local radios found yet** | Indicador | Se muestra cuando el descubrimiento no devuelve resultados. Reemplaza la lista de radios. |
| **Retry Discovery** | Botón | Vuelve a ejecutar el escaneo de descubrimiento LAN inmediatamente. |
| **Connect Selected Radio** | Botón | Conecta a la radio resaltada en la lista **Available radios**. |
| **Connect by IP** | Botón | Acceso directo al modo de conexión Manual. |
| **Remote with SmartLink** | Botón | Acceso directo al modo de conexión SmartLink. |
| **Open Network Diagnostics** | Botón | Abre la visualización de diagnósticos de red para inspeccionar la conectividad. |
| **Radio IP address** | Campo de texto | Ingrese la dirección IP para usar en una conexión manual. Se guarda como `ManualRadioIp`. |
| **Advanced: Source path** | Cuadro combinado | Selecciona la interfaz de red local utilizada para la conexión manual. Se guarda como `ManualBindSource`. |
| **Use low bandwidth mode** | Casilla de verificación | Activa flujos de tasa reducida para enlaces lentos. Se guarda como `LowBandwidthMode`. |
| **Enable adaptive frame-rate throttle** | Casilla de verificación | Cuando está marcada, reduce automáticamente la tasa de fotogramas de FFT/waterfall cuando la calidad de la red se degrada. Se guarda como `AdaptiveThrottleEnabled`. Por defecto está desmarcada. |
| **Connect to last radio on start up** | Casilla de verificación | Cuando está marcada, AetherSDR se conecta automáticamente a la última radio usada al iniciar y en la sonda de descubrimiento por difusión/radio enrutada. Cuando está desmarcada, se abre el diálogo de conexión y el usuario debe elegir una radio manualmente cada sesión. Se guarda como `AutoConnectToLastRadio`. Por defecto está marcada. |
| **Disconnect** | Botón | Desconecta la radio actual. |

## Indicadores

| Indicador | Significado |
|---|---|
| **Status label** | Muestra el estado actual de la conexión: buscando, conectando, conectado o con error. |
| **Manual result label** | Muestra el texto de resultado tras sondear una IP manual (éxito o error). |
| **Source warning label** | Advierte cuando la interfaz de red de origen seleccionada está desactualizada o es inalcanzable. |

## Conexión SmartLink

| Control | Tipo | Comportamiento |
|---|---|---|
| **SmartLink account: Email** | Campo de texto | Su dirección de correo electrónico de la cuenta SmartLink. Se guarda como `SmartLinkEmail`. |
| **SmartLink account: Password** | Campo de texto | Su contraseña de la cuenta SmartLink (no se guarda). |
| **Sign In** | Botón | Autentica con SmartLink. |
| **Sign Out** | Botón | Cierra sesión de SmartLink. |
| **Remote radios** | Lista | Enumera las radios WAN SmartLink disponibles para su cuenta. |
| **Connect Remote Radio** | Botón | Inicia una conexión WAN a la radio remota seleccionada. |

## Menú contextual de la lista de radios

Haga clic derecho en una radio de la lista **Available radios** para mostrar un menú contextual. La acción disponible depende del tipo de radio:

| Acción | Comportamiento |
|---|---|
| **Set Nickname...** | Abre un diálogo para asignar un apodo personalizado a la radio. El apodo se almacena en el lado del cliente y se muestra en la lista de radios en escaneos de descubrimiento posteriores. Esta opción está disponible solo para radios sin un almacén de nombres integrado (como HL2 o radios simuladas). Para radios FlexRadio, configure el nombre de la radio desde Radio Setup mientras está conectado. |

## Consejos

- El aviso "No local radios found yet" también se muestra mientras el descubrimiento aún está en progreso inmediatamente después del inicio. Espere unos segundos antes de concluir que la radio es inalcanzable.
- Si la radio y la computadora están en subredes diferentes o está usando una VPN, los paquetes de descubrimiento mDNS no cruzarán el límite de la red. Haga clic en **Connect by IP** e ingrese la dirección IP de la radio directamente.
- Las redes Wi-Fi para invitados comúnmente bloquean el tráfico entre dispositivos. Si está en Wi-Fi, verifique si su punto de acceso aplica aislamiento de clientes.
- Si comparte la computadora con otros operadores o prefiere elegir una radio explícitamente cada sesión, desmarque **Connect to last radio on start up**. AetherSDR abrirá el diálogo de conexión en cada inicio en lugar de conectarse automáticamente.
- El control **Advanced: Source path** le permite elegir qué interfaz de red local usar para conexiones manuales/VPN. Seleccione la NIC que tenga la mejor ruta hacia su radio.
- Active **Use low bandwidth mode** cuando se conecte a través de un enlace lento o poco confiable para reducir las tasas de flujo de audio y datos.
- Active **Enable adaptive frame-rate throttle** para permitir que AetherSDR reduzca automáticamente la tasa de fotogramas de FFT/waterfall cuando la calidad de la red se degrade. Esto ayuda a mantener una conexión estable en enlaces intermitentes. La reducción se reanuda a la tasa de fotogramas completa cuando la calidad de la red mejora.
- Haga clic derecho en una radio que no sea Flex en la lista **Available radios** y seleccione **Set Nickname...** para asignarle un nombre personalizado que persista entre reinicios.

## Solución de problemas

- **Retry Discovery no hace nada y la lista sigue vacía** — Es posible que la radio esté en una subred diferente, detrás de una VPN o bloqueada por un cortafuegos de host. Haga clic en **Connect by IP** e ingrese la dirección IP de la radio manualmente, o haga clic en **Open Network Diagnostics** para más detalles.
- **La radio aparece brevemente y luego desaparece** — Inestabilidad de red o un cortafuegos que descarta tráfico mDNS de forma intermitente. Verifique sus reglas de cortafuegos y vuelva a intentarlo. Si el problema persiste, use **Connect by IP** para una conexión estable.
- **Open Network Diagnostics no muestra información útil** — Vaya a `Settings > Network...` para abrir la visualización completa de diagnósticos de red.
- **AetherSDR se conecta a la radio equivocada al iniciar** — Desmarque **Connect to last radio on start up** para que el diálogo de conexión se abra al iniciar, luego seleccione la radio deseada manualmente.
- **La conexión manual falla** — Verifique que **Advanced: Source path** esté configurado en una interfaz de red válida. Si el **Source warning label** está visible, seleccione una NIC diferente o reconecte su red.
- **El inicio de sesión de SmartLink falla** — Verifique que su correo electrónico y contraseña sean correctos. Si ha cambiado su contraseña de SmartLink recientemente, cierre sesión y vuelva a iniciarla con las nuevas credenciales.

## Relacionado

- [Connect to a local LAN radio](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Log in to SmartLink to see remote radios](log-in-to-smartlink-to-see-remote-radios.md)
- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
