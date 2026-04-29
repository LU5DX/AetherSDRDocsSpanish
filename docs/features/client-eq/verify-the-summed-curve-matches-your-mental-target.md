# Verificar que la curva sumada coincide con el objetivo previsto

Después de ajustar las bandas en el editor de EQ paramétrico, use los mosaicos del applet para confirmar que la curva de respuesta de EQ sumada refleja la forma general que se tenía en mente, con la superposición del analizador en vivo mostrando cómo se alinea el audio real con ella.

## Antes de comenzar

- La etapa de EQ que desea verificar debe estar habilitada. Si el mosaico "Aetherial TX EQ" o "Aetherial RX EQ" está oculto, habilite la etapa de EQ correspondiente a través del widget CHAIN primero.
- Las bandas deben estar configuradas previamente. Si aún no ha agregado ni ajustado bandas, consulte [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).

## Pasos

1. Ubique el subcontenedor "Aetherial TX EQ" o "Aetherial RX EQ" dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Observe el área de la curva — la pantalla de 110 px de altura que muestra una cuadrícula, la respuesta de EQ sumada, la superposición del analizador FFT en vivo y la traza de pico retenido.
3. Trace la curva de respuesta de EQ sumada a lo largo del eje de frecuencia. Esta refleja la respuesta acumulada de todas las bandas habilitadas para esa ruta.
4. Compare la forma de la curva con el objetivo previsto. Los picos, los shelves y los cortes paso-alto o paso-bajo aparecen como desviaciones respecto a una línea plana.
5. Observe la superposición del analizador en vivo mientras el audio pasa por la ruta. La superposición muestra la FFT en tiempo real del audio en esa ruta, lo que permite confirmar que la respuesta moldeada está afectando el espectro de la manera esperada.
6. Observe la traza de pico retenido (línea color blanco apagado) para identificar los contenedores de frecuencia que han alcanzado niveles altos recientemente. La traza decae aproximadamente a 10 dB/seg entre actualizaciones, por lo que las resonancias transitorias permanecen visibles durante un breve tiempo después de producirse.
7. Si la curva no coincide con el objetivo, haga doble clic en la etapa de EQ en el widget CHAIN para volver a abrir el editor sin marco ("Aetherial Parametric EQ — TX" o "— RX") y ajuste las bandas allí.

## Qué hace cada control

| Control | Descripción | Notas |
|---|---|---|
| Área del analizador / curva | Muestra la cuadrícula, la respuesta de EQ sumada, la superposición del analizador FFT en vivo y la traza de pico retenido para la ruta bloqueada del mosaico (TX o RX). | Solo lectura en el mosaico del applet. La edición requiere el editor flotante. |
| Respuesta de EQ sumada | La respuesta de frecuencia acumulada de todas las bandas habilitadas en esta ruta. Aparece plana cuando ninguna banda altera la respuesta; con forma cuando una o más bandas están activas. Se atenúa en gris cuando la etapa de EQ está en bypass. | Persistida mediante `ClientEqTxBands` (TX) o `ClientEqRxBands` (RX). |
| Superposición del analizador en vivo | FFT en tiempo real del audio que pasa por esta ruta. Aparece inactiva cuando no hay audio presente y en funcionamiento cuando el audio está activo. Rellena con un degradado cian desde 0 dB en la parte superior hasta transparente en la parte inferior. | Proporciona confirmación visual de que la curva está afectando la señal real. |
| Traza de pico retenido | Línea color blanco apagado dibujada sobre el analizador en vivo. Cada contenedor de frecuencia retiene el nivel más alto observado y luego decae aproximadamente a 10 dB/seg. Deja de decaer cuando **Peak Hold** está marcado en el editor flotante. | Ayuda a identificar resonancias y picos duros durante el ajuste. Visible tanto en el mosaico del applet como en el editor flotante. |
| Peak Hold | Botón de activación en la barra de encabezado del editor flotante. Cuando está marcado (fondo ámbar), la traza de pico retenido deja de decaer — el nivel más alto observado en cada contenedor de frecuencia se mantiene hasta que se desactiva el botón. | Se encuentra únicamente en el editor flotante, no en el mosaico del applet acoplado. Desactívelo para reanudar el decaimiento normal. |
| Familia de filtros | Cuadro combinado en la barra de encabezado del editor flotante. Selecciona la matemática utilizada para los filtros en cascada HP y LP. Opciones: Butterworth (banda de paso máximamente plana), Chebyshev (caída más pronunciada con 1 dB de rizado en la banda de paso), Bessel (fase lineal / caída más suave), Elíptico (transición más pronunciada con rizado en ambas bandas). Predeterminado: Butterworth. | Se aplica únicamente a los tipos de filtro HP y LP. Las bandas de pico y shelf utilizan su propia topología fija de segundo orden independientemente. Persistida por separado según la ruta: `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. |
| Reset | Botón en la barra de encabezado del editor flotante. Restablece todas las bandas a la plantilla predeterminada de 10 bandas, restaura el número de bandas predeterminado y restablece la familia de filtros a Butterworth. Guarda inmediatamente. | Información sobre herramienta: "Reset all bands to default values". Se encuentra únicamente en el editor flotante. |
| Output Fader | Fader vertical combinado con medidor de nivel en el borde derecho del editor flotante. Arrastre para establecer la ganancia maestra post-EQ; la rueda de desplazamiento ajusta en pasos de 0.5 dB; haga doble clic para restablecer a 0 dB. La barra de nivel detrás del control muestra el pico post-EQ suavizado en tiempo real con el mismo degradado verde-ámbar-rojo que el medidor de nivel Tube. | Persistido por separado según la ruta: `ClientEqTxMasterGain` / `ClientEqRxMasterGain`. Información sobre herramienta: "Output gain (dB). Drag to set, wheel for fine step, double-click to reset to 0 dB." El rango de ganancia es lineal de 0.0 a ~4.0; las etiquetas de la escala van de -40 a 0 dB. Se encuentra únicamente en el editor flotante — no en el mosaico del applet acoplado. |

## Consejos

- El mosaico del applet es solo de lectura. No se realiza ninguna edición aquí. Todos los cambios de banda deben realizarse en el editor sin marco abierto desde el widget CHAIN.
- Hay un mosaico por lado. "Aetherial TX EQ" está bloqueado a la ruta TX; "Aetherial RX EQ" está bloqueado a la ruta RX. No comparten un selector.
- Use **Peak Hold** en el editor flotante para congelar la traza de pico retenido mientras ajusta una banda. Esto facilita verificar si una resonancia ha sido reducida sin que la traza decaiga entre ajustes. Desactive **Peak Hold** cuando haya terminado para reanudar el decaimiento normal.
- Si la curva aparece plana pero se espera una forma moldeada, verifique si la etapa de EQ está en bypass. Una etapa en bypass no aplica sus bandas a la ruta de audio aunque la pantalla de la curva pueda seguir renderizando la forma. Consulte [Aplicar bypass a la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).
- Use **Reset** en el editor flotante para devolver el EQ a un punto de partida conocido. Todas las bandas, el número de bandas y la familia de filtros se restauran a sus valores predeterminados y se guardan inmediatamente.

## Resolución de problemas

- **El mosaico del applet no es visible** — La etapa de EQ no está habilitada. Habilítela a través del widget CHAIN o del editor flotante. El mosaico permanece oculto hasta que la etapa correspondiente esté activa.
- **La curva sumada es plana a pesar de tener bandas configuradas** — Es posible que todas las bandas tengan una ganancia de 0 dB, o que la etapa de EQ esté en bypass. Abra el editor sin marco para inspeccionar la configuración de cada banda, o verifique el estado de bypass en el widget CHAIN.
- **La superposición del analizador en vivo está inactiva** — No hay audio pasando por esa ruta. En RX, asegúrese de que la radio esté recibiendo y que el enrutamiento de audio esté activo. En TX, asegúrese de que se esté procesando una señal a través de la cadena TX DSP.
- **La traza de pico retenido no se mueve** — Verifique si **Peak Hold** está marcado en el editor flotante. Si está marcado (fondo ámbar), la traza está congelada intencionalmente. Desactívelo para reanudar el decaimiento.

## Relacionados

- [Descripción general del Aetherial Parametric EQ (TX / RX)](overview.md)
- [Inspeccionar la curva de EQ de TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva de EQ de RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Aplicar bypass a la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
