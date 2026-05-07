# Forzar un único color para el texto de las marcas

Sobrescriba los colores individuales asignados por su fuente de clúster DX y renderice todas las etiquetas de marcas en un solo color elegido. Es útil cuando los colores predeterminados entran en conflicto con el tema del panadapter o son difíciles de leer.

## Antes de comenzar

- Las marcas deben estar habilitadas. Si el conmutador `IsSpotsEnabled` muestra "Disabled", actívelo primero; consulte [Activar o desactivar marcas](turn-spots-on-or-off.md).
- Abra el cuadro de diálogo de configuración de marcas haciendo clic derecho en la superposición de marcas en el panadapter.

## Pasos

1. En el cuadro de diálogo de configuración de marcas, localice la fila **Override Colors:**.
2. Haga clic en el botón de conmutación para que muestre **Enabled**. Esto se guarda como `IsSpotsOverrideColorsEnabled`.
3. Haga clic en el botón de muestra de color inmediatamente a la derecha de **Enabled**. Se abrirá un selector de color.
4. Seleccione el color que desea para todas las etiquetas de texto de las marcas y luego haga clic en **OK**.
5. La muestra de color se actualiza para mostrar su color elegido. Todas las marcas en el panadapter se renderizan inmediatamente en ese color. El valor elegido se guarda como `SpotsOverrideColor`.

Para revertir a los colores individuales de las marcas, haga clic nuevamente en el conmutador **Override Colors:** para que muestre **Disabled**.

## Función de cada control

| Control | Valor predeterminado | Clave guardada |
|---|---|---|
| Conmutador **Override Colors:** | Disabled | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto de marcas (botón de muestra) | `#FFFF00` | `SpotsOverrideColor` |
| Conmutador **Spot Lines:** | Enabled | `IsSpotsLinesEnabled` |

## Líneas de marcas

El conmutador **Spot Lines:** dibuja una línea vertical desde la línea de base del espectro hasta cada etiqueta de marca. Está habilitado de forma predeterminada.

Para ocultar las líneas de marcas, haga clic en el conmutador **Spot Lines:** para que muestre **Disabled**. Esto guarda `IsSpotsLinesEnabled` como `False`. Deshabilitar las líneas de marcas es útil durante concursos, donde muchas marcas muy juntas crean desorden visual en el panadapter.

Para restaurar las líneas de marcas, haga clic nuevamente en el conmutador para que muestre **Enabled**.

## Consejos

- El selector de color solo tiene efecto mientras **Override Colors:** muestra **Enabled**. Puede preseleccionar un color mientras el conmutador está en Disabled; se aplicará la próxima vez que habilite la sobrescritura.
- Si el texto de las marcas sigue siendo difícil de leer después de configurar el color, ajuste el contraste del fondo usando los controles **Override Background:** — consulte [Elegir un color de fondo personalizado para marcas](pick-a-custom-background-color-for-spots.md) y [Ajustar la opacidad del fondo de las marcas](adjust-spot-background-opacity.md).
- Durante concursos, deshabilitar **Spot Lines:** mientras mantiene las marcas habilitadas reduce el desorden sin perder las etiquetas de frecuencia.

## Relacionados

- [Activar o desactivar marcas](turn-spots-on-or-off.md)
- [Elegir un color de fondo personalizado para marcas](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de las marcas](adjust-spot-background-opacity.md)
