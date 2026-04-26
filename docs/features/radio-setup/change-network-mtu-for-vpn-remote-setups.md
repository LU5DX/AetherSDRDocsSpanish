# Cambiar el MTU de red para configuraciones VPN/remotas

El ajuste de MTU de red controla el tamaño máximo de paquete que la radio envía a través de la red. Reducirlo evita la fragmentación de paquetes en túneles VPN y otros enlaces con MTU de ruta reducido, lo que de otro modo puede causar interrupciones de audio o inestabilidad de conexión durante la operación remota.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña `Network` no es accesible mientras está desconectado.
- Conozca el MTU de su túnel VPN o enlace remoto. Un punto de partida habitual para OpenVPN es 1400 bytes; los túneles WireGuard suelen usar 1420 bytes.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña `Network`.
3. Localice el spinbox `Network MTU:`.
4. Establezca el valor igual o inferior al MTU de su VPN o enlace remoto.
5. Haga clic en `Apply` para enviar la nueva configuración de red a la radio.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|---|
| `Network MTU:` | Spinbox | Establece el MTU de paquetes salientes en bytes en la radio. | — | — | — |
| `Apply` | Botón | Envía la configuración actual de la pestaña `Network` a la radio. | — | — | — |

No hay ninguna clave de `AppSettings` persistida asociada con `Network MTU:`. El valor se almacena en la radio, no en la configuración local de AetherSDR.

## Consejos

- Si también experimenta variación de audio (jitter) a través de una VPN, considere aumentar `Audio Buffer:` (50–1000 ms) en la pestaña `Audio` después de ajustar el MTU. Un búfer más grande compensa la latencia y el jitter adicionales comunes en enlaces remotos.
- El interruptor `Enforce Private IP Connections:` en la misma pestaña rechaza conexiones desde direcciones que no sean RFC1918. Desactívelo solo si su VPN asigna direcciones de rango público a los extremos del túnel.

## Solución de problemas

- **Interrupciones de audio o desconexiones frecuentes tras cambiar el MTU** — El valor puede seguir siendo demasiado grande para la ruta. Reduzca `Network MTU:` entre 20 y 40 bytes y haga clic en `Apply` de nuevo. Repita hasta que el enlace sea estable.
- **`Apply` no tiene efecto visible** — Confirme que la radio sigue conectada. La pestaña `Network` requiere una conexión activa con la radio; si la radio se desconectó entre el momento en que abrió el diálogo y cuando hizo clic en `Apply`, vuelva a conectar e inténtelo de nuevo.

## Relacionado

- [Cambiar la radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre audio Opus o sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
