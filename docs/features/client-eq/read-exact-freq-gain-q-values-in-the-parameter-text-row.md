# Leer valores exactos de frecuencia/ganancia/Q en la fila de texto de parámetros

La fila de texto de parámetros muestra la frecuencia, ganancia y valor Q precisos para cada banda de EQ de un solo vistazo. Úsela para confirmar ajustes exactos después de arrastrar bandas en el lienzo, o para identificar qué banda está seleccionada antes de realizar ajustes.

## Antes de comenzar

- La fila de texto de parámetros solo es visible en la ventana flotante ClientEqEditor, no en el mosaico acoplado de la applet. Abra primero el editor.
- Debe existir al menos una banda de EQ. La fila muestra una columna por ranura de banda, hasta ocho bandas.

## Pasos

1. Abra el editor flotante para el lado que desea inspeccionar. Haga doble clic en la etapa EQ del widget CHAIN en el lado TX o RX. La ventana del editor se titula "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX".
2. Localice la fila de texto de parámetros en la parte inferior del área del lienzo del editor. Muestra una columna por banda, cada una con los valores de Freq, Gain y Q de esa banda. La fila tiene un fondo transparente para no oscurecer la franja del plan de frecuencias de audio justo encima de ella en el lienzo.
3. Lea los valores directamente. La fila se actualiza en vivo mientras arrastra los controles de banda en el lienzo; no se requiere ninguna acción adicional.
4. Para leer los valores de una banda específica, haga clic en su columna en la fila de texto de parámetros. Esto selecciona esa banda, resaltando su control en el lienzo y su icono en la fila de iconos de tipo de filtro superior.

## Editar parámetros de banda numéricamente

Puede escribir valores exactos de frecuencia, ganancia o Q para cualquier banda directamente en la fila de texto de parámetros. Esto es útil para ajustes precisos que son difíciles de lograr arrastrando.

1. Haga clic derecho en una columna de la fila de texto de parámetros para abrir el menú de entrada numérica.
2. Elija el parámetro que desea editar: Freq, Gain o Q.
3. Escriba el nuevo valor y presione Enter. El cambio se confirma de inmediato, los ajustes de EQ se guardan y la curva del lienzo se redibuja para reflejar el nuevo valor.

## Qué hace cada control

| Control                              | Comportamiento                                                                                                                                                                                                                                                                                                         | Valor predeterminado                                                                                                                                                                                                              |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Fila de texto de parámetros          | Muestra Freq, Gain y Q para cada una de las ocho ranuras de banda. Se actualiza en vivo durante los arrastres en el lienzo. Al hacer clic en una columna se selecciona esa banda. Haga clic derecho en una columna para editar cualquier parámetro numéricamente mediante un menú contextual. Cada columna tiene un fondo transparente para que la franja del plan de frecuencias en la parte inferior del lienzo permanezca visible sobre la fila. | —                                                                                                                                                                                                                                 |
| Fila de iconos de tipo de filtro     | Fila de iconos sobre el lienzo, uno por ranura de banda. Al hacer clic en un icono se selecciona esa banda y se cicla su tipo de filtro. La banda seleccionada se resalta tanto en la fila de iconos como en la fila de texto de parámetros.                                                                              | —                                                                                                                                                                                                                                 |
| Suavizado (Smoothing)                | Aplica promediado de potencia en fracción de octava a la traza del analizador para visualización, no afecta el cálculo de EQ. Fracción más baja = más suave (1/3 es lo más suave; 1/96 está efectivamente desactivado). Compartido entre los editores TX y RX.                                                          | Tooltip: 'Suavizado de fracción de octava aplicado a la traza del analizador. Fracción más baja = más suave (1/3 = más, 1/96 = desactivado). Afecta solo la visualización: el cálculo de EQ no cambia.' Ubicado en la franja del encabezado del editor (solo editor flotante). |
| Retención de pico (Peak Hold)        | Cuando está marcada, la traza de retención de pico por bin en el analizador deja de decaer; el nivel más alto observado de cada frecuencia se mantiene hasta que se desactiva el botón. | Fondo ámbar cuando está marcada. Ubicado en la franja del encabezado del editor (solo editor flotante, no en el mosaico acoplado de la applet). |
| Familia de filtros (Filter family)   | Selecciona las matemáticas de la cascada HP/LP. Butterworth = banda de paso máximamente plana; Chebyshev = caída más abrupta con 1 dB de rizado en banda de paso; Bessel = fase lineal / caída más suave; Elliptic = transición más abrupta con rizado en ambas bandas. | Butterworth. Se aplica solo a los tipos de filtro HP y LP; las bandas de pico y shelving usan su propia topología fija de segundo orden independientemente. Se conserva por separado por ruta: `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. Ubicado en la franja del encabezado del editor. |
| Restablecer (Reset)                  | Restablece todas las bandas a la plantilla predeterminada de 10 bandas, restaura el número de bandas predeterminado y restablece la familia de filtros a Butterworth. Se guarda inmediatamente. | Tooltip: 'Restablecer todas las bandas a los valores predeterminados'. Ubicado en la franja del encabezado del editor (solo editor flotante). |
| Fader de salida (Output Fader)       | Fader vertical combinado + medidor de nivel en el borde derecho del editor flotante. Arrastre para ajustar la ganancia maestra posterior a EQ; la rueda de desplazamiento ajusta en pasos de 0.5 dB; doble clic restablece a 0 dB. Haga clic en la visualización del valor para editar la ganancia numéricamente: escriba un valor en dB y presione Enter o haga clic fuera para confirmar. La barra de nivel detrás del control muestra el pico posterior a EQ suavizado en tiempo real con el mismo gradiente verde-ámbar-rojo que el medidor de nivel del tubo. | 0 dB (lineal 1.0). Rango -36.0 a +12.0 dB. Tooltip: 'Ganancia de salida (dB). Arrastre para ajustar, rueda para paso fino, doble clic para restablecer a 0 dB. Haga clic en el valor para escribir dB exactos.' Se conserva por separado por ruta: `ClientEqTxMasterGain` / `ClientEqRxMasterGain`. Ubicado solo en el editor flotante, no en el mosaico acoplado de la applet. |
| Guías de límite de filtro (TX / RX)  | Líneas verticales amarillas discontinuas superpuestas en el lienzo en el corte de filtro bajo/alto actual de TX (mosaico TX) o en los bordes de la banda de paso de RX (mosaico RX). Al pasar el cursor cerca de una línea, el cursor cambia a una flecha de cambio de tamaño horizontal. Arrastrar una línea en el editor mueve el corte de filtro correspondiente de la radio en tiempo real. | Arrastrar las guías de corte de TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías de RX escribe en el SliceModel activo. Pase 0 para un borde para suprimir esa guía. |

## Consejos

- Arrastrar un control de banda en el lienzo actualiza la fila de texto de parámetros en tiempo real, para que pueda observar los valores numéricos cambiar mientras ajusta de oído.
- Hacer clic en una columna de la fila de texto de parámetros equivale a hacer clic en el icono correspondiente en la fila de iconos de tipo de filtro: ambos seleccionan la misma banda.
- Las bandas que están omitidas (bypassed) muestran iconos atenuados (35 % de opacidad) en la fila de iconos superior; sus valores aún aparecen en la fila de texto de parámetros.
- La fila de texto de parámetros y sus columnas de banda individuales usan un fondo transparente. Si la fila parecía cubrir u oscurecer la franja del plan de frecuencias en la parte inferior del lienzo en una versión anterior, esto se corrigió en v0.9.7.
- Haga clic derecho en una columna para ingresar valores numéricos exactos en lugar de arrastrar; útil para ajustes precisos de filtro.
- La visualización del valor del Fader de salida ahora es un campo de texto en línea. Haga clic en el valor dB mostrado para editarlo directamente. Presione Enter o haga clic fuera para confirmar el valor. Presione Escape para cancelar la edición y restaurar el valor anterior.

## Relacionados

- [Abrir el editor sin marco para agregar/eliminar/ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Cambiar el tipo de filtro de una banda haciendo clic en su icono en la fila de iconos](change-a-band-s-filter-type-by-clicking-its-icon-in-the-icon-row.md)
- [Verificar que la curva sumada coincida con su objetivo mental](verify-the-summed-curve-matches-your-mental-target.md)
