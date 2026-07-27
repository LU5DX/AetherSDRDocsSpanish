# Desconectar de la Radio Actual

Esta página explica cómo desconectar AetherSDR de una FLEX-8600 conectada. Esto se realiza para cambiar de radio, modificar el modo de conexión o finalizar la sesión de forma limpia.

## Antes de comenzar

- AetherSDR debe estar actualmente conectado a una radio. Si no hay ninguna radio conectada, el panel de conexión (ConnectionPanel) ya se muestra y no es necesaria ninguna acción.

## Pasos

1. Abra `Settings > Connect to Radio...`.
2. Haga clic en `Disconnect`.

AetherSDR finaliza la conexión y vuelve al panel de conexión (ConnectionPanel), donde puede conectarse a otra radio o elegir un modo de conexión diferente.

## Consejos

- Después de desconectar, el ajuste `ConnectionMode` conserva el último modo seleccionado (Local, Remote with SmartLink o Connect by IP), por lo que el panel se reabre en la misma página que usó anteriormente.
- Si desea reconectarse inmediatamente a la misma radio, la lista de `Available radios` en la página Local aún la mostrará tan pronto como el descubrimiento la encuentre de nuevo. Haga clic en la entrada y luego en `Connect Selected Radio`.

## Conexión automática al inicio

La casilla de verificación **Connect to last radio on start up** controla si AetherSDR se reconecta automáticamente al iniciar la aplicación.

| Configuración | Clave | Valor predeterminado |
|---|---|---|
| Connect to last radio on start up | `AutoConnectToLastRadio` | Habilitado |

- Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y cuando el descubrimiento por difusión (broadcast-discovery) o la sonda de radio enrutada (routed-radio probe) la encuentran. No se requiere acción manual.
- Cuando no está marcada, el panel de conexión (ConnectionPanel) se abre en cada inicio y debe seleccionar una radio manualmente cada sesión.

Para cambiar esta configuración, abra el panel de conexión y marque o desmarque **Connect to last radio on start up**. La preferencia se guarda de inmediato.

## Direcciones IP recientes (Modo Manual / VPN)

Cuando se conecta usando la página Manual, AetherSDR ahora guarda hasta tres direcciones IP utilizadas recientemente. El campo **Radio IP address** es un menú desplegable editable. Haga clic en la flecha para seleccionar una dirección anterior o escriba una nueva directamente. Las direcciones se validan y normalizan al guardarse; las entradas duplicadas o mal formadas se descartan automáticamente.

Si utilizó anteriormente el ajuste heredado **LastRoutedRadioIp**, AetherSDR importa esa dirección a la lista de direcciones recientes la primera vez que se inicia después de la actualización. El valor se almacena en `RecentConnectByIpAddresses`.

## Conexión manual: ruta de origen y opciones de ancho de banda reducido

En la página de conexión Manual, dentro de **Advanced**: panel contraíble titulado **Advanced**, puede configurar:

- **Source path** (`ManualBindSource`): Selecciona la interfaz de red local utilizada para la conexión manual. El menú desplegable enumera todas las NIC disponibles. Si la NIC seleccionada se vuelve obsoleta o inaccesible, aparece una advertencia debajo del campo.
- **Use low bandwidth mode** (`LowBandwidthMode`): Cuando está marcado, AetherSDR utiliza flujos de velocidad reducida para enlaces lentos o de alta latencia. Útil para conexiones VPN o por satélite.
- **Enable adaptive frame-rate throttle** (`AdaptiveThrottleEnabled`, valor predeterminado `False`): Cuando está marcado, AetherSDR reduce automáticamente las velocidades de fotogramas FFT y waterfall cuando la calidad de la red se degrada. Esto ayuda a mantener una interfaz de usuario con buena capacidad de respuesta en enlaces lentos o congestionados.

## Formulario de inicio de sesión accesible

El formulario de inicio de sesión de SmartLink ahora es accesible para los administradores de contraseñas del sistema operativo. macOS Passwords, Windows Authenticator y KDE Wallet leen el árbol de accesibilidad para asociar los campos de credenciales.

- El campo **Email** tiene el nombre accesible "SmartLink account email" y la descripción accesible "FlexRadio account email address used to sign in to SmartLink".
- El campo **Password** tiene el nombre accesible "SmartLink account password" y la descripción accesible "FlexRadio account password used to sign in to SmartLink".
- El contenedor del formulario se denomina "smartlinkLoginForm" para que los administradores de contraseñas puedan delimitar el par de credenciales.

Los botones de modo de conexión (Local, Remote with SmartLink, Connect by IP) también tienen nombres accesibles.

## Modo sin marco

El panel de conexión ahora admite el modo sin marco. Cuando está habilitado (controlado por el ajuste `FramelessWindow`, valor predeterminado `True`), el diálogo no tiene la barra de título de ventana nativa. En su lugar, se muestra una barra de título personalizada en la parte superior del diálogo. La barra de título incluye el título del diálogo y se puede usar para arrastrar o cerrar la ventana, según el sistema operativo.

- Si `FramelessWindow` está configurado en `True`, se muestra la barra de título personalizada.
- Si está configurado en `False`, se utilizan las decoraciones de ventana estándar del sistema operativo.
- El cambio surte efecto la próxima vez que se abra el panel de conexión.

La geometría del diálogo solo se restaura cuando el panel estaba visible previamente, lo que evita una colocación extraña al cambiar el modo sin marco mientras está oculto.

## Estilo adaptable al tema

El panel de conexión ahora utiliza variables de tema para los colores en lugar de valores fijos. Esto garantiza que el panel se integre con el tema de aplicación seleccionado. Los siguientes elementos respetan los colores del tema:

- El fondo del panel utiliza `{{color.background.0}}`
- Los bordes de los cuadros de grupo utilizan `{{color.background.2}}`
- Las etiquetas de texto utilizan `{{color.text.primary}}`

Los cambios de tema se aplican cuando se abre o actualiza el panel.

## Mejoras en la lista de radios locales

La lista de radios locales ahora tiene dimensiones limitadas para que se desplace internamente cuando se descubren más radios de las que caben. Esto evita que la lista crezca más allá del diálogo en pantallas pequeñas (por ejemplo, un panel de tableta de 1024x600 píxeles). La lista tiene:

- Altura mínima: 120 píxeles
- Altura máxima: 240 píxeles
- Política de barra de desplazamiento vertical: se muestra según sea necesario
- Modo de desplazamiento vertical: desplazamiento píxel a píxel

## Menú contextual de apodo de radio

Puede hacer clic derecho en una radio descubierta en la lista de radios locales para establecer un apodo personalizado sin necesidad de conectarse primero. Esto es útil para radios que no son Flex (por ejemplo, HL2, backends de simulador) que no tienen un almacén de nombres en la radio. El apodo se conserva claveado por número de serie y se recoge en el siguiente barrido de descubrimiento.

Para establecer un apodo:

1. Haga clic derecho en una radio en la lista de **Available radios**.
2. Seleccione la opción para establecer un apodo en el menú contextual.
3. Introduzca el apodo deseado en el diálogo que aparece.
4. Haga clic en **OK** para guardar.

El apodo se muestra en la lista de radios en los barridos de descubrimiento posteriores. Las radios FlexRadio no admiten apodos del lado del cliente; sus nombres se establecen desde Radio Setup mientras están conectadas.

## Relacionados

- [Conectarse a una radio LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse a una radio remota a través de SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Reintentar el descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Descripción general de Conectarse a una radio](../../features/connection/overview.md)
