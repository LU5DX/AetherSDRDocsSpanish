# Congele la traza de retención de pico del analizador para localizar resonancias mientras ajusta

La traza de retención de pico marca el nivel de energía más alto observado en cada frecuencia desde el último reinicio. Congelarla detiene la caída normal de ~10 dB/segundo para que la traza permanezca estacionaria mientras ajusta las bandas de EQ o los bordes de la banda pasante — facilitando la identificación de resonancias y picos agresivos.

## Antes de comenzar

- Abra el editor flotante para el lado TX o RX de EQ. El botón `Peak Hold` está únicamente en la barra de encabezado del editor — no está disponible en el mosaico acoplado de la aplicación. Consulte [Open the frameless editor to add / remove / tune bands on either side](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).
- Asegúrese de que el audio esté pasando por la ruta de EQ para que el analizador FFT en vivo esté activo y la traza de retención de pico esté acumulando datos.

## Pasos

1. Abra el editor flotante para el lado que desea inspeccionar (TX o RX) haciendo doble clic en la etapa de EQ en el widget CHAIN.
2. Deje que el audio se ejecute durante unos segundos para que la traza de retención de pico se construya en todo el rango de frecuencia.
3. Haga clic en `Peak Hold` en la barra de encabezado del editor. El botón se vuelve ámbar para confirmar que está marcado.
4. Ajuste sus bandas de EQ, frecuencias de corte del filtro u otras configuraciones mientras lee la traza congelada. La traza permanece estacionaria independientemente del nivel de señal actual.
5. Vuelva a hacer clic en `Peak Hold` para desmarcarlo. La traza reanuda la caída normal (~10 dB/segundo).

## Qué hace cada control

| Control                             | Ubicación                                                                                                                                                                                                                                                                                                                                                                        | Valor predeterminado                                                                                                                                                                                                              |
|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Peak Hold`                         | Barra de encabezado del editor                                                                                                                                                                                                                                                                                                                                                   | Sin marcar                                                                                                                                                                                                                        |
| `Smoothing`                         | Barra de encabezado del editor                                                                                                                                                                                                                                                                                                                                                   | `Off (1/96)`                                                                                                                                                                                                                      |
| Smoothing                           | Aplica un promediado de potencia de octava fraccional a la traza del analizador para su visualización — no afecta los cálculos de EQ. Fracción más baja = más suavizado (1/3 es lo más suavizado; 1/96 está efectivamente desactivado). Compartido entre los editores TX y RX.                                                                                                  | Tooltip: 'Fractional-octave smoothing applied to the analyzer trace. Lower fraction = smoother (1/3 = most, 1/96 = off). Affects display only — EQ math is unchanged.' Ubicado en la barra de encabezado del editor (solo editor flotante). |
| Fila de iconos de tipo de filtro    | Una fila de 8 iconos pintados personalizados (uno por ranura de banda) en la parte superior del área del lienzo del editor. Cada icono dibuja la forma del filtro actual (campana de pico, rampa de estante, pendiente HP/LP) en el color de la paleta de su banda. Haga clic en un icono para recorrer los tipos de filtro para esa banda; al hacer clic también selecciona la banda, resaltando su manija en el lienzo y su columna en la fila de parámetros. | Ubicado solo en el editor flotante. Los iconos se atenúan al 35 % de opacidad cuando la banda está desviada. Implementado por ClientEqIconRow.                                                                                 |
| Fila de texto de parámetros         | Una fila de 8 columnas de texto (una por ranura de banda) debajo del lienzo que muestra los valores de Frecuencia, Ganancia y Q de cada banda. Los valores se actualizan en vivo durante los arrastres en el lienzo. Al hacer clic en una columna se selecciona esa banda.                                                                                                        | Ubicado solo en el editor flotante. Implementado por ClientEqParamRow.                                                                                                                                                             |
| Líneas guía de corte de filtro (TX / RX) | Líneas amarillas discontinuas verticales superpuestas en el lienzo en los cortes de filtro alto/bajo de TX actuales de la radio (mosaico TX) o los bordes de la banda pasante de RX (mosaico RX). Al pasar el cursor cerca de una línea, el cursor cambia a una flecha de redimensionamiento horizontal. Arrastrar una línea en el editor mueve el corte de filtro correspondiente de la radio en tiempo real.                                        | Arrastrar las guías de corte de TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías de RX escribe en el SliceModel activo. Pase 0 para un borde para suprimir esa guía.              |

## Consejos

- La traza de retención de pico rastrea los contenedores de frecuencia sin procesar incluso cuando el suavizado de visualización (combo `Smoothing`) está configurado en un valor grueso como `1/3`. Si aparece una resonancia en la traza congelada pero se ve redondeada con un ajuste de suavizado grueso, cambie `Smoothing` a `Off (1/96)` para ver el detalle completo del contenedor.
- Para borrar los datos de pico acumulados sin desactivar y activar `Peak Hold`, desmarque y luego vuelva a marcar inmediatamente el botón después de un momento de silencio o señal reducida.
- Las líneas guía de corte de filtro amarillas discontinuas permanecen arrastrables mientras `Peak Hold` está activo. Esto le permite alinear los bordes de la banda pasante de la radio directamente con las características visibles en la traza congelada.

## Solución de problemas

- **El botón `Peak Hold` no está visible** — El botón está solo en el editor flotante, no en el mosaico acoplado de la aplicación `Aetherial TX EQ` o `Aetherial RX EQ`. Abra el editor flotante haciendo doble clic en la etapa de EQ en el widget CHAIN.
- **La traza decae inmediatamente después de hacer clic en `Peak Hold`** — Confirme que el botón muestra un fondo ámbar, lo que indica que está marcado. Un solo clic que se registre como doble clic puede desmarcar el botón nuevamente. Haga clic una vez firmemente y verifique el estado ámbar.

## Relacionado

- [Open the frameless editor to add / remove / tune bands on either side](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Smooth the analyzer display for easier reading with the Smoothing combo](smooth-the-analyzer-display-for-easier-reading-with-the-smoothing-combo.md)
- [Drag the TX or RX filter cutoff guide line to move the radio passband](drag-the-tx-or-rx-filter-cutoff-guide-line-to-move-the-radio-passband.md)
- [Inspect the TX EQ curve and live spectrum](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspect the RX EQ curve and live spectrum](inspect-the-rx-eq-curve-and-live-spectrum.md)
