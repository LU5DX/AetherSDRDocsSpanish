# Editar el nombre de una memoria en línea

Cambie el nombre de un canal de memoria almacenado directamente en la tabla de Memorias sin abrir un cuadro de diálogo separado.

## Antes de comenzar

- Abra **Settings > Memory...** para mostrar el cuadro de diálogo Memory Channels.
- La radio debe estar conectada.

## Pasos

1. Haga clic en una fila de la tabla de Memorias para seleccionarla. Solo se puede editar una memoria a la vez.

2. Realice una de las siguientes acciones para entrar en el modo de edición en línea del campo Nombre:
   - Haga clic en **Edit**.
   - Presione **F2** o **Ctrl+E**.

3. Escriba el nuevo nombre.

4. Presione **Enter** para confirmar, o presione **Esc** para cancelar.

## Función de cada control

| Control | Comportamiento |
|---------|----------------|
| Botón **Edit** | Entra en modo de edición en línea en la columna Nombre de la memoria seleccionada. Solo está habilitado cuando hay exactamente una memoria seleccionada. |
| **F2** / **Ctrl+E** | Atajo de teclado que activa el mismo modo de edición que el botón **Edit**. |

## Consejos

- La columna Nombre admite hasta el límite de caracteres establecido por el firmware de la radio. AetherSDR codifica el nombre según lo requiera el protocolo SmartSDR.
- Para cancelar la edición, presione **Esc** antes de presionar Enter.
- El cuadro de diálogo Memory Channels utiliza un marco **PersistentDialog** que recuerda su tamaño y posición entre sesiones. La geometría se almacena en la configuración `MemoryDialogGeometry` y se restaura la próxima vez que se abra el cuadro de diálogo.

## Relacionado

- [Resumen de canales de memoria](overview.md)
- [Agregar una memoria desde la sintonizadora activa](add-a-memory-from-the-active-slice.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
- [Sintonizar la radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
