# Ajustar la opacidad del fondo de los spots

Use el control deslizante **Background Opacity:** para controlar qué tan transparente u opaco aparece el recuadro de fondo dibujado detrás de cada etiqueta de spot en el panadapter.

## Antes de comenzar

- Abra el diálogo Spot Settings haciendo clic derecho sobre la capa de spots en cualquier panadapter.
- Confirme que el interruptor **Override Background:** **Enabled** esté activo (debe mostrar "Enabled"). El control deslizante de opacidad no tiene efecto visible si el dibujo de fondo está desactivado.

## Pasos

1. En el diálogo Spot Settings, localice la fila **Background Opacity:** cerca de la parte inferior de los controles.
2. Arrastre el control deslizante hacia la izquierda para disminuir la opacidad (más transparente) o hacia la derecha para aumentarla (más opaco).
3. El valor numérico junto al control deslizante se actualiza de inmediato. El panadapter refleja el cambio en tiempo real.
4. Cierre el diálogo cuando termine. El valor se guarda automáticamente en `SpotsOverrideBgOpacity`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Control deslizante **Background Opacity:** | 48 | 0 – 100 | `SpotsOverrideBgOpacity` |
| Interruptor **Override Background:** **Enabled** | Enabled | Enabled / Disabled | `IsSpotsOverrideBackgroundColorsEnabled` |
| Interruptor **Override Background:** **Auto** | Enabled | Enabled / Disabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo del spot | `#000000` | Cualquier color | `SpotsOverrideBgColor` |

## Consejos

- Un valor de 0 hace el fondo completamente transparente; el texto del spot sigue siendo visible pero no tiene recuadro de respaldo. Un valor de 100 hace el fondo completamente opaco.
- Si **Override Background:** **Auto** está habilitado, AetherSDR elige el color de fondo automáticamente para garantizar contraste. El selector de color manual y el control deslizante de opacidad siguen aplicándose.

## Solución de problemas

- **Cambiar el control deslizante no tiene efecto en el panadapter** — Verifique que **Override Background:** **Enabled** muestre "Enabled". Si muestra "Disabled", haga clic una vez para habilitar el dibujo de fondo y luego ajuste el control deslizante.
- **Los spots no son visibles en absoluto** — Confirme que el interruptor **Spots:** muestre "Enabled". Consulte [Activar o desactivar los spots](turn-spots-on-or-off.md).

## Relacionados

- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Descripción general de Spot Settings](overview.md)
