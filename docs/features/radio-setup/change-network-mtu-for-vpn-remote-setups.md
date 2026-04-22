# Cambiar el MTU de red para configuraciones VPN/remotas

Ajuste el valor de MTU que la radio utiliza para los paquetes salientes. Reducir el MTU evita la fragmentación de paquetes al conectarse a través de una VPN o enlace WAN donde el MTU de ruta es menor que el predeterminado.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña **Network** solo es accesible con una conexión de radio activa.
- Conozca el MTU de su túnel VPN o ruta de red remota. Un valor de inicio habitual para túneles OpenVPN o WireGuard es 1400 bytes; consulte la documentación de su proveedor VPN o router si no está seguro.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el control giratorio **Network MTU:**.
4. Establezca el valor para que coincida con el MTU de su ruta de red.
5. Haga clic en **Apply** para enviar el nuevo MTU a la radio.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Network MTU:** | Establece el MTU de paquetes salientes en bytes en la radio. | — | — | — |
| **Apply** | Envía la configuración de red actual, incluido el valor de MTU, a la radio. | — | — | — |

## Consejos

- Si también experimenta cortes de audio o audio entrecortado a través del mismo enlace VPN, considere aumentar **Audio Buffer:** (50–1000 ms) en la pestaña **Audio** para absorber el jitter introducido por el túnel.

## Solución de problemas

- **El audio o el flujo de datos se interrumpe tras cambiar el MTU** — El nuevo valor puede ser demasiado bajo o demasiado alto para la ruta. Verifique el MTU de cada salto entre la radio y su cliente, luego establezca **Network MTU:** al MTU más bajo encontrado en esa ruta. Haga clic en **Apply** nuevamente después de cada ajuste.
- **Apply no tiene efecto visible** — Confirme que la radio sigue conectada. La pestaña **Network** requiere una conexión de radio activa. Si la conexión se interrumpió, vuelva a conectarse e inténtelo de nuevo.

## Relacionados

- [Cambiar la radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre audio Opus o sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
