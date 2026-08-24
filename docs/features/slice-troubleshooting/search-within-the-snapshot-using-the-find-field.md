# Búsqueda dentro de la instantánea mediante el campo Buscar

Use el campo Buscar (Find) en el cuadro de diálogo Solución de problemas de slices para localizar texto específico dentro de la pestaña actual, ya sea el Resumen del problema o la instantánea JSON. Esto le permite saltar rápidamente a un ID de slice, nombre de antena o mensaje de error en particular sin desplazarse por todo el contenido.

## Antes de comenzar

- Debe haber una conexión de radio activa.
- Abra el cuadro de diálogo Solución de problemas de slices mediante `Help > Slice Troubleshooting...`.

## Pasos

1. Abra el cuadro de diálogo Solución de problemas de slices usando `Help > Slice Troubleshooting...`.
2. Seleccione la pestaña que desea buscar: **Issue Summary** o **JSON**.
3. Haga clic en el campo **Find:** (texto de marcador de posición: "Search snapshot...").
4. Escriba el texto que desea localizar. El campo tiene un botón de borrar (X) para eliminar su entrada.
5. Presione **Enter** o haga clic en **Find Next** para saltar a la siguiente coincidencia. La búsqueda se envuelve dentro de la pestaña actual.
6. Lea la etiqueta de estado debajo del campo de búsqueda: muestra `<N> match(es) in current tab.` El número se actualiza mientras escribe.

## Qué hace cada control

| Control | Comportamiento |
| --- | --- |
| **Find:** | Campo de texto para ingresar un término de búsqueda. Resalta las coincidencias en la pestaña activa. Los términos vacíos no producen coincidencias. |
| **Find Next** | Salta a la siguiente coincidencia del término de búsqueda en la pestaña activa. Se envuelve dentro de la pestaña actual. |
| Etiqueta de estado | Muestra la cantidad de coincidencias en la pestaña actual, p. ej. "5 match(es) in current tab." También muestra resultados de copia/exportación como "Copied to clipboard". |

## Consejos

- La búsqueda se limita únicamente a la pestaña activa: cambie de pestaña para buscar en el contenido de esa pestaña.
- Dado que la búsqueda se envuelve, puede recorrer todas las coincidencias haciendo clic repetidamente en **Find Next** o presionando **Enter**.

## Relacionado

- [Descripción general de Solución de problemas de slices](overview.md)
- [Capturar una instantánea de slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntarlo a un informe de errores](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
