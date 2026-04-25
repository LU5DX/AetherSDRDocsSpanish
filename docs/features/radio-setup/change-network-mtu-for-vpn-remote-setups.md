# Cambiar el MTU de red para configuraciones VPN/remotas

Reducir el MTU de red evita la fragmentación IP cuando el tráfico de radio pasa por un túnel VPN o un enlace WAN con un MTU de ruta menor que el predeterminado de Ethernet. Configure este valor en la radio para que los paquetes salientes quepan dentro del túnel sin ser descartados ni reensamblados.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network no es accesible mientras está desconectado.
- Conozca el MTU de su túnel VPN o enlace remoto. Un punto de partida común para OpenVPN es 1400 bytes; los túneles WireGuard suelen usar 1420 bytes.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el cuadro de número **Network MTU:**.
4. Establezca el valor en bytes para que coincida con el MTU de su túnel.
5. Haga clic en **Apply** para enviar el nuevo MTU a la radio.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Network MTU:** | MTU de salida en bytes enviado por la radio. Redúzcalo cuando los paquetes se fragmenten o se descarten en una ruta VPN o WAN. | — | — | — |
| **Apply** | Envía la configuración de red actual, incluido el valor de MTU, a la radio. | — | — | — |

## Consejos

- Si el audio se interrumpe o los datos del panadapter se pierden de forma intermitente a través de una VPN, aumente también el valor de **Audio Buffer:** (ubicado en la pestaña **Audio**) para compensar el jitter adicional. Ese ajuste acepta valores entre 50 y 1000 ms.
- Los campos **IP Address / Mask / MAC Address** en la misma pestaña son de solo lectura y confirman qué interfaz está usando la radio.

## Solución de problemas

- **Apply no tiene efecto visible** — Verifique que la radio siga conectada. Si la conexión se interrumpió, cierre y vuelva a abrir `Settings > Radio Setup...`, reconecte y aplique de nuevo.
- **El audio sigue cortándose después de reducir el MTU** — El MTU controla los paquetes de radio salientes. Verifique también que el MTU de la interfaz de red del sistema operativo host esté configurado al mismo valor o menor, y considere aumentar **Audio Buffer:** en la pestaña **Audio**.

## Relacionados

- [Cambiar la radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
