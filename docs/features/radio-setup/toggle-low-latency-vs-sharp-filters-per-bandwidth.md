# Alternar entre filtros de baja latencia y filtros de corte nítido por ancho de banda

La pestaña **Filters** en Radio Setup permite elegir entre filtros DSP de baja latencia y de corte nítido para cada ancho de banda de recepción, y opcionalmente forzar los filtros de baja latencia al usar modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña **Filters** solo está disponible cuando hay una conexión de radio activa.
- Abra Radio Setup mediante `Settings > Radio Setup...`.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.
3. Haga clic en el botón de alternancia **Low Latency / Sharp Filters** para cambiar entre las dos familias de filtros para el ancho de banda actual. El botón refleja la selección activa.
4. Para forzar los filtros de baja latencia siempre que un modo digital (DIGU o DIGL) esté activo, marque **Use Low Latency Filters for Digital Modes**.
5. Cierre el cuadro de diálogo. La configuración surte efecto de inmediato.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Low Latency / Sharp Filters** | Botón de alternancia | Cambia la preferencia de familia de filtros entre baja latencia y corte nítido para el ancho de banda seleccionado. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Cuando está marcada, anula la elección de filtro por ancho de banda y utiliza filtros de baja latencia siempre que haya un slice DIGU o DIGL activo. |

## Consejos

- Los filtros de baja latencia reducen el retardo de procesamiento, lo cual beneficia la decodificación de modos digitales en tiempo real y el CW. Los filtros de corte nítido ofrecen mayor selectividad en las faldas, lo que resulta más útil en condiciones de banda congestionada para SSB.
- La casilla **Use Low Latency Filters for Digital Modes** se aplica a todos los anchos de banda, por lo que no es necesario cambiar la configuración por ancho de banda cada vez que cambie a un modo digital.

## Relacionados

- [Descripción general de Radio Setup](overview.md)
- [Seleccionar el modo iámbico A o B para el keyer del radio](select-iambic-mode-a-or-b-for-the-radio-keyer.md)
