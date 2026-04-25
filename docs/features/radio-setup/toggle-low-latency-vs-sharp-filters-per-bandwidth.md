# Alternar filtros de baja latencia o filtros selectivos por ancho de banda

Use esta página para elegir si AetherSDR aplica filtros de baja latencia o filtros selectivos (alta selectividad) para cada ancho de banda del receptor, y para forzar filtros de baja latencia específicamente en modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña **Filters** no es accesible sin una conexión de radio activa.
- Abra el cuadro de diálogo Radio Setup mediante `Settings > Radio Setup...`.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.
3. Haga clic en **Low Latency / Sharp Filters** para alternar entre las dos familias de filtros para el ancho de banda actual. El botón refleja la selección activa.
4. Para forzar filtros de baja latencia siempre que un modo digital (DIGU o DIGL) esté activo, marque **Use Low Latency Filters for Digital Modes**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Low Latency / Sharp Filters** | Botón de alternancia | Cambia la preferencia de familia de filtros entre baja latencia y selectivos (alta selectividad) para el ancho de banda activo. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Cuando está marcada, los filtros de baja latencia se aplican automáticamente cuando el modo es DIGU o DIGL, independientemente del alternador global indicado arriba. |

## Consejos

- Los filtros de baja latencia reducen el retardo de procesamiento, lo cual beneficia a los modos digitales y la decodificación en tiempo real. Los filtros selectivos ofrecen flancos más pronunciados para una mejor supresión de señales adyacentes en fonia y CW.
- La casilla **Use Low Latency Filters for Digital Modes** permite mantener filtros selectivos para SSB y CW, al tiempo que se obtiene latencia reducida en DIGU/DIGL sin necesidad de cambiar manualmente.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
