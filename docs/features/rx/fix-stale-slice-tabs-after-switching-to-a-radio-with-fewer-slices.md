# Corregir pestañas de slice obsoletas después de conectarse a una radio con menos slices

Al desconectarse de una radio y conectarse a otra que tiene menos slices, la fila de pestañas de slice del applet RX (botones A a H) puede mostrar pestañas de la sesión anterior. Esta página explica cómo eliminar esas pestañas obsoletas y restaurar un estado limpio.

## Antes de comenzar

- Ya se ha desconectado de la primera radio y está conectado, o a punto de conectarse, a una segunda radio con menos slices disponibles.
- El applet RX está visible en el Panel de Applets. Si no lo está, haga clic en el botón **RX** de la bandeja en la barra lateral derecha.

## Pasos

1. Desconéctese de la radio actual si aún no lo ha hecho. Use `Settings > Connect to Radio...` para abrir el diálogo de conexión, luego cierre o cancele la conexión existente.
2. Observe la fila de pestañas de slice en la parte superior del applet RX. Si aún se muestran pestañas (por ejemplo A, B, C, D) de la radio anterior, están obsoletas.
3. Conéctese a la nueva radio usando `Settings > Connect to Radio...` y seleccione la radio de destino.
4. Una vez establecida la nueva conexión, AetherSDR llama internamente a `clearSliceButtons()` al desconectarse, lo que elimina todos los botones de pestaña de slice generados y restaura la insignia de slice estática. La fila de pestañas de slice se volverá a poblar para coincidir con el número máximo de slices de la nueva radio.
5. Confirme que la fila de pestañas de slice ahora muestra solo el número correcto de pestañas (limitado al máximo de hardware de la nueva radio). Si la nueva radio admite solo un slice, la fila de pestañas se oculta por completo y solo se muestra la insignia de slice.

## Qué hace cada control

| Control | Comportamiento | Predeterminado |
|---------|----------|---------|
| Pestañas de slice (A..H) | Selecciona a qué slice está vinculado el applet RX; emite sliceActivationRequested. | Fila oculta si maxSlices <= 1. clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectarse (v0.9.5.1, #2254). Las conexiones de clic en botones de slice están protegidas contra controladores de señal duplicados en reconexiones. |
| Insignia de slice | Muestra la letra del slice vinculado actualmente. Se muestra siempre; es el único indicador de slice visible cuando la fila de pestañas está oculta. | A |
| 🔓 / 🔒 | Alterna el bloqueo de sintonía en el slice; un slice bloqueado ignora los cambios de frecuencia. | 🔓 (desbloqueado) |
| ANT1 (antena RX) | Abre un menú con las antenas disponibles; al seleccionar una se establece slice->setRxAntenna. Se completa desde ant_list de la radio. | ANT1 |
| ANT1 (antena TX) | Abre un menú con las antenas capaces de TX; establece slice->setTxAntenna. Los puertos de antena solo RX (prefijo 'RX') se filtran. | ANT1 |
| 2.7K (ancho de filtro) | Muestra el ancho de filtro actual en kHz. Se actualiza al aplicar un preajuste de filtro. | 2.7K |
| QSK | Se ilumina en ámbar cuando el break-in CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW. | apagado (gris) |
| TX (insignia) | Haga clic para establecer este slice como slice de TX (llama a slice->setTxSlice). | Ninguno |
| Combo de modo | Establece el modo del slice; reconfigura los preajustes de filtro y paso para el nuevo modo. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). | USB |
| Etiqueta de frecuencia | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para cambiar al modo de edición. | 0.000.000 |
| Edición de frecuencia | Ingrese MHz y presione Enter para sintonizar y re-centrar; admite escalado automático de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y descarta el editor. | Ninguno |
| STEP | `<` / `>` o la rueda del ratón recorren los tamaños de paso por modo; emite stepSizeChanged. La lista de pasos depende del modo del slice. | 100 Hz (índice 2) |
| Preajustes de ancho de filtro | Haga clic para aplicar un ancho de filtro preajustado; haga clic derecho para guardar el ancho actual como preajuste. La lectura de ancho usa lógica sensible al modo para que los modos SSB/digitales muestren el ancho etiquetado correcto. Las palabras clave Widen/Narrow (si están asignadas a atajos de teclado) recorren la lista de preajustes por modo para una geometría de borde correcta según el modo. | Lista por modo |
| Widget de banda de paso del filtro | Arrastre los bordes lo/hi para ajustar la banda de paso del filtro; emite filterChanged (lo, hi). | Ninguno |
| Modo de tono (FM) | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. | Off |
| Valor de tono CTCSS | Selecciona la frecuencia de tono CTCSS enviada con la transmisión. Habilitado solo cuando Tone mode = CTCSS TX. | Ninguno |
| Offset (FM) | Establece la frecuencia de offset del repetidor FM en MHz. | 0.0 MHz |
| − (offset abajo) | Establece la dirección del offset del repetidor hacia 'abajo' (TX por debajo de RX). | Ninguno |
| Simplex | Establece la dirección del offset del repetidor a simplex (TX = RX). | marcado |
| + (offset arriba) | Establece la dirección del offset del repetidor hacia 'arriba' (TX por encima de RX). | Ninguno |
| REV | Invierte el signo del offset de TX para trabajar con un par de repetidores invertido. | Ninguno |
| 🔊 / 🔇 (silencio) | Silencia la salida de audio del slice. | 🔊 (sin silenciar) |
| Ganancia AF | Ajusta la ganancia de salida de audio del slice; emite afGainChanged. | 70 |
| Panorámica L / R | Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100). El doble clic restablece a 50 (centro). | 50 |
| SQL | Activa el squelch en el nivel actual del deslizador. | Ninguno |
| Nivel de squelch | Ajusta el umbral de squelch; solo tiene efecto cuando SQL está activado. | 20 |
| Modo AGC | Establece el modo AGC del slice. Opciones: Off, Slow, Med, Fast. Oculto en modos de la familia FM. | Med |
| Umbral AGC | Establece el umbral AGC (o nivel de apagado AGC cuando el modo AGC es Off). La información sobre herramientas refleja qué valor se está ajustando. | 65 |
| RIT | Activa/desactiva la sintonización incremental de recepción. | Ninguno |
| RIT 0 | Pone a cero el offset de RIT. | Ninguno |
| Offset RIT | `<` / `>` o la rueda del ratón ajustan el offset de RIT en pasos de 10 Hz. | +0 Hz |
| XIT | Activa/desactiva la sintonización incremental de transmisión. | Ninguno |
| XIT 0 | Pone a cero el offset de XIT. | Ninguno |
| Offset XIT | `<` / `>` o la rueda del ratón ajustan el offset de XIT en pasos de 10 Hz. | +0 Hz |

## Consejos

- Los botones de pestaña de slice están limitados por el máximo de hardware de la radio conectada. Una radio que admite dos slices nunca mostrará más de dos pestañas, independientemente de lo que tuviera la radio anterior.
- Las conexiones duplicadas de controladores de señal están protegidas en las reconexiones, por lo que reconectarse a la misma radio varias veces no multiplicará las respuestas de clic en las pestañas.
- Los atajos de teclado **Widen** y **Narrow** (o acciones MIDI/GPIO equivalentes) recorren la banda de paso del filtro del slice activo a través de la lista de preajustes por modo mediante `stepFilterWidth()`. Esto garantiza que todos los modos (LSB, CWL, DIGL, RTTY, AM, CW, USB) produzcan una geometría de borde correcta según el modo.

## Solución de problemas

- **Quedan pestañas obsoletas después de reconectarse** — Esto puede ocurrir si el evento de desconexión no se disparó limpiamente. Desconéctese nuevamente usando `Settings > Connect to Radio...`, espere a que la insignia de slice reaparezca en lugar de las pestañas, luego reconéctese.
- **La fila de pestañas falta por completo después de conectarse** — Si la nueva radio informa un número máximo de slices de 1 o menos, la fila de pestañas se oculta intencionalmente. Solo se muestra la insignia de slice. Este es un comportamiento esperado.
- **La lectura del ancho de filtro parece incorrecta después de un cambio de modo** — El formateador de ancho de filtro (`formatFilterWidth()`) se comparte con el panel VFO y utiliza lógica sensible al modo. Si la lectura parece incorrecta, intente recorrer los preajustes de filtro para actualizar el valor mostrado.

## Relacionado

- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Descripción general de controles RX](overview.md)
- [Comprendiendo slices y VFOs](../../getting-started/concepts/understanding-slices.md)
