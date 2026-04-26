# Alternar entre filtros de baja latencia y filtros nítidos por ancho de banda

La pestaña **Filters** en Radio Setup permite elegir entre filtros DSP de baja latencia y filtros nítidos para cada ancho de banda de recepción, y opcionalmente forzar filtros de baja latencia en modos digitales. Use filtros de baja latencia cuando necesite un retardo de procesamiento mínimo; use filtros nítidos cuando necesite una mayor atenuación en la banda de rechazo.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña **Filters** no es accesible sin una conexión activa al radio.
- Abra Radio Setup mediante `Settings > Radio Setup...`.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.
3. Para cada entrada de ancho de banda, haga clic en el botón de alternancia **Low Latency / Sharp Filters** para cambiar entre las dos familias de filtros. El botón refleja la selección actual para ese ancho de banda.
4. Si opera en modos digitales (DIGU/DIGL) y desea que los filtros de baja latencia se apliquen automáticamente, marque la opción **Use Low Latency Filters for Digital Modes**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Low Latency / Sharp Filters** | Botón de alternancia | Cambia la preferencia de familia de filtros entre baja latencia y nítido para el ancho de banda asociado. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Cuando está marcada, fuerza los filtros de baja latencia siempre que el slice esté en modo DIGU o DIGL, independientemente de la configuración por ancho de banda. |

## Consejos

- Los filtros nítidos tienen flancos más pronunciados y mejor rechazo de señales adyacentes, lo que beneficia la operación SSB y CW en bandas congestionadas. Los filtros de baja latencia reducen el retardo de grupo, lo que beneficia a los decodificadores de modos digitales sensibles a la latencia de procesamiento.
- La casilla **Use Low Latency Filters for Digital Modes** actúa como anulación: incluso si un ancho de banda está configurado con filtros nítidos, los slices en modo digital usarán filtros de baja latencia cuando esta opción esté marcada.

## Relacionados

- [Descripción general de Radio Setup](overview.md)
- [Seleccionar dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
