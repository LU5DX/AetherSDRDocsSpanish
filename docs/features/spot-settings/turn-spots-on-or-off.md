# Activar o desactivar los spots

Los spots de DX aparecen como superposiciones en el panadapter. Esta página explica cómo habilitar o deshabilitar por completo la visualización de spots y describe todos los controles del cuadro de diálogo Spot Settings.

## Antes de comenzar

- Abra un panadapter. El cuadro de diálogo Spot Settings no está disponible desde el menú principal.
- Los spots requieren una fuente SpotHub activa para mostrarse. Consulte `Settings > SpotHub...` para configurar su cluster de DX u otras fuentes de spots.

## Pasos

1. Haga clic derecho en el panadapter para abrir el menú contextual.
2. Seleccione la opción de superposición Spots para abrir el cuadro de diálogo **Spot Settings**.
3. Haga clic en el botón de alternancia junto a **Spots:** para cambiar entre **Enabled** y **Disabled**.
4. Cierre el cuadro de diálogo. El cambio surte efecto de inmediato.

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Spots:** | Botón de alternancia | Enabled | `IsSpotsEnabled` | Control maestro para la visualización de spots de DX en el panadapter. |
| **Memories:** | Botón de alternancia | Disabled | `IsMemoriesShownOnPanadapter` | Muestra los canales de memoria del radio como superposiciones similares a spots en el panadapter. |
| **Levels:** | Control deslizante | 3 | `SpotsStackLevels` | Número de filas de apilamiento vertical que se usan cuando varios spots están cerca de la misma frecuencia. Rango: 1–10. |
| **Position:** | Control deslizante | 50 | `SpotsPosition` | Posición vertical de la superposición de spots en el panadapter, como porcentaje desde la parte superior. Rango: 0–100. |
| **Font Size:** | Control deslizante | 16 | `SpotsFontSize` | Tamaño del texto de las etiquetas de spots. Rango: 8–32. |
| **Spot Lifetime:** | Control deslizante | 30 min | `SpotsLifetime` | Tiempo que un spot permanece visible antes de expirar. Usa una escala no lineal: 10–55 segundos, luego 5–55 minutos, luego 1–24 horas. |
| **Override Colors:** | Botón de alternancia | Disabled | `IsSpotsOverrideColorsEnabled` | Fuerza a que todo el texto de los spots use un único color en lugar de los colores asignados por la fuente. |
| Selector de color del texto del spot | Botón de acción | #FFFF00 | `SpotsOverrideColor` | Abre un selector de color para elegir el color de texto alternativo. Activo solo cuando **Override Colors:** está en Enabled. |
| **Override Background: Enabled** | Botón de alternancia | Enabled | `IsSpotsOverrideBackgroundColorsEnabled` | Dibuja un fondo de color detrás de cada etiqueta de spot. |
| **Override Background: Auto** | Botón de alternancia | Enabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Selecciona automáticamente un color de fondo que contraste con el color del texto del spot. |
| Selector de color de fondo del spot | Botón de acción | #000000 | `SpotsOverrideBgColor` | Abre un selector de color para elegir el color de fondo. Se usa cuando **Override Background: Auto** está en Disabled. |
| **Background Opacity:** | Control deslizante | 48 | `SpotsOverrideBgOpacity` | Valor alfa (transparencia) del fondo del spot. Rango: 0–100. |
| **Clear All Spots** | Botón de acción | — | — | Elimina todos los spots actuales del panadapter de inmediato. No afecta el estado habilitado. |

El indicador **Total Spots:** en la parte superior del cuadro de diálogo muestra la cantidad de spots activos que se están rastreando en ese momento.

## Consejos

- Deshabilitar **Spots:** oculta la superposición pero no desconecta las fuentes SpotHub. Los spots continúan acumulándose en segundo plano; volver a habilitarlo restaura la fuente actual.
- Si los spots se ven visualmente saturados, aumente **Levels:** para distribuirlos en más filas verticales, o disminuya **Spot Lifetime:** para que los spots más antiguos expiren antes.
- **Override Background: Auto** anula el selector de color de fondo. Para usar un color de fondo personalizado, deshabilite primero **Override Background: Auto** y luego use el selector de color de fondo del spot.

## Solución de problemas

- **El botón de alternancia de Spots está en Enabled pero no aparecen spots en el panadapter** — Es posible que no haya ninguna fuente de spots configurada o conectada. Abra `Settings > SpotHub...` y verifique que al menos una fuente esté activa y conectada.
- **El control deslizante de Spot Lifetime se restablece al reiniciar** — El cuadro de diálogo migra de una configuración anterior basada en minutos a una basada en segundos en la primera carga. Si configuró el tiempo de vida antes de actualizar, abra Spot Settings, reajuste el control deslizante **Spot Lifetime:** y cierre el cuadro de diálogo para guardar.

## Relacionados

- [Descripción general de Spot Settings](overview.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad de spots y la posición vertical](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar el tiempo de vida de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
