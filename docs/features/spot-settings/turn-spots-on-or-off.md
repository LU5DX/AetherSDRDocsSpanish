# Activar o desactivar los spots

Los spots DX provenientes de fuentes cluster aparecen como superposiciones en el panadapter. Esta página explica cómo habilitar o deshabilitar esa visualización usando el conmutador maestro de spots en el cuadro de diálogo Spot Settings.

## Antes de empezar

- Debe haber un panadapter visible en la ventana principal.
- Las fuentes de spots (DX cluster, RBN, etc.) deben configurarse a través de `Settings > SpotHub...` si desea que aparezcan spots en vivo una vez que active la superposición.

## Pasos

1. Haga clic derecho en cualquier lugar del panadapter para abrir el menú contextual.
2. Seleccione la opción de superposición de spots para abrir el cuadro de diálogo **Spot Settings**.
3. Localice el botón conmutador **Spots:** en la parte superior del cuadro de diálogo.
4. Haga clic en el botón para alternar entre **Enabled** y **Disabled**.
   - El botón muestra el estado actual como texto: "Enabled" o "Disabled". El estado marcado (fondo resaltado) también indica el estado activo.
   - Cuando está en **Enabled**, los spots DX se dibujan en el panadapter.
   - Cuando está en **Disabled**, no se dibuja ningún spot. La configuración se guarda inmediatamente; no se necesita confirmación adicional.

## Qué hace cada control

| Etiqueta                         | Tipo          | Predeterminado | Clave de configuración                |
|----------------------------------|---------------|----------------|----------------------------------------|
| **Spots:**                       | Botón conmutador | Enabled        | `IsSpotsEnabled`                       |
| **Memories:**                    | Botón conmutador | Disabled       | `IsMemorySpotsEnabled`                 |
| **Levels:**                      | Deslizador    | 3              | `SpotsMaxLevel`                        |
| **Position:**                    | Deslizador    | 50             | `SpotsStartingHeightPercentage`        |
| **Font Size:**                   | Deslizador    | 16             | `SpotFontSize`                         |
| **Spot Lifetime:**               | Deslizador    | —              | `DxClusterSpotLifetimeSec`             |
| **Override Colors:**             | Botón conmutador | Disabled       | `IsSpotsOverrideColorsEnabled`         |
| Selector de color de texto del spot | Botón        | `#FFFF00`      | `SpotsOverrideColor`                   |
| **Override Background:**         | Botón conmutador | Enabled        | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto**    | Botón conmutador | Enabled        | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo del spot | Botón      | `#000000`      | `SpotsOverrideBgColor`                 |
| **Background Opacity:**          | Deslizador    | 48             | `SpotsBackgroundOpacity`               |
| **Spot Lines:**                  | Botón conmutador | Enabled        | `IsSpotsLinesEnabled`                  |
| **Clear All Spots**              | Botón         | —              | —                                      |

El indicador **Total Spots:** en la parte inferior del cuadro de diálogo muestra cuántos spots en vivo se están rastreando actualmente.

### Detalles de los controles

**Spots:** Este conmutador maestro activa o desactiva las superposiciones de spots DX. El texto del botón se actualiza dinámicamente para mostrar el estado actual: "Enabled" cuando los spots están activos, "Disabled" cuando no lo están. Desactivarlo no borra los spots almacenados en el búfer; reaparecen cuando los vuelve a activar.

**Memories:** Activa o desactiva las superposiciones de canales de memoria en el panadapter. El texto del botón se actualiza dinámicamente para mostrar el estado actual. La clave de configuración cambió de `IsMemoriesShownOnPanadapter` en v0.9.7.

**Override Colors:** Fuerza un solo color de texto para todos los spots. El texto del botón se actualiza dinámicamente para mostrar el estado actual. Cuando está habilitado, el botón selector de color se activa.

**Override Background:** Habilita el dibujo de un fondo debajo del texto del spot. El texto del botón se actualiza dinámicamente para mostrar el estado actual. Cuando está habilitado, el conmutador Auto y el selector de color se activan.

**Spot Lines:** Dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot. El texto del botón se actualiza dinámicamente para mostrar el estado actual. Desactívelo durante concursos para reducir el desorden visual. Este control se añadió en v0.9.7 (issue #2349).

**Spot Lifetime:** Utiliza una escala no lineal que va desde 10 segundos hasta 24 horas. El valor se almacena en segundos en `DxClusterSpotLifetimeSec`. En la primera lectura, cualquier valor guardado previamente bajo la antigua clave basada en minutos `DxClusterSpotLifetime` se migra automáticamente.

### Cambios de clave de configuración en v0.9.7

Varias claves de configuración fueron renombradas. Si referencia estas claves en scripts o herramientas de configuración externas, actualícelas en consecuencia.

| Control                 | Clave antigua                  | Clave nueva                     |
|-------------------------|--------------------------------|----------------------------------|
| **Memories:**           | `IsMemoriesShownOnPanadapter`  | `IsMemorySpotsEnabled`           |
| **Levels:**             | `SpotsStackLevels`             | `SpotsMaxLevel`                  |
| **Position:**           | `SpotsPosition`                | `SpotsStartingHeightPercentage`  |
| **Font Size:**          | `SpotsFontSize`                | `SpotFontSize`                   |
| **Spot Lifetime:**      | `SpotsLifetime`                | `DxClusterSpotLifetimeSec`       |
| **Background Opacity:** | `SpotsOverrideBgOpacity`       | `SpotsBackgroundOpacity`         |

## Consejos

- Cambiar **Spots:** a **Disabled** no borra los spots almacenados en el búfer. Cuando lo vuelva a activar, los spots que aún no hayan expirado reaparecerán.
- Los botones conmutadores en el cuadro de diálogo Spot Settings ahora muestran su estado actual como etiqueta de texto: "Enabled" cuando están activos, "Disabled" cuando están inactivos. El estado marcado (fondo resaltado) también indica si la función está activa.
- El deslizador **Spot Lifetime:** usa una escala no lineal: pasos finos en segundos en el extremo inferior, luego minutos, luego horas hasta 24 horas.
- Desactive **Spot Lines:** durante concursos para mantener el panadapter despejado mientras conserva las etiquetas de los spots.
- El cuadro de diálogo Spot Settings ahora sigue el tema actual. Las etiquetas de título y el indicador Total Spots usan el color de texto primario del tema para una apariencia consistente en diferentes perfiles de tema.

## Relacionados

- [Resumen de Spot Settings](overview.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar la vida útil de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un solo color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Borrar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
