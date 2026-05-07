# Habilitar el modo de bajo ancho de banda para enlaces lentos

El modo de bajo ancho de banda reduce la velocidad de las transmisiones de audio y datos enviadas desde la radio. Úselo al conectarse a través de un enlace lento o congestionado — como un punto de acceso celular, una VPN de larga distancia o una conexión satelital — para reducir las interrupciones y mejorar la estabilidad.

## Antes de comenzar

- AetherSDR debe estar abierto y aún no conectado a una radio, o debe desconectarse primero antes de cambiar esta configuración.
- Sepa qué modo de conexión está utilizando: Local, SmartLink o Manual. La casilla de verificación `LowBandwidthMode` está presente en el panel de conexión independientemente del modo.

## Pasos

1. Abra el panel de conexión. Aparece automáticamente antes de que se conecte una radio. Si ya hay una radio conectada, haga clic en `Settings > Connect to Radio...` y desconéctese primero.
2. Localice la casilla de verificación **Use low bandwidth mode** cerca de la parte inferior del panel de conexión.
3. Marque **Use low bandwidth mode** para habilitar transmisiones de velocidad reducida.
4. Proceda a conectarse usando su modo preferido — **Local**, **SmartLink** o **Manual** — como de costumbre.

## Qué hace cada control

| Control | Tipo | Valor predeterminado |
|---|---|---|
| Use low bandwidth mode | Casilla de verificación | (no establecido) |
| Connect to last radio on start up | Casilla de verificación. Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y durante la detección por difusión / sonda de radio enrutada. Cuando no está marcada, se abre el cuadro de diálogo de conexión y el usuario debe elegir una radio manualmente cada sesión. Se almacena como `AutoConnectToLastRadio`. | Verdadero (marcado). Nuevo en v0.9.7. Los usuarios existentes conservan el comportamiento anterior automáticamente. |
| Radio IP address | Cuadro combinado editable. Almacena hasta tres direcciones IP utilizadas recientemente. Seleccione una dirección anterior del menú desplegable o escriba una nueva. El campo reemplaza la entrada de texto simple utilizada en versiones anteriores. Se almacena como `ManualRadioIp`; las entradas recientes se almacenan como `RecentConnectByIpAddresses`. | (no establecido) |

## Consejos

- Active **Use low bandwidth mode** antes de iniciar la conexión. El modo se negocia en el momento de la conexión.
- Si el audio aún se corta después de habilitar el modo de bajo ancho de banda, verifique su VPN o ruta de enrutamiento usando `Settings > Network...`.
- El campo **Radio IP address** ahora recuerda hasta tres direcciones recientes. Si guardó previamente una IP bajo la configuración heredada `LastRoutedRadioIp`, AetherSDR la migra automáticamente la primera vez que abre el panel de conexión.
- Para evitar que AetherSDR se conecte automáticamente al iniciar — por ejemplo, cuando desee elegir una radio diferente — desmarque **Connect to last radio on start up**.

## Relacionado

- [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Pick the local network interface used for a manual connection](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Operating remotely over SmartLink](../../operating/remote/remote-operation-smartlink.md)
