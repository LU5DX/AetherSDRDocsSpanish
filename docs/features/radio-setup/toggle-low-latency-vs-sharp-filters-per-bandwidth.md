# Alternar filtros de baja latencia vs. filtros pronunciados por ancho de banda

Use esta página para cambiar la familia de filtros DSP de la radio entre respuesta de baja latencia y respuesta pronunciada, y para forzar filtros de baja latencia en modos digitales. Los filtros de baja latencia reducen el retardo de procesamiento a costa de una caída más gradual; los filtros pronunciados maximizan el rechazo de señales adyacentes.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Filters no es accesible cuando está desconectado.
- Abra Radio Setup mediante `Settings > Radio Setup...`.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.
3. Haga clic en **Low Latency / Sharp Filters** para alternar entre las dos familias de filtros. El botón refleja la selección actual.
4. Si desea que los filtros de baja latencia se apliquen automáticamente cuando un slice esté en modo DIGU o DIGL, marque **Use Low Latency Filters for Digital Modes**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|---|
| **Low Latency / Sharp Filters** | Botón de alternancia | Cambia la familia de filtros aplicada a todos los slices de recepción: baja latencia (menor retardo) o pronunciado (faldas más empinadas). | — | — |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Cuando está marcada, anula la selección de familia de filtros y utiliza filtros de baja latencia siempre que un slice esté en modo digital (DIGU/DIGL). | — | — |

## Relacionado

- [Descripción general de Radio Setup](overview.md)
