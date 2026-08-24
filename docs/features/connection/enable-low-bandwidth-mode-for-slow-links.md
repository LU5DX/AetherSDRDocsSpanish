# Conectarse a una radio

El panel de conexión es la primera pantalla que se muestra cuando se inicia AetherSDR. Permite elegir entre una radio de la LAN local, una radio remota SmartLink o una conexión manual/VPN por IP.

## Modos de conexión

Elija uno de los tres modos con los botones en la parte superior del panel:

- **Local** — detecta y se conecta a radios en su red local.
- **SmartLink** — se conecta a radios WAN a través de su cuenta FlexRadio SmartLink.
- **Manual** — se conecta directamente a una radio por dirección IP o nombre de host, incluso a través de VPN.

## Antes de comenzar

- AetherSDR debe estar abierto y aún no conectado a una radio, o debe desconectarse primero antes de cambiar la configuración de conexión.
- Sepa qué modo de conexión está utilizando: Local, SmartLink o Manual.

## Conectarse a una radio local

1. Abra el panel de conexión. Aparece automáticamente antes de que una radio esté conectada. Si ya hay una radio conectada, haga clic en `Settings > Connect to Radio...` y desconéctese primero.
2. Confirme que **Local** esté seleccionado en la parte superior del panel.
3. Espere a que finalice la detección. La lista **Available radios** se llena con las radios encontradas en su LAN.
4. Haga clic en la radio a la que desea conectarse y luego haga clic en **Connect Selected Radio**.
5. Si no se encuentran radios, haga clic en **Retry Discovery** para volver a ejecutar la detección en la LAN.

## Conectarse a través de SmartLink

1. Abra el panel de conexión.
2. Haga clic en **Remote with SmartLink** en la parte superior del panel.
3. Ingrese el **Email** y la **Password** de su cuenta SmartLink y luego haga clic en **Sign In**.
4. Cuando la lista **Remote radios** se llene con las radios disponibles para su cuenta, haga clic en la radio que desee.
5. Haga clic en **Connect Remote Radio** para iniciar la conexión WAN.
6. Para cerrar sesión de SmartLink, haga clic en **Sign Out**.

## Conectarse por IP o nombre de host (manual / VPN)

1. Abra el panel de conexión.
2. Haga clic en **Connect by IP** en la parte superior del panel.
3. En el campo **Radio IP address**, ingrese la dirección IP o el nombre de host de la radio.
   - Las direcciones numéricas se canonican, por lo que `192.168.001.5` y `192.168.1.5` se consideran la misma dirección.
   - Se admiten nombres de host, incluidos nombres mDNS como `ic-705.local`. El campo recuerda tanto nombres de host como direcciones numéricas.
   - El campo almacena hasta tres direcciones usadas recientemente. Seleccione una dirección anterior del menú desplegable o escriba una nueva.
4. Si la máquina local tiene más de una interfaz de red, use **Advanced: Source path** para elegir la NIC utilizada para esta conexión.
5. Marque **Use low bandwidth mode** si se está conectando a través de un enlace lento.
6. Haga clic en **Connect by IP (manual)** para iniciar la conexión.

## Habilitar el modo de bajo ancho de banda

El modo de bajo ancho de banda reduce la tasa de flujos de audio y datos enviados desde la radio. Úselo cuando se conecte a través de un enlace lento o congestionado — como un punto de acceso celular, una VPN de larga distancia o una conexión satelital — para reducir las interrupciones y mejorar la estabilidad.

1. En el panel de conexión, localice la casilla **Use low bandwidth mode** cerca de la parte inferior.
2. Marque **Use low bandwidth mode** para habilitar flujos de tasa reducida.
3. Conéctese usando su modo preferido como de costumbre. El ajuste se negocia en el momento de la conexión.

## Qué hace cada control

| Control | Tipo | Predeterminado |
|---|---|---|
| Local / SmartLink / Manual (botones de modo) | Botón de opción | Local |
| Available radios | Lista | (sin definir) |
| Connect Selected Radio | Botón pulsador | — |
| No local radios found yet | Indicador | — |
| Retry Discovery | Botón pulsador | — |
| Remote with SmartLink | Botón pulsador | — |
| Connect by IP | Botón pulsador | — |
| Open Network Diagnostics | Botón pulsador | — |
| SmartLink account: Email | Campo de texto | (sin definir) |
| SmartLink account: Password | Campo de texto | (sin definir) |
| Sign In | Botón pulsador | — |
| Sign Out | Botón pulsador | — |
| Remote radios | Lista | (sin definir) |
| Connect Remote Radio | Botón pulsador | — |
| Radio IP address | Campo de texto. Acepta direcciones IP numéricas y nombres de host. Almacena hasta tres direcciones usadas recientemente. Se guarda como `ManualRadioIp`; las entradas recientes se guardan como `RecentConnectByIpAddresses`. | (sin definir) |
| Network Diagnostics | Botón pulsador | — |
| Connect by IP (manual) | Botón pulsador | — |
| Advanced: Source path | Cuadro combinado | (sin definir) |
| Use low bandwidth mode | Casilla de verificación | (sin definir) |
| Connect to last radio on start up | Casilla de verificación. Cuando está marcada, AetherSDR se conecta automáticamente a la última radio usada al iniciar y durante la detección por difusión / sonda de radio enrutada. Cuando está desmarcada, se abre el diálogo de conexión y el usuario debe elegir una radio manualmente en cada sesión. Se guarda como `AutoConnectToLastRadio`. | Verdadero (marcada). Nuevo en v0.9.7. Los usuarios existentes conservan el comportamiento anterior automáticamente. |
| Disconnect | Botón pulsador | — |

## Indicadores

| Indicador | Significado |
|---|---|
| Etiqueta de estado | Estado actual de la conexión (buscando / conectando / conectado / con error). |
| Etiqueta de resultado manual | Texto de resultado después de sondear una IP manual (éxito o error). |
| Etiqueta de advertencia de origen | Advierte cuando la NIC de origen seleccionada está obsoleta o es inalcanzable. |

## Consejos

- Habilite **Use low bandwidth mode** antes de iniciar la conexión. Este ajuste se negocia en el momento de la conexión.
- La lista de radios locales ahora se muestra con hasta 240 píxeles de alto y se desplaza internamente. En pantallas pequeñas (p. ej., un panel de 1024x600), la lista ya no crece más allá del botón Connect — las radios restantes siempre son accesibles mediante la barra de desplazamiento vertical.
- Haga clic con el botón derecho en cualquier radio detectada en la lista local para establecer un apodo personalizado sin conectarse primero. Las radios que no son Flex (HL2, simulador, etc.) guardan el apodo en el lado del cliente por número de serie; las radios Flex no ofrecen esta opción para evitar conflictos con el nombre configurado en la radio a través de Radio Setup.
- Si el audio aún se interrumpe después de habilitar el modo de bajo ancho de banda, verifique su VPN o ruta mediante `Settings > Network...`.
- El campo **Radio IP address** ahora recuerda hasta tres direcciones recientes. Si guardó anteriormente una IP bajo el ajuste heredado `LastRoutedRadioIp`, AetherSDR la migra automáticamente la primera vez que abre el panel de conexión.
- Para evitar que AetherSDR se conecte automáticamente al iniciar — por ejemplo, cuando desea elegir una radio diferente — desmarque **Connect to last radio on start up**.
- El panel de conexión ahora usa una ventana sin marco con una barra de título personalizada cuando **FramelessWindow** está habilitado en la configuración (predeterminado: True). El título **Connect to Radio** aparece en la barra de título de la ventana. Para redimensionar el diálogo, arrastre desde cualquier borde o esquina. Cuando la ventana sin marco se oculta y luego se vuelve a mostrar, se conserva su geometría anterior.
- Al sondear una IP manual, AetherSDR recopila información de estado de la radio, como modelo, apodo, indicativo y estado MultiFlex durante la negociación de la conexión. Esta información aparece en la lista de radios después de una sonda exitosa.
- El formulario de inicio de sesión de SmartLink ahora incluye ayudas de accesibilidad para gestores de contraseñas en macOS, Windows y Linux. Los gestores de contraseñas pueden reconocer y autocompletar credenciales en los campos de la cuenta SmartLink.

## Relacionado

- [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Pick the local network interface used for a manual connection](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Operating remotely over SmartLink](../../operating/remote/remote-operation-smartlink.md)
