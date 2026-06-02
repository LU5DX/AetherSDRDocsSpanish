# Desconectar de la Radio Actual

Esta página explica cómo desconectar AetherSDR de una FLEX-8600 conectada. Esto se hace para cambiar de radio, cambiar los modos de conexión o cerrar la sesión de forma limpia.

## Antes de comenzar

- AetherSDR debe estar conectado actualmente a una radio. Si no hay ninguna radio conectada, el panel ConnectionPanel ya se muestra y no se requiere ninguna acción.

## Pasos

1. Abra `Settings > Connect to Radio...`.
2. Haga clic en `Disconnect`.

AetherSDR finaliza la conexión y vuelve al panel ConnectionPanel, donde puede conectarse a una radio diferente o elegir un modo de conexión distinto.

## Consejos

- Después de desconectar, el ajuste `ConnectionMode` conserva el último modo seleccionado (Local, Remote with SmartLink o Connect by IP), por lo que el panel se reabre en la misma página que usó anteriormente.
- Si tiene la intención de reconectarse a la misma radio inmediatamente, la lista `Available radios` en la página Local aún la mostrará tan pronto como la descubra de nuevo. Haga clic en la entrada y luego haga clic en `Connect Selected Radio`.

## Conexión automática al inicio

La casilla de verificación **Connect to last radio on start up** controla si AetherSDR se reconecta automáticamente cuando se inicia la aplicación.

| Ajuste | Clave | Predeterminado |
|---|---|---|
| Connect to last radio on start up | `AutoConnectToLastRadio` | Habilitado |

- Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al inicio y cuando el descubrimiento por difusión o una sonda de radio enrutada la encuentra. No se requiere ninguna acción manual.
- Cuando está desmarcada, el panel ConnectionPanel se abre en cada inicio y debe seleccionar una radio manualmente en cada sesión.

Para cambiar este ajuste, abra el panel ConnectionPanel y marque o desmarque **Connect to last radio on start up**. La preferencia se guarda inmediatamente.

## Direcciones IP recientes (Modo Manual / VPN)

Cuando se conecta usando la página Manual, AetherSDR ahora guarda hasta tres direcciones IP utilizadas recientemente. El campo **Radio IP address** es un menú desplegable editable. Haga clic en la flecha para seleccionar una dirección anterior, o escriba una nueva directamente. Las direcciones se validan y normalizan al guardarse; los duplicados y las entradas mal formadas se descartan automáticamente.

Si usó anteriormente el ajuste heredado **LastRoutedRadioIp**, AetherSDR importa esa dirección a la lista de direcciones recientes la primera vez que se inicia después de la actualización. El valor se almacena en `RecentConnectByIpAddresses`.

## Conexión manual: Ruta de origen y opciones de ancho de banda bajo

En la página de conexión Manual, debajo de **Advanced**: panel contraíble titulado **Advanced**, puede configurar:

- **Source path** (`ManualBindSource`): Selecciona la interfaz de red local utilizada para la conexión manual. El menú desplegable lista todas las NIC disponibles. Si la NIC seleccionada se vuelve obsoleta o inaccesible, aparece una advertencia debajo del campo.
- **Use low bandwidth mode** (`LowBandwidthMode`): Cuando está marcada, AetherSDR utiliza flujos de velocidad reducida para enlaces lentos o de alta latencia. Útil para conexiones VPN o por satélite.
- **Enable adaptive frame-rate throttle** (`AdaptiveThrottleEnabled`, predeterminado `False`): Cuando está marcada, AetherSDR reduce automáticamente las tasas de fotogramas de FFT y waterfall cuando la calidad de la red se degrada. Esto ayuda a mantener una interfaz de usuario receptiva en enlaces lentos o congestionados.

## Formulario de inicio de sesión accesible

El formulario de inicio de sesión de SmartLink ahora es accesible para los administradores de contraseñas del sistema operativo. macOS Passwords, Windows Authenticator y KDE Wallet leen el árbol de accesibilidad para asociar los campos de credenciales.

- El campo **Email** tiene el nombre accesible "SmartLink account email" y la descripción accesible "FlexRadio account email address used to sign in to SmartLink".
- El campo **Password** tiene el nombre accesible "SmartLink account password" y la descripción accesible "FlexRadio account password used to sign in to SmartLink".
- El contenedor del formulario se denomina "smartlinkLoginForm" para que los administradores de contraseñas puedan delimitar el par de credenciales.

Los botones de modo de conexión (Local, Remote with SmartLink, Connect by IP) también tienen nombres accesibles.

## Modo sin marco

El panel Connection Panel ahora admite el modo sin marco. Cuando está habilitado (controlado por el ajuste `FramelessWindow`, predeterminado `True`), el diálogo no tiene una barra de título de ventana nativa. En su lugar, se muestra una barra de título personalizada en la parte superior del diálogo. La barra de título incluye el título del diálogo y se puede usar para arrastrar o cerrar la ventana, según el sistema operativo.

- Si `FramelessWindow` está establecido en `True`, se muestra la barra de título personalizada.
- Si está establecido en `False`, se utilizan las decoraciones de ventana estándar del sistema operativo.
- El cambio surte efecto la próxima vez que se abra el panel Connection Panel.

La geometría del diálogo solo se restaura cuando el panel estaba visible anteriormente, lo que evita una ubicación extraña al cambiar el modo sin marco mientras está oculto.

## Estilo sensible al tema

El panel Connection Panel ahora utiliza variables de tema para los colores en lugar de valores codificados. Esto garantiza que el panel se integre con el tema de la aplicación seleccionado. Los siguientes elementos respetan los colores del tema:

- El fondo del panel utiliza `{{color.background.0}}`
- Los bordes del cuadro de grupo utilizan `{{color.background.2}}`
- Las etiquetas de texto utilizan `{{color.text.primary}}`

Los cambios de tema surten efecto cuando se abre o actualiza el panel.

## Relacionado

- [Connect to a local LAN radio](connect-to-a-local-lan-radio.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Retry discovery when no radios appear](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Connect to a Radio overview](../../features/connection/overview.md)
