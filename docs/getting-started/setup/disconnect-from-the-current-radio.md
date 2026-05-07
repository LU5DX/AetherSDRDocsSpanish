# Desconectar de la Radio Actual

Esta página explica cómo desconectar AetherSDR de un FLEX-8600 al que está conectado. Puede hacer esto para cambiar de radio, modificar los modos de conexión o cerrar su sesión de forma limpia.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio en ese momento. Si no hay ninguna radio conectada, el ConnectionPanel ya estará visible y no es necesario realizar ninguna acción.

## Pasos

1. Abra `Settings > Connect to Radio...`.
2. Haga clic en `Disconnect`.

AetherSDR interrumpe la conexión y vuelve al ConnectionPanel, donde puede conectarse a una radio diferente o elegir un modo de conexión distinto.

## Consejos

- Tras desconectar, el ajuste `ConnectionMode` conserva el modo seleccionado por última vez (Local, Remote with SmartLink o Connect by IP), de modo que el panel se reabre en la misma página que usó anteriormente.
- Si desea reconectarse inmediatamente a la misma radio, la lista `Available radios` de la página Local seguirá mostrándola en cuanto la detección la encuentre de nuevo. Haga clic en la entrada y luego en `Connect Selected Radio`.

## Conexión automática al inicio

La casilla **Connect to last radio on start up** controla si AetherSDR se reconecta automáticamente cuando se inicia la aplicación.

| Ajuste | Clave | Valor predeterminado |
|---|---|---|
| Connect to last radio on start up | `AutoConnectToLastRadio` | Activado |

- Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al iniciarse y cuando la detección por difusión o la sonda de radio enrutada la encuentra. No se requiere ninguna acción manual.
- Cuando está desmarcada, el ConnectionPanel se abre en cada inicio y debe seleccionar una radio manualmente en cada sesión.

Para cambiar este ajuste, abra el ConnectionPanel y marque o desmarque **Connect to last radio on start up**. La preferencia se guarda de inmediato.

## Direcciones IP recientes (modo Manual/VPN)

Cuando se conecta usando la página Manual, AetherSDR ahora guarda hasta tres direcciones IP utilizadas recientemente. El campo **Radio IP address** es un menú desplegable editable. Haga clic en la flecha para elegir una dirección anterior o escriba una nueva directamente. Las direcciones se validan y normalizan al guardarse; los duplicados y las entradas mal formadas se descartan automáticamente.

Si usó anteriormente el ajuste heredado **LastRoutedRadioIp**, AetherSDR importa esa dirección a la lista de direcciones recientes la primera vez que se inicia tras la actualización. El valor se almacena en `RecentConnectByIpAddresses`.

## Relacionado

- [Connect to a local LAN radio](connect-to-a-local-lan-radio.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Retry discovery when no radios appear](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Connect to a Radio overview](../../features/connection/overview.md)
