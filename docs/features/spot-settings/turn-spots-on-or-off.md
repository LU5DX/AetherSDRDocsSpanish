# Activar o desactivar los spots

Los spots de DX provenientes de las fuentes de cluster configuradas pueden mostrarse u ocultarse en el panadapter en cualquier momento. Use el interruptor maestro de spots para habilitar o deshabilitar toda la capa de spots sin modificar ningún otro ajuste.

## Antes de comenzar

- Abra un panadapter. El diálogo Spot Settings se accede desde el menú contextual del panadapter.
- Asegúrese de que al menos una fuente de spots esté configurada en `Settings > SpotHub...` si desea que los spots aparezcan al habilitarlos.

## Pasos

1. Haga clic derecho en cualquier lugar del panadapter para abrir el menú contextual.
2. Seleccione la opción de capa de spots para abrir el diálogo **Spot Settings**.
3. Localice la fila **Spots:**.
4. Haga clic en el botón de interruptor para alternar entre **Enabled** y **Disabled**.

El cambio surte efecto de inmediato. La etiqueta del botón se actualiza para reflejar el estado actual y `IsSpotsEnabled` se guarda.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento | Clave de ajuste |
|---|---|---|---|
| Interruptor **Spots:** | Enabled | Interruptor maestro. Oculta o muestra todos los spots de DX en el panadapter. | `IsSpotsEnabled` |
| Interruptor **Memories:** | Disabled | Muestra los canales de memoria de la radio como marcadores similares a spots en el panadapter. | `IsMemoriesShownOnPanadapter` |
| Control deslizante **Levels:** | 3 | Número de filas de apilamiento vertical que se usan cuando los spots se superponen. Rango: 1–10. | `SpotsStackLevels` |
| Control deslizante **Position:** | 50 | Posición vertical de la banda de spots en el panadapter, como porcentaje desde la parte superior. Rango: 0–100. | `SpotsPosition` |
| Control deslizante **Font Size:** | 16 | Tamaño de texto para las etiquetas de spots. Rango: 8–32 pt. | `SpotsFontSize` |
| Control deslizante **Spot Lifetime:** | 30 min | Tiempo que un spot permanece visible antes de expirar. Los pasos van desde 10 sec hasta 24 hrs. | `SpotsLifetime` |
| Interruptor **Override Colors:** | Disabled | Fuerza a que todas las etiquetas de spots usen un único color de texto en lugar de los colores asignados por el cluster. | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto del spot | `#FFFF00` | Abre un selector de color para elegir el color de texto de sustitución. Activo solo cuando **Override Colors:** está en Enabled. | `SpotsOverrideColor` |
| Interruptor **Override Background: Enabled** | Enabled | Dibuja un fondo sólido detrás de cada etiqueta de spot. | `IsSpotsOverrideBackgroundColorsEnabled` |
| Interruptor **Override Background: Auto** | Enabled | Elige automáticamente un color de fondo que contraste con el color del texto. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo del spot | `#000000` | Abre un selector de color para elegir un color de fondo manual. Se usa cuando Auto está en Disabled. | `SpotsOverrideBgColor` |
| Control deslizante **Background Opacity:** | 48 | Valor alfa para el fondo del spot. Rango: 0–100. | `SpotsOverrideBgOpacity` |
| **Clear All Spots** | — | Elimina todos los spots que se muestran actualmente en el panadapter. No afecta los ajustes. | — |

## Consejos

- El indicador **Total Spots:** en el diálogo muestra cuántos spots se están rastreando actualmente, incluso cuando el interruptor **Spots:** está en Disabled.
- Deshabilitar **Spots:** no borra la lista interna de spots. Al volver a habilitarlo, se restauran todos los spots que aún no hayan expirado.
- Si desea ocultar los spots solo temporalmente, desactive **Spots:** en lugar de desconectar su fuente de cluster en `Settings > SpotHub...`.

## Solución de problemas

- **El interruptor Spots está en Enabled pero no aparece ningún spot en el panadapter** — Aún no se han recibido spots, o todos los spots recibidos caen fuera del rango de frecuencia actual del panadapter. Verifique su conexión al cluster en `Settings > SpotHub...`. El contador **Total Spots:** será cero si no ha llegado ningún dato.
- **Los spots reaparecen tras reiniciar aunque los haya deshabilitado** — El ajuste `IsSpotsEnabled` se guarda de inmediato al activar el interruptor. Si los spots aparecen, es posible que el interruptor haya sido reactivado por otra sesión o por la carga de un perfil.

## Relacionados

- [Descripción general de Spot Settings](overview.md)
- [Superponer canales de memoria en el panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Cambiar la densidad de spots y la posición vertical](change-spot-density-and-vertical-position.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Borrar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
