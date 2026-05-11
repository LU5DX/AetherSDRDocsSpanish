# Desconectar de la Radio Actual

Esta página explica cómo desconectar AetherSDR de un FLEX-8600 conectado. Deberá hacerlo para cambiar de radio, cambiar los modos de conexión o cerrar su sesión de forma ordenada.

## Antes de comenzar

- AetherSDR debe estar actualmente conectado a una radio. Si no hay ninguna radio conectada, el ConnectionPanel ya se muestra y no es necesario realizar ninguna acción.

## Pasos

1. Abra `Settings > Connect to Radio...`.
2. Haga clic en `Disconnect`.

AetherSDR cierra la conexión y vuelve al ConnectionPanel, donde puede conectarse a una radio diferente o elegir un modo de conexión distinto.

## Consejos

- Después de desconectar, el ajuste `ConnectionMode` conserva el último modo seleccionado (Local, Remote with SmartLink o Connect by IP), por lo que el panel se reabre en la misma página que usó anteriormente.
- Si tiene la intención de reconectarse a la misma radio inmediatamente, la lista `Available radios` de la página Local aún la mostrará en cuanto la detección la encuentre nuevamente. Haga clic en la entrada y luego haga clic en `Connect Selected Radio`.

## Conexión automática al inicio

La casilla de verificación **Connect to last radio on start up** controla si AetherSDR se reconecta automáticamente cuando la aplicación se inicia.

| Ajuste | Clave | Valor predeterminado |
|---|---|---|
| Connect to last radio on start up | `AutoConnectToLastRadio` | Habilitado |

- Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y cuando la detección por difusión o una sonda de radio enrutada la encuentra. No se requiere ninguna acción manual.
- Cuando no está marcada, el ConnectionPanel se abre en cada inicio y debe seleccionar una radio manualmente cada sesión.

Para cambiar esta configuración, abra el ConnectionPanel y marque o desmarque **Connect to last radio on start up**. La preferencia se guarda de inmediato.

## Direcciones IP recientes (Modo Manual / VPN)

Cuando se conecta usando la página Manual, AetherSDR ahora guarda hasta tres direcciones IP usadas recientemente. El campo **Radio IP address** es un menú desplegable editable. Haga clic en la flecha para elegir una dirección anterior o escriba una nueva directamente. Las direcciones se validan y normalizan al guardarse; los duplicados y las entradas mal formadas se descartan automáticamente.

Si usó anteriormente el ajuste heredado **LastRoutedRadioIp**, AetherSDR importa esa dirección a la lista de direcciones recientes la primera vez que se inicia después de una actualización. El valor se almacena en `RecentConnectByIpAddresses`.

## Conexión manual: Ruta de origen y opciones de ancho de banda bajo

En la página de conexión Manual, bajo **Advanced**: panel contraíble titulado **Advanced**, puede configurar:

- **Source path** (`ManualBindSource`): Selecciona la interfaz de red local utilizada para la conexión manual. El menú desplegable lista todas las NIC disponibles. Si la NIC seleccionada se vuelve obsoleta o inaccesible, aparece una advertencia debajo del campo.
- **Use low bandwidth mode** (`LowBandwidthMode`): Cuando está marcado, AetherSDR utiliza flujos de velocidad reducida para enlaces lentos o de alta latencia. Útil para conexiones VPN o por satélite.

## Modo sin marco

El Connection Panel ahora admite el modo sin marco. Cuando está habilitado (controlado por el ajuste `FramelessWindow`, valor predeterminado `True`), el diálogo no tiene barra de título de ventana nativa. En su lugar, se muestra una barra de título personalizada en la parte superior del diálogo. La barra de título incluye el título del diálogo y se puede usar para arrastrar o cerrar la ventana, según el sistema operativo.

- Si `FramelessWindow` está configurado en `True`, se muestra la barra de título personalizada.
- Si está configurado en `False`, se utilizan las decoraciones de ventana estándar del sistema operativo.
- El cambio surte efecto la próxima vez que se abra el Connection Panel.

## Relacionado

- [Connect to a local LAN radio](connect-to-a-local-lan-radio.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Retry discovery when no radios appear](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Connect to a Radio overview](../../features/connection/overview.md)
