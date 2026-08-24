# Diálogo de Configuración de Spots

El diálogo **Spot Settings** proporciona un control rápido y autónomo sobre cómo se renderizan los spots de DX y las superposiciones de canales de memoria en el panadapter. Puede ajustar la visibilidad, la densidad, la posición vertical, el tamaño del texto, la vida útil, las líneas de spot y las anulaciones de color.

## Abrir el diálogo Spot Settings

- Haga clic con el botón derecho en cualquier lugar de la superposición de spots en el panadapter.
- Seleccione **Spot Settings** en el menú contextual.

## Antes de comenzar

- El conmutador **Spots:** activa o desactiva toda la visualización de spots. Si muestra "Disabled", haga clic en él para habilitar los spots primero.

## Qué hacen los controles

| Control                          | Predeterminado                                                                                         | Rango                              |
|----------------------------------|--------------------------------------------------------------------------------------------------------|------------------------------------|
| **Spots:**                       | Enabled                                                                                                | On/Off                             |
| **Memories:**                    | Disabled                                                                                               | On/Off                             |
| **Kiwi DX:**                     | Disabled                                                                                               | On/Off                             |
| **Levels:**                      | 3                                                                                                      | 1–10                               |
| **Position:**                    | 50                                                                                                     | 0–100 (% desde arriba)             |
| **Font Size:**                   | 16                                                                                                     | 8–32 puntos                        |
| **Spot Lifetime:**               | 10 min                                                                                                 | 10 seg – 24 hrs (pasos no lineales)|
| **Override Colors:**             | Disabled                                                                                               | On/Off                             |
| Selector de color de texto de spot| `#FFFF00`                                                                                             | (color)                            |
| **Override Background: Enabled** | Enabled                                                                                                | On/Off                             |
| **Override Background: Auto**    | Enabled                                                                                                | On/Off                             |
| Selector de color de fondo de spot| `#000000`                                                                                             | (color)                            |
| **Background Opacity:**          | 48                                                                                                     | 0–100 (0 = transparente)           |
| **Spot Lines:**                  | Enabled                                                                                                | On/Off                             |
| **Clear All Spots**              | –                                                                                                      | –                                  |

## Spots de Kiwi DX

**Kiwi DX:** superpone spots de la base de datos comunitaria de DX de KiwiSDR en la tira de la banda. Estos incluyen balizas, estaciones de servicios y estaciones de señales horarias que normalmente no son reportadas por las fuentes de clúster de DX de aficionados.

Para habilitar los spots de Kiwi DX:

1. En el diálogo Spot Settings, localice la fila **Kiwi DX:**.
2. Haga clic en el botón de conmutación para que muestre **Enabled**. Esto se guarda como `ShowKiwiDxSpots`.
3. Los spots de Kiwi DX aparecen en la tira de banda inmediatamente.

Para deshabilitar los spots de Kiwi DX, haga clic nuevamente en el conmutador para que muestre **Disabled**.

## Indicador

| Indicador | Significado |
|---|---|
| **Total Spots:** | Conteo en vivo de spots de DX actualmente rastreados en el panadapter. |

## Estado de visualización de los botones de conmutación

Cada botón de conmutación en el diálogo Spot Settings actualiza su etiqueta para reflejar el estado habilitado o deshabilitado actual. Cuando un conmutador está habilitado, el botón muestra **Enabled**; cuando está deshabilitado, muestra **Disabled**. Esto aplica a los siguientes controles:

- **Spots:**
- **Memories:**
- **Kiwi DX:**
- **Override Colors:**
- **Override Background: Enabled**
- **Spot Lines:**

## Líneas de spot

**Spot Lines:** dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot. Está habilitado por defecto.

Para ocultar las líneas de spot, haga clic en el conmutador para que muestre **Disabled**. Esto establece `IsSpotsLinesEnabled` en `False`. Deshabilitar las líneas de spot es útil durante concursos donde muchos spots muy cercanos crean desorden visual en el panadapter.

Para restaurar las líneas de spot, haga clic nuevamente en el conmutador para que muestre **Enabled**.

## Forzar un solo color de texto de spot

Anule los colores por spot asignados por su fuente de clúster de DX y renderice todas las etiquetas de spot en un solo color elegido. Útil cuando los colores predeterminados contrastan con su tema del panadapter o son difíciles de leer.

1. En el diálogo Spot Settings, localice la fila **Override Colors:**.
2. Haga clic en el botón de conmutación para que muestre **Enabled**. Esto se guarda como `IsSpotsOverrideColorsEnabled`.
3. Haga clic en el botón de muestra de color inmediatamente a la derecha de **Enabled**. Se abre un diálogo de selector de color.
4. Seleccione el color que desea para todas las etiquetas de texto de spot y luego haga clic en **OK**.
5. La muestra se actualiza para mostrar su color elegido. Todos los spots en el panadapter se renderizan inmediatamente en ese color. El valor elegido se guarda como `SpotsOverrideColor`.

Para volver a los colores por spot, haga clic nuevamente en el conmutador **Override Colors:** para que muestre **Disabled**.

## Consejos

- El selector de color solo tiene efecto mientras **Override Colors:** muestra **Enabled**. Puede pre-seleccionar un color mientras el conmutador aún está en Disabled; se aplicará la próxima vez que habilite la anulación.
- Si el texto de los spots sigue siendo difícil de leer después de configurar el color, ajuste el contraste del fondo usando los controles de **Override Background:** — consulte [Elegir un color de fondo personalizado para spots](pick-a-custom-background-color-for-spots.md) y [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md).
- Durante concursos, deshabilitar **Spot Lines:** mientras mantiene los spots habilitados reduce el desorden sin perder las etiquetas de frecuencia.
- Los spots de Kiwi DX complementan los spots de clúster de DX de aficionados. Puede ejecutar ambas fuentes simultáneamente habilitando **Spots:** y **Kiwi DX:** juntos.

## Relacionado

- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Elegir un color de fondo personalizado para spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
