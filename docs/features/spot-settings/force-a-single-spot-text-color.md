# Forzar un color de texto único para todos los spots

De forma predeterminada, AetherSDR colorea cada spot de DX según su fuente o modo. Esta página explica cómo anular ese comportamiento y mostrar el texto de todos los spots en un color de su elección.

## Antes de comenzar

- Los spots deben estar habilitados. Si el botón "Spots:" muestra "Disabled", consulte [Activar o desactivar los spots](turn-spots-on-or-off.md) primero.
- Abra el diálogo Spot Settings haciendo clic derecho sobre la superposición de spots en el panadapter.

## Pasos

1. En el diálogo Spot Settings, localice la fila "Override Colors:".
2. Haga clic en el botón de alternancia hasta que muestre "Enabled". Esto activa `IsSpotsOverrideColorsEnabled` y fuerza el texto de todos los spots a un único color.
3. Haga clic en el pequeño botón de muestra de color ubicado inmediatamente a la derecha del botón "Enabled". Se abre un diálogo selector de color.
4. Seleccione el color que desea y confirme. La muestra se actualiza para reflejar su elección, y el texto de todos los spots en el panadapter cambia de inmediato.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Botón "Override Colors:" | Habilita o deshabilita la anulación de color único para el texto de todos los spots. | Disabled | `IsSpotsOverrideColorsEnabled` |
| Selector de color del texto de spots | Abre el diálogo selector de color para elegir el color de texto de anulación. | `#FFFF00` | `SpotsOverrideColor` |

## Consejos

- El color elegido se guarda de inmediato. No existe un botón Save separado.
- Si desea alto contraste, elija un color que contraste con el fondo de su panadapter. El amarillo (`#FFFF00`) es el valor predeterminado porque se lee con claridad sobre fondos oscuros.
- La anulación se aplica a todos los spots independientemente de su fuente (clúster de DX, RBN, WSJTX, etc.).

## Solución de problemas

- **El botón muestra "Enabled" pero los colores de los spots no han cambiado** — Confirme que "Spots:" esté configurado en "Enabled" en el mismo diálogo. Si los spots están deshabilitados, la anulación no tiene efecto visible.
- **El selector de color se cierra sin cambiar la muestra** — Cerró el diálogo sin confirmar un color. Haga clic en el botón de muestra nuevamente y seleccione un color antes de cerrar.

## Relacionado

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Aumentar o reducir el tamaño de la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
