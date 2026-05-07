# Eliminar uno o más recuerdos

Elimine los canales de memoria almacenados que ya no necesite. AetherSDR solicita confirmación antes de eliminar, por lo que ninguna memoria se pierde accidentalmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Canales de memoria requiere una conexión de radio activa.
- Sepa qué memorias desea eliminar. Use el campo Buscar: o Perfil: para reducir primero la lista si es necesario.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Canales de memoria.
2. Seleccione la memoria o memorias que desea eliminar:
   - Haga clic en una sola fila para seleccionarla.
   - Haga clic con la tecla Mayús presionada en una segunda fila para seleccionar un rango contiguo.
   - En Linux y Windows, haga clic con la tecla Ctrl presionada en filas individuales para agregarlas o eliminarlas de la selección. En macOS, use la tecla Comando.
   - Haga clic en Seleccionar todo para seleccionar cada fila mostrada actualmente en la tabla.
3. Confirme su selección verificando el indicador de recuento de selección en el área inferior derecha del diálogo (mostrado como `<N> seleccionados`).
4. Haga clic en Eliminar.
5. Confirme la eliminación en el diálogo de confirmación que aparece.

Las memorias seleccionadas se eliminan permanentemente de la radio.

## Consejos

- Si tiene una lista de memorias larga, use el campo Buscar: o el cuadro combinado Perfil: para filtrar la tabla antes de usar Seleccionar todo. Esto le permite seleccionar y eliminar rápidamente un subconjunto de memorias sin tener que elegir cada fila manualmente.
- La eliminación no se puede deshacer desde dentro de AetherSDR. Exporte sus memorias antes de una eliminación masiva si es posible que las necesite más adelante.

## Relacionados

- [Exportar memorias para respaldo o compartir](export-memories-for-backup-or-sharing.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Descripción general de Canales de memoria](overview.md)
