# Recuperar una memoria del ATU

La recuperación de memoria del ATU permite que la radio aplique una configuración del sintonizador previamente almacenada en el momento en que cambia a una frecuencia que coincide con una memoria guardada, evitando una resintonización completa en bandas donde el ATU ya encontró una buena concordancia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los TX Controls no están disponibles sin una conexión de radio.
- El ATU de la radio debe tener al menos una memoria almacenada. Ejecute una sintonización completa del ATU primero si no existen memorias.
- El botón TX del panel lateral derecho debe estar activo para que el applet TX Controls sea visible.

## Pasos

1. Haga clic en el botón TX del panel lateral derecho para abrir el applet TX Controls (si aún no está visible).
2. Haga clic en MEM en la fila de botones TUNE / MOX / ATU / MEM.
   - MEM es un botón de alternancia. Cuando la recuperación de memoria está activada, el estado del botón cambia a seleccionado.
   - El indicador Mem en la fila de perfil se ilumina en verde cuando el ATU está usando activamente una memoria almacenada en la frecuencia actual.
3. Para desactivar la recuperación de memoria, haga clic en MEM nuevamente.

## Qué hace cada control

| Control | Tipo | Comportamiento | Notas |
|---------|------|----------------|-------|
| MEM | Botón de alternancia | Activa o desactiva la recuperación de memoria del ATU. Cuando está activo, la radio aplica una configuración de ATU almacenada para la frecuencia actual en lugar de resintonizar. | Deshabilitado cuando el TGXL está en modo OPERATE. |
| Mem | Indicador | Se ilumina en verde cuando el ATU está usando activamente una memoria. Tenue cuando no hay ninguna memoria en uso. | Refleja el estado del ATU informado por la radio. |
| Success | Indicador | Se ilumina en verde cuando el estado del ATU es Successful u OK. | |
| Byp | Indicador | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass. | |

## Solución de problemas

- **MEM aparece en gris y no se puede hacer clic** — El TGXL está en modo OPERATE. MEM está deshabilitado en este estado. Saque el TGXL del modo OPERATE antes de habilitar la recuperación de memoria.
- **El indicador Mem permanece tenue después de habilitar MEM** — No existe ninguna memoria de ATU almacenada para la frecuencia actual. Use el ATU para ejecutar un ciclo de sintonización completo en esta frecuencia primero; esto almacenará una nueva memoria.

## Relacionados

- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Iniciar una portadora de sintonización para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Descripción general de TX Controls](overview.md)
