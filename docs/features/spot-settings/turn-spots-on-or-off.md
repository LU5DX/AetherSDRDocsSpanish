# Activar o desactivar los spots

Los spots de DX provenientes de fuentes de clúster aparecen como superposiciones en el panadaptador. Esta página explica cómo habilitar o deshabilitar esa visualización usando el interruptor maestro de spots en el cuadro de diálogo Spot Settings.

## Antes de comenzar

- Debe haber un panadaptador visible en la ventana principal.
- Las fuentes de spots (clúster DX, RBN, etc.) deben configurarse mediante `Settings > SpotHub...` si desea que los spots en vivo aparezcan al habilitar la superposición.

## Pasos

1. Haga clic derecho en cualquier lugar del panadaptador para abrir el menú contextual.
2. Seleccione la opción de superposición de spots para abrir el cuadro de diálogo **Spot Settings**.
3. Localice el botón de alternancia **Spots:** en la parte superior del cuadro de diálogo.
4. Haga clic en el botón para alternar entre **Enabled** y **Disabled**.
   - Cuando está en **Enabled**, los spots de DX se dibujan en el panadaptador.
   - Cuando está en **Disabled**, no se dibuja ningún spot. La configuración se guarda de inmediato; no se necesita confirmación adicional.

## Qué hace cada control

| Etiqueta                          | Tipo              | Valor predeterminado | Clave de configuración                   |
|-----------------------------------|-------------------|----------------------|------------------------------------------|
| **Spots:**                        | Botón de alternancia | Enabled            | `IsSpotsEnabled`                         |
| **Memories:**                     | Botón de alternancia | Disabled           | `IsMemorySpotsEnabled`                   |
| **Levels:**                       | Control deslizante | 3                    | `SpotsMaxLevel`                          |
| **Position:**                     | Control deslizante | 50                   | `SpotsStartingHeightPercentage`          |
| **Font Size:**                    | Control deslizante | 16                   | `SpotFontSize`                           |
| **Spot Lifetime:**                | Control deslizante | —                    | `DxClusterSpotLifetimeSec`               |
| **Override Colors:**              | Botón de alternancia | Disabled           | `IsSpotsOverrideColorsEnabled`           |
| Selector de color de texto del spot | Botón           | `#FFFF00`            | `SpotsOverrideColor`                     |
| **Override Background: Enabled**  | Botón de alternancia | Enabled            | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto**     | Botón de alternancia | Enabled            | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo del spot | Botón          | `#000000`            | `SpotsOverrideBgColor`                   |
| **Background Opacity:**           | Control deslizante | 48                   | `SpotsBackgroundOpacity`                 |
| **Spot Lines:**                   | Botón de alternancia | Enabled            | `IsSpotsLinesEnabled`                    |
| **Clear All Spots**               | Botón             | —                    | —                                        |

El indicador **Total Spots:** en la parte inferior del cuadro de diálogo muestra cuántos spots en vivo están siendo rastreados actualmente.

### Detalles de los controles

**Spot Lines:** dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot. Deshabilítelo durante concursos para reducir el desorden visual. Este control se agregó en la versión v0.9.7 (problema #2349).

**Spot Lifetime:** utiliza una escala no lineal que va de 10 segundos a 24 horas. El valor se almacena en segundos en `DxClusterSpotLifetimeSec`. En la primera lectura, cualquier valor guardado previamente bajo la clave anterior basada en minutos `DxClusterSpotLifetime` se migra automáticamente.

### Cambios de claves de configuración en v0.9.7

Varias claves de configuración fueron renombradas. Si hace referencia a estas claves en scripts o herramientas de configuración externas, actualícelas según corresponda.

| Control                 | Clave anterior               | Nueva clave                       |
|-------------------------|--------------------------------|-----------------------------------|
| **Memories:**           | `IsMemoriesShownOnPanadapter` | `IsMemorySpotsEnabled`            |
| **Levels:**             | `SpotsStackLevels`            | `SpotsMaxLevel`                   |
| **Position:**           | `SpotsPosition`               | `SpotsStartingHeightPercentage`   |
| **Font Size:**          | `SpotsFontSize`               | `SpotFontSize`                    |
| **Spot Lifetime:**      | `SpotsLifetime`               | `DxClusterSpotLifetimeSec`        |
| **Background Opacity:** | `SpotsOverrideBgOpacity`      | `SpotsBackgroundOpacity`          |

## Consejos

- Cambiar **Spots:** a **Disabled** no borra los spots almacenados en búfer. Cuando lo vuelva a habilitar, los spots que aún no hayan expirado reaparecerán.
- El control deslizante **Spot Lifetime:** utiliza una escala no lineal: pasos finos en segundos en el extremo inferior, luego minutos y luego horas hasta 24 horas.
- Deshabilite **Spot Lines:** durante concursos para mantener el panadaptador sin desorden mientras conserva las etiquetas de los spots.

## Relacionado

- [Spot Settings overview](overview.md)
- [Overlay memory channels on the panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Change spot density and vertical position](change-spot-density-and-vertical-position.md)
- [Enlarge or shrink the spot font](enlarge-or-shrink-the-spot-font.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
- [Force a single spot text color](force-a-single-spot-text-color.md)
- [Pick a custom background color for spots](pick-a-custom-background-color-for-spots.md)
- [Adjust spot background opacity](adjust-spot-background-opacity.md)
- [Clear every spot from the panadapter](clear-every-spot-from-the-panadapter.md)
