# Activar el modo de bajo ancho de banda para enlaces lentos

El modo de bajo ancho de banda reduce la tasa de los flujos de audio y datos enviados desde la radio. Úselo cuando se conecte a través de un enlace lento o congestionado — como un punto de acceso celular, una VPN de larga distancia o una conexión por satélite — para reducir interrupciones y mejorar la estabilidad.

## Antes de comenzar

- AetherSDR debe estar abierto y aún no conectado a una radio, o debe desconectarse primero antes de cambiar este ajuste.
- Identifique el modo de conexión que está utilizando: Local, SmartLink o Manual. La casilla `LowBandwidthMode` está disponible en el panel de conexión independientemente del modo.

## Pasos

1. Abra el panel de conexión. Aparece automáticamente antes de conectar una radio. Si ya hay una radio conectada, haga clic en `Settings > Connect to Radio...` y desconéctese primero.
2. Localice la casilla **Use low bandwidth mode** cerca de la parte inferior del panel de conexión.
3. Marque **Use low bandwidth mode** para activar los flujos de tasa reducida.
4. Proceda a conectarse usando su modo preferido — **Local**, **SmartLink** o **Manual** — de forma normal.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Clave persistente | Comportamiento |
|---|---|---|---|---|
| Use low bandwidth mode | Casilla | (no definido) | `LowBandwidthMode` | Cuando está marcada, AetherSDR solicita flujos de audio y datos de tasa reducida a la radio, adecuados para enlaces lentos o congestionados. |

## Consejos

- Active este ajuste antes de iniciar la conexión. El modo se negocia en el momento de conectarse.
- Si el audio sigue cortándose después de activar el modo de bajo ancho de banda, verifique su ruta VPN o de enrutamiento en `Settings > Network...`.

## Relacionados

- [Conectarse por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Conectarse a una radio remota mediante SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Seleccionar la interfaz de red local para una conexión manual](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Operación remota mediante SmartLink](../../operating/remote/remote-operation-smartlink.md)
