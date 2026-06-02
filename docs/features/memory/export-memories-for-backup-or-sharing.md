# Exportar memorias para respaldo o compartir

Exporte sus canales de memoria almacenados a un archivo CSV para guardarlos de forma segura o compartirlos con otros operadores. Puede exportar todas las memorias de una vez o una selección específica.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El cuadro de diálogo Canales de memoria requiere una conexión activa con el radio.
- Debe tener al menos un canal de memoria almacenado en el radio.

## Pasos

1. Abra `Settings > Memory...` para abrir el cuadro de diálogo Canales de memoria.
2. Seleccione las memorias que desea exportar de la tabla de memorias. Haga clic en una fila para seleccionarla. Mayús+clic para seleccionar un rango. Ctrl+clic (o Comando+clic en macOS) para agregar o eliminar filas individuales.
3. Para exportar todas las memorias, haga clic en `Select All` para seleccionar todas las filas antes de continuar.
4. Haga clic en `Export...`.
5. En el cuadro de diálogo de archivo que se abre, confirme o cambie la ruta de destino y el nombre del archivo. El nombre de archivo predeterminado tiene el formato `AetherSDR_Memorias_<fecha-hora>_v<versión>.csv` y se coloca en la carpeta `Documentos` de su directorio de usuario.
6. Confirme el guardado. AetherSDR escribe las memorias seleccionadas en el archivo CSV.

## Notas sobre la ventana del cuadro de diálogo

El cuadro de diálogo Canales de memoria utiliza una barra de título personalizada con un fondo degradado de 18 px. La barra de título muestra "Memory Channels" con un glifo de agarre en el lado izquierdo. Puede:

- Haga clic y arrastre la barra de título para mover el cuadro de diálogo.
- Haga doble clic en la barra de título para alternar entre el estado maximizado y restaurado.
- Haga clic en cualquier borde o esquina y arrastre para cambiar el tamaño del cuadro de diálogo. El cursor cambia para indicar la dirección de redimensionamiento. La zona de ajuste de redimensionamiento tiene 12 píxeles de ancho mediante FramelessResizer.
- Haga clic en el botón de minimizar (—) para minimizar el cuadro de diálogo.
- Haga clic en el botón de maximizar (□) para maximizar o restaurar el cuadro de diálogo.
- Haga clic en el botón de cerrar (×) para cerrar el cuadro de diálogo. Presione Escape para limpiar primero el campo de búsqueda, luego cierre el cuadro de diálogo con una segunda pulsación.

El cuadro de diálogo recuerda su geometría entre sesiones. Cuando se vuelve a abrir, restaura su tamaño y posición anteriores.

La tabla de memorias utiliza colores de fondo temáticos determinados por el tema de aplicación activo. El color de fila alterno y el resaltado del elemento seleccionado se configuran para coincidir con el esquema de colores del tema activo.

## Consejos

- Si desea exportar solo las memorias que pertenecen a un perfil específico, use el cuadro combinado `Profile:` para filtrar primero la tabla a ese perfil, luego haga clic en `Select All` antes de hacer clic en `Export...`.
- El archivo exportado se ordena por frecuencia, luego por índice de memoria interno, independientemente del orden de clasificación actual de la tabla.
- El archivo CSV exportado se puede importar nuevamente a AetherSDR usando `Import...`.

## Relacionado

- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Descripción general de Canales de memoria](overview.md)
