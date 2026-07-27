# Conectar a una Radio

Utilice el panel de conexión para conectar AetherSDR a una FLEX-8600. Puede conectar a una radio en su red LAN local, a una radio remota a través de SmartLink, o a una radio con una dirección IP manual (para conexiones VPN o de red enrutada).

El panel de conexión se abre automáticamente cuando AetherSDR se inicia y no hay ninguna radio conectada. También puede abrirlo en cualquier momento a través de `Settings > Connect to Radio...`.

## Antes de comenzar

- La FLEX-8600 debe estar encendida y accesible en su red.
- Para conexiones LAN: Confirme que ninguna VPN, aislamiento de invitados en Wi-Fi, o cortafuegos del anfitrión esté bloqueando el tráfico de descubrimiento mDNS en su red local.
- Para SmartLink: Asegúrese de tener una cuenta válida de FlexRadio SmartLink.

## Modos de conexión

El panel de conexión tiene tres modos, seleccionados mediante los botones de opción en la parte superior:

- **Local** — Descubre y conecta radios en su LAN local.
- **SmartLink** — Conecta radios remotas a través del servicio SmartLink de FlexRadio.
- **Manual** — Conecta a una radio con una dirección IP específica, útil para conexiones VPN o de red enrutada.

El panel recuerda su último modo y lo restaura en el siguiente inicio.

## Pasos del modo Local

1. Haga clic en **Local**.
2. Espere unos segundos a que se complete la lista de **Available radios**. AetherSDR escucha paquetes de descubrimiento de la radio; esto normalmente se completa en unos segundos.
3. Haga clic en su radio en la lista de **Available radios** para resaltarla.
4. Haga clic en **Connect Selected Radio**.

La etiqueta de estado en la parte inferior del panel se actualiza a través de los estados de búsqueda, conexión y, finalmente, conectado a medida que se establece el enlace.

### Configurar un apodo personalizado para radios descubiertas

Haga clic derecho en cualquier radio de la lista **Available radios** para abrir un menú contextual con la opción **Set Nickname...**. Esto es útil para radios que no tienen un almacén de nombres en la propia radio (como HL2 o backends de simulación). El apodo se guarda asociado al número de serie y se muestra en posteriores barridos de descubrimiento.

Para las radios FlexRadio, el nombre de la radio se configura desde el menú de configuración de la propia radio mientras está conectada; la función de apodo no se ofrece para radios Flex para evitar tener dos fuentes de verdad.

## Pasos del modo SmartLink

1. Haga clic en **SmartLink**.
2. Introduzca el correo electrónico de su cuenta SmartLink en el campo **SmartLink account: Email**.
3. Introduzca la contraseña de su cuenta en el campo **SmartLink account: Password**.
4. Haga clic en **Sign In**.
5. Espere a que la lista **Remote radios** se complete con las radios disponibles para su cuenta.
6. Haga clic en una radio de la lista para resaltarla.
7. Haga clic en **Connect Remote Radio**.

Para cerrar sesión en SmartLink, haga clic en **Sign Out**.

## Pasos del modo Manual

1. Haga clic en **Manual**.
2. Introduzca la dirección IP de la radio en el campo **Radio IP address**.
   - También puede hacer clic en la flecha desplegable para seleccionar una dirección utilizada anteriormente.
3. (Opcional) Haga clic en **Advanced: Source path** para seleccionar una interfaz de red específica.
4. (Opcional) Marque **Use low bandwidth mode** si está en un enlace lento o con límite de datos.
5. (Opcional) Marque **Enable adaptive frame-rate throttle** para reducir automáticamente la tasa de cuadros FFT/waterfall cuando la calidad de la red se degrada.
6. Haga clic en **Connect by IP (manual)**.

La etiqueta de estado muestra el resultado de la conexión, y la **Manual result label** proporciona detalles adicionales.

## Qué hace cada control

| Control | Qué hace | Configuración persistida |
|---|---|---|
| **Local / SmartLink / Manual** | Cambia el panel entre los tres modos de conexión. El modo predeterminado en el primer inicio es **Local**. | `ConnectionMode` |
| **Available radios** | Lista las radios FLEX-8600 descubiertas en la LAN mediante mDNS. Se completa automáticamente; no requiere entrada. Haga clic derecho en una radio para configurar un apodo personalizado (solo para radios que no sean Flex). | — |
| **Connect Selected Radio** | Conecta a la radio LAN resaltada. Solo está habilitado cuando hay una radio seleccionada en la lista. | — |
| **No local radios found yet** | Mensaje que se muestra cuando el descubrimiento no arroja resultados. Reemplaza la lista hasta que se encuentre una radio o se reintente el descubrimiento. | — |
| **Retry Discovery** | Vuelve a ejecutar el descubrimiento LAN inmediatamente. Aparece dentro del mensaje de estado vacío. | — |
| **Remote with SmartLink** | Acceso directo al modo **SmartLink**. Aparece dentro del mensaje de estado vacío. | `ConnectionMode` |
| **Connect by IP** | Acceso directo al modo **Manual**. Aparece dentro del mensaje de estado vacío. | `ConnectionMode` |
| **Open Network Diagnostics** | Abre la ventana de diagnóstico de red. Aparece dentro del mensaje de estado vacío. | — |
| **SmartLink account: Email** | Dirección de correo electrónico utilizada para iniciar sesión en SmartLink. Se guarda entre sesiones. | `SmartLinkEmail` |
| **SmartLink account: Password** | Contraseña utilizada para iniciar sesión en SmartLink. No se guarda entre sesiones. | — |
| **Sign In** | Autentica con SmartLink utilizando el correo electrónico y la contraseña proporcionados. | — |
| **Sign Out** | Cierra la sesión actual de SmartLink. | — |
| **Remote radios** | Lista las radios WAN de SmartLink disponibles para la cuenta que ha iniciado sesión. | — |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en la lista **Remote radios**. | — |
| **Radio IP address** | La dirección IP utilizada para una conexión manual o VPN. El campo acepta entrada escrita y también muestra hasta tres direcciones usadas recientemente en un menú desplegable para reutilización rápida. Las direcciones se normalizan y deduplican antes de guardarse. | `ManualRadioIp` / `RecentConnectByIpAddresses` |
| **Network Diagnostics** | Abre la ventana de diagnóstico de red desde la página Manual. | — |
| **Connect by IP (manual)** | Inicia la conexión manual o VPN a la dirección introducida en **Radio IP address**. | — |
| **Advanced: Source path** | Selecciona la interfaz de red local utilizada para la conexión manual. Úselo cuando el ordenador tenga múltiples NIC y AetherSDR se esté vinculando a la incorrecta. | `ManualBindSource` |
| **Use low bandwidth mode** | Activa flujos de audio y datos de tasa reducida. Úselo en enlaces lentos o con límite de datos. | `LowBandwidthMode` |
| **Enable adaptive frame-rate throttle** | Reduce automáticamente la tasa de cuadros FFT/waterfall cuando la calidad de la red se degrada, ayudando a mantener la estabilidad de la conexión en enlaces no fiables. Sin marcar por defecto. | `AdaptiveThrottleEnabled` |
| **Connect to last radio on start up** | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y cada vez que un sondeo de descubrimiento por difusión o de radio enrutada tiene éxito. Cuando no está marcado, la pantalla de conexión se abre al iniciar y debe elegir una radio manualmente cada sesión. Marcado por defecto para que los usuarios existentes mantengan su comportamiento actual. | `AutoConnectToLastRadio` |
| **Disconnect** | Desconecta de la radio actualmente conectada. | — |

## Direcciones IP recientes (modo Manual)

El campo **Radio IP address** es un cuadro combinado desplegable que recuerda las últimas tres direcciones a las que se conectó correctamente. Haga clic en la flecha para ver la lista y seleccionar una dirección anterior, o escriba una nueva directamente en el campo.

Las direcciones se normalizan (se recortan y analizan a través de `QHostAddress`) antes de almacenarse, de modo que formas equivalentes de la misma dirección no se guarden como duplicados. La lista se escribe en la configuración `RecentConnectByIpAddresses` como un array JSON compacto.

Si está actualizando desde una versión anterior a la v0.9.7, la dirección única almacenada anteriormente en `LastRoutedRadioIp` se transfiere automáticamente como la primera entrada de la nueva lista. No se requiere migración manual.

## Apariencia de la ventana

El panel de conexión es un diálogo sin marco con una barra de título personalizada. La barra de título muestra "Connect to Radio" e incluye botones de control de ventana estándar. Esta apariencia se puede controlar mediante la configuración `FramelessWindow`.

Cuando el panel está oculto durante una alternancia del modo sin marco, su geometría se conserva solo si el panel estaba visible en el momento de la alternancia.

## Tamaño de la lista de radios

La lista **Available radios** tiene una altura limitada (mínimo 120 px, máximo 240 px) con una barra de desplazamiento vertical siempre disponible. Esto evita que la lista crezca más allá del diálogo en pantallas pequeñas, como paneles Raspberry Pi de 1024×600, asegurando que el botón Connect y los controles inferiores permanezcan accesibles.

## Consejos

- Si la lista tarda en completarse, espere al menos 10-15 segundos antes de usar **Retry Discovery**. La radio envía paquetes de descubrimiento periódicamente y es posible que AetherSDR aún no haya recibido el primero.
- Si su ordenador tiene múltiples interfaces de red, es posible que AetherSDR esté escuchando en la incorrecta. Si el descubrimiento falla constantemente, considere cambiar al modo **Manual** y especificar la interfaz con **Advanced: Source path**.
- Si comparte un ordenador y no desea que AetherSDR se conecte a una radio antes de tener la oportunidad de elegir una, desmarque **Connect to last radio on start up**.
- **Enable adaptive frame-rate throttle** es útil en enlaces con latencia variable o pérdida de paquetes, como hotspots celulares o Wi-Fi compartido. Cuando está habilitado, AetherSDR reduce automáticamente las tasas de datos visuales para preservar la estabilidad de la conexión.

## Solución de problemas

- **Aparece "No local radios found yet" y no desaparece** — Los paquetes de descubrimiento de la radio no llegan a AetherSDR. Causas comunes: la radio y el ordenador están en diferentes VLANs o subredes, el aislamiento de AP invitado en Wi-Fi está habilitado, o una VPN de software está interceptando el tráfico multicast. Haga clic en **Open Network Diagnostics** para obtener detalles, o cambie al modo **Manual** si conoce la dirección IP de la radio.
- **Connect Selected Radio está atenuado** — No hay ninguna radio seleccionada en la lista **Available radios**. Haga clic primero en una radio de la lista.
- **La etiqueta de estado muestra un error después de hacer clic en Connect Selected Radio** — La radio fue descubierta pero la conexión TCP falló. Verifique que ningún cortafuegos esté bloqueando el puerto del protocolo SmartSDR, y que ningún otro cliente compatible con SmartSDR tenga la conexión exclusiva.
- **El menú desplegable de Radio IP address muestra una dirección antigua o inalcanzable** — Escriba una nueva dirección directamente en el campo. La entrada antigua desaparecerá de la lista una vez que se hayan realizado tres conexiones exitosas más recientes.
- **AetherSDR se conecta a la radio equivocada al iniciar** — Desmarque **Connect to last radio on start up**. AetherSDR abrirá entonces la pantalla de conexión en cada inicio para que pueda elegir la radio manualmente.
- **Los campos de inicio de sesión de SmartLink no se autocompletan con un gestor de contraseñas** — Asegúrese de que su gestor de contraseñas esté configurado para reconocer el formulario como un inicio de sesión de cuenta SmartLink. Los campos de correo electrónico y contraseña están etiquetados adecuadamente en el árbol de accesibilidad para macOS Passwords, Windows Authenticator y KDE Wallet.
- **El menú contextual no aparece en la lista de radios** — Solo la lista **Available radios** del modo Local admite el menú contextual con clic derecho. La lista **Remote radios** de SmartLink no ofrece esta función.

## Relacionado

- [Retry discovery when no radios appear](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Pick the local network interface used for a manual connection](pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Enable low-bandwidth mode for slow links](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Disconnect from the current radio](disconnect-from-the-current-radio.md)
- [Make your first QSO with AetherSDR](../tutorials/first-qso.md)
