# Desconectarse de la Radio Actual

Esta página explica cómo desconectar AetherSDR de un FLEX-8600 conectado. Puede hacer esto para cambiar de radio, cambiar el modo de conexión o cerrar su sesión de forma ordenada.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio en este momento. Si no hay ninguna radio conectada, el ConnectionPanel ya está visible y no se requiere ninguna acción.

## Pasos

1. Abra `Settings > Connect to Radio...`.
2. Haga clic en `Disconnect`.

AetherSDR interrumpe la conexión y regresa al ConnectionPanel, donde puede conectarse a una radio diferente o elegir un modo de conexión distinto.

## Consejos

- Después de desconectarse, la configuración `ConnectionMode` conserva el último modo seleccionado (Local, Remote with SmartLink o Connect by IP), por lo que el panel se vuelve a abrir en la misma página que usó anteriormente.
- Si desea reconectarse a la misma radio de inmediato, la lista `Available radios` de la página Local seguirá mostrándola en cuanto el descubrimiento de red la detecte nuevamente. Haga clic en la entrada y luego haga clic en `Connect Selected Radio`.

## Relacionados

- [Conectarse a una radio en la red LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse a una radio remota a través de SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Reintentar el descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Descripción general de Connect to a Radio](../../features/connection/overview.md)
