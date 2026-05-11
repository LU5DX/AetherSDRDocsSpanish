# Exportar memorias para respaldo o compartir

Exporte sus canales de memoria almacenados a un archivo CSV para resguardarlos o compartirlos con otros operadores. Puede exportar todas las memorias de una vez o una selección específica.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo de Canales de Memoria requiere una conexión activa con la radio.
- Debe tener al menos un canal de memoria almacenado en la radio.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo de Canales de Memoria.
2. Seleccione las memorias que desea exportar de la tabla de memorias. Haga clic en una fila para seleccionarla. Mayús+clic para seleccionar un rango. Ctrl+clic (o Comando+clic en macOS) para agregar o eliminar filas individuales.
3. Para exportar todas las memorias, haga clic en `Select All` para seleccionar todas las filas antes de continuar.
4. Haga clic en `Export...`.
5. En el diálogo de archivo que se abre, confirme o cambie la ruta de destino y el nombre del archivo. El nombre de archivo predeterminado tiene el formato `AetherSDR_Memories_<fecha-hora>_v<versión>.csv` y se coloca en la carpeta `Documents` de su usuario.
6. Confirme el guardado. AetherSDR escribe las memorias seleccionadas en el archivo CSV.

## Notas sobre la ventana del diálogo

El diálogo de Canales de Memoria utiliza un diseño de ventana sin marco (añadido en v26.5.1). La barra de título muestra "Memory Channels" con un ícono de agarre en el lado izquierdo. Puede:

- Hacer clic y arrastrar la barra de título para mover el diálogo.
- Hacer doble clic en la barra de título para alternar entre el estado maximizado y restaurado.
- Hacer clic en cualquier borde o esquina y arrastrar para redimensionar el diálogo. El cursor cambia para indicar la dirección de redimensionamiento. La zona de redimensionamiento tiene 12 píxeles de ancho.
- Hacer clic en el botón de minimizar (—) para minimizar el diálogo.
- Hacer clic en el botón de maximizar (□) para maximizar o restaurar el diálogo.
- Hacer clic en el botón de cerrar (×) para cerrar el diálogo. Presione Escape para limpiar primero el campo de búsqueda, luego cierre el diálogo con una segunda pulsación.

## Consejos

- Si desea exportar solo las memorias pertenecientes a un grupo particular, use el cuadro combinado `Profile:` para filtrar la tabla a ese grupo primero, luego haga clic en `Select All` antes de hacer clic en `Export...`.
- El archivo exportado se ordena por frecuencia, luego por índice de memoria interno, independientemente del orden de ordenación actual de la tabla.
- El archivo CSV exportado puede importarse de nuevo a AetherSDR usando `Import...`.

## Relacionado

- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Resumen de Canales de Memoria](overview.md)
