# Buscar todas las acciones en una categoría

El cuadro de diálogo Atajos de teclado incluye un filtro de categorías que reduce la tabla de acciones a un solo grupo de acciones relacionadas. Úselo cuando desee revisar o editar todas las combinaciones en un área; por ejemplo, todas las acciones de VFO o todas las acciones del panadapter, sin desplazarse por la lista completa.

## Antes de comenzar

- No se requiere conexión de radio.
- Abra el cuadro de diálogo mediante `View > Configure Shortcuts...`.

## Pasos

1. Abra `View > Configure Shortcuts...`.
2. En la fila de filtros sobre la tabla de acciones, localice el cuadro combinado **Category:**.
3. Haga clic en **Category:** y seleccione la categoría que desea ver.
4. La tabla de acciones se actualiza inmediatamente para mostrar solo las acciones de esa categoría, con las columnas **Action**, **Category**, **Current Key** y **Default Key**.
5. Para volver a la lista completa, establezca **Category:** en **All**.

## Consejos

- Puede combinar **Category:** con el campo de texto **Filter:** para reducir aún más los resultados. Ambos filtros se aplican simultáneamente: la tabla muestra solo las filas que coinciden tanto con el texto como con la categoría seleccionada.
- El mapa de teclado sobre la tabla utiliza teclas codificadas por colores según la categoría. La fila de leyenda debajo del mapa identifica qué color pertenece a cada categoría, para que pueda identificar las teclas de una categoría de un vistazo antes de abrir el filtro.
- El cuadro de diálogo ahora admite estilos adaptables al tema. Los colores de las etiquetas de teclas, las etiquetas de categorías y la tecla seleccionada se adaptan automáticamente al tema actual.

## Importar y exportar atajos de teclado

El cuadro de diálogo incluye los botones **Import...** y **Export...** en la fila inferior de botones. Úselos para transferir sus combinaciones de atajos de teclado personalizadas entre instalaciones de AetherSDR o para compartirlas con otros operadores.

### Exportar atajos

1. Abra `View > Configure Shortcuts...`.
2. Haga clic en **Export...**.
3. En el cuadro de diálogo de archivos, elija una ubicación y un nombre para el archivo CSV. El cuadro de diálogo recuerda el último directorio que usó.
4. Haga clic en **Save**. AetherSDR escribe un archivo CSV que contiene el nombre de la acción, la tecla actual y la tecla predeterminada para cada combinación.

### Importar atajos

1. Abra `View > Configure Shortcuts...`.
2. Haga clic en **Import...**.
3. En el cuadro de diálogo de archivos, busque y seleccione un archivo CSV exportado anteriormente.
4. Haga clic en **Open**. AetherSDR lee el archivo y aplica las combinaciones importadas.

   - Si una acción en el archivo no existe en su versión de AetherSDR, se omite y se enumera en el resumen de importación.
   - Si una combinación importada usa una tecla que ya está asignada, la combinación local existente para esa tecla se borra (se desplaza) y se enumera en el resumen.
5. Después de la importación, la tabla de acciones y el mapa de teclado se actualizan para mostrar las nuevas combinaciones. Un cuadro de mensaje informa la cantidad de acciones importadas y, si corresponde, la cantidad de combinaciones omitidas o desplazadas. Haga clic en **Show Details...** para ver las listas completas.

## Relacionado

- [Descripción general de los atajos de teclado](overview.md)
- [Reasignar un atajo de teclado](rebind-a-keyboard-shortcut.md)
- [Ver la tecla predeterminada para cualquier acción](see-the-default-key-for-any-action.md)
