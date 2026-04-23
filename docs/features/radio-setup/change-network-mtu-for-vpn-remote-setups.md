# Cambiar el MTU de red para configuraciones VPN/remotas

Ajuste el MTU de red saliente que el radio Flex utiliza al enviar datos a los clientes. Reducir el MTU evita la fragmentación en VPNs y otros enlaces con un tamaño máximo de paquete menor que una conexión Ethernet estándar.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña **Network** solo está disponible mientras haya una conexión activa.
- Conozca el MTU de su VPN o enlace remoto antes de modificar este valor. Su administrador de red o la documentación de la VPN deben indicarlo.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el control giratorio **Network MTU:**.
4. Establezca el valor igual o inferior al MTU de su VPN o enlace remoto.
5. Haga clic en **Apply** para enviar la nueva configuración de red al radio.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|---|
| **Network MTU:** | Control giratorio | Establece el MTU saliente en bytes que el radio utiliza al enviar paquetes. | — | — | — |
| **Apply** | Botón | Envía la configuración de red actual, incluido el valor de MTU, al radio. | — | — | — |

Este valor no se guarda en ninguna clave de configuración de AetherSDR; se almacena directamente en el radio.

## Consejos

- Si también experimenta cortes de audio a través de una VPN, aumente el valor de **Audio Buffer:** (50–1000 ms) en la pestaña **Audio**. Un búfer más grande absorbe el jitter adicional que los paquetes fragmentados o desordenados pueden causar en enlaces de alta latencia.
- El interruptor **Enforce Private IP Connections:** en la misma pestaña restringe el radio a pares RFC 1918. Si su VPN asigna una IP pública a la interfaz del cliente, deshabilite ese interruptor antes de conectarse de forma remota.

## Solución de problemas

- **El audio se interrumpe o la conexión se cae poco después de cambiar el MTU** — el valor puede seguir siendo demasiado grande para la ruta. Reduzca el MTU en pasos pequeños (por ejemplo, de 50 bytes a la vez) y haga clic en **Apply** después de cada cambio hasta que la conexión se estabilice.
- **Apply no tiene efecto visible** — confirme que el radio sigue conectado. Si la conexión se interrumpió, vuelva a conectarse mediante `Settings > Connect to Radio...`, reabra `Settings > Radio Setup...`, navegue hasta la pestaña **Network**, vuelva a introducir el valor de MTU y haga clic en **Apply** nuevamente.

## Relacionados

- [Cambiar el radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre audio Opus o sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
