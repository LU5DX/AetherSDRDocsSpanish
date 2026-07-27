# Eliminar uno o más recuerdos

Elimine los canales de memoria almacenados que ya no necesite. AetherSDR solicita confirmación antes de eliminar, por lo que ninguna memoria se pierde accidentalmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Canales de Memoria requiere una conexión activa con la radio.
- Sepa qué recuerdos desea eliminar. Use Buscar: o Perfil: para filtrar primero la lista si es necesario.

## Pasos

1. Abra `Configuración > Memoria...` para abrir el diálogo Canales de Memoria.
2. Seleccione la memoria o las memorias que desea eliminar:
   - Haga clic en una sola fila para seleccionarla.
   - Haga Mayús+clic en una segunda fila para seleccionar un rango contiguo.
   - En Linux y Windows, use Ctrl+clic en filas individuales para agregarlas o eliminarlas de la selección. En macOS, use Comando+clic.
   - Presione Ctrl+Mayús+A o haga clic en Seleccionar Todo para seleccionar todas las filas visibles (respetando búsqueda y filtro).
3. Confirme su selección verificando el indicador de conteo de selección en la parte inferior derecha del diálogo (mostrado como `<N> de <M> seleccionados`).
4. Haga clic en Quitar (la etiqueta del botón cambia a "Quitar Seleccionados" cuando más de una fila está seleccionada). Alternativamente, presione Suprimir o Retroceso.
5. Confirme la eliminación en el diálogo de confirmación que aparece.

Las memorias seleccionadas se eliminan permanentemente de la radio. Para eliminaciones por lotes, un diálogo de progreso muestra el estado de la eliminación.

## Consejos

- Si tiene una lista larga de memorias, use el campo Buscar: o el cuadro combinado Perfil: para filtrar la tabla antes de usar Seleccionar Todo. Esto le permite seleccionar y eliminar rápidamente un subconjunto de memorias sin tener que elegir cada fila manualmente.
- La eliminación no se puede deshacer desde AetherSDR. Exporte sus memorias antes de una eliminación masiva si podría necesitarlas después.
- Presione Escape para limpiar el campo Buscar:; presionar Escape nuevamente cierra el diálogo.
- Haga doble clic en la barra de título para alternar maximizar/restaurar el diálogo.
- Para mover el diálogo, haga clic y arrastre la barra de título. Para redimensionar el diálogo, haga clic y arrastre cualquier borde o esquina — el cursor cambia para indicar la dirección de redimensionamiento. El borde superior está reservado para arrastrar la barra de título; el redimensionamiento desde el borde superior no está disponible en la zona de impacto de 12 px.
- La apariencia del diálogo sigue el tema activo. La tabla de memoria utiliza colores alternados de fila del tema.

## Relacionado

- [Exportar memorias para respaldo o para compartir](exportar-memorias-para-respaldo-o-para-compartir.md)
- [Buscar memorias por nombre](buscar-memorias-por-nombre.md)
- [Filtrar memorias por perfil](filtrar-memorias-por-perfil.md)
- [Importar memorias desde un archivo CSV/JSON](importar-memorias-desde-un-archivo-csv-json.md)
- [Descripción general de Canales de Memoria](descripcion-general.md)
