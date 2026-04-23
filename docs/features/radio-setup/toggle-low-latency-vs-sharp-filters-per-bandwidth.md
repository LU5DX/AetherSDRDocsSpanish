# Alternar entre filtros de baja latencia y filtros nítidos por ancho de banda

Use esta página para cambiar entre las familias de filtros de baja latencia y filtros nítidos para cada ancho de banda de recepción, y para forzar los filtros de baja latencia al operar en modos digitales. Elegir la familia de filtros adecuada implica un compromiso entre el retardo de audio y la pendiente de la falda del filtro.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Filters no es accesible sin una conexión de radio activa.
- Abra Radio Setup haciendo clic en `Settings > Radio Setup...`.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.
3. Para cada ancho de banda que desee cambiar, haga clic en **Low Latency / Sharp Filters** para alternar entre las dos familias de filtros. El botón refleja el estado actual para ese ancho de banda.
4. Para forzar los filtros de baja latencia siempre que un modo digital (DIGU o DIGL) esté activo, marque **Use Low Latency Filters for Digital Modes**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Low Latency / Sharp Filters** | Botón de alternancia | Cambia la familia de filtros para el ancho de banda seleccionado entre baja latencia y nítido. Los filtros de baja latencia reducen el retardo de procesamiento; los filtros nítidos ofrecen faldas más pronunciadas con mayor retardo. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Cuando está marcada, los filtros de baja latencia se aplican automáticamente a los slices DIGU y DIGL, independientemente de la configuración por ancho de banda. |

## Consejos

- Use filtros nítidos para SSB o CW cuando el rechazo de canales adyacentes sea más importante que el retardo.
- Use filtros de baja latencia al operar modos digitales que dependen de decodificación sensible al tiempo, o habilite **Use Low Latency Filters for Digital Modes** para que esto se aplique de forma automática.

## Relacionados

- [Descripción general de Radio Setup](overview.md)
