# Elegir un color de fondo personalizado para los spots

Establezca un color de fondo específico que aparecerá detrás de las etiquetas de los spots en el panadapter. Utilice esta opción cuando el contraste de color automático no sea adecuado para su pantalla o condiciones de operación.

## Antes de comenzar

- Abra el cuadro de diálogo Spot Settings haciendo clic derecho en la superposición de spots en un panadapter.
- Confirme que el botón "Override Background: Enabled" muestre "Enabled". El selector de color de fondo no tiene efecto cuando el fondo está deshabilitado.
- Desactive "Override Background: Auto" si desea que el color elegido surta efecto. Cuando "Auto" está activo, AetherSDR selecciona el color de fondo automáticamente e ignora el selector de color manual.

## Pasos

1. Haga clic derecho en la superposición de spots en el panadapter y abra Spot Settings.
2. Localice la fila **Override Background:**.
3. Si el botón "Enabled" muestra "Disabled", haga clic en él para que muestre "Enabled". Este valor se persiste en `IsSpotsOverrideBackgroundColorsEnabled`.
4. Si el botón "Auto" muestra "Enabled", haga clic en él para que muestre "Disabled". Este valor se persiste en `IsSpotsOverrideToAutoBackgroundColorEnabled`. Mientras "Auto" esté activo, el selector de color manual queda anulado.
5. Haga clic en el pequeño botón de muestra de color a la derecha de "Auto". Esto abre el cuadro de diálogo de color del sistema titulado "Spot Background Color".
6. Seleccione el color deseado y confirme la selección.
7. La muestra se actualiza inmediatamente y el fondo del panadapter detrás de las etiquetas de los spots cambia al color elegido. El valor se persiste en `SpotsOverrideBgColor`.

## Función de cada control

| Etiqueta | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| Spots: | Botón de alternancia | Enabled | Activación general de la visualización de spots DX. La etiqueta del botón muestra "Enabled" cuando está marcado y "Disabled" cuando no lo está. Se persiste en `IsSpotsEnabled`. |
| Memories: | Botón de alternancia | Disabled | Activa o desactiva las superposiciones de canales de memoria en el panadapter. La etiqueta del botón muestra "Enabled" cuando está marcado y "Disabled" cuando no lo está. La clave de configuración cambió de `IsMemoriesShownOnPanadapter` en v0.9.7. Se persiste en `IsMemorySpotsEnabled`. |
| Levels: | Deslizador (1–10) | 3 | Filas de apilamiento vertical para los spots. La clave de configuración cambió de `SpotsStackLevels` en v0.9.7. Se persiste en `SpotsMaxLevel`. |
| Position: | Deslizador (0–100) | 50 | Posición vertical en el panadapter como porcentaje. La clave de configuración cambió de `SpotsPosition` en v0.9.7. Se persiste en `SpotsStartingHeightPercentage`. |
| Font Size: | Deslizador (8–32) | 16 | Tamaño del texto de los spots en puntos. La clave de configuración cambió de `SpotsFontSize` en v0.9.7. Se persiste en `SpotFontSize`. |
| Spot Lifetime: | Deslizador (pasos no lineales) | (varía) | Tiempo que los spots permanecen antes de desvanecerse. Escala no lineal de 10 segundos a 24 horas. Se almacena en segundos. La clave de configuración cambió de `SpotsLifetime` en v0.9.7. Migra la clave anterior basada en minutos `DxClusterSpotLifetime` en la primera lectura. Se persiste en `DxClusterSpotLifetimeSec`. |
| Override Colors: | Botón de alternancia | Disabled | Fuerza un solo color de texto para todos los spots. La etiqueta del botón muestra "Enabled" cuando está marcado y "Disabled" cuando no lo está. Se persiste en `IsSpotsOverrideColorsEnabled`. |
| Selector de color de texto de spots | Botón pulsador (muestra) | `#FFFF00` | Abre un cuadro de diálogo de color para el color del texto. Se persiste en `SpotsOverrideColor`. |
| Override Background: Enabled | Botón de alternancia | Enabled | Dibuja un fondo debajo del texto de los spots. La etiqueta del botón muestra "Enabled" cuando está marcado y "Disabled" cuando no lo está. Se persiste en `IsSpotsOverrideBackgroundColorsEnabled`. |
| Override Background: Auto | Botón de alternancia | Enabled | Selecciona automáticamente el color de fondo para contraste. Cuando está habilitado, el selector de color manual se ignora. La etiqueta del botón siempre muestra "Auto" independientemente del estado. Se persiste en `IsSpotsOverrideToAutoBackgroundColorEnabled`. |
| Selector de color de fondo de spots | Botón pulsador (muestra) | `#000000` | Abre un cuadro de diálogo de color para el color de fondo. Se persiste en `SpotsOverrideBgColor`. |
| Background Opacity: | Deslizador (0–100) | 48 | Alfa del fondo de los spots. 0 = completamente transparente, 100 = completamente opaco. La clave de configuración cambió de `SpotsOverrideBgOpacity` en v0.9.7. Se persiste en `SpotsBackgroundOpacity`. |
| Spot Lines: | Botón de alternancia | Enabled | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. La etiqueta del botón muestra "Enabled" cuando está marcado y "Disabled" cuando no lo está. Desactive durante concursos para reducir el desorden visual. Nuevo en v0.9.7 (#2349). Se persiste en `IsSpotsLinesEnabled`. |
| Clear All Spots | Botón pulsador | — | Elimina todos los spots del panadapter. |

## Indicadores

| Etiqueta | Significado |
|---|---|
| Total Spots: | Muestra el recuento de spots activos actualmente rastreados. |

## Consejos

- Establecer la opacidad en 0 hace que el fondo sea completamente transparente independientemente del color elegido. Si el fondo desaparece después de elegir un color, verifique el deslizador "Background Opacity:".
- "Override Background: Auto" tiene como valor predeterminado "Enabled", por lo que un cuadro de diálogo recién abierto ignorará cualquier color manual hasta que desactive "Auto".
- "Spot Lines:" tiene como valor predeterminado "Enabled". Si las líneas verticales desde la línea base del espectro hasta las etiquetas de los spots añaden desorden durante un concurso, haga clic en el botón de alternancia para que muestre "Disabled". Esto se persiste en `IsSpotsLinesEnabled`.

## Solución de problemas

- **El selector de color no tiene efecto visible en el panadapter** — Confirme que "Override Background: Enabled" muestre "Enabled" y "Override Background: Auto" muestre "Disabled". Ambas condiciones deben cumplirse para que se muestre un color de fondo manual.
- **El fondo es invisible a pesar de los estados correctos de los botones** — Verifique el deslizador "Background Opacity:". Si está en 0, el fondo es completamente transparente. Consulte [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md).
- **Las líneas de los spots no son visibles** — Confirme que "Spot Lines:" muestre "Enabled". La alternancia se persiste en `IsSpotsLinesEnabled`. Este control se agregó en v0.9.7; si está utilizando una versión anterior, la configuración no está disponible.

## Relacionado

- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Forzar un solo color de texto para los spots](force-a-single-spot-text-color.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Resumen de Spot Settings](overview.md)
