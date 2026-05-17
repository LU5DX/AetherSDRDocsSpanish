# Desconectar de la Radio Actual

Esta página explica cómo desconectar AetherSDR de un FLEX-8600 conectado. Deberá hacer esto para cambiar de radio, cambiar los modos de conexión o cerrar su sesión de forma limpia.

## Antes de comenzar

- AetherSDR debe estar actualmente conectado a una radio. Si no hay ninguna radio conectada, el ConnectionPanel ya se muestra y no es necesario realizar ninguna acción.

## Pasos

1. Abra `Settings > Connect to Radio...`.
2. Haga clic en `Disconnect`.

AetherSDR cierra la conexión y regresa al ConnectionPanel, donde puede conectarse a una radio diferente o elegir un modo de conexión distinto.

## Consejos

- Después de desconectar, la configuración `ConnectionMode` conserva el último modo seleccionado (Local, Remote con SmartLink o Connect by IP), por lo que el panel se reabre en la misma página que utilizó anteriormente.
- Si tiene la intención de reconectarse inmediatamente a la misma radio, la lista `Available radios` en la página Local aún la mostrará tan pronto como la descubrimiento la encuentre nuevamente. Haga clic en la entrada y luego haga clic en `Connect Selected Radio`.

## Conexión automática al inicio

La casilla de verificación **Connect to last radio on start up** controla si AetherSDR se reconecta automáticamente cuando se inicia la aplicación.

| Configuración | Clave | Valor predeterminado |
|---|---|---|
| Connect to last radio on start up | `AutoConnectToLastRadio` | Habilitado |

- Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y cuando el descubrimiento por difusión o una sonda de radio enrutada la encuentra. No se requiere ninguna acción manual.
- Cuando no está marcada, el ConnectionPanel se abre en cada inicio y debe seleccionar una radio manualmente en cada sesión.

Para cambiar esta configuración, abra el ConnectionPanel y marque o desmarque **Connect to last radio on start up**. La preferencia se guarda inmediatamente.

## Direcciones IP recientes (Modo Manual / VPN)

Cuando se conecta usando la página Manual, AetherSDR ahora guarda hasta tres direcciones IP de uso reciente. El campo **Radio IP address** es un menú desplegable editable. Haga clic en la flecha para seleccionar una dirección anterior, o escriba una nueva directamente. Las direcciones se validan y normalizan al guardarse; los duplicados y las entradas mal formadas se descartan automáticamente.

Si utilizó anteriormente la configuración heredada **LastRoutedRadioIp**, AetherSDR importa esa dirección a la lista de direcciones recientes la primera vez que se inicia después de la actualización. El valor se almacena en `RecentConnectByIpAddresses`.

## Conexión manual: Ruta de origen y opciones de ancho de banda bajo

En la página de conexión Manual, bajo **Advanced**: panel contraíble titulado **Advanced**, puede configurar:

- **Source path** (`ManualBindSource`): Selecciona la interfaz de red local utilizada para la conexión manual. El menú desplegable lista todas las NIC disponibles. Si la NIC seleccionada se vuelve obsoleta o inaccesible, aparece una advertencia debajo del campo.
- **Use low bandwidth mode** (`LowBandwidthMode`): Cuando está marcada, AetherSDR utiliza flujos de tasa reducida para enlaces lentos o de alta latencia. Útil para conexiones VPN o por satélite.

## Modo sin marco

El Connection Panel ahora es compatible con el modo sin marco. Cuando está habilitado (controlado por la configuración `FramelessWindow`, valor predeterminado `True`), el diálogo no tiene una barra de título de ventana nativa. En su lugar, se muestra una barra de título personalizada en la parte superior del diálogo. La barra de título incluye el título del diálogo y se puede usar para arrastrar o cerrar la ventana, según el sistema operativo.

- Si `FramelessWindow` está configurado en `True`, se muestra la barra de título personalizada.
- Si está configurado en `False`, se utilizan las decoraciones de ventana estándar del SO.
- El cambio surte efecto la próxima vez que se abra el Connection Panel.

La geometría del diálogo solo se restaura cuando el panel estaba visible anteriormente, lo que evita una ubicación extraña al cambiar el modo sin marco mientras está oculto.

## Relacionado

- [Conectarse a una radio LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse a una radio remota a través de SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Reintentar descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Descripción general de Conexión a una Radio](../../features/connection/overview.md)
