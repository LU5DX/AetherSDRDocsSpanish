# Conexión a una radio

Use el panel de conexión para conectar AetherSDR a una FLEX-8600. Puede conectarse a una radio en su LAN local, a una radio remota a través de SmartLink, o a una radio con una dirección IP manual (para conexiones por VPN o redes enrutadas).

El panel de conexión se abre automáticamente cuando AetherSDR se inicia y no hay ninguna radio conectada. También puede abrirlo en cualquier momento mediante `Settings > Connect to Radio...`.

## Antes de empezar

- La FLEX-8600 debe estar encendida y accesible en su red.
- Para conexiones LAN: Confirme que ninguna VPN, aislamiento de invitados Wi-Fi o firewall del host esté bloqueando el tráfico mDNS/detección en su red local.
- Para SmartLink: Asegúrese de tener una cuenta válida de FlexRadio SmartLink.

## Modos de conexión

El panel de conexión tiene tres modos, seleccionados mediante los botones de opción en la parte superior:

- **Local** — Descubre y conecta radios en su LAN local.
- **SmartLink** — Conecta radios remotas a través del servicio SmartLink de FlexRadio.
- **Manual** — Conecta una radio en una dirección IP específica, útil para conexiones por VPN o redes enrutadas.

El panel recuerda su último modo y lo restaura en el siguiente inicio.

## Pasos del modo Local

1. Haga clic en **Local**.
2. Espere unos segundos a que se complete la lista **Available radios**. AetherSDR escucha los paquetes de detección de la radio; esto normalmente se completa en pocos segundos.
3. Haga clic en su radio en la lista **Available radios** para resaltarla.
4. Haga clic en **Connect Selected Radio**.

La etiqueta de estado en la parte inferior del panel se actualiza a través de los estados de búsqueda, conexión y conectado a medida que se establece el enlace.

### Configurar un apodo personalizado para las radios descubiertas

Haga clic derecho en cualquier radio de la lista **Available radios** para abrir un menú contextual con la opción **Set Nickname...**. Esto es útil para radios que no tienen un almacén de nombres en la propia radio (como HL2 o backends de simulación). El apodo se guarda identificado por número de serie y se muestra en las siguientes pasadas de detección.

Para radios FlexRadio, el nombre de la radio se configura desde el menú de configuración de la propia radio mientras está conectada; la función de apodo no se ofrece para radios Flex para evitar dos fuentes de verdad.

## Pasos del modo SmartLink

1. Haga clic en **SmartLink**.
2. Introduzca el correo de su cuenta SmartLink en el campo **SmartLink account: Email**.
3. Introduzca la contraseña de su cuenta en el campo **SmartLink account: Password**.
4. Haga clic en **Sign In**.
5. Espere a que la lista **Remote radios** se complete con las radios disponibles para su cuenta.
6. Haga clic en una radio de la lista para resaltarla.
7. Haga clic en **Connect Remote Radio**.

Para cerrar sesión de SmartLink, haga clic en **Sign Out**.

## Pasos del modo Manual

1. Haga clic en **Manual**.
2. Introduzca la dirección IP o el nombre de host de la radio en el campo **Radio IP address**.
   - También puede hacer clic en la flecha del menú desplegable para seleccionar una dirección utilizada anteriormente.
3. (Opcional) Seleccione el tipo de radio en el menú desplegable **Radio type** (FlexRadio / Icom / HL2). El panel recuerda el tipo para cada dirección que introduzca.
4. (Opcional) Haga clic en **Advanced: Source path** para seleccionar una interfaz de red específica.
5. (Opcional) Marque **Use low bandwidth mode** si está en un enlace lento o con límite de datos.
6. (Opcional) Marque **Enable adaptive frame-rate throttle** para reducir automáticamente la frecuencia de cuadros del FFT/panadapter cuando la calidad de la red se degrade.
7. Haga clic en **Connect by IP (manual)**.

La etiqueta de estado muestra el resultado de la conexión, y la **Manual result label** proporciona detalles adicionales.

### Nombres de host en el modo Manual

El campo **Radio IP address** acepta tanto direcciones IP numéricas como nombres de host. Esto es importante para radios documentadas con un nombre de host en lugar de una IP — por ejemplo, la dirección predeterminada de la IC-705 es `ic-705.local`. Anteriormente, los nombres de host se descartaban silenciosamente de la lista de direcciones recientes; en v26.8.4 y versiones posteriores se recuerdan y reutilizan igual que las direcciones numéricas. Los nombres de host se validan de forma conservadora (letras, dígitos, puntos, guiones, guiones bajos, con extremos alfanuméricos, hasta 253 caracteres) antes de guardarse.

## Qué hace cada control

| Control | Qué hace | Configuración persistente |
|---|---|---|
| **Local / SmartLink / Manual** | Cambia el panel entre los tres modos de conexión. El modo predeterminado en el primer inicio es **Local**. | `ConnectionMode` |
| **Available radios** | Lista las radios FLEX-8600 descubiertas en la LAN mediante mDNS. Se completa automáticamente; no requiere entrada. Haga clic derecho en una radio para configurar un apodo personalizado (solo para radios que no son Flex). | — |
| **Connect Selected Radio** | Conecta a la radio LAN resaltada. Solo se habilita cuando hay una radio seleccionada en la lista. | — |
| **No local radios found yet** | Aviso que se muestra cuando la detección no devuelve resultados. Reemplaza la lista hasta que se encuentre una radio o se reintente la detección. | — |
| **Retry Discovery** | Vuelve a ejecutar la detección LAN inmediatamente. Aparece dentro del aviso de estado vacío. | — |
| **Remote with SmartLink** | Acceso directo al modo **SmartLink**. Aparece dentro del aviso de estado vacío. | `ConnectionMode` |
| **Connect by IP** | Acceso directo al modo **Manual**. Aparece dentro del aviso de estado vacío. | `ConnectionMode` |
| **Open Network Diagnostics** | Abre la ventana de diagnósticos de red. Aparece dentro del aviso de estado vacío. | — |
| **SmartLink account: Email** | Dirección de correo utilizada para iniciar sesión en SmartLink. Se guarda entre sesiones. | `SmartLinkEmail` |
| **SmartLink account: Password** | Contraseña utilizada para iniciar sesión en SmartLink. No se guarda entre sesiones; se almacena en el llavero del sistema operativo cuando se usa el backend de Icom. | — |
| **Sign In** | Autentica con SmartLink usando el correo y la contraseña proporcionados. | — |
| **Sign Out** | Cierra la sesión actual de SmartLink. | — |
| **Remote radios** | Lista las radios WAN de SmartLink disponibles para la cuenta con sesión iniciada. | — |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en la lista **Remote radios**. | — |
| **Radio IP address** | La dirección IP o nombre de host utilizada para una conexión manual o VPN. El campo acepta entrada escrita y también muestra hasta tres direcciones utilizadas recientemente en un menú desplegable para reutilizarlas rápidamente. Las direcciones se normalizan y deduplican antes de guardarse. | `ManualRadioIp` / `RecentConnectByIpAddresses` |
| **Radio type** | Selecciona la familia de radio para la conexión manual (FlexRadio, Icom o HL2). El panel recuerda el tipo para cada dirección que introduzca. Los perfiles antiguos sin tipo se tratan como FlexRadio. | `ConnectByIpRadioFamily` |
| **Network Diagnostics** | Abre la ventana de diagnósticos de red desde la página Manual. | — |
| **Connect by IP (manual)** | Inicia la conexión manual o VPN a la dirección introducida en **Radio IP address**. | — |
| **Advanced: Source path** | Selecciona la interfaz de red local utilizada para la conexión manual. Úselo cuando el equipo tenga múltiples NIC y AetherSDR se esté vinculando a la incorrecta. | `ManualBindSource` |
| **Use low bandwidth mode** | Habilita flujos de audio y datos a velocidad reducida. Úselo en enlaces lentos o con límite de datos. | `LowBandwidthMode` |
| **Enable adaptive frame-rate throttle** | Reduce automáticamente la frecuencia de cuadros del FFT/panadapter cuando la calidad de la red se degrada, lo que ayuda a mantener la estabilidad de la conexión en enlaces poco fiables. Desmarcado por defecto. | `AdaptiveThrottleEnabled` |
| **Connect to last radio on start up** | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y cada vez que una sonda de descubrimiento por difusión o de radio enrutada tenga éxito. Cuando está desmarcado, la pantalla de conexión se abre al iniciar y debe elegir una radio manualmente cada sesión. Marcado por defecto para que los usuarios existentes mantengan su comportamiento actual. | `AutoConnectToLastRadio` |
| **Disconnect** | Desconecta de la radio actualmente conectada. | — |

## Direcciones IP recientes (modo Manual)

El campo **Radio IP address** es un cuadro combinado desplegable que recuerda las últimas tres direcciones a las que se conectó correctamente. Haga clic en la flecha para ver la lista y seleccionar una dirección anterior, o escriba una nueva directamente en el campo.

Las direcciones se normalizan (se recortan y, si son numéricas, se canonizan) antes de almacenarse para que las formas equivalentes de la misma dirección no se guarden como duplicados. Los nombres de host también se aceptan y se almacenan tal como se escriben. La lista se escribe en la configuración `RecentConnectByIpAddresses` como una matriz JSON compacta.

Si está actualizando desde una versión anterior a v0.9.7, la dirección única almacenada anteriormente en `LastRoutedRadioIp` se traslada automáticamente como primera entrada de la nueva lista. No se requiere migración manual.

## Selección del tipo de radio (modo Manual)

El menú desplegable **Radio type** junto al campo **Radio IP address** le permite especificar a qué familia de radio se está conectando: **FlexRadio** (la predeterminada), **Icom** o **HL2**. El panel recuerda el tipo que eligió para cada dirección, por lo que alternar entre una FlexRadio y una Icom en direcciones diferentes no requiere volver a seleccionar el tipo cada vez.

Los perfiles escritos por versiones anteriores a la existencia del selector no contienen información de tipo y se tratan como FlexRadio, preservando el comportamiento que tenía antes.

## Apariencia de la ventana

El panel de conexión es un diálogo sin marco con una barra de título personalizada. La barra de título muestra "Connect to Radio" e incluye los botones estándar de control de ventana. Esta apariencia se puede controlar mediante la configuración `FramelessWindow`.

Cuando el panel está oculto durante una alternancia del modo sin marco, su geometría solo se conserva si el panel estaba visible en el momento de la alternancia.

## Dimensionado de la lista de radios

La lista **Available radios** tiene una altura limitada (mínimo 120 px, máximo 240 px) con una barra de desplazamiento vertical siempre disponible. Esto evita que la lista crezca más allá del diálogo en pantallas pequeñas como los paneles Raspberry Pi de 1024×600, garantizando que el botón Connect y los controles inferiores sigan siendo accesibles.

## Consejos

- Si la lista tarda en completarse, espere al menos 10–15 segundos antes de usar **Retry Discovery**. La radio envía paquetes de detección periódicos y AetherSDR puede no haber recibido el primero todavía.
- Si su equipo tiene múltiples interfaces de red, AetherSDR puede estar escuchando en la incorrecta. Si la detección falla sistemáticamente, considere cambiar al modo **Manual** y especificar la interfaz con **Advanced: Source path**.
- Si comparte un equipo y no desea que AetherSDR se conecte a una radio antes de tener la oportunidad de elegir una, desmarque **Connect to last radio on start up**.
- **Enable adaptive frame-rate throttle** es útil en enlaces con latencia variable o pérdida de paquetes, como puntos de acceso celulares o Wi-Fi compartido. Cuando está habilitado, AetherSDR reduce automáticamente las tasas de datos visuales para preservar la estabilidad de la conexión.
- Si su radio está documentada con un nombre de host (por ejemplo, `ic-705.local` para la IC-705), puede escribir ese nombre directamente en el campo **Radio IP address** — se recordará igual que una dirección numérica.

## Solución de problemas

- **Aparece "No local radios found yet" y no desaparece** — Los paquetes de detección de la radio no están llegando a AetherSDR. Causas comunes: la radio y el equipo están en diferentes VLAN o subredes, el aislamiento de invitados Wi-Fi del punto de acceso está habilitado, o una VPN de software está interceptando el tráfico multicast. Haga clic en **Open Network Diagnostics** para obtener detalles, o cambie al modo **Manual** si conoce la dirección IP de la radio.
- **Connect Selected Radio está atenuado** — No hay ninguna radio seleccionada en la lista **Available radios**. Haga clic primero en una radio de la lista.
- **La etiqueta de estado muestra un error después de hacer clic en Connect Selected Radio** — La radio fue descubierta pero la conexión TCP falló. Verifique que ningún firewall esté bloqueando el puerto del protocolo SmartSDR y que ningún otro cliente compatible con SmartSDR tenga la conexión exclusiva.
- **El menú desplegable Radio IP address muestra una dirección antigua o inaccesible** — Escriba una nueva dirección directamente en el campo. La entrada antigua saldrá de la lista después de que se hayan realizado tres conexiones exitosas más recientes.
- **La selección del tipo de radio sigue revirtiéndose** — El panel recuerda el tipo por dirección. Si se está conectando a una radio diferente en la misma dirección, seleccione el tipo correcto del menú desplegable antes de conectarse; se recordará para esa dirección.
- **AetherSDR se conecta a la radio incorrecta al iniciar** — Desmarque **Connect to last radio on start up**. AetherSDR abrirá entonces la pantalla de conexión en cada inicio para que pueda elegir la radio manualmente.
- **Los campos de inicio de sesión de SmartLink no se autocompletan con un gestor de contraseñas** — Asegúrese de que su gestor de contraseñas esté configurado para reconocer el formulario como un inicio de sesión de cuenta SmartLink. Los campos de correo y contraseña están etiquetados adecuadamente en el árbol de accesibilidad para macOS Passwords, Windows Authenticator y KDE Wallet.
- **El menú de clic derecho no aparece en la lista de radios** — Solo la lista **Available radios** del modo Local admite el menú contextual de clic derecho. La lista **Remote radios** de SmartLink no ofrece esta función.

## Relacionado

- [Reintentar detección cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Conectar a una radio remota a través de SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Elegir la interfaz de red local utilizada para una conexión manual](pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Habilitar el modo de ancho de banda reducido para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Desconectar de la radio actual](disconnect-from-the-current-radio.md)
- [Haga su primer QSO con AetherSDR](../tutorials/first-qso.md)
