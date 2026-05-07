# Exportar memorias para copia de seguridad o para compartir

Exporte sus canales de memoria almacenados a un archivo CSV para guardarlos de forma segura o para compartirlos con otros operadores. Puede exportar todas las memorias a la vez o una selección específica.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El cuadro de diálogo de Canales de Memoria requiere una conexión activa con la radio.
- Debe tener al menos un canal de memoria almacenado en la radio.

## Pasos

1. Abra `Settings > Memory...` para abrir el cuadro de diálogo de Canales de Memoria.
2. Seleccione las memorias que desea exportar de la tabla de memorias. Haga clic en una fila para seleccionarla. Mayús+clic para seleccionar un rango. Ctrl+clic (o Comando+clic en macOS) para agregar o eliminar filas individuales.
3. Para exportar cada memoria, haga clic en `Select All` para seleccionar todas las filas antes de continuar.
4. Haga clic en `Export...`.
5. En el cuadro de diálogo de archivo que se abre, confirme o cambie la ruta de destino y el nombre del archivo. El nombre de archivo predeterminado tiene la forma `AetherSDR_Memories_<fecha-hora>_v<versión>.csv` y se coloca en su carpeta `Documents` del usuario.
6. Confirme el guardado. AetherSDR escribe las memorias seleccionadas en el archivo CSV.

## Consejos

- Si desea exportar solo las memorias que pertenecen a un grupo en particular, use el cuadro combinado `Profile:` para filtrar primero la tabla a ese grupo, luego haga clic en `Select All` antes de hacer clic en `Export...`.
- El archivo exportado se ordena por frecuencia, luego por índice de memoria interno, independientemente del orden de clasificación actual de la tabla.
- El archivo CSV exportado se puede importar de nuevo a AetherSDR usando `Import...`.

## Relacionado

- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Resumen de Canales de Memoria](overview.md)
