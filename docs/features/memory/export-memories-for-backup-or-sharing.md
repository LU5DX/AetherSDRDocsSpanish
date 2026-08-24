# Exportar memorias para respaldo o uso compartido

Exporte sus canales de memoria guardados a un archivo CSV para mantenerlos a salvo o para compartirlos con otros operadores. Puede exportar todas las memorias a la vez o una selección específica.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Memory Channels requiere una conexión activa con la radio.
- Debe tener al menos un canal de memoria guardado en la radio.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Seleccione las memorias que desea exportar en la tabla de memorias. Haga clic en una fila para seleccionarla. Shift-clic para seleccionar un rango. Ctrl-clic (o Command-clic en macOS) para agregar o quitar filas individuales.
3. Para exportar todas las memorias, haga clic en `Select All` para seleccionar todas las filas antes de continuar.
4. Haga clic en `Export...`.
5. En el diálogo de archivo que se abre, confirme o cambie la ruta de destino y el nombre del archivo. El nombre de archivo predeterminado tiene el formato `AetherSDR_Memories_<fecha-hora>_v<versión>.csv` y se coloca en la carpeta `Documents` de su usuario.
6. Confirme el guardado. AetherSDR escribe las memorias seleccionadas en el archivo CSV.

## Notas sobre la ventana del diálogo

El diálogo Memory Channels utiliza una barra de título personalizada con un fondo de gradiente de 18 px. La barra de título muestra "Memory Channels" con un glifo de agarre en el lado izquierdo. Puede:

- Hacer clic y arrastrar la barra de título para mover el diálogo.
- Hacer doble clic en la barra de título para alternar entre maximizado y restaurado.
- Hacer clic en cualquier borde o esquina y arrastrar para redimensionar el diálogo. El cursor cambia para indicar la dirección del redimensionamiento. La zona de interacción para redimensionar tiene 12 píxeles de ancho mediante FramelessResizer.
- Hacer clic en el botón de minimizar (—) para minimizar el diálogo.
- Hacer clic en el botón de maximizar (□) para maximizar o restaurar el diálogo.
- Hacer clic en el botón de cerrar (×) para cerrar el diálogo. Presione Escape para limpiar primero el campo de búsqueda y luego cierre el diálogo con una segunda pulsación.

El diálogo recuerda su geometría entre sesiones. Cuando se vuelve a abrir, restaura su tamaño y posición anteriores.

La tabla de memorias utiliza colores de fondo temáticos determinados por el tema de la aplicación actual. El color alterno de fila y el resaltado del elemento seleccionado se configuran para coincidir con el esquema de colores del tema activo.

## Edición de memorias

La tabla de memorias muestra las siguientes columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. La tabla se puede ordenar haciendo clic en los encabezados de columna para Frequency, Name o Mode.

Para editar una memoria:

1. Seleccione exactamente una fila de memoria en la tabla.
2. Haga clic en `Edit`, o presione F2 o Ctrl+E. El campo Name entra en modo de edición en línea.
3. Edite los valores del campo directamente en la tabla. Presione Enter para confirmar o Escape para cancelar.

### Edición en línea con delegados de cuadro combinado

A partir de v26.7.4, muchos campos de memoria utilizan editores dedicados de cuadro combinado cuando ingresa al modo de edición en línea. Esto acelera la entrada de datos al presentar una lista de selección de valores válidos, al mismo tiempo que permite la entrada escrita cuando corresponde.

- **Mode, Offset Direction, Tone Mode, Tone Value, Step, Group**: Un cuadro combinado se abre inmediatamente al comenzar a editar la celda. Seleccione un valor de la lista o escriba un valor personalizado.
- **Frequency y Repeater Offset**: Los editores con validación de punto flotante aceptan solo entrada numérica con notación decimal estándar.
- **Rx Filter Low, Rx Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset**: Los editores con validación de enteros aceptan solo números enteros.
- **Name**: Editor de texto simple sin validación.

El cuadro combinado se despliega con un temporizador de cero demora, de modo que elegir un valor es efectivamente un solo clic una vez que la celda está en edición.

### Eliminación de memorias

Para eliminar memorias:

1. Seleccione una o más filas en la tabla. Use Ctrl+Shift+A para seleccionar todas las filas visibles, o presione Delete/Backspace para eliminar las filas seleccionadas.
2. Haga clic en `Remove` (la etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada).
3. Confirme la eliminación cuando se le solicite. Un diálogo de progreso muestra el avance de la eliminación por lotes.

## Búsqueda y filtrado

Use el campo `Search:` en la parte superior del diálogo para filtrar la tabla por nombre de memoria. El campo tiene un botón de limpiar; presione Enter para enviar. Presione Ctrl+F para enfocar el campo de búsqueda.

Use el cuadro combinado `Profile:` para filtrar por un perfil global o de transmisión activo. La lista recopila los nombres de perfil de los perfiles globales y de transmisión de la radio.

## Agregar memorias desde el slice activo

Para crear una nueva memoria desde el slice actualmente activo:

1. Asegúrese de que el slice que desea usar esté activo.
2. Haga clic en `Add` o presione Ctrl+N. Se crea una nueva fila de memoria a partir de la configuración del slice activo.

La variante con insignia de letra de slice se eliminó en v26.8.4; agregar siempre apunta al slice activo.

## Sintonizar una memoria

Para sintonizar el slice activo a una memoria guardada:

1. Seleccione exactamente una fila de memoria en la tabla.
2. Haga clic en `Tune`. El slice activo se sintoniza a la frecuencia guardada.

También puede hacer doble clic en una fila de memoria para sintonizarla directamente.

## Notas sobre la ventana del diálogo

El diálogo Memory Channels utiliza una barra de título personalizada con un fondo de gradiente de 18 px. La barra de título muestra "Memory Channels" con un glifo de agarre en el lado izquierdo. Puede:

- Hacer clic y arrastrar la barra de título para mover el diálogo.
- Hacer doble clic en la barra de título para alternar entre maximizado y restaurado.
- Hacer clic en cualquier borde o esquina y arrastrar para redimensionar el diálogo. El cursor cambia para indicar la dirección del redimensionamiento. La zona de interacción para redimensionar tiene 12 píxeles de ancho mediante FramelessResizer.
- Hacer clic en el botón de minimizar (—) para minimizar el diálogo.
- Hacer clic en el botón de maximizar (□) para maximizar o restaurar el diálogo.
- Hacer clic en el botón de cerrar (×) para cerrar el diálogo. Presione Escape para limpiar primero el campo de búsqueda y luego cierre el diálogo con una segunda pulsación.

El diálogo recuerda su geometría entre sesiones. Cuando se vuelve a abrir, restaura su tamaño y posición anteriores.

El diálogo muestra un indicador de recuento de selección en el formato "<N> de <M> seleccionados" para que pueda realizar un seguimiento de cuántas filas están seleccionadas.

## Consejos

- Si desea exportar solo las memorias que pertenecen a un perfil particular, use el cuadro combinado `Profile:` para filtrar primero la tabla a ese perfil, luego haga clic en `Select All` antes de hacer clic en `Export...`.
- El archivo exportado se ordena por frecuencia y luego por índice de memoria interno, independientemente del orden de clasificación actual de la tabla.
- El archivo CSV exportado se puede importar de nuevo a AetherSDR usando `Import...`.

## Relacionado

- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Descripción general de Memory Channels](overview.md)
