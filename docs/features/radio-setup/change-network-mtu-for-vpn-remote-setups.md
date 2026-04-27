# Cambiar el MTU de red para configuraciones VPN/remotas

La configuración de MTU de red controla el tamaño máximo de paquete que el radio envía a través de la red. Reducirlo evita la fragmentación cuando se conecta a través de una VPN u otro túnel que disminuye el MTU de ruta disponible.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Network no es accesible cuando está desconectado.
- Conozca el MTU de su túnel VPN o ruta de red. Los MTU comunes de VPN son 1400–1450 bytes; una ruta Ethernet estándar es 1500 bytes.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el spinbox **Network MTU:**.
4. Establezca el valor para que coincida con el MTU de su ruta de red.
5. Haga clic en **Apply** para enviar el nuevo MTU al radio.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Network MTU:** | Tamaño del paquete saliente en bytes. Redúzcalo cuando opere a través de una VPN o cualquier enlace con un MTU reducido. | — | — | — |
| **Apply** | Envía la configuración actual de la pestaña Network, incluido el valor de MTU, al radio. | — | — | — |

## Consejos

- Si no está seguro de qué MTU usar, comience en 1400 bytes y auméntelo hasta observar pérdida de paquetes o interrupciones de audio; luego retroceda 10–20 bytes.
- La configuración **Audio Buffer:** (que se encuentra en la pestaña **Audio**) puede ayudar a absorber el jitter en enlaces VPN de forma independiente al ajuste de MTU. Consulte [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md).

## Solución de problemas

- **Apply no tiene efecto visible** — Confirme que el radio sigue conectado. Si la conexión se interrumpió, vuelva a conectarse mediante `Settings > Connect to Radio...` y repita los pasos.
- **El audio se interrumpe tras cambiar el MTU** — El nuevo valor puede ser todavía demasiado grande para la ruta. Reduzca **Network MTU:** otros 20–50 bytes y haga clic en **Apply** nuevamente.

## Relacionados

- [Cambiar el radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
