# Activar el modo de bajo ancho de banda para enlaces lentos

El modo de bajo ancho de banda reduce la tasa de datos de los flujos de audio y del panadapter (panorámica de espectro) provenientes del radio. Úselo al conectarse a través de un enlace lento o congestionado — como una conexión celular, una VPN de baja velocidad o internet satelital — donde los flujos a tasa completa provocarían interrupciones de audio o inestabilidad en la conexión.

## Antes de comenzar

- El panel "Connect to a Radio" debe estar visible. Si AetherSDR ya está conectado a un radio, desconéctese primero.
- El modo de bajo ancho de banda se aplica en el momento de la conexión. Debe activarlo antes de hacer clic en un botón de conexión.

## Pasos

1. Abra el panel de conexión. Si no está visible, haga clic en `Settings > Connect to Radio...`.
2. Seleccione el modo de conexión que desea usar: haga clic en `On This Network`, `Remote with SmartLink` o `Connect by IP`. La casilla `Use low bandwidth mode` está disponible en los tres modos.
3. Marque `Use low bandwidth mode`.
4. Continúe con la conexión normalmente — haga clic en `Connect Selected Radio`, `Connect Remote Radio` o `Connect by IP` según el modo elegido.

## Qué hace cada control

| Control | Tipo | Comportamiento | Ajuste persistente |
|---|---|---|---|
| `Use low bandwidth mode` | Casilla de verificación | Habilita flujos de audio y de panadapter a tasa reducida para la conexión. | `LowBandwidthMode` |

## Sugerencias

- El ajuste es persistente. Una vez marcado, `Use low bandwidth mode` permanece habilitado en sesiones futuras hasta que lo desmarque.
- Si se encuentra en una LAN local rápida, deje esta opción sin marcar. Los flujos a tasa reducida disminuyen la calidad de audio y la velocidad de actualización del panadapter de forma innecesaria.

## Solución de problemas

- **Las interrupciones de audio persisten incluso con el modo de bajo ancho de banda activado** — Es posible que el enlace sea demasiado lento o con demasiada pérdida de paquetes incluso para los flujos a tasa reducida. Verifique su VPN o la ruta de red con `Settings > Network...`.

## Relacionados

- [Conectarse a un radio en una LAN local](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Conectarse a un radio remoto a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Seleccionar la interfaz de red local para una conexión manual](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
