# Desconectarse de la radio actual

Esta página explica cómo desconectar AetherSDR de una FLEX-8600 conectada. Esto se hace para cambiar de radio, modificar los modos de conexión o cerrar la sesión de forma ordenada.

## Antes de empezar

- AetherSDR debe estar actualmente conectado a una radio. Si no hay ninguna radio conectada, el ConnectionPanel ya se muestra y no se requiere ninguna acción.

## Pasos

1. Abra `Settings > Connect to Radio...`.
2. Haga clic en `Disconnect`.

AetherSDR finaliza la conexión y vuelve al ConnectionPanel, donde puede conectarse a otra radio o elegir un modo de conexión diferente.

## Consejos

- Después de desconectarse, el ajuste `ConnectionMode` conserva el último modo seleccionado (Local, Remote with SmartLink o Connect by IP), por lo que el panel se reabre en la misma página que utilizó anteriormente.
- Si tiene intención de reconectarse a la misma radio de inmediato, la lista `Available radios` de la página Local seguirá mostrándola en cuanto la detección la encuentre de nuevo. Haga clic en la entrada y luego en `Connect Selected Radio`.

## Conexión automática al inicio

La casilla **Connect to last radio on start up** controla si AetherSDR se reconecta automáticamente al iniciar la aplicación.

| Configuración | Clave | Valor predeterminado |
|---|---|---|
| Connect to last radio on start up | `AutoConnectToLastRadio` | Habilitado |

- Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al inicio y cuando la detección por difusión o una sonda de radio enrutada la encuentra. No se requiere ninguna acción manual.
- Cuando no está marcada, el ConnectionPanel se abre en cada inicio y debe seleccionar una radio manualmente en cada sesión.

Para cambiar este ajuste, abra el ConnectionPanel y marque o desmarque **Connect to last radio on start up**. La preferencia se guarda inmediatamente.

## Direcciones IP recientes (modo Manual / VPN)

Cuando se conecta mediante la página Manual, AetherSDR ahora guarda hasta tres direcciones utilizadas recientemente. El campo **Radio IP address** es un menú desplegable editable que acepta tanto direcciones IP numéricas como nombres de host, por ejemplo `ic-705.local`. Haga clic en la flecha para elegir una dirección anterior, o escriba una nueva directamente. Las direcciones numéricas se canonicalizan (de modo que `192.168.001.5` y `192.168.1.5` cuentan como una sola entrada); los nombres de host se validan con un conjunto de caracteres conservador (letras, dígitos, punto, guion, guion bajo, alfanumérico en ambos extremos, hasta 253 caracteres). Los duplicados y las entradas mal formadas se descartan automáticamente.

Si anteriormente usó el ajuste heredado **LastRoutedRadioIp**, AetherSDR importa esa dirección a la lista de direcciones recientes la primera vez que se inicia tras la actualización. El valor se almacena en `RecentConnectByIpAddresses`.

## Conexión manual: ruta de origen y opciones de ancho de banda reducido

En la página de conexión Manual, bajo **Advanced**: panel plegable titulado **Advanced**, puede configurar:

- **Source path** (`ManualBindSource`): Selecciona la interfaz de red local utilizada para la conexión manual. El menú desplegable enumera todas las NIC disponibles. Si la NIC seleccionada deja de ser válida o queda inaccesible, aparece una advertencia debajo del campo.
- **Use low bandwidth mode** (`LowBandwidthMode`): Cuando está marcada, AetherSDR utiliza flujos de velocidad reducida para enlaces lentos o de alta latencia. Útil para conexiones VPN o por satélite.
- **Enable adaptive frame-rate throttle** (`AdaptiveThrottleEnabled`, valor predeterminado `False`): Cuando está marcada, AetherSDR reduce automáticamente las velocidades de fotogramas de FFT y del waterfall cuando la calidad de la red se degrada. Esto ayuda a mantener una interfaz receptiva en enlaces lentos o congestionados.

## Selección de familia de radio en modo Manual

La página Manual ahora recuerda qué familia de radio (Flex o Icom) se utilizó para cada conexión manual. El menú desplegable **Advanced: Source path** va acompañado de un selector de familia de radio que se conserva por dirección guardada:

- Los perfiles antiguos anteriores al selector se tratan como Flex, preservando el comportamiento de las instalaciones existentes.
- Cuando se reconecta a una dirección manual utilizada previamente, la familia de radio correcta se selecciona automáticamente.

## Formulario de inicio de sesión accesible

El formulario de inicio de sesión de SmartLink ahora es accesible para los gestores de contraseñas del sistema operativo. macOS Passwords, Windows Authenticator y KDE Wallet leen el árbol de accesibilidad para asociar los campos de credenciales.

- El campo **Email** tiene el nombre accesible "SmartLink account email" y la descripción accesible "FlexRadio account email address used to sign in to SmartLink".
- El campo **Password** tiene el nombre accesible "SmartLink account password" y la descripción accesible "FlexRadio account password used to sign in to SmartLink".
- El contenedor del formulario se denomina "smartlinkLoginForm" para que los gestores de contraseñas puedan delimitar el par de credenciales.

Los botones de modo de conexión (Local, Remote with SmartLink, Connect by IP) también tienen nombres accesibles.

## Modo sin marco

El ConnectionPanel ahora admite el modo sin marco. Cuando está habilitado (controlado por el ajuste `FramelessWindow`, valor predeterminado `True`), el diálogo no tiene barra de título nativa de la ventana. En su lugar, se muestra una barra de título personalizada en la parte superior del diálogo. La barra de título incluye el título del diálogo y puede utilizarse para arrastrar o cerrar la ventana, según el sistema operativo.

- Si `FramelessWindow` está establecido en `True`, se muestra la barra de título personalizada.
- Si está establecido en `False`, se utilizan los adornos estándar de ventana del sistema operativo.
- El cambio surte efecto la próxima vez que se abra el ConnectionPanel.

La geometría del diálogo solo se restaura cuando el panel estaba visible anteriormente, lo que evita una colocación incorrecta al cambiar el modo sin marco mientras está oculto.

## Estilo sensible al tema

El ConnectionPanel ahora utiliza variables de tema para los colores en lugar de valores fijos. Esto garantiza que el panel se integre con el tema de la aplicación seleccionado. Los siguientes elementos respetan los colores del tema:

- El fondo del panel utiliza `{{color.background.0}}`
- Los bordes de los cuadros de grupo utilizan `{{color.background.2}}`
- Las etiquetas de texto utilizan `{{color.text.primary}}`

Los cambios de tema surten efecto cuando se abre o se actualiza el panel.

## Mejoras en la lista de radios locales

La lista de radios locales ahora tiene dimensiones limitadas para que se desplace internamente cuando se descubren más radios de las que caben. Esto evita que la lista crezca más allá del diálogo en pantallas pequeñas (por ejemplo, un panel de tableta de 1024x600). La lista tiene:

- Altura mínima: 120 píxeles
- Altura máxima: 240 píxeles
- Política de barra de desplazamiento vertical: se muestra según sea necesario
- Modo de desplazamiento vertical: desplazamiento por píxel

## Menú contextual del apodo de la radio

Puede hacer clic con el botón derecho en una radio descubierta en la lista de radios locales para establecer un apodo personalizado sin conectarse primero. Esto es útil para radios que no son Flex (por ejemplo, HL2, backends de simulador) que no tienen un almacén de nombres en la propia radio. El apodo se conserva asociado al número de serie y se recoge en el siguiente barrido de detección.

Para establecer un apodo:

1. Haga clic con el botón derecho en una radio de la lista **Available radios**.
2. Seleccione la opción para establecer un apodo en el menú contextual.
3. Escriba el apodo deseado en el diálogo que aparece.
4. Haga clic en **OK** para guardar.

El apodo se muestra en la lista de radios en los barridos de detección posteriores. Las radios FlexRadio no admiten apodos en el lado del cliente: sus nombres se establecen desde Radio Setup mientras se está conectado.

## Relacionados

- [Connect to a local LAN radio](connect-to-a-local-lan-radio.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Retry discovery when no radios appear](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Connect to a Radio overview](../../features/connection/overview.md)
