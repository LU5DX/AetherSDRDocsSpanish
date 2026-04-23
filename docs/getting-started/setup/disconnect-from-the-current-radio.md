# Desconectarse de la radio actual

Esta página explica cómo desconectar AetherSDR de una radio Flex. Puede hacer esto para conectarse a una radio diferente, cambiar el modo de conexión o cerrar su sesión de forma ordenada.

## Antes de comenzar

- AetherSDR debe estar ya conectado a una radio. Si no está conectado, el ConnectionPanel ya se muestra y no es necesario realizar ninguna acción.

## Pasos

1. Abra `Settings > Connect to Radio...`.
2. Haga clic en `Disconnect`.

AetherSDR cierra la conexión con la radio y regresa al ConnectionPanel, donde puede elegir una nueva radio o modo de conexión.

## Consejos

- Después de desconectarse, su último `ConnectionMode` es recordado. El ConnectionPanel se vuelve a abrir en el modo que utilizó anteriormente: `Local`, `Remote with SmartLink` o `Connect by IP`.
- Si tiene intención de reconectarse a la misma radio local, espere a que vuelva a aparecer en la lista `Available radios` antes de hacer clic en `Connect Selected Radio`. El descubrimiento de radios se reinicia automáticamente tras la desconexión.

## Relacionados

- [Descripción general de Conectar a una radio](../../features/connection/overview.md)
- [Conectarse a una radio en red LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse a una radio remota a través de SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Reintentar el descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
