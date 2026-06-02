# Activar o desactivar los spots

Los spots de DX provenientes de fuentes cluster aparecen como superposiciones en el panadaptador. Esta página explica cómo habilitar o deshabilitar esa visualización usando el conmutador maestro de spots en el diálogo Spot Settings.

## Antes de comenzar

- Debe haber un panadaptador visible en la ventana principal.
- Las fuentes de spots (DX cluster, RBN, etc.) deben configurarse a través de `Settings > SpotHub...` si desea que aparezcan spots activos una vez que habilite la superposición.

## Pasos

1. Haga clic derecho en cualquier lugar del panadaptador para abrir el menú contextual.
2. Seleccione la opción de superposición de spots para abrir el diálogo **Spot Settings**.
3. Localice el botón conmutador **Spots:** en la parte superior del diálogo.
4. Haga clic en el botón para alternar entre **Enabled** y **Disabled**.
   - Cuando está en **Enabled**, los spots de DX se dibujan en el panadaptador.
   - Cuando está en **Disabled**, no se dibuja ningún spot. La configuración se guarda inmediatamente; no se necesita confirmación adicional.

## Qué hace cada control

| Etiqueta                          | Tipo           | Valor predeterminado | Clave de configuración                    |
|-----------------------------------|----------------|----------------------|-------------------------------------------|
| **Spots:**                        | Botón conmutador | Enabled            | `IsSpotsEnabled`                          |
| **Memories:**                     | Botón conmutador | Disabled           | `IsMemorySpotsEnabled`                    |
| **Levels:**                       | Deslizador     | 3                    | `SpotsMaxLevel`                           |
| **Position:**                     | Deslizador     | 50                   | `SpotsStartingHeightPercentage`           |
| **Font Size:**                    | Deslizador     | 16                   | `SpotFontSize`                            |
| **Spot Lifetime:**                | Deslizador     | —                    | `DxClusterSpotLifetimeSec`                |
| **Override Colors:**              | Botón conmutador | Disabled          | `IsSpotsOverrideColorsEnabled`            |
| Selector de color de texto del spot | Botón       | `#FFFF00`            | `SpotsOverrideColor`                      |
| **Override Background: Enabled**  | Botón conmutador | Enabled           | `IsSpotsOverrideBackgroundColorsEnabled`  |
| **Override Background: Auto**     | Botón conmutador | Enabled           | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo del spot | Botón     | `#000000`            | `SpotsOverrideBgColor`                    |
| **Background Opacity:**           | Deslizador     | 48                   | `SpotsBackgroundOpacity`                  |
| **Spot Lines:**                   | Botón conmutador | Enabled           | `IsSpotsLinesEnabled`                     |
| **Clear All Spots**               | Botón          | —                    | —                                         |

El indicador **Total Spots:** en la parte inferior del diálogo muestra cuántos spots activos se están rastreando actualmente.

### Detalles de los controles

**Spot Lines:** dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot. Desactive esta opción durante concursos para reducir el desorden visual. Este control se agregó en v0.9.7 (issue #2349).

**Spot Lifetime:** utiliza una escala no lineal que va desde 10 segundos hasta 24 horas. El valor se almacena en segundos en `DxClusterSpotLifetimeSec`. En la primera lectura, cualquier valor guardado previamente bajo la antigua clave basada en minutos `DxClusterSpotLifetime` se migra automáticamente.

### Cambios de claves de configuración en v0.9.7

Varias claves de configuración fueron renombradas. Si hace referencia a estas claves en scripts o herramientas de configuración externas, actualícelas en consecuencia.

| Control             | Clave antigua                  | Clave nueva                      |
|---------------------|--------------------------------|----------------------------------|
| **Memories:**       | `IsMemoriesShownOnPanadapter`  | `IsMemorySpotsEnabled`           |
| **Levels:**         | `SpotsStackLevels`             | `SpotsMaxLevel`                  |
| **Position:**       | `SpotsPosition`                | `SpotsStartingHeightPercentage`  |
| **Font Size:**      | `SpotsFontSize`                | `SpotFontSize`                   |
| **Spot Lifetime:**  | `SpotsLifetime`                | `DxClusterSpotLifetimeSec`       |
| **Background Opacity:** | `SpotsOverrideBgOpacity`   | `SpotsBackgroundOpacity`         |

## Consejos

- Alternar **Spots:** a **Disabled** no elimina los spots almacenados en búfer. Cuando lo vuelva a habilitar, los spots que aún no hayan expirado reaparecerán.
- El deslizador **Spot Lifetime:** utiliza una escala no lineal: pasos finos en segundos en el extremo inferior, luego minutos, y luego horas hasta 24 horas.
- Desactive **Spot Lines:** durante concursos para mantener el panadaptador despejado mientras conserva las etiquetas de los spots.
- El diálogo Spot Settings ahora sigue el tema actual. Las etiquetas de título y el indicador Total Spots utilizan el color de texto principal del tema para una apariencia consistente en diferentes perfiles de tema.

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
