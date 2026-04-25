# Forzar un único color de texto para los spots

De forma predeterminada, AetherSDR colorea cada spot de DX según su fuente o modo. Esta página explica cómo anular ese comportamiento y mostrar todo el texto de los spots en un color de su elección.

## Antes de comenzar

- El diálogo Spot Settings debe estar abierto. Haga clic derecho sobre la capa de spots en el panadapter para abrirlo.
- Los spots deben estar activos. Si el botón `IsSpotsEnabled` muestra "Disabled", actívelo primero (consulte [Activar o desactivar los spots](turn-spots-on-or-off.md)).

## Pasos

1. Abra el diálogo Spot Settings haciendo clic derecho sobre la capa de spots en el panadapter.
2. Localice la fila **Override Colors:**.
3. Haga clic en el botón de alternancia hasta que muestre **Enabled**. Esto activa la anulación de color único y guarda `IsSpotsOverrideColorsEnabled`.
4. Haga clic en el pequeño botón de muestra de color (swatch) que se encuentra inmediatamente a la derecha del botón **Enabled**. Se abre un diálogo selector de color titulado "Spot Text Color".
5. Seleccione el color deseado y confírmelo. La muestra se actualiza para reflejar su elección, y el color se guarda en `SpotsOverrideColor`.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|
| Botón de alternancia **Override Colors:** | Disabled | Cuando está en Enabled, todo el texto de los spots se muestra en un único color en lugar de los colores por fuente. | `IsSpotsOverrideColorsEnabled` |
| Selector de color del texto de spots (botón swatch) | `#FFFF00` | Abre el diálogo selector de color. El color seleccionado se aplica a todo el texto de los spots cuando Override Colors está en Enabled. | `SpotsOverrideColor` |

## Sugerencias

- La muestra de color refleja el color guardado actualmente incluso cuando **Override Colors:** está en Disabled. Puede preseleccionar un color antes de activar la anulación.
- El color de texto predeterminado es `#FFFF00` (amarillo). Si desea volver al valor predeterminado, abra el selector de color e ingrese ese valor manualmente.

## Solución de problemas

- **Los spots siguen mostrando múltiples colores después de activar Override Colors** — Confirme que el botón de alternancia muestre **Enabled** (no **Disabled**). Si muestra Disabled, haga clic una vez para activarlo.
- **El selector de color se cierra pero la muestra no cambia** — Es probable que haya cerrado el diálogo sin confirmar un color. Abra el selector nuevamente, seleccione un color y haga clic en OK.

## Relacionados

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Seleccionar un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
