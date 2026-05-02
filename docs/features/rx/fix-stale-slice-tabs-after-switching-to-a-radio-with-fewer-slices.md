# Solucionar pestañas de slice obsoletas al cambiar a una radio con menos slices

Cuando se desconecta de una radio y se conecta a otra que tiene menos slices, la fila de pestañas de slice del applet RX (botones de la A a la H) puede seguir mostrando pestañas de la sesión anterior. Esta página explica cómo eliminar esas pestañas obsoletas y restaurar un estado limpio.

## Antes de comenzar

- Ya se ha desconectado de la primera radio y está conectado, o está a punto de conectarse, a una segunda radio con menos slices disponibles.
- El applet RX es visible en el Panel de Applets. Si no lo es, haga clic en el botón de bandeja **RX** de la barra lateral derecha.

## Pasos

1. Desconéctese de la radio actual si aún no lo ha hecho. Use `Settings > Connect to Radio...` para abrir el diálogo de conexión, luego cierre o cancele la conexión existente.
2. Observe la fila de pestañas de slice en la parte superior del applet RX. Si las pestañas de la radio anterior (por ejemplo, A, B, C, D) siguen apareciendo, están obsoletas.
3. Conéctese a la nueva radio usando `Settings > Connect to Radio...` y seleccione la radio de destino.
4. Una vez establecida la nueva conexión, AetherSDR ejecuta `clearSliceButtons()` internamente al desconectarse, lo cual elimina todos los botones de pestañas de slice generados y restaura la insignia de slice estática. La fila de pestañas de slice se volverá a poblar para coincidir con el número máximo de slices de la nueva radio.
5. Confirme que la fila de pestañas de slice ahora muestra solo el número correcto de pestañas (limitado al máximo de hardware de la nueva radio). Si la nueva radio admite un solo slice, la fila de pestañas se oculta por completo y solo se muestra la insignia de slice.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX. La fila se oculta cuando el número máximo de slices de la radio es 1 o menos. Al desconectarse, todos los botones de pestañas generados se eliminan y se restaura la insignia de slice estática. | — | — |
| Insignia de slice | Muestra la letra del slice vinculado actualmente. Se muestra en todo momento; es el único indicador de slice visible cuando la fila de pestañas está oculta. | A | — |

## Consejos

- Los botones de pestañas de slice están limitados por el máximo de hardware de la radio conectada. Una radio que admite dos slices nunca mostrará más de dos pestañas, independientemente de lo que tuviera la radio anterior.
- Las conexiones duplicadas de manejadores de señal están protegidas entre reconexiones, por lo que reconectarse a la misma radio múltiples veces no multiplicará las respuestas a los clics en las pestañas.

## Solución de problemas

- **Las pestañas obsoletas permanecen después de reconectarse** — Esto puede ocurrir si el evento de desconexión no se ejecutó correctamente. Desconéctese de nuevo usando `Settings > Connect to Radio...`, espere a que la insignia de slice reaparezca en lugar de las pestañas y luego reconéctese.
- **La fila de pestañas desaparece por completo al conectarse** — Si la nueva radio reporta un número máximo de slices de 1 o menos, la fila de pestañas se oculta intencionalmente. Solo se muestra la insignia de slice. Este es el comportamiento esperado.

## Relacionado

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Descripción general de los controles RX](overview.md)
- [Comprender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
