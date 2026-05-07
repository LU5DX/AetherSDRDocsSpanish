# Seleccionar un color de fondo personalizado para las marcas

Establezca un color de fondo específico que aparezca detrás de las etiquetas de las marcas en el panadapter. Utilice esta opción cuando el contraste de color automático no sea adecuado para su pantalla o condiciones de operación.

## Antes de comenzar

- Abra el cuadro de diálogo Spot Settings haciendo clic derecho en la superposición de marcas en un panadapter.
- Confirme que "Override Background: Enabled" esté activo (el botón muestra "Enabled"). El selector de color de fondo no tiene efecto cuando el fondo está deshabilitado.
- Desactive "Override Background: Auto" si desea que el color que elija surta efecto. Cuando "Auto" está activo, AetherSDR selecciona el color de fondo automáticamente e ignora el selector de color manual.

## Pasos

1. Haga clic derecho en la superposición de marcas en el panadapter y abra Spot Settings.
2. Localice la fila **Override Background:**.
3. Si el botón "Enabled" muestra "Disabled", haga clic en él para que muestre "Enabled". Este valor se persiste en `IsSpotsOverrideBackgroundColorsEnabled`.
4. Si el botón "Auto" muestra "Enabled", haga clic en él para que muestre "Disabled". Este valor se persiste en `IsSpotsOverrideToAutoBackgroundColorEnabled`. Mientras "Auto" esté activo, el selector de color manual quedará anulado.
5. Haga clic en el pequeño botón de muestra de color a la derecha de "Auto". Esto abre el cuadro de diálogo de color del sistema titulado "Spot Background Color".
6. Seleccione el color deseado y confirme la selección.
7. La muestra de color se actualiza de inmediato y el fondo del panadapter detrás de las etiquetas de las marcas cambia al color elegido. El valor se persiste en `SpotsOverrideBgColor`.

## Función de cada control

| Etiqueta | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| Override Background: Enabled | Botón de alternancia | Enabled | Se persiste en `IsSpotsOverrideBackgroundColorsEnabled`. |
| Override Background: Auto | Botón de alternancia | Enabled | Se persiste en `IsSpotsOverrideToAutoBackgroundColorEnabled`. Cuando está habilitado, el selector de color manual se ignora. |
| Selector de color de fondo de marcas | Botón pulsador (muestra de color) | `#000000` | Abre un cuadro de diálogo de color. Se persiste en `SpotsOverrideBgColor`. |
| Background Opacity: | Deslizador (0–100) | 48 | Transparencia del fondo de la marca. 0 = completamente transparente, 100 = completamente opaco. Se persiste en `SpotsBackgroundOpacity`. La clave de configuración cambió de `SpotsOverrideBgOpacity` en v0.9.7. |
| Spot Lines: | Botón de alternancia | Enabled | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de marca. Desactívelo durante concursos para reducir el desorden visual. Se persiste en `IsSpotsLinesEnabled`. Nuevo en v0.9.7. |

## Consejos

- Establecer la opacidad en 0 hace que el fondo sea completamente transparente, independientemente del color elegido. Si el fondo desaparece después de seleccionar un color, revise el deslizador "Background Opacity:".
- "Override Background: Auto" está habilitado de manera predeterminada, por lo que un cuadro de diálogo recién abierto ignorará cualquier color manual hasta que desactive "Auto".
- "Spot Lines:" está habilitado de manera predeterminada. Si las líneas verticales desde la línea base del espectro hasta las etiquetas de las marcas añaden desorden durante un concurso, haga clic en la alternancia para que muestre "Disabled". Este valor se persiste en `IsSpotsLinesEnabled`.

## Solución de problemas

- **El selector de color no tiene efecto visible en el panadapter** — Confirme que "Override Background: Enabled" muestre "Enabled" y que "Override Background: Auto" muestre "Disabled". Ambas condiciones deben cumplirse para que se muestre un color de fondo manual.
- **El fondo es invisible a pesar de los estados correctos de las alternancias** — Revise el deslizador "Background Opacity:". Si está en 0, el fondo es completamente transparente. Consulte [Ajustar la opacidad del fondo de las marcas](adjust-spot-background-opacity.md).
- **Las líneas de las marcas no son visibles** — Confirme que "Spot Lines:" muestre "Enabled". La alternancia se persiste en `IsSpotsLinesEnabled`. Este control se agregó en v0.9.7; si está ejecutando una versión anterior, la opción no está disponible.

## Relacionado

- [Ajustar la opacidad del fondo de las marcas](adjust-spot-background-opacity.md)
- [Forzar un solo color de texto para las marcas](force-a-single-spot-text-color.md)
- [Activar o desactivar las marcas](turn-spots-on-or-off.md)
- [Descripción general de Spot Settings](overview.md)
