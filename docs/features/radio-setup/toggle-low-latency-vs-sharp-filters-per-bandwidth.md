# Alternar filtros de baja latencia vs. filtros nítidos por ancho de banda

La pestaña **Filters** permite elegir entre las familias de filtros de baja latencia y filtros nítidos para cada ancho de banda, y opcionalmente forzar los filtros de baja latencia al operar en modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña **Filters** no está disponible cuando no hay ninguna radio conectada.
- Abra Radio Setup mediante `Settings > Radio Setup...`.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.
3. Haga clic en **Low Latency / Sharp Filters** para alternar entre las dos familias de filtros para el ancho de banda actual. El estado del botón refleja cuál familia está activa.
4. Para forzar los filtros de baja latencia siempre que opere en DIGU o DIGL, active la casilla **Use Low Latency Filters for Digital Modes**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Low Latency / Sharp Filters** | Botón de alternancia | Cambia la familia de filtros entre baja latencia y nítidos para cada ajuste de ancho de banda. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Cuando está activada, los filtros de baja latencia se aplican automáticamente en DIGU y DIGL, independientemente del botón de alternancia global. |

## Consejos

- Los filtros de baja latencia reducen el retardo de procesamiento a costa de una menor selectividad en las faldas. Los filtros nítidos mejoran el rechazo de señales adyacentes, pero añaden latencia. Para concursos en CW o trabajo con señales débiles, los filtros nítidos son generalmente preferibles. Para la decodificación de modos digitales donde el tiempo importa, los filtros de baja latencia pueden reducir los errores de decodificación.
- La casilla **Use Low Latency Filters for Digital Modes** actúa de forma independiente del botón de alternancia por ancho de banda, de modo que es posible usar filtros nítidos en SSB y CW mientras los modos digitales cambian automáticamente a baja latencia.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
