# Exportar memorias para respaldo o compartir

Exporte sus canales de memoria almacenados a un archivo CSV para guardarlos o compartirlos con otros operadores. Puede exportar todas las memorias a la vez o una selección específica.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Memory Channels requiere una conexión activa con la radio.
- Debe tener al menos un canal de memoria almacenado en la radio.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Seleccione las memorias que desea exportar de la tabla de memorias. Haga clic en una fila para seleccionarla. Mayús+clic para seleccionar un rango. Ctrl+clic (o Comando+clic en macOS) para agregar o eliminar filas individuales.
3. Para exportar todas las memorias, haga clic en `Select All` para seleccionar todas las filas antes de continuar.
4. Haga clic en `Export...`.
5. En el diálogo de archivo que se abre, confirme o cambie la ruta de destino y el nombre del archivo. El nombre de archivo predeterminado tiene el formato `AetherSDR_Memories_<fecha-hora>_v<versión>.csv` y se coloca en la carpeta `Documents` de su usuario.
6. Confirme el guardado. AetherSDR escribe las memorias seleccionadas en el archivo CSV.

## Notas sobre la ventana del diálogo

El diálogo Memory Channels utiliza una barra de título personalizada con un fondo degradado de 18 px. La barra de título muestra "Memory Channels" con un glifo de agarre en el lado izquierdo. Puede:

- Hacer clic y arrastrar la barra de título para mover el diálogo.
- Hacer doble clic en la barra de título para alternar entre el estado maximizado y restaurado.
- Hacer clic en cualquier borde o esquina y arrastrar para redimensionar el diálogo. El cursor cambia para indicar la dirección de redimensionamiento. La zona de ajuste de redimensionamiento tiene 12 píxeles de ancho a través de FramelessResizer.
- Hacer clic en el botón minimizar (—) para minimizar el diálogo.
- Hacer clic en el botón maximizar (□) para maximizar o restaurar el diálogo.
- Hacer clic en el botón cerrar (×) para cerrar el diálogo. Presione Escape para borrar primero el campo de búsqueda, luego cierre el diálogo con una segunda pulsación.

El diálogo recuerda su geometría entre sesiones. Cuando se reabre, restaura su tamaño y posición anteriores.

La tabla de memorias utiliza colores de fondo temáticos determinados por el tema actual de la aplicación. El color de fila alterna y el resaltado del elemento seleccionado se configuran para coincidir con el esquema de colores del tema activo.

## Edición en línea con delegados de cuadro combinado

A partir de v26.7.4, muchos campos de memoria utilizan editores de cuadro combinado dedicados cuando ingresa al modo de edición en línea. Esto acelera la entrada de datos al presentar una lista de selección de valores válidos, y al mismo tiempo permite la entrada escrita cuando corresponde.

- **Mode, Offset Direction, Tone Mode, Tone Value, Step, Group**: Un cuadro combinado se abre inmediatamente cuando comienza a editar la celda. Seleccione un valor de la lista o escriba un valor personalizado.
- **Frequency y Repeater Offset**: Editores validados para flotantes que solo aceptan entrada numérica con notación decimal estándar.
- **Rx Filter Low, Rx Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset**: Editores validados para enteros que solo aceptan números enteros.
- **Name**: Editor de texto plano sin validación.

El cuadro combinado se abre con un temporizador de retardo cero, por lo que seleccionar un valor es efectivamente un solo clic una vez que la celda está siendo editada.

## Consejos

- Si desea exportar solo las memorias pertenecientes a un perfil particular, use el cuadro combinado `Profile:` para filtrar primero la tabla a ese perfil, luego haga clic en `Select All` antes de hacer clic en `Export...`.
- El archivo exportado está ordenado por frecuencia y luego por índice de memoria interno, independientemente del orden de clasificación actual de la tabla.
- El archivo CSV exportado se puede importar nuevamente a AetherSDR usando `Import...`.

## Relacionado

- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Resumen de Memory Channels](overview.md)
