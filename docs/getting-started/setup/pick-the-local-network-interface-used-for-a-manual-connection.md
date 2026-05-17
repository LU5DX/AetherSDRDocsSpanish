# Seleccionar la interfaz de red local para una conexión manual

Al conectarse por IP a través de una VPN o una red enrutada, AetherSDR le permite elegir qué interfaz de red local (NIC) utiliza su computadora para llegar a la radio. Esto es importante cuando su equipo tiene múltiples interfaces de red y la ruta predeterminada no conduce a la radio.

## Antes de comenzar

- Debe conocer la dirección IP de la radio. Consulte [Conectarse por IP a través de una VPN o una red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md).
- El ConnectionPanel debe estar visible. Aparece automáticamente antes de conectar una radio, o puede abrirlo mediante `Settings > Connect to Radio...`.

## Pasos

1. En el ConnectionPanel, haga clic en `Connect by IP` para cambiar a la página de modo manual.
2. Ingrese la dirección IP de la radio en el campo `Radio IP address`. Este valor se guarda como `ManualRadioIp`. Si se ha conectado a esta radio anteriormente, puede abrir la lista desplegable `Radio IP address` y seleccionarla de la lista de direcciones recientes en lugar de escribirla nuevamente.
3. Localice el cuadro combinado `Advanced: Source path` debajo del campo de dirección IP.
4. Abra el cuadro combinado y seleccione la interfaz de red local que desea usar para esta conexión. La interfaz seleccionada se guarda como `ManualBindSource`.
5. Si la interfaz guardada anteriormente ya no está disponible, aparecerá una `Source warning label` debajo del cuadro combinado indicando que la fuente guardada está obsoleta o es inalcanzable. Seleccione una interfaz actualmente disponible antes de continuar.
6. Haga clic en `Connect by IP` para iniciar la conexión.

## Función de cada control

| Control | Función | Clave persistida |
|---|---|---|
| `Radio IP address` | Dirección IP o nombre de host de la radio a conectar. Se muestra como un cuadro combinado editable; la lista desplegable muestra hasta tres direcciones usadas recientemente. | `ManualRadioIp` |
| `Advanced: Source path` | Selecciona la NIC local a la que AetherSDR se vincula al abrir la conexión. Déjelo en la entrada automática predeterminada a menos que necesite forzar una interfaz específica. | `ManualBindSource` |
| `Use low bandwidth mode` | Reduce las tasas de datos del flujo para enlaces lentos o congestionados. | `LowBandwidthMode` |
| `Connect to last radio on start up` | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y durante la detección por difusión / sonda de radio enrutada. Cuando está desmarcado, se abre el diálogo de conexión y el usuario debe seleccionar una radio manualmente cada sesión. Marcado por defecto. | `AutoConnectToLastRadio` |
| `Connect by IP` (botón) | Inicia la conexión manual usando la IP y la ruta de origen configuradas arriba. | — |
| `Network Diagnostics` (botón) | Abre el diálogo de Diagnóstico de Red para ayudar a solucionar problemas de conectividad. | — |

## Consejos

- Si la interfaz guardada anteriormente no está disponible, la `Source warning label` muestra el nombre (o ID) de la interfaz guardada y la última dirección IPv4 conocida. Elija una interfaz diferente de `Advanced: Source path` antes de conectar.
- En un equipo con una sola interfaz de red, la selección de `Advanced: Source path` no tiene efecto práctico. Es más útil en equipos con interfaces cableadas, inalámbricas y VPN separadas.
- Si está en un enlace lento como una conexión celular o satelital, habilite `Use low bandwidth mode` en la misma página antes de hacer clic en `Connect by IP`.
- El campo `Radio IP address` conserva las tres direcciones usadas más recientemente. Seleccione una dirección anterior de la lista desplegable para evitar volver a escribirla.
- Si desmarca `Connect to last radio on start up`, AetherSDR abre el diálogo de conexión en cada inicio y espera a que seleccione una radio manualmente.
- En la versión 0.9.2.1, la lista de radios remotas SmartLink tiene una altura máxima fija. Si tiene muchas radios remotas, desplácese dentro de la lista para alcanzar las entradas que no son visibles de inmediato.
- El ConnectionPanel conserva su geometría de ventana al alternar el modo sin marco.

## Solución de problemas

- **`Source warning label` aparece después de seleccionar una interfaz** — La interfaz guardada en `ManualBindSource` ya no está presente o no tiene una dirección activa. Abra `Advanced: Source path` y seleccione una interfaz actualmente disponible.
- **La conexión falla inmediatamente después de hacer clic en `Connect by IP`** — La `Manual result label` debajo del botón muestra el error. Verifique que la IP en `Radio IP address` sea accesible desde la interfaz seleccionada en `Advanced: Source path`. Use `Network Diagnostics` en la misma página para verificar la accesibilidad.

## Relacionado

- [Conectarse por IP a través de una VPN o una red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Habilitar el modo de bajo ancho de banda para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Conectarse a una radio LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse a una radio remota a través de SmartLink](connect-to-a-remote-radio-through-smartlink.md)
