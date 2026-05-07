# Conectar a una radio en una LAN local

Utilice esta página para conectar AetherSDR a una FLEX-8600 que se encuentre en la misma LAN que su computadora. AetherSDR descubre la radio automáticamente mediante mDNS; no se requiere dirección IP.

## Antes de comenzar

- La FLEX-8600 debe estar encendida y accesible en la misma red local que su computadora.
- AetherSDR debe estar ejecutándose. La pantalla de conexión aparece automáticamente antes de conectar cualquier radio, o después de una desconexión.
- Confirme que ninguna VPN, aislamiento de Wi-Fi para invitados o firewall del anfitrión esté bloqueando el tráfico mDNS/detección en su red.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente al iniciar. También puede abrirla en cualquier momento mediante `Settings > Connect to Radio...`.
2. Haga clic en **Local**. Este es el modo predeterminado, por lo que es posible que ya esté seleccionado.
3. Espere unos segundos a que se complete la lista **Available radios**. AetherSDR escucha los paquetes de descubrimiento de la radio; esto normalmente se completa en unos segundos.
4. Haga clic en su radio en la lista **Available radios** para resaltarla.
5. Haga clic en **Connect Selected Radio**.

La etiqueta de estado en la parte inferior del panel se actualiza a través de los estados de conexión y conectado a medida que se establece el enlace.

## Función de cada control

| Control | Función | Configuración persistente |
|---|---|---|
| **Local / SmartLink / Manual** | Cambia el panel entre los tres modos de conexión. El modo predeterminado al primer inicio es **Local**. | `ConnectionMode` |
| **Available radios** | Muestra las radios FLEX-8600 descubiertas en la LAN mediante mDNS. Se completa automáticamente; no requiere entrada. | — |
| **Connect Selected Radio** | Se conecta a la radio resaltada. Solo está habilitado cuando hay una radio seleccionada en la lista. | — |
| **No local radios found yet** | Mensaje que se muestra cuando la detección no devuelve resultados. Reemplaza la lista hasta que se encuentre una radio o se reintente la detección. | — |
| **Retry Discovery** | Vuelve a ejecutar la detección LAN inmediatamente. Aparece dentro del cuadro informativo de estado vacío. | — |
| **Connect by IP** | Acceso directo al modo **Manual**. Aparece dentro del cuadro informativo de estado vacío. | `ConnectionMode` |
| **Remote with SmartLink** | Acceso directo al modo **SmartLink**. Aparece dentro del cuadro informativo de estado vacío. | `ConnectionMode` |
| **Open Network Diagnostics** | Abre la ventana de diagnóstico de red. Aparece dentro del cuadro informativo de estado vacío. | — |
| **SmartLink account: Email** | Dirección de correo electrónico utilizada para iniciar sesión en SmartLink. Se guarda entre sesiones. | `SmartLinkEmail` |
| **SmartLink account: Password** | Contraseña utilizada para iniciar sesión en SmartLink. No se guarda entre sesiones. | — |
| **Sign In** | Autentica con SmartLink usando el correo electrónico y la contraseña proporcionados. | — |
| **Sign Out** | Cierra la sesión actual de SmartLink. | — |
| **Remote radios** | Muestra las radios WAN de SmartLink disponibles para la cuenta con sesión iniciada. | — |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en la lista **Remote radios**. | — |
| **Radio IP address** | La dirección IP utilizada para una conexión manual o VPN. El campo acepta entrada escrita y también muestra hasta tres direcciones usadas recientemente en un menú desplegable para reutilizarlas rápidamente. Las direcciones se normalizan y deduplican antes de guardarse. | `ManualRadioIp` / `RecentConnectByIpAddresses` |
| **Network Diagnostics** | Abre la ventana de diagnóstico de red desde la página Manual. | — |
| **Connect by IP (manual)** | Inicia la conexión manual o VPN a la dirección ingresada en **Radio IP address**. | — |
| **Advanced: Source path** | Selecciona la interfaz de red local utilizada para la conexión manual. Use esto cuando la computadora tenga múltiples NIC y AetherSDR se esté vinculando a la incorrecta. | `ManualBindSource` |
| **Use low bandwidth mode** | Habilita flujos de audio y datos de velocidad reducida. Úselo en enlaces lentos o con límite de datos. | `LowBandwidthMode` |
| **Connect to last radio on start up** | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y cada vez que una sonda de descubrimiento por difusión o de radio enrutada tiene éxito. Cuando no está marcado, la pantalla de conexión se abre al iniciar y debe elegir una radio manualmente cada sesión. Está marcado por defecto para que los usuarios existentes mantengan su comportamiento actual. | `AutoConnectToLastRadio` |
| **Disconnect** | Desconecta la radio conectada actualmente. | — |

## Direcciones IP recientes (Modo manual)

A partir de la versión 0.9.7, el campo **Radio IP address** es un cuadro combinado desplegable que recuerda las últimas tres direcciones a las que se conectó correctamente. Haga clic en la flecha para ver la lista y seleccionar una dirección anterior, o escriba una nueva directamente en el campo.

Las direcciones se normalizan (recortadas y analizadas a través de `QHostAddress`) antes de almacenarse, de modo que las formas equivalentes de la misma dirección no se guarden como duplicadas. La lista se escribe en la configuración `RecentConnectByIpAddresses` como una matriz JSON compacta.

Si está actualizando desde una versión anterior a la 0.9.7, la dirección única almacenada previamente en `LastRoutedRadioIp` se transfiere automáticamente como la primera entrada en la nueva lista. No se requiere migración manual.

## Consejos

- Si la lista se completa lentamente, espere al menos 10–15 segundos antes de usar **Retry Discovery**. La radio envía paquetes de descubrimiento periódicamente y es posible que AetherSDR aún no haya recibido el primero.
- Si su computadora tiene múltiples interfaces de red, es posible que AetherSDR esté escuchando en la incorrecta. Si la detección falla constantemente, considere cambiar al modo **Manual** y especificar la interfaz con **Advanced: Source path**.
- Si comparte una computadora y no desea que AetherSDR se conecte a una radio antes de tener la oportunidad de elegir una, desmarque **Connect to last radio on start up**.

## Solución de problemas

- **"No local radios found yet" aparece y no desaparece** — Los paquetes de descubrimiento de la radio no llegan a AetherSDR. Causas comunes: la radio y la computadora están en diferentes VLAN o subredes, el aislamiento AP de Wi-Fi para invitados está habilitado, o una VPN de software está interceptando el tráfico multicast. Haga clic en **Open Network Diagnostics** para obtener detalles, o cambie al modo **Manual** si conoce la dirección IP de la radio.
- **Connect Selected Radio está atenuado** — No hay ninguna radio seleccionada en la lista **Available radios**. Haga clic primero en una radio de la lista.
- **La etiqueta de estado muestra un error después de hacer clic en Connect Selected Radio** — La radio fue descubierta pero la conexión TCP falló. Verifique que ningún firewall esté bloqueando el puerto del protocolo SmartSDR y que ningún otro cliente compatible con SmartSDR tenga la conexión exclusiva.
- **El menú desplegable Radio IP address muestra una dirección antigua o inalcanzable** — Escriba una nueva dirección directamente en el campo. La entrada antigua desaparecerá de la lista después de que se hayan realizado tres conexiones exitosas más recientes.
- **AetherSDR se conecta a la radio incorrecta al iniciar** — Desmarque **Connect to last radio on start up**. AetherSDR abrirá entonces la pantalla de conexión en cada inicio para que pueda elegir la radio manualmente.

## Relacionado

- [Retry discovery when no radios appear](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Pick the local network interface used for a manual connection](pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Enable low-bandwidth mode for slow links](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Disconnect from the current radio](disconnect-from-the-current-radio.md)
- [Make your first QSO with AetherSDR](../tutorials/first-qso.md)
