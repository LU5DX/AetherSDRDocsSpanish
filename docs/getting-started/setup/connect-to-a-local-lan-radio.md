# Conectar a una Radio

Utilice el panel de conexión para conectar AetherSDR a un FLEX-8600. Puede conectarse a una radio en su red local (LAN), a una radio remota a través de SmartLink, o a una radio mediante una dirección IP manual (para conexiones VPN o redes enrutadas).

El panel de conexión se abre automáticamente cuando AetherSDR se inicia y no hay ninguna radio conectada. También puede abrirlo en cualquier momento a través de `Settings > Connect to Radio...`.

## Antes de comenzar

- El FLEX-8600 debe estar encendido y accesible en su red.
- Para conexiones LAN: Confirme que ninguna VPN, aislamiento de Wi-Fi para invitados o cortafuegos del equipo esté bloqueando el tráfico mDNS/descubrimiento en su red local.
- Para SmartLink: Asegúrese de tener una cuenta válida de FlexRadio SmartLink.

## Modos de conexión

El panel de conexión tiene tres modos, seleccionados mediante los botones de opción en la parte superior:

- **Local** — Descubre y conecta radios en su red local.
- **SmartLink** — Conecta radios remotas a través del servicio SmartLink de FlexRadio.
- **Manual** — Conecta una radio a una dirección IP específica, útil para conexiones VPN o redes enrutadas.

El panel recuerda su último modo y lo restaura en el siguiente inicio.

## Pasos para el modo Local

1. Haga clic en **Local**.
2. Espere unos segundos a que se complete la lista de **Available radios**. AetherSDR escucha los paquetes de descubrimiento de la radio; esto normalmente se completa en unos segundos.
3. Haga clic en su radio en la lista **Available radios** para resaltarla.
4. Haga clic en **Connect Selected Radio**.

La etiqueta de estado en la parte inferior del panel se actualiza a través de los estados de búsqueda, conexión y, finalmente, conectado a medida que se establece el enlace.

## Pasos para el modo SmartLink

1. Haga clic en **SmartLink**.
2. Ingrese el correo electrónico de su cuenta SmartLink en el campo **SmartLink account: Email**.
3. Ingrese la contraseña de su cuenta en el campo **SmartLink account: Password**.
4. Haga clic en **Sign In**.
5. Espere a que la lista de **Remote radios** se complete con las radios disponibles para su cuenta.
6. Haga clic en una radio de la lista para resaltarla.
7. Haga clic en **Connect Remote Radio**.

Para cerrar sesión en SmartLink, haga clic en **Sign Out**.

## Pasos para el modo Manual

1. Haga clic en **Manual**.
2. Ingrese la dirección IP de la radio en el campo **Radio IP address**.
   - También puede hacer clic en la flecha desplegable para seleccionar una dirección utilizada anteriormente.
3. (Opcional) Haga clic en **Advanced: Source path** para seleccionar una interfaz de red específica.
4. (Opcional) Marque **Use low bandwidth mode** si se encuentra en un enlace lento o con límite de datos.
5. Haga clic en **Connect by IP (manual)**.

La etiqueta de estado muestra el resultado de la conexión, y la **Manual result label** proporciona detalles adicionales.

## Función de cada control

| Control | Función | Ajuste persistente |
|---|---|---|
| **Local / SmartLink / Manual** | Cambia el panel entre los tres modos de conexión. El modo predeterminado en el primer inicio es **Local**. | `ConnectionMode` |
| **Available radios** | Enumera las radios FLEX-8600 descubiertas en la LAN mediante mDNS. Se completa automáticamente; no requiere entrada de datos. | — |
| **Connect Selected Radio** | Conecta la radio LAN resaltada. Solo está habilitado cuando se selecciona una radio en la lista. | — |
| **No local radios found yet** | Mensaje mostrado cuando el descubrimiento no arroja resultados. Reemplaza la lista hasta que se encuentre una radio o se reintente el descubrimiento. | — |
| **Retry Discovery** | Vuelve a ejecutar el descubrimiento LAN inmediatamente. Aparece dentro del mensaje de estado vacío. | — |
| **Remote with SmartLink** | Acceso directo al modo **SmartLink**. Aparece dentro del mensaje de estado vacío. | `ConnectionMode` |
| **Connect by IP** | Acceso directo al modo **Manual**. Aparece dentro del mensaje de estado vacío. | `ConnectionMode` |
| **Open Network Diagnostics** | Abre la ventana de diagnóstico de red. Aparece dentro del mensaje de estado vacío. | — |
| **SmartLink account: Email** | Dirección de correo electrónico utilizada para iniciar sesión en SmartLink. Se guarda entre sesiones. | `SmartLinkEmail` |
| **SmartLink account: Password** | Contraseña utilizada para iniciar sesión en SmartLink. No se guarda entre sesiones. | — |
| **Sign In** | Autentica con SmartLink utilizando el correo electrónico y la contraseña proporcionados. | — |
| **Sign Out** | Cierra la sesión actual de SmartLink. | — |
| **Remote radios** | Enumera las radios WAN de SmartLink disponibles para la cuenta con sesión iniciada. | — |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en la lista **Remote radios**. | — |
| **Radio IP address** | La dirección IP utilizada para una conexión manual o VPN. El campo acepta entrada escrita y también muestra hasta tres direcciones utilizadas recientemente en un menú desplegable para reutilización rápida. Las direcciones se normalizan y deduplican antes de guardarse. | `ManualRadioIp` / `RecentConnectByIpAddresses` |
| **Network Diagnostics** | Abre la ventana de diagnóstico de red desde la página Manual. | — |
| **Connect by IP (manual)** | Inicia la conexión manual o VPN a la dirección ingresada en **Radio IP address**. | — |
| **Advanced: Source path** | Selecciona la interfaz de red local utilizada para la conexión manual. Úselo cuando el equipo tenga múltiples NIC y AetherSDR se esté vinculando a la incorrecta. | `ManualBindSource` |
| **Use low bandwidth mode** | Habilita flujos de audio y datos de velocidad reducida. Úselo en enlaces lentos o con límite de datos. | `LowBandwidthMode` |
| **Connect to last radio on start up** | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y siempre que una sonda de descubrimiento por difusión o radio enrutada tenga éxito. Cuando no está marcado, la pantalla de conexión se abre al iniciar y debe elegir una radio manualmente cada sesión. Por defecto está marcado para que los usuarios existentes mantengan su comportamiento actual. | `AutoConnectToLastRadio` |
| **Disconnect** | Desconecta la radio actualmente conectada. | — |

## Direcciones IP recientes (modo Manual)

El campo **Radio IP address** es un cuadro combinado desplegable que recuerda las últimas tres direcciones a las que se conectó exitosamente. Haga clic en la flecha para ver la lista y seleccionar una dirección anterior, o escriba una nueva directamente en el campo.

Las direcciones se normalizan (se recortan y analizan mediante `QHostAddress`) antes de almacenarse, de modo que formas equivalentes de la misma dirección no se guarden como duplicadas. La lista se escribe en el ajuste `RecentConnectByIpAddresses` como una matriz JSON compacta.

Si está actualizando desde una versión anterior a v0.9.7, la dirección única almacenada anteriormente en `LastRoutedRadioIp` se transfiere automáticamente como la primera entrada de la nueva lista. No se requiere migración manual.

## Apariencia de la ventana

El panel de conexión es un diálogo sin marco con una barra de título personalizada. La barra de título muestra "Connect to Radio" e incluye los botones de control de ventana estándar. Esta apariencia se puede controlar mediante el ajuste `FramelessWindow`.

## Consejos

- Si la lista tarda en completarse, espere al menos 10–15 segundos antes de usar **Retry Discovery**. La radio envía paquetes de descubrimiento periódicamente y es posible que AetherSDR aún no haya recibido el primero.
- Si su equipo tiene múltiples interfaces de red, es posible que AetherSDR esté escuchando en la incorrecta. Si el descubrimiento falla constantemente, considere cambiar al modo **Manual** y especificar la interfaz con **Advanced: Source path**.
- Si comparte un equipo y no desea que AetherSDR se conecte a una radio antes de tener la oportunidad de elegir una, desmarque **Connect to last radio on start up**.

## Solución de problemas

- **Aparece "No local radios found yet" y no desaparece** — Los paquetes de descubrimiento de la radio no llegan a AetherSDR. Causas comunes: la radio y el equipo están en diferentes VLAN o subredes, el aislamiento AP de Wi-Fi para invitados está habilitado, o una VPN de software está interceptando el tráfico multidifusión. Haga clic en **Open Network Diagnostics** para obtener detalles, o cambie al modo **Manual** si conoce la dirección IP de la radio.
- **Connect Selected Radio está atenuado** — No hay ninguna radio seleccionada en la lista **Available radios**. Haga clic primero en una radio de la lista.
- **La etiqueta de estado muestra un error después de hacer clic en Connect Selected Radio** — La radio fue descubierta pero la conexión TCP falló. Verifique que ningún cortafuegos esté bloqueando el puerto del protocolo SmartSDR y que ningún otro cliente compatible con SmartSDR tenga la conexión exclusiva.
- **El menú desplegable de Radio IP address muestra una dirección antigua o inalcanzable** — Escriba una nueva dirección directamente en el campo. La entrada antigua desaparecerá de la lista después de que se hayan realizado tres conexiones exitosas más recientes.
- **AetherSDR se conecta a la radio incorrecta al iniciar** — Desmarque **Connect to last radio on start up**. AetherSDR abrirá entonces la pantalla de conexión en cada inicio para que pueda elegir la radio manualmente.

## Relacionado

- [Retry discovery when no radios appear](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Pick the local network interface used for a manual connection](pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Enable low-bandwidth mode for slow links](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Disconnect from the current radio](disconnect-from-the-current-radio.md)
- [Make your first QSO with AetherSDR](../tutorials/first-qso.md)
