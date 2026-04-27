# Elegir un color de fondo personalizado para los spots

Establezca un color de fondo específico que aparezca detrás de las etiquetas de spots en el panadapter. Utilice esta opción cuando el contraste de color automático no sea adecuado para su pantalla o condiciones de operación.

## Antes de comenzar

- Abra el diálogo Spot Settings haciendo clic derecho sobre la capa de spots en un panadapter.
- Confirme que "Override Background: Enabled" esté activo (el botón muestra "Enabled"). El selector de color de fondo no tiene efecto cuando el fondo está desactivado.
- Desactive "Override Background: Auto" si desea que su color elegido surta efecto. Cuando "Auto" está activo, AetherSDR selecciona el color de fondo automáticamente e ignora el selector de color manual.

## Pasos

1. Haga clic derecho sobre la capa de spots en el panadapter y abra Spot Settings.
2. Localice la fila **Override Background:**.
3. Si el botón "Enabled" muestra "Disabled", haga clic en él para que muestre "Enabled". Este valor se guarda en `IsSpotsOverrideBackgroundColorsEnabled`.
4. Si el botón "Auto" muestra "Enabled", haga clic en él para que muestre "Disabled". Este valor se guarda en `IsSpotsOverrideToAutoBackgroundColorEnabled`. Mientras "Auto" esté activo, el selector de color manual queda anulado.
5. Haga clic en el pequeño botón de muestra de color a la derecha de "Auto". Esto abre el diálogo de color del sistema titulado "Spot Background Color".
6. Seleccione el color deseado y confirme la selección.
7. La muestra se actualiza de inmediato y el fondo del panadapter detrás de las etiquetas de spots cambia al color elegido. El valor se guarda en `SpotsOverrideBgColor`.

## Función de cada control

| Etiqueta | Tipo | Valor predeterminado | Clave de persistencia | Comportamiento |
|---|---|---|---|---|
| Override Background: Enabled | Botón de alternancia | Enabled | `IsSpotsOverrideBackgroundColorsEnabled` | Dibuja un fondo con color detrás del texto de los spots. Debe estar activo para que cualquier configuración de color de fondo tenga efecto. |
| Override Background: Auto | Botón de alternancia | Enabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Cuando está activo, AetherSDR elige el color de fondo automáticamente para optimizar el contraste. Desactívelo para usar el selector de color manual. |
| Selector de color de fondo de spots | Botón de acción (muestra) | `#000000` | `SpotsOverrideBgColor` | Abre el diálogo "Spot Background Color". El color elegido se aplica únicamente cuando "Enabled" está activo y "Auto" está desactivado. |
| Background Opacity: | Control deslizante | 48 | `SpotsOverrideBgOpacity` | Controla la transparencia del fondo de los spots. Rango: 0–100. |

## Consejos

- Establecer la opacidad en 0 hace que el fondo sea completamente transparente, independientemente del color elegido. Si el fondo desaparece después de seleccionar un color, verifique el control deslizante "Background Opacity:".
- "Override Background: Auto" está activado ("Enabled") de forma predeterminada, por lo que un diálogo recién abierto ignorará cualquier color manual hasta que desactive "Auto".

## Resolución de problemas

- **El selector de color no tiene efecto visible en el panadapter** — Confirme que "Override Background: Enabled" muestre "Enabled" y que "Override Background: Auto" muestre "Disabled". Ambas condiciones deben cumplirse para que se muestre un color de fondo manual.
- **El fondo es invisible a pesar de los estados correctos de los botones** — Verifique el control deslizante "Background Opacity:". Si está en 0, el fondo es completamente transparente. Consulte [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md).

## Temas relacionados

- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Descripción general de Spot Settings](overview.md)
