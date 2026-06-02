# Forzar un color de texto único para todos los spots

Anule los colores individuales asignados por su fuente de clúster DX y renderice todas las etiquetas de spots en un único color elegido. Útil cuando los colores predeterminados no combinan con el tema de su panadapter o son difíciles de leer.

## Antes de comenzar

- Los spots deben estar habilitados. Si el conmutador `IsSpotsEnabled` muestra "Disabled", actívelo primero; consulte [Activar o desactivar spots](turn-spots-on-or-off.md).
- Abra el cuadro de diálogo Spot Settings haciendo clic derecho en la superposición de spots del panadapter.

## Pasos

1. En el cuadro de diálogo Spot Settings, localice la fila **Override Colors:**.
2. Haga clic en el botón conmutador para que muestre **Enabled**. Este cambio se guarda como `IsSpotsOverrideColorsEnabled`.
3. Haga clic en la muestra de color que está justo a la derecha de **Enabled**. Se abrirá un cuadro de diálogo selector de color.
4. Seleccione el color que desee para todas las etiquetas de texto de spots y luego haga clic en **OK**.
5. La muestra se actualizará para mostrar el color elegido. Todos los spots del panadapter se renderizarán inmediatamente en ese color. El valor elegido se guarda como `SpotsOverrideColor`.

Para revertir a los colores individuales por spot, vuelva a hacer clic en el conmutador **Override Colors:** para que muestre "Disabled".

## Qué hace cada control

| Control | Valor predeterminado | Clave guardada |
|---|---|---|
| Conmutador **Override Colors:** | Disabled | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto de spots (botón de muestra) | `#FFFF00` | `SpotsOverrideColor` |
| Conmutador **Spot Lines:** | Enabled | `IsSpotsLinesEnabled` |

## Líneas de spots

El conmutador **Spot Lines:** dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot. Está habilitado de forma predeterminada.

Para ocultar las líneas de spots, haga clic en el conmutador **Spot Lines:** para que muestre "Disabled". Esto guarda `IsSpotsLinesEnabled` como `False`. Deshabilitar las líneas de spots es útil durante concursos donde muchos spots muy cercanos entre sí crean desorden visual en el panadapter.

Para restaurar las líneas de spots, vuelva a hacer clic en el conmutador para que muestre "Enabled".

## Consejos

- El selector de color solo tiene efecto mientras **Override Colors:** muestra **Enabled**. Puede preseleccionar un color mientras el conmutador todavía está en Disabled; se aplicará la próxima vez que active la anulación.
- Si el texto de los spots sigue siendo difícil de leer después de configurar el color, ajuste el contraste del fondo usando los controles de **Override Background:** — consulte [Elegir un color de fondo personalizado para spots](pick-a-custom-background-color-for-spots.md) y [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md).
- Durante concursos, deshabilitar **Spot Lines:** mientras se mantienen los spots habilitados reduce el desorden sin perder las etiquetas de frecuencia.

## Relacionados

- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Elegir un color de fondo personalizado para spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
