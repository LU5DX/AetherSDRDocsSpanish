# Ampliar o reducir el tamaño de fuente de los spots

Use esta página para aumentar o disminuir el tamaño del texto de los spots de DX que se muestran en el panadapter. Una fuente más grande facilita la lectura de los indicativos de un vistazo; una fuente más pequeña reduce el desorden visual cuando la banda está ocupada.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a la radio para cambiar este ajuste.
- Abra el cuadro de diálogo Spot Settings haciendo clic derecho sobre la capa de spots en cualquier panadapter.

## Pasos

1. En el cuadro de diálogo Spot Settings, localice la fila **Font Size:**.
2. Arrastre el control deslizante **Font Size:** hacia la izquierda para disminuir el tamaño de fuente, o hacia la derecha para aumentarlo.
3. Lea el valor actual en el indicador numérico a la derecha del control deslizante.
4. Cierre el cuadro de diálogo cuando termine. El cambio surte efecto de inmediato y se guarda automáticamente.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| Control deslizante **Font Size:** | Establece el tamaño del texto de las etiquetas de spots en el panadapter. | 16 | 8 – 32 (pt) | `SpotsFontSize` |

## Consejos

- El valor que aparece junto al control deslizante refleja el tamaño de fuente actual en puntos. El panadapter se actualiza en tiempo real mientras arrastra, de modo que puede evaluar el resultado sin cerrar el cuadro de diálogo.
- Si los spots se superponen con tamaños de fuente más grandes, reduzca el número de filas de apilamiento con el control deslizante **Levels:**, o ajuste el control deslizante **Position:** para dar a los spots más espacio vertical. Consulte [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md).

## Relacionados

- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Descripción general de Spot Settings](overview.md)
