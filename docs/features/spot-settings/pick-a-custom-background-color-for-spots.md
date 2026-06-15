# Elegir un color de fondo personalizado para los spots

Establezca un color de fondo específico que aparecerá detrás de las etiquetas de los spots en el panadapter. Utilícelo cuando el contraste de color automático no sea adecuado para su pantalla o condiciones de operación.

## Antes de comenzar

- Abra el cuadro de diálogo Spot Settings haciendo clic derecho en la superposición de spots en un panadapter.
- Confirme que "Override Background: Enabled" esté activo (el botón muestra "Enabled"). El selector de color de fondo no tiene efecto cuando el fondo está deshabilitado.
- Desactive "Override Background: Auto" si desea que el color elegido tenga efecto. Cuando "Auto" está activo, AetherSDR selecciona el color de fondo automáticamente e ignora el selector de color manual.

## Pasos

1. Haga clic derecho en la superposición de spots en el panadapter y abra Spot Settings.
2. Localice la fila **Override Background:**.
3. Si el botón "Enabled" muestra un estado rojo/deshabilitado, haga clic en él para que muestre un estado verde/habilitado. Esto se conserva en `IsSpotsOverrideBackgroundColorsEnabled`.
4. Si el botón "Auto" muestra un estado verde/habilitado, haga clic en él para que muestre un estado rojo/deshabilitado. Esto se conserva en `IsSpotsOverrideToAutoBackgroundColorEnabled`. Mientras "Auto" esté activo, el selector de color manual queda anulado.
5. Haga clic en el pequeño botón de muestra de color a la derecha de "Auto". Esto abre el cuadro de diálogo de color del sistema titulado "Spot Background Color".
6. Seleccione el color deseado y confirme la selección.
7. La muestra se actualiza inmediatamente y el fondo del panadapter detrás de las etiquetas de los spots cambia al color elegido. El valor se conserva en `SpotsOverrideBgColor`.

## Función de cada control

| Etiqueta | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| Spots: | Botón de alternancia | Habilitado | Activación principal para la visualización de spots DX. Se conserva en `IsSpotsEnabled`. La etiqueta del botón siempre muestra "Enabled" independientemente del estado; el estado marcado se indica mediante color (verde = habilitado, rojo = deshabilitado). |
| Memories: | Botón de alternancia | Deshabilitado | Activa o desactiva las superposiciones de canales de memoria en el panadapter. La clave de configuración cambió de `IsMemoriesShownOnPanadapter` en v0.9.7. Se conserva en `IsMemorySpotsEnabled`. La etiqueta del botón siempre muestra "Enabled" independientemente del estado. |
| Levels: | Deslizador (1–10) | 3 | Filas de apilamiento vertical para spots. La clave de configuración cambió de `SpotsStackLevels` en v0.9.7. Se conserva en `SpotsMaxLevel`. |
| Position: | Deslizador (0–100) | 50 | Posición vertical en el panadapter como porcentaje. La clave de configuración cambió de `SpotsPosition` en v0.9.7. Se conserva en `SpotsStartingHeightPercentage`. |
| Font Size: | Deslizador (8–32) | 16 | Tamaño del texto de los spots en puntos. La clave de configuración cambió de `SpotsFontSize` en v0.9.7. Se conserva en `SpotFontSize`. |
| Spot Lifetime: | Deslizador (pasos no lineales) | (varía) | Tiempo que los spots permanecen antes de desvanecerse. Escala no lineal desde 10 segundos hasta 24 horas. Se almacena en segundos. La clave de configuración cambió de `SpotsLifetime` en v0.9.7. Migra la clave anterior basada en minutos `DxClusterSpotLifetime` en la primera lectura. Se conserva en `DxClusterSpotLifetimeSec`. |
| Override Colors: | Botón de alternancia | Deshabilitado | Fuerza un único color de texto para todos los spots. Se conserva en `IsSpotsOverrideColorsEnabled`. La etiqueta del botón siempre muestra "Enabled" independientemente del estado. |
| Selector de color de texto de spots | Botón pulsador (muestra) | `#FFFF00` | Abre un cuadro de diálogo de color para el color del texto. Se conserva en `SpotsOverrideColor`. |
| Override Background: Enabled | Botón de alternancia | Habilitado | Dibuja un fondo debajo del texto de los spots. Se conserva en `IsSpotsOverrideBackgroundColorsEnabled`. La etiqueta del botón siempre muestra "Enabled" independientemente del estado. |
| Override Background: Auto | Botón de alternancia | Habilitado | Selecciona automáticamente el color de fondo para el contraste. Cuando está habilitado, se ignora el selector de color manual. Se conserva en `IsSpotsOverrideToAutoBackgroundColorEnabled`. La etiqueta del botón siempre muestra "Enabled" independientemente del estado. |
| Selector de color de fondo de spots | Botón pulsador (muestra) | `#000000` | Abre un cuadro de diálogo de color para el color de fondo. Se conserva en `SpotsOverrideBgColor`. |
| Background Opacity: | Deslizador (0–100) | 48 | Alfa del fondo de los spots. 0 = completamente transparente, 100 = completamente opaco. La clave de configuración cambió de `SpotsOverrideBgOpacity` en v0.9.7. Se conserva en `SpotsBackgroundOpacity`. |
| Spot Lines: | Botón de alternancia | Habilitado | Dibuja líneas verticales desde la línea de base del espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir el desorden visual. Nuevo en v0.9.7 (#2349). Se conserva en `IsSpotsLinesEnabled`. La etiqueta del botón siempre muestra "Enabled" independientemente del estado. |
| Clear All Spots | Botón pulsador | — | Elimina todos los spots del panadapter. |

## Indicadores

| Etiqueta | Significado |
|---|---|
| Total Spots: | Muestra el recuento de spots activos actualmente rastreados. |

## Consejos

- Establecer la opacidad en 0 hace que el fondo sea completamente transparente independientemente del color elegido. Si el fondo desaparece después de elegir un color, verifique el deslizador "Background Opacity:".
- "Override Background: Auto" tiene como valor predeterminado "Enabled", por lo que un cuadro de diálogo recién abierto ignorará cualquier color manual hasta que desactive "Auto".
- "Spot Lines:" tiene como valor predeterminado "Enabled". Si las líneas verticales desde la línea de base del espectro hasta las etiquetas de los spots agregan desorden durante un concurso, haga clic en la alternancia para que muestre un estado rojo/deshabilitado. Esto se conserva en `IsSpotsLinesEnabled`.

## Solución de problemas

- **El selector de color no tiene efecto visible en el panadapter** — Confirme que "Override Background: Enabled" muestre verde/habilitado y "Override Background: Auto" muestre rojo/deshabilitado. Ambas condiciones deben cumplirse para que se muestre un color de fondo manual.
- **El fondo es invisible a pesar de los estados correctos de las alternancias** — Verifique el deslizador "Background Opacity:". Si está en 0, el fondo es completamente transparente. Consulte [Adjust spot background opacity](adjust-spot-background-opacity.md).
- **Las líneas de los spots no son visibles** — Confirme que "Spot Lines:" muestre verde/habilitado. La alternancia se conserva en `IsSpotsLinesEnabled`. Este control se agregó en v0.9.7; si está utilizando una versión anterior, la configuración no está disponible.

## Relacionados

- [Adjust spot background opacity](adjust-spot-background-opacity.md)
- [Force a single spot text color](force-a-single-spot-text-color.md)
- [Turn spots on or off](turn-spots-on-or-off.md)
- [Spot Settings overview](overview.md)
