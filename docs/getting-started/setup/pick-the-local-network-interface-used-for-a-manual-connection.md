# Seleccionar la interfaz de red local para una conexión manual

Al conectarse por IP a través de una VPN o una red enrutada, AetherSDR permite elegir qué interfaz de red local (NIC) utiliza su computadora para llegar al radio. Esto es importante cuando la máquina tiene múltiples interfaces de red y la ruta predeterminada no conduce al radio.

## Antes de comenzar

- Debe conocer la dirección IP del radio. Consulte [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md).
- El ConnectionPanel debe estar visible. Aparece automáticamente antes de conectar un radio, o ábralo desde `Settings > Connect to Radio...`.

## Pasos

1. En el ConnectionPanel, haga clic en `Connect by IP` para cambiar a la página del modo Manual.
2. Ingrese la dirección IP del radio en el campo `Radio IP address`. Este valor se guarda como `ManualRadioIp`.
3. Localice el cuadro combinado `Advanced: Source path` debajo del campo de dirección IP.
4. Abra el cuadro combinado y seleccione la interfaz de red local que desea usar para esta conexión. La interfaz seleccionada se guarda como `ManualBindSource`.
5. Si la interfaz guardada anteriormente ya no está disponible, aparece una etiqueta `Source warning label` debajo del cuadro combinado, indicando que la fuente guardada es obsoleta o inaccesible. Seleccione una interfaz disponible actualmente antes de continuar.
6. Haga clic en `Connect by IP` para iniciar la conexión.

## Qué hace cada control

| Control | Función | Clave persistida |
|---|---|---|
| `Radio IP address` | La dirección IP o nombre de host del radio al que conectarse. | `ManualRadioIp` |
| `Advanced: Source path` | Selecciona la NIC local a la que AetherSDR se enlaza al abrir la conexión. Déjelo en la entrada automática predeterminada a menos que necesite forzar una interfaz específica. | `ManualBindSource` |
| `Use low bandwidth mode` | Reduce las tasas de datos del flujo para enlaces lentos o congestionados. | `LowBandwidthMode` |
| `Connect by IP` (botón) | Inicia la conexión manual usando la IP y la ruta de origen configuradas anteriormente. | — |

## Consejos

- Si la interfaz guardada anteriormente no está disponible, la etiqueta `Source warning label` muestra el nombre (o ID) de la interfaz guardada y la última dirección IPv4 conocida. Elija una interfaz diferente desde `Advanced: Source path` antes de conectarse.
- En una máquina con una sola interfaz de red, la selección de `Advanced: Source path` no tiene efecto práctico. Es más útil en máquinas con interfaces separadas de cable, inalámbrica y VPN.
- Si se encuentra en un enlace lento, como una conexión celular o satelital, active `Use low bandwidth mode` en la misma página antes de hacer clic en `Connect by IP`.
- En la versión v0.9.2.1, la lista de radios remotos SmartLink tiene una altura máxima fija. Si tiene muchos radios remotos, desplácese dentro de la lista para llegar a las entradas que no son inmediatamente visibles.

## Solución de problemas

- **Aparece `Source warning label` después de seleccionar una interfaz** — La interfaz guardada en `ManualBindSource` ya no está presente o no tiene una dirección activa. Abra `Advanced: Source path` y seleccione una interfaz disponible actualmente.
- **La conexión falla inmediatamente después de hacer clic en `Connect by IP`** — La etiqueta `Manual result label` debajo del botón muestra el error. Verifique que la IP en `Radio IP address` sea accesible desde la interfaz seleccionada en `Advanced: Source path`. Use `Network Diagnostics` en la misma página para comprobar la accesibilidad.

## Relacionados

- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Activar el modo de bajo ancho de banda para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Conectarse a un radio en red LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse a un radio remoto a través de SmartLink](connect-to-a-remote-radio-through-smartlink.md)
