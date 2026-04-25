# Desconectarse de la radio actual

Esta página explica cómo desconectar AetherSDR de un FLEX-8600 conectado. Puede hacer esto para cambiar de radio, modificar el modo de conexión o cerrar la sesión de forma ordenada.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio en este momento. Si no hay ninguna radio conectada, el ConnectionPanel ya se muestra y no es necesario realizar ninguna acción.

## Pasos

1. Abra `Settings > Connect to Radio...`.
2. Haga clic en `Disconnect`.

AetherSDR cierra la conexión y regresa al ConnectionPanel, donde puede conectarse a una radio diferente o elegir un modo de conexión distinto.

## Consejos

- Después de desconectarse, el ajuste `ConnectionMode` conserva el último modo seleccionado (Local, Remote with SmartLink o Connect by IP), por lo que el panel se vuelve a abrir en la misma página que usó anteriormente.
- Si desea volver a conectarse a la misma radio de inmediato, la lista `Available radios` de la página Local la mostrará nuevamente en cuanto el descubrimiento la detecte. Haga clic en la entrada y luego en `Connect Selected Radio`.

## Relacionados

- [Conectarse a una radio en la LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse a una radio remota mediante SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Reintentar el descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Descripción general de Connect to a Radio](../../features/connection/overview.md)
