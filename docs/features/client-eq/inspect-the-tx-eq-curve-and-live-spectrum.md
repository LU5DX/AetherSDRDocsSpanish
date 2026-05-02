# Inspeccionar la curva de EQ de TX y el espectro en vivo

El applet "Aetherial TX EQ" muestra la curva de respuesta EQ combinada, una superposición del analizador FFT en vivo y una traza de pico retenido para la ruta de audio de TX. Use esta vista para monitorear cómo se está moldeando su señal de transmisión sin abrir el editor completo.

## Antes de comenzar

- El sub-contenedor "Aetherial TX EQ" permanece oculto hasta que la etapa TX EQ esté habilitada. Habilítela desde el widget CHAIN o desde el editor flotante ("Aetherial Parametric EQ — TX") antes de esperar que aparezca el applet.
- El applet se encuentra dentro del contenedor padre Aetherial Audio (TXDSP) en el panel de applets. Si el panel de applets no está visible, verifique `View > Applet Panel`.

## Pasos

1. Ubique el contenedor padre Aetherial Audio (TXDSP) en el panel de applets.
2. Encuentre el sub-contenedor "Aetherial TX EQ" dentro de él.
3. Observe el área del analizador / curva — la pantalla que muestra la cuadrícula, la curva de respuesta EQ combinada, la superposición del analizador FFT en vivo y la traza de pico retenido para la ruta de TX.
4. Observe la línea de respuesta EQ combinada, que refleja la respuesta en frecuencia acumulada de todas las bandas de TX habilitadas.
5. Observe la superposición del analizador en vivo, que muestra la FFT en tiempo real del audio que pasa por la ruta de TX. La superposición permanece inactiva cuando no hay audio presente y activa cuando el audio fluye por la ruta de TX.
6. Observe la traza de pico retenido — una línea blanco apagado que registra el nivel más alto detectado en cada bin de frecuencia y decae aproximadamente 10 dB/sec. La traza opera sobre bins sin procesar, por lo que la detección de picos es exacta a nivel de muestra; el suavizado de la pantalla se aplica de forma independiente y no afecta los valores de pico subyacentes. Para congelar la traza en su máximo actual, abra el editor flotante y habilite el botón Peak Hold.
7. Observe las líneas guía de corte de filtro amarillas discontinuas superpuestas sobre el lienzo. Estas marcan las frecuencias de corte bajas y altas del filtro de TX actual de la radio. En el applet acoplado, las líneas son solo de visualización; arrástrelas en el editor flotante para mover la banda de paso de la radio en tiempo real.
8. Observe la franja de plan de banda de audio en la parte inferior del lienzo. Esta franja de 14 px muestra las regiones de modulación E-SSB / SSB / AM-FM como referencia y siempre está visible.

## Qué hace cada control

| Control | Descripción | Editable en el applet |
|---|---|---|
| Área del analizador / curva | ClientEqCurveWidget — mínimo 110 px de altura en el applet acoplado, vinculado a la ruta indicada en la construcción (Path::Tx o Path::Rx). Muestra una cuadrícula de frecuencia logarítmica (20 Hz–20 kHz, ±18 dB), la respuesta EQ combinada, un analizador con gradiente relleno FFT en vivo (refresco a 25 Hz) y una traza de pico retenido que decae ~10 dB/sec entre actualizaciones. Líneas verticales amarillas discontinuas marcan los cortes de filtro bajo/alto de TX actual de la radio (tile de TX) o los bordes de la banda de paso de RX (tile de RX). | Solo visualización en el applet; la edición ocurre en el ClientEqEditor sin marco. La traza de pico retenido puede congelarse (deja de decaer) mediante el botón Peak Hold en la barra de herramientas del editor. Las líneas guía de corte son arrastrables en el lienzo del editor para mover la banda de paso de la radio en tiempo real. |
| Respuesta EQ combinada | Muestra la respuesta en frecuencia acumulada de todas las bandas de TX habilitadas. Aparece plana cuando ninguna banda está moldeando la señal. Se atenúa en gris cuando la etapa EQ está en bypass. | No |
| Superposición del analizador en vivo | FFT en tiempo real del audio en la ruta de TX. Inactivo cuando no hay audio presente; activo cuando fluye el audio. Se refresca a 25 Hz. | No |
| Traza de pico retenido | Línea blanco apagado que muestra el nivel máximo por bin observado desde el último reinicio. Opera sobre bins sin procesar, por lo que la detección de picos es exacta a nivel de muestra. Decae aproximadamente 10 dB/sec en operación normal. El suavizado de la pantalla se aplica a la traza de pico de forma independiente mediante `ClientEqSmoothingFraction` y afecta únicamente la representación visual. Se congela en el nivel más alto observado cuando Peak Hold está habilitado en el editor flotante. | No — use el botón Peak Hold en el editor flotante |
| Peak Hold | Botón de alternancia en la franja de encabezado del editor flotante. Cuando está activado (fondo ámbar), la traza de pico retenido deja de decaer y se mantiene en el nivel más alto observado para cada frecuencia. Desactívelo para reanudar la decaída normal. | Solo editor flotante |
| Smoothing | Cuadro combinado en la franja de encabezado del editor flotante. Aplica promediado de potencia por octava fraccional a la traza del analizador para la pantalla — no afecta el cálculo del EQ. Opciones: Off (1/96), 1/24, 1/12, 1/6, 1/3. Fracción menor = más suave (1/3 es la más suavizada; 1/96 es efectivamente Off). El suavizado se ejecuta después de la actualización de pico retenido en cada fotograma, por lo que tanto la traza en vivo como la de pico retenido reflejan los datos actuales antes de aplicar el promediado. Compartido entre los editores de TX y RX. Se guarda como `ClientEqSmoothingFraction`. Información emergente: "Fractional-octave smoothing applied to the analyzer trace. Lower fraction = smoother (1/3 = most, 1/96 = off). Affects display only — EQ math is unchanged." | Solo editor flotante |
| Filter family | Cuadro combinado en la franja de encabezado del editor flotante. Selecciona la matemática de la cascada HP/LP: Butterworth (banda de paso máximamente plana), Chebyshev (caída más pronunciada con 1 dB de rizado en la banda de paso), Bessel (fase lineal / caída más suave) o Elliptic (transición más pronunciada con rizado en ambas bandas). El valor predeterminado es Butterworth. Se aplica únicamente a los tipos de filtro HP y LP; las bandas de pico y estante usan su propia topología fija de 2.º orden independientemente. Se guarda como `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. | Solo editor flotante |
| Reset | Botón pulsador en la franja de encabezado del editor flotante. Restablece todas las bandas a la plantilla predeterminada de 10 bandas, restaura el número de bandas predeterminado y restablece la familia de filtros a Butterworth. Guarda inmediatamente. Información emergente: "Reset all bands to default values". | Solo editor flotante |
| Output Fader | Fader vertical combinado con medidor de nivel en el borde derecho del editor flotante. Arrástrelo para establecer la ganancia maestra post-EQ; la rueda de desplazamiento ajusta en pasos de 0.5 dB; doble clic restablece a 0 dB. Rango: -36 a +12 dB. La barra de nivel detrás del control muestra el pico post-EQ suavizado en tiempo real con el mismo degradado verde-ámbar-rojo que el medidor de nivel Tube. Se guarda como `ClientEqTxMasterGain` / `ClientEqRxMasterGain`. | Solo editor flotante |
| Fila de iconos de tipo de filtro | Una fila de 8 iconos dibujados a medida (uno por ranura de banda) en la parte superior del área del lienzo del editor. Cada icono dibuja la forma del filtro actual (campana de pico, rampa de estante, pendiente HP/LP) en el color de paleta de su banda. Haga clic en un icono para ciclar por los tipos de filtro de esa banda; al hacer clic también se selecciona la banda, resaltando su control en el lienzo y su columna en la fila de parámetros. Los iconos se atenúan al 35 % de opacidad cuando la banda está en bypass. | Solo editor flotante |
| Fila de texto de parámetros | Una fila de 8 columnas de texto (una por ranura de banda) debajo del lienzo que muestra los valores de Freq, Gain y Q de cada banda. Los valores se actualizan en vivo durante los arrastres en el lienzo. Hacer clic en una columna selecciona esa banda. | Solo editor flotante |
| Líneas guía de corte de filtro (TX / RX) | Líneas verticales amarillas discontinuas superpuestas sobre el lienzo en los cortes de filtro bajo/alto de TX actual de la radio (tile de TX) o los bordes de la banda de paso de RX (tile de RX). Al acercar el cursor a una línea, este cambia a una flecha de cambio de tamaño horizontal. Arrastrar una línea en el editor mueve el corte de filtro correspondiente de la radio en tiempo real. Los applets de TX y RX reciben las actualizaciones de corte de forma independiente: el applet de TX ignora los cambios de corte de RX y el applet de RX ignora los cambios de corte de TX. Pase 0 para un borde a fin de suprimir esa guía. | Solo visualización en el applet; arrastrables únicamente en el editor flotante |
| Franja de plan de banda de audio | Una franja de 14 px permanentemente visible en la parte inferior del lienzo del EQ. Muestra las regiones de modulación E-SSB / SSB / AM-FM como referencia de frecuencia. La interacción del cursor en esta área está excluida de la detección de controles de banda. | No |

La edición de bandas requiere el editor flotante. Consulte [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en ambos lados](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).

## Consejos

- El applet es solo de visualización. Toda la edición de bandas — agregar, eliminar y ajustar — ocurre en el editor flotante "Aetherial Parametric EQ — TX", que se abre haciendo doble clic en la etapa TX EQ en el widget CHAIN.
- Use la traza de pico retenido en el applet acoplado para identificar resonancias y picos agresivos mientras ajusta otros controles. Abra el editor flotante y haga clic en Peak Hold para congelar la traza en su máximo actual antes de realizar un ajuste fino.
- Dado que el suavizado se ejecuta después de cada actualización de pico retenido, habilitar Smoothing en el editor flotante no provoca que la traza de pico se retrase respecto al analizador en vivo — ambas se suavizan desde el mismo fotograma actual.
- Las líneas guía de corte de filtro amarillas discontinuas en el applet se actualizan automáticamente cada vez que cambian los ajustes de filtro de TX o RX de la radio. Para ajustar la banda de paso, arrastre las líneas guía en el editor flotante en lugar de navegar a los controles de filtro de la radio por separado.
- Para flotar, extraer u ocultar el sub-contenedor "Aetherial TX EQ", haga clic derecho en su barra de título.

## Solución de problemas

- **El sub-contenedor "Aetherial TX EQ" no está visible** — El applet permanece oculto hasta que la etapa TX EQ esté habilitada. Habilítela desde el widget CHAIN o desde el editor flotante. Consulte [Poner en bypass la etapa EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).
- **La superposición del analizador en vivo aparece inactiva** — No hay audio pasando por la ruta de TX. Debe haber audio de transmisión presente para que la superposición FFT funcione.
- **La traza de pico retenido no se mueve** — Peak Hold está habilitado en el editor flotante. Haga clic en Peak Hold nuevamente para reanudar la decaída normal.
- **Las líneas guía de corte de filtro no están visibles** — La radio ha reportado un valor de corte de 0 para ese borde, lo que suprime la línea guía correspondiente. Verifique los ajustes de filtro de TX o RX de la radio.

## Relacionados

- [Descripción general de Aetherial Parametric EQ (TX / RX)](overview.md)
- [Inspeccionar la curva de EQ de RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Poner en bypass la etapa EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en ambos lados](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Verificar que la curva combinada coincida con su objetivo](verify-the-summed-curve-matches-your-mental-target.md)
