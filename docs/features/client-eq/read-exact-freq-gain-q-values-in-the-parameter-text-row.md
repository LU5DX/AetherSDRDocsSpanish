# Leer los valores exactos de frecuencia, ganancia y Q en la fila de texto de parámetros

La fila de texto de parámetros muestra la frecuencia, la ganancia y el valor Q precisos de cada banda del ecualizador de un solo vistazo. Úsela para confirmar ajustes exactos después de arrastrar bandas en el lienzo, o para identificar qué banda está seleccionada antes de realizar cambios.

## Antes de comenzar

- La fila de texto de parámetros solo es visible en la ventana flotante ClientEqEditor, no en el mosaico del applet acoplado. Abra primero el editor.
- Debe existir al menos una banda de EQ. La fila muestra una columna por ranura de banda, hasta un máximo de ocho bandas.

## Pasos

1. Abra el editor flotante para el lado que desea inspeccionar. Haga doble clic en la etapa de EQ en el widget CHAIN del lado TX o RX. La ventana del editor se titula "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX".
2. Localice la fila de texto de parámetros en la parte inferior del área del lienzo del editor. Muestra una columna por banda, cada una con los valores Freq, Gain y Q de esa banda.
3. Lea los valores directamente. La fila se actualiza en tiempo real mientras arrastra los controles de banda en el lienzo — no se requiere ninguna acción adicional.
4. Para leer los valores de una banda específica, haga clic en su columna en la fila de texto de parámetros. Esto selecciona esa banda, resaltando su control en el lienzo y su ícono en la fila de íconos de tipo de filtro que aparece encima.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de ajuste |
|---|---|---|---|
| Fila de texto de parámetros | Muestra Freq, Gain y Q para cada una de las ocho ranuras de banda. Se actualiza en tiempo real durante los arrastres en el lienzo. Hacer clic en una columna selecciona esa banda. | — | — |
| Fila de íconos de tipo de filtro | Fila de íconos sobre el lienzo, uno por ranura de banda. Hacer clic en un ícono selecciona esa banda y cambia su tipo de filtro en ciclo. La banda seleccionada se resalta tanto en la fila de íconos como en la fila de texto de parámetros. | — | — |

## Consejos

- Arrastrar un control de banda en el lienzo actualiza la fila de texto de parámetros en tiempo real, de modo que puede observar cómo cambian los valores numéricos mientras ajusta el sonido por oído.
- Hacer clic en una columna de la fila de texto de parámetros equivale a hacer clic en el ícono correspondiente en la fila de íconos de tipo de filtro — ambas acciones seleccionan la misma banda.
- Las bandas que están desactivadas (bypass) muestran íconos atenuados (opacidad al 35%) en la fila de íconos; sus valores siguen apareciendo en la fila de texto de parámetros.

## Temas relacionados

- [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Cambiar el tipo de filtro de una banda haciendo clic en su ícono en la fila de íconos](change-a-band-s-filter-type-by-clicking-its-icon-in-the-icon-row.md)
- [Verificar que la curva sumada coincida con el objetivo deseado](verify-the-summed-curve-matches-your-mental-target.md)
