# Forzar un único color de texto para todos los spots

De forma predeterminada, AetherSDR muestra cada spot DX en un color determinado por su fuente o modo. Activar la anulación de color obliga a que todas las etiquetas de spot se muestren en un único color elegido por usted, lo que facilita la lectura del panadapter de un vistazo.

## Antes de comenzar

- Los spots deben estar habilitados. Si el indicador `IsSpotsEnabled` muestra "Disabled", habilítelo primero — consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).
- Abra el diálogo Spot Settings haciendo clic derecho sobre la capa de spots en el panadapter y seleccionando la opción de configuración de spots en el menú contextual.

## Pasos

1. En el diálogo Spot Settings, localice la fila **Override Colors:**.
2. Haga clic en el botón de alternancia hasta que muestre "Enabled". El ajuste `IsSpotsOverrideColorsEnabled` se guarda de inmediato.
3. Haga clic en el pequeño botón de muestra de color situado a la derecha del alternador. Se abre un diálogo de selección de color titulado "Spot Text Color".
4. Seleccione el color deseado y confirme. La muestra se actualiza para reflejar su elección y el color se guarda en `SpotsOverrideColor`.

Para volver a los colores individuales por spot, haga clic de nuevo en el alternador **Override Colors:** hasta que muestre "Disabled".

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento | Clave de ajuste |
|---|---|---|---|
| Alternador **Override Colors:** | Disabled | Cuando está en "Enabled", reemplaza todos los colores de texto de los spots por el único color definido en el selector de color. Cuando está en "Disabled", cada spot usa el color asignado por su fuente. | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto de spot (botón de muestra) | `#FFFF00` (amarillo) | Abre el selector "Spot Text Color". El color elegido se aplica a todas las etiquetas de spot cuando **Override Colors:** está en "Enabled". | `SpotsOverrideColor` |

## Sugerencias

- El selector de color solo tiene efecto cuando **Override Colors:** está en "Enabled". Puede preseleccionar un color mientras el alternador está en "Disabled" y activarlo más adelante.
- El amarillo (`#FFFF00`) es el color de anulación predeterminado. Ofrece buen contraste sobre el fondo oscuro predeterminado del panadapter con la opacidad de fondo predeterminada de 48.

## Solución de problemas

- **Los spots siguen apareciendo en múltiples colores después de activar Override Colors:** — Confirme que el alternador muestra "Enabled" (estado verde) y no "Disabled". Al hacer clic en el alternador se cambia su estado y se guarda de inmediato; no se requiere ningún botón Apply.
- **El selector de color se cierra pero la muestra no se actualiza** — El selector fue descartado con Cancel o la ventana se cerró sin seleccionar un color. Haga clic de nuevo en el botón de muestra y confirme la selección de un color.

## Relacionado

- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Aumentar o reducir el tamaño de la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
