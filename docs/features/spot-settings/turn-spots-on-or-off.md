# Activar o desactivar los avisos (spots)

Los avisos DX procedentes de fuentes de clúster aparecen como superposiciones en el panadapter. Esta página explica cómo habilitar o deshabilitar esa visualización mediante el conmutador maestro de avisos en el cuadro de diálogo **Spot Settings**.

## Antes de comenzar

- Debe haber un panadapter visible en la ventana principal.
- Las fuentes de avisos (DX cluster, RBN, etc.) deben configurarse mediante `Settings > SpotHub...` si desea que aparezcan avisos en vivo una vez que habilite la superposición.

## Pasos

1. Haga clic con el botón derecho en cualquier parte del panadapter para abrir el menú contextual.
2. Seleccione la opción de superposición de avisos para abrir el cuadro de diálogo **Spot Settings**.
3. Localice el botón de conmutación **Spots:** en la parte superior del cuadro de diálogo.
4. Haga clic en el botón para alternar entre **Enabled** y **Disabled**.
   - El botón muestra el estado actual como su etiqueta de texto: "Enabled" o "Disabled". El estado marcado (fondo resaltado) también indica el estado activo.
   - Cuando está en **Enabled**, los avisos DX se dibujan en el panadapter.
   - Cuando está en **Disabled**, no se dibuja ningún aviso. El ajuste se guarda inmediatamente; no se necesita confirmación adicional.

## Qué hace cada control

| Etiqueta                        | Tipo                                                                                                    | Predeterminado                 |
|---------------------------------|---------------------------------------------------------------------------------------------------------|--------------------------------|
| **Spots:**                      | Botón de conmutación                                                                                    | Enabled                        |
| **Memories:**                   | Botón de conmutación                                                                                    | Disabled                       |
| **Kiwi DX:**                    | Botón de conmutación                                                                                    | Disabled                       |
| **Levels:**                     | Deslizador                                                                                              | 3                              |
| **Position:**                   | Deslizador                                                                                              | 50                             |
| **Font Size:**                  | Deslizador                                                                                              | 16                             |
| **Spot Lifetime:**              | Deslizador                                                                                              | —                              |
| **Override Colors:**            | Botón de conmutación                                                                                    | Disabled                       |
| Selector de color de texto      | Botón                                                                                                   | `#FFFF00`                      |
| **Override Background:**        | Botón de conmutación                                                                                    | Enabled                        |
| **Override Background: Auto**   | Botón de conmutación                                                                                    | Enabled                        |
| Selector de color de fondo      | Botón                                                                                                   | `#000000`                      |
| **Background Opacity:**         | Deslizador                                                                                              | 48                             |
| **Spot Lines:**                 | Botón de conmutación                                                                                    | Enabled                        |
| **Clear All Spots**             | Botón                                                                                                   | —                              |

El indicador **Total Spots:** en la parte inferior del cuadro de diálogo muestra cuántos avisos en vivo se están rastreando actualmente.

### Detalles del control

**Spots:** Este conmutador maestro activa o desactiva las superposiciones de avisos DX. El texto del botón se actualiza dinámicamente para mostrar el estado actual: "Enabled" cuando los avisos están activos, "Disabled" cuando no lo están. Desactivar esto no borra los avisos almacenados en búfer: reaparecen cuando lo vuelve a habilitar.

**Memories:** Activa o desactiva las superposiciones de canales de memoria en el panadapter. El texto del botón se actualiza dinámicamente para mostrar el estado actual. La clave de ajuste cambió de `IsMemoriesShownOnPanadapter` en la v0.9.7.

**Kiwi DX:** Superpone los avisos de la base de datos comunitaria KiwiSDR DX (balizas, utilidades, señales horarias) en la franja del plan de bandas. El texto del botón se actualiza dinámicamente para mostrar el estado actual. Este control se añadió en la v26.8.4. El valor predeterminado es **Disabled**; la clave de ajuste es `ShowKiwiDxSpots`.

**Override Colors:** Fuerza un único color de texto para todos los avisos. El texto del botón se actualiza dinámicamente para mostrar el estado actual. Cuando está habilitado, el botón selector de color se vuelve activo.

**Override Background:** Habilita el dibujo de un fondo bajo el texto de los avisos. El texto del botón se actualiza dinámicamente para mostrar el estado actual. Cuando está habilitado, el conmutador Auto y el selector de color se vuelven activos.

**Spot Lines:** Dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de aviso. El texto del botón se actualiza dinámicamente para mostrar el estado actual. Desactívelo durante concursos para reducir el desorden visual. Este control se añadió en la v0.9.7 (problema #2349).

**Spot Lifetime:** Utiliza una escala no lineal que va de 10 segundos a 24 horas. El valor se almacena en segundos en `DxClusterSpotLifetimeSec`. En la primera lectura, cualquier valor guardado previamente bajo la antigua clave basada en minutos `DxClusterSpotLifetime` se migra automáticamente.

### Cambios de claves de ajuste en la v0.9.7

Varias claves de ajuste fueron renombradas. Si hace referencia a estas claves en scripts o herramientas de configuración externas, actualícelas en consecuencia.

| Control                  | Clave antigua                     | Clave nueva                         |
|--------------------------|-----------------------------------|-------------------------------------|
| **Memories:**            | `IsMemoriesShownOnPanadapter`     | `IsMemorySpotsEnabled`              |
| **Levels:**              | `SpotsStackLevels`                | `SpotsMaxLevel`                     |
| **Position:**            | `SpotsPosition`                   | `SpotsStartingHeightPercentage`     |
| **Font Size:**           | `SpotsFontSize`                   | `SpotFontSize`                      |
| **Spot Lifetime:**       | `SpotsLifetime`                   | `DxClusterSpotLifetimeSec`          |
| **Background Opacity:**  | `SpotsOverrideBgOpacity`          | `SpotsBackgroundOpacity`            |

## Consejos

- Cambiar **Spots:** a **Disabled** no borra los avisos almacenados en búfer. Cuando lo vuelva a habilitar, los avisos que aún no hayan expirado reaparecerán.
- Los botones de conmutación en el cuadro de diálogo **Spot Settings** ahora muestran su estado actual como etiqueta de texto: "Enabled" cuando están activos, "Disabled" cuando están inactivos. El estado marcado (fondo resaltado) también indica si la función está activa.
- El deslizador **Spot Lifetime:** utiliza una escala no lineal: pasos finos en segundos en el extremo inferior, luego minutos, y luego horas hasta 24 horas.
- Desactive **Spot Lines:** durante concursos para mantener el panadapter sin desorden visual y conservar las etiquetas de avisos.
- Los avisos de **Kiwi DX:** se almacenan en el ajuste `ShowKiwiDxSpots`. Esta función está desactivada por defecto.
- El cuadro de diálogo **Spot Settings** ahora sigue el tema actual. Las etiquetas de título y el indicador **Total Spots** utilizan el color de texto principal del tema para una apariencia coherente entre diferentes perfiles de tema.

## Relacionado

- [Resumen de Spot Settings](overview.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los avisos](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los avisos](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar la vida útil de los avisos](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un único color de texto para los avisos](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los avisos](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los avisos](adjust-spot-background-opacity.md)
- [Borrar todos los avisos del panadapter](clear-every-spot-from-the-panadapter.md)
