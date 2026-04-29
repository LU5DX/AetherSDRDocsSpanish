# Exportar memorias para respaldo o intercambio

Exporte sus canales de memoria almacenados a un archivo CSV para guardarlos de forma segura o compartirlos con otros operadores. Puede exportar todas las memorias a la vez o una selección específica.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Memory Channels requiere una conexión activa con el radio.
- Debe tener al menos un canal de memoria almacenado en el radio.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Seleccione las memorias que desea exportar desde la tabla de memorias. Haga clic en una fila para seleccionarla. Haga Shift-clic para seleccionar un rango. Haga Ctrl-clic (o Command-clic en macOS) para agregar o quitar filas individuales.
3. Para exportar todas las memorias, haga clic en `Select All` para seleccionar todas las filas antes de continuar.
4. Haga clic en `Export...`.
5. En el diálogo de archivo que se abre, confirme o cambie la ruta de destino y el nombre del archivo. El nombre de archivo predeterminado tiene la forma `AetherSDR_Memories_<date-time>_v<version>.csv` y se coloca en su carpeta `Documents` de inicio.
6. Confirme el guardado. AetherSDR escribe las memorias seleccionadas en el archivo CSV.

## Consejos

- Si desea exportar solo las memorias pertenecientes a un grupo específico, use el cuadro combinado `Profile:` para filtrar la tabla a ese grupo primero, luego haga clic en `Select All` antes de hacer clic en `Export...`.
- El archivo exportado está ordenado por frecuencia y luego por índice interno de memoria, independientemente del orden de clasificación actual de la tabla.
- El archivo CSV exportado puede importarse de nuevo a AetherSDR usando `Import...`.

## Relacionado

- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Descripción general de Memory Channels](overview.md)
