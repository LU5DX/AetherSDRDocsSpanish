# Conectar a una Radio

Utilice el panel de conexión para conectar AetherSDR a una FLEX-8600. Puede conectarse a una radio en su LAN local, a una radio remota a través de SmartLink, o a una radio en una dirección IP manual (para conexiones VPN o de red enrutada).

El panel de conexión se abre automáticamente cuando AetherSDR se inicia y no hay ninguna radio conectada. También puede abrirlo en cualquier momento a través de `Settings > Connect to Radio...`.

## Antes de comenzar

- La FLEX-8600 debe estar encendida y accesible en su red.
- Para conexiones LAN: Confirme que ninguna VPN, aislamiento de invitados Wi-Fi o firewall del anfitrión esté bloqueando el tráfico de descubrimiento mDNS en su red local.
- Para SmartLink: Asegúrese de tener una cuenta válida de FlexRadio SmartLink.

## Modos de conexión

El panel de conexión tiene tres modos, seleccionados mediante los botones de opción en la parte superior:

- **Local** — Descubre y conecta radios en su LAN local.
- **SmartLink** — Conecta radios remotas a través del servicio SmartLink de FlexRadio.
- **Manual** — Conecta una radio en una dirección IP específica, útil para conexiones VPN o de red enrutada.

El panel recuerda su último modo y lo restaura en el próximo inicio.

## Pasos del modo Local

1. Haga clic en **Local**.
2. Espere unos segundos a que la lista **Available radios** se complete. AetherSDR escucha los paquetes de descubrimiento de la radio; esto normalmente se completa en unos segundos.
3. Haga clic en su radio en la lista **Available radios** para seleccionarla.
4. Haga clic en **Connect Selected Radio**.

La etiqueta de estado en la parte inferior del panel se actualiza a través de los estados de búsqueda, conexión y luego conectado a medida que se establece el enlace.

## Pasos del modo SmartLink

1. Haga clic en **SmartLink**.
2. Ingrese el correo electrónico de su cuenta SmartLink en el campo **SmartLink account: Email**.
3. Ingrese la contraseña de su cuenta en el campo **SmartLink account: Password**.
4. Haga clic en **Sign In**.
5. Espere a que la lista **Remote radios** se complete con las radios disponibles para su cuenta.
6. Haga clic en una radio de la lista para seleccionarla.
7. Haga clic en **Connect Remote Radio**.

Para cerrar sesión en SmartLink, haga clic en **Sign Out**.

## Pasos del modo Manual

1. Haga clic en **Manual**.
2. Ingrese la dirección IP de la radio en el campo **Radio IP address**.
   - También puede hacer clic en la flecha desplegable para seleccionar una dirección utilizada anteriormente.
3. (Opcional) Haga clic en **Advanced: Source path** para seleccionar una interfaz de red específica.
4. (Opcional) Marque **Use low bandwidth mode** si está en un enlace lento o medido.
5. Haga clic en **Connect by IP (manual)**.

La etiqueta de estado muestra el resultado de la conexión, y la **Manual result label** proporciona detalles adicionales.

## Función de cada control

| Control | Función | Configuración persistente |
|---|---|---|
| **Local / SmartLink / Manual** | Cambia el panel entre los tres modos de conexión. El modo predeterminado en el primer inicio es **Local**. | `ConnectionMode` |
| **Available radios** | Enumera las radios FLEX-8600 descubiertas en la LAN mediante mDNS. Se completa automáticamente; no requiere entrada. | — |
| **Connect Selected Radio** | Se conecta a la radio LAN seleccionada. Solo está habilitado cuando hay una radio seleccionada en la lista. | — |
| **No local radios found yet** | Mensaje que se muestra cuando el descubrimiento no devuelve resultados. Reemplaza la lista hasta que se encuentre una radio o se reintente el descubrimiento. | — |
| **Retry Discovery** | Vuelve a ejecutar el descubrimiento LAN inmediatamente. Aparece dentro del mensaje de estado vacío. | — |
| **Remote with SmartLink** | Acceso directo al modo **SmartLink**. Aparece dentro del mensaje de estado vacío. | `ConnectionMode` |
| **Connect by IP** | Acceso directo al modo **Manual**. Aparece dentro del mensaje de estado vacío. | `ConnectionMode` |
| **Open Network Diagnostics** | Abre la ventana de diagnóstico de red. Aparece dentro del mensaje de estado vacío. | — |
| **SmartLink account: Email** | Dirección de correo electrónico utilizada para iniciar sesión en SmartLink. Se guarda entre sesiones. | `SmartLinkEmail` |
| **SmartLink account: Password** | Contraseña utilizada para iniciar sesión en SmartLink. No se guarda entre sesiones. | — |
| **Sign In** | Autentica con SmartLink usando el correo electrónico y la contraseña proporcionados. | — |
| **Sign Out** | Cierra la sesión actual de SmartLink. | — |
| **Remote radios** | Enumera las radios WAN de SmartLink disponibles para la cuenta autenticada. | — |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en la lista **Remote radios**. | — |
| **Radio IP address** | La dirección IP utilizada para una conexión manual o VPN. El campo acepta entrada de texto y también muestra hasta tres direcciones utilizadas recientemente en un menú desplegable para reutilización rápida. Las direcciones se normalizan y deduplican antes de guardarse. | `ManualRadioIp` / `RecentConnectByIpAddresses` |
| **Network Diagnostics** | Abre la ventana de diagnóstico de red desde la página Manual. | — |
| **Connect by IP (manual)** | Inicia la conexión manual o VPN a la dirección ingresada en **Radio IP address**. | — |
| **Advanced: Source path** | Selecciona la interfaz de red local utilizada para la conexión manual. Utilícelo cuando la computadora tenga varias NIC y AetherSDR se esté vinculando a la incorrecta. | `ManualBindSource` |
| **Use low bandwidth mode** | Habilita flujos de audio y datos de velocidad reducida. Utilícelo en enlaces lentos o medidos. | `LowBandwidthMode` |
| **Connect to last radio on start up** | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al inicio y cada vez que una sonda de descubrimiento de transmisión o radio enrutada tiene éxito. Cuando no está marcado, la pantalla de conexión se abre al inicio y debe elegir una radio manualmente cada sesión. Está marcado de forma predeterminada para que los usuarios existentes mantengan su comportamiento actual. | `AutoConnectToLastRadio` |
| **Disconnect** | Desconecta la radio actualmente conectada. | — |

## Direcciones IP recientes (modo Manual)

El campo **Radio IP address** es un cuadro combinado desplegable que recuerda las últimas tres direcciones a las que se conectó exitosamente. Haga clic en la flecha para ver la lista y seleccionar una dirección anterior, o escriba una nueva directamente en el campo.

Las direcciones se normalizan (recortan y analizan a través de `QHostAddress`) antes de almacenarse, de modo que las formas equivalentes de la misma dirección no se guarden como duplicados. La lista se escribe en la configuración `RecentConnectByIpAddresses` como una matriz JSON compacta.

Si está actualizando desde una versión anterior a v0.9.7, la dirección única almacenada anteriormente en `LastRoutedRadioIp` se transfiere automáticamente como la primera entrada en la nueva lista. No se requiere migración manual.

## Apariencia de la ventana

El panel de conexión es un diálogo sin marco con una barra de título personalizada. La barra de título muestra "Connect to Radio" e incluye botones de control de ventana estándar. Esta apariencia se puede controlar mediante la configuración `FramelessWindow`.

Cuando el panel está oculto durante una alternancia del modo sin marco, su geometría se conserva solo si el panel era visible en el momento de la alternancia.

## Consejos

- Si la lista tarda en completarse, espere al menos 10–15 segundos antes de usar **Retry Discovery**. La radio envía paquetes de descubrimiento periódicos y es posible que AetherSDR aún no haya recibido el primero.
- Si su computadora tiene múltiples interfaces de red, es posible que AetherSDR esté escuchando en la incorrecta. Si el descubrimiento falla constantemente, considere cambiar al modo **Manual** y especificar la interfaz con **Advanced: Source path**.
- Si comparte una computadora y no desea que AetherSDR se conecte a una radio antes de tener la oportunidad de elegir una, desmarque **Connect to last radio on start up**.

## Solución de problemas

- **Aparece "No local radios found yet" y no desaparece** — Los paquetes de descubrimiento de la radio no llegan a AetherSDR. Causas comunes: la radio y la computadora están en diferentes VLAN o subredes, el aislamiento de AP Wi-Fi para invitados está habilitado, o una VPN de software está interceptando el tráfico multidifusión. Haga clic en **Open Network Diagnostics** para más detalles, o cambie al modo **Manual** si conoce la dirección IP de la radio.
- **Connect Selected Radio está atenuado** — No hay ninguna radio seleccionada en la lista **Available radios**. Haga clic primero en una radio de la lista.
- **La etiqueta de estado muestra un error después de hacer clic en Connect Selected Radio** — La radio fue descubierta pero la conexión TCP falló. Verifique que ningún firewall esté bloqueando el puerto del protocolo SmartSDR, y que ningún otro cliente compatible con SmartSDR tenga la conexión exclusiva.
- **El menú desplegable Radio IP address muestra una dirección antigua o inalcanzable** — Escriba una nueva dirección directamente en el campo. La entrada anterior se eliminará de la lista una vez que se hayan realizado tres nuevas conexiones exitosas.
- **AetherSDR se conecta a la radio incorrecta al inicio** — Desmarque **Connect to last radio on start up**. AetherSDR abrirá la pantalla de conexión en cada inicio para que pueda elegir la radio manualmente.

## Relacionado

- [Reintentar descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Conectar a una radio remota a través de SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Elegir la interfaz de red local utilizada para una conexión manual](pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Habilitar el modo de ancho de banda bajo para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Desconectar la radio actual](disconnect-from-the-current-radio.md)
- [Realice su primer QSO con AetherSDR](../tutorials/first-qso.md)
