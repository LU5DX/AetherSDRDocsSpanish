# Cambiar el MTU de red para configuraciones VPN/remotas

La configuración de MTU de red controla el tamaño máximo de unidad de transmisión (en bytes) que utiliza la radio para los paquetes de red salientes. Reducirlo evita la fragmentación de paquetes cuando el tráfico de la radio pasa a través de un túnel VPN u otro enlace con un MTU de ruta reducido.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network no está disponible mientras no haya conexión.
- Conozca el MTU de su túnel VPN o enlace remoto. Un valor inicial común para túneles OpenVPN o WireGuard es 1400 bytes.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el campo numérico **Network MTU:**.
4. Establezca el valor igual o menor al MTU de su túnel.
5. Haga clic en **Apply** para enviar el nuevo MTU a la radio.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Network MTU:** | Establece el MTU saliente en bytes para el tráfico de red de la radio. | — | — | — |
| **Apply** | Envía la configuración actual de la pestaña Network, incluido el valor de MTU, a la radio. | — | — | — |

## Consejos

- Los cambios surten efecto en la radio inmediatamente después de hacer clic en **Apply**. No es necesario desconectarse y volver a conectarse.
- Si el audio se interrumpe o el panadapter se detiene intermitentemente a través de una VPN, considere también aumentar **Audio Buffer:** (50–1000 ms) en la pestaña **Audio** para absorber el jitter adicional.

## Solución de problemas

- **Apply no tiene efecto visible** — Confirme que AetherSDR sigue conectado a la radio. La pestaña Network requiere una conexión de radio activa. Desconéctese y vuelva a conectarse, luego inténtelo de nuevo.
- **El audio sigue cortándose después de reducir el MTU** — La pérdida de paquetes y el jitter de la VPN pueden requerir también un búfer de audio más grande. Consulte [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md).

## Relacionado

- [Cambiar la radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre audio Opus o sin compresión para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
