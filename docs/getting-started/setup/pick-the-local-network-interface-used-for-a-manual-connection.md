# Seleccione la interfaz de red local para una conexión manual

Al conectarse por IP a través de una VPN o una red enrutada, AetherSDR le permite elegir qué interfaz de red local (NIC) utiliza su computadora para llegar a la radio. Esto es importante cuando su máquina tiene múltiples interfaces de red y la ruta predeterminada no conduce a la radio.

## Antes de comenzar

- Debe conocer la dirección IP de la radio. Vea [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md).
- El ConnectionPanel debe estar visible. Aparece automáticamente antes de conectar una radio, o ábralo mediante `Settings > Connect to Radio...`.

## Pasos

1. En el ConnectionPanel, haga clic en `Connect by IP` para cambiar a la página de modo Manual.
2. Ingrese la dirección IP de la radio en el campo `Radio IP address`. Este valor se guarda como `ManualRadioIp`. Si se ha conectado a esta radio antes, puede abrir la lista desplegable `Radio IP address` y seleccionarla en lugar de volver a escribirla.
3. Localice el cuadro combinado `Advanced: Source path` debajo del campo de dirección IP.
4. Abra el cuadro combinado y seleccione la interfaz de red local que desea usar para esta conexión. La interfaz seleccionada se guarda como `ManualBindSource`.
5. Si la interfaz que guardó previamente ya no está disponible, aparece una `Source warning label` debajo del cuadro combinado indicando que la fuente guardada no es válida o es inalcanzable. Seleccione una interfaz actualmente disponible antes de continuar.
6. Haga clic en `Connect by IP` para iniciar la conexión.

## Qué hace cada control

| Control | Qué hace | Clave persistida |
|---|---|---|
| `Radio IP address` | La dirección IP o nombre de host de la radio a conectar. Se muestra como un cuadro combinado editable; la lista desplegable muestra hasta tres direcciones usadas recientemente. | `ManualRadioIp` |
| `Advanced: Source path` | Selecciona la NIC local que AetherSDR utiliza al abrir la conexión. Déjelo en la entrada automática predeterminada a menos que necesite forzar una interfaz específica. | `ManualBindSource` |
| `Use low bandwidth mode` | Reduce las tasas de datos del flujo para enlaces lentos o congestionados. | `LowBandwidthMode` |
| `Connect to last radio on start up` | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio usada al iniciar y durante la detección por difusión / sondeo de radio enrutada. Cuando no está marcado, se abre el diálogo de conexión y el usuario debe seleccionar una radio manualmente cada sesión. Marcado por defecto. | `AutoConnectToLastRadio` |
| `Connect by IP` (botón) | Inicia la conexión manual usando la IP y la ruta de origen configuradas arriba. | — |

## Consejos

- Si la interfaz guardada previamente no está disponible, la `Source warning label` muestra el nombre (o ID) de la interfaz guardada y la última dirección IPv4 conocida. Elija una interfaz diferente de `Advanced: Source path` antes de conectar.
- En una máquina con una sola interfaz de red, la selección en `Advanced: Source path` no tiene efecto práctico. Es más útil en máquinas con interfaces separadas: cableada, inalámbrica y VPN.
- Si está en un enlace lento como una conexión celular o satelital, active `Use low bandwidth mode` en la misma página antes de hacer clic en `Connect by IP`.
- El campo `Radio IP address` conserva las tres direcciones más recientemente usadas. Seleccione una dirección anterior de la lista desplegable para evitar volver a escribirla.
- Si desmarca `Connect to last radio on start up`, AetherSDR abre el diálogo de conexión en cada inicio y espera a que seleccione una radio manualmente.
- En v0.9.2.1 la lista de radios remotas SmartLink tiene una altura máxima fija. Si tiene muchas radios remotas, desplácese dentro de la lista para alcanzar las entradas que no son visibles de inmediato.

## Solución de problemas

- **`Source warning label` aparece después de seleccionar una interfaz** — La interfaz guardada en `ManualBindSource` ya no está presente o no tiene una dirección activa. Abra `Advanced: Source path` y seleccione una interfaz actualmente disponible.
- **La conexión falla inmediatamente después de hacer clic en `Connect by IP`** — La `Manual result label` debajo del botón muestra el error. Verifique que la IP en `Radio IP address` sea alcanzable desde la interfaz seleccionada en `Advanced: Source path`. Use `Network Diagnostics` en la misma página para verificar la accesibilidad.

## Relacionado

- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Enable low-bandwidth mode for slow links](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Connect to a local LAN radio](connect-to-a-local-lan-radio.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
