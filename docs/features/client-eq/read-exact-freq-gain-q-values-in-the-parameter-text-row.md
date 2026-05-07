# Leer valores exactos de frecuencia/ganancia/Q en la fila de texto de parámetros

La fila de texto de parámetros muestra la frecuencia, ganancia y valor Q precisos para cada banda EQ de un solo vistazo. Úsela para confirmar ajustes exactos después de arrastrar bandas en el lienzo, o para identificar qué banda está seleccionada antes de realizar ajustes.

## Antes de comenzar

- La fila de texto de parámetros solo es visible en la ventana flotante ClientEqEditor, no en el mosaico acoplado del applet. Abra primero el editor.
- Debe existir al menos una banda EQ. La fila muestra una columna por ranura de banda, hasta un máximo de ocho bandas.

## Pasos

1. Abra el editor flotante para el lado que desea inspeccionar. Haga doble clic en la etapa EQ del widget CHAIN en el lado TX o RX. La ventana del editor se titula "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX".
2. Localice la fila de texto de parámetros en la parte inferior del área del lienzo del editor. Muestra una columna por banda, cada una con los valores de Freq, Gain y Q de esa banda. La fila tiene un fondo transparente para no ocultar la franja del plan de banda de audio ubicada inmediatamente encima en el lienzo.
3. Lea los valores directamente. La fila se actualiza en vivo mientras arrastra los controles de banda en el lienzo; no se requiere ninguna acción adicional.
4. Para leer valores de una banda específica, haga clic en su columna en la fila de texto de parámetros. Esto selecciona esa banda, resaltando su control en el lienzo y su icono en la fila de iconos de tipo de filtro ubicada encima.

## Qué hace cada control

| Control                              | Comportamiento                                                                                                                                                                                                                                                                                                                                                               | Predeterminado                                                                                                                                                                                                                               |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Fila de texto de parámetros          | Muestra Freq, Gain y Q para cada una de las ocho ranuras de banda. Se actualiza en vivo durante los arrastres en el lienzo. Hacer clic en una columna selecciona esa banda. Cada columna tiene un fondo transparente para que la franja del plan de banda en la parte inferior del lienzo permanezca visible sobre la fila.                                                   | —                                                                                                                                                                                                                                            |
| Fila de iconos de tipo de filtro     | Fila de iconos sobre el lienzo, uno por ranura de banda. Hacer clic en un icono selecciona esa banda y cambia cíclicamente su tipo de filtro. La banda seleccionada se resalta tanto en la fila de iconos como en la fila de texto de parámetros.                                                                                                                             | —                                                                                                                                                                                                                                            |
| Suavizado (Smoothing)                | Aplica promediado de potencia por fracción de octava a la traza del analizador para su visualización; no afecta el cálculo EQ. Fracción más baja = más suavizado (1/3 es el máximo suavizado; 1/96 está efectivamente desactivado). Compartido entre los editores TX y RX.                                                                                                  | Tooltip: 'Suavizado por fracción de octava aplicado a la traza del analizador. Fracción más baja = más suavizado (1/3 = máximo, 1/96 = desactivado). Afecta solo la visualización; el cálculo EQ no cambia.' Ubicado en la barra de encabezado del editor (solo editor flotante). |
| Líneas guía de corte de filtro (TX/RX) | Líneas amarillas discontinuas superpuestas en el lienzo en los cortes de filtro bajo/alto actuales de la radio (mosaico TX) o en los bordes de la banda pasante RX (mosaico RX). Al pasar el cursor cerca de una línea, el cursor cambia a una flecha de redimensionamiento horizontal. Arrastrar una línea en el editor mueve el corte de filtro correspondiente de la radio en tiempo real. | Arrastrar las guías de corte TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías RX escribe en el SliceModel activo. Pase 0 para un borde para suprimir esa guía.                         |

## Consejos

- Arrastrar un control de banda en el lienzo actualiza la fila de texto de parámetros en tiempo real, para que pueda observar los valores numéricos cambiar mientras ajusta con el oído.
- Hacer clic en una columna de la fila de texto de parámetros equivale a hacer clic en el icono correspondiente en la fila de iconos de tipo de filtro; ambos seleccionan la misma banda.
- Las bandas que están omitidas (bypassed) muestran iconos atenuados (35 % de opacidad) en la fila de iconos superior; sus valores siguen apareciendo en la fila de texto de parámetros.
- La fila de texto de parámetros y sus columnas de banda individuales usan un fondo transparente. Si en una versión anterior la fila parecía cubrir u oscurecer la franja del plan de banda en la parte inferior del lienzo, esto se ha corregido en v0.9.7.

## Relacionados

- [Abra el editor sin marco para agregar/eliminar/ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Cambie el tipo de filtro de una banda haciendo clic en su icono en la fila de iconos](change-a-band-s-filter-type-by-clicking-its-icon-in-the-icon-row.md)
- [Verifique que la curva sumada coincida con su objetivo mental](verify-the-summed-curve-matches-your-mental-target.md)
