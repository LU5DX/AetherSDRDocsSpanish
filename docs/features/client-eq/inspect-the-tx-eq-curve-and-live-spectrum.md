# Inspeccionar la curva del EQ de TX y el espectro en vivo

El applet "Aetherial TX EQ" muestra la curva de respuesta EQ sumada, una superposición de analizador FFT en tiempo real y una traza de pico retenido para la ruta de audio de TX. Use esta vista para monitorear cómo se está moldeando su señal de transmisión sin abrir el editor completo.

## Antes de comenzar

- El subcontenedor "Aetherial TX EQ" permanece oculto hasta que la etapa TX EQ esté habilitada. Habilítela mediante el widget CHAIN o el editor flotante ("Aetherial Parametric EQ — TX") antes de que el applet aparezca.
- El applet se encuentra dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets. Si el panel de applets no está visible, verifique `View > Applet Panel`.

## Pasos

1. Localice el contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Encuentre el subcontenedor "Aetherial TX EQ" dentro de él.
3. Observe el área del analizador / curva — la pantalla que muestra la cuadrícula, la curva de respuesta EQ sumada, la superposición del analizador FFT en tiempo real y la traza de pico retenido para la ruta de TX.
4. Observe la línea de respuesta EQ sumada, que refleja la respuesta en frecuencia acumulada de todas las bandas de TX habilitadas.
5. Observe la superposición del analizador en tiempo real, que muestra la FFT en tiempo real del audio que pasa por la ruta de TX. La superposición está inactiva cuando no hay audio presente y activa cuando el audio fluye por la ruta de TX.
6. Observe la traza de pico retenido — una línea blanquecina que registra el nivel más alto detectado en cada bin de frecuencia y decae aproximadamente a 10 dB/seg. Para congelar la traza en su máximo actual, abra el editor flotante y habilite el botón Peak Hold.

## Qué hace cada control

| Control | Descripción | Editable en el applet |
|---|---|---|
| Área del analizador / curva | Muestra la cuadrícula, la curva de respuesta EQ sumada, la superposición del analizador FFT en tiempo real y la traza de pico retenido para la ruta de TX. | No — solo visualización |
| Respuesta EQ sumada | Muestra la respuesta en frecuencia acumulada de todas las bandas de TX habilitadas. Aparece plana cuando ninguna banda está moldeando la señal. Se atenúa en gris cuando la etapa EQ está en bypass. | No |
| Superposición del analizador en tiempo real | FFT en tiempo real del audio en la ruta de TX. Inactiva cuando no hay audio presente; activa cuando fluye audio. | No |
| Traza de pico retenido | Línea blanquecina que muestra el nivel máximo por bin observado desde el último reinicio. Decae aproximadamente a 10 dB/seg en operación normal. Se congela en el nivel máximo observado cuando Peak Hold está habilitado en el editor flotante. | No — use el botón Peak Hold en el editor flotante |
| Peak Hold | Botón de alternancia en la barra de encabezado del editor flotante. Cuando está activado (fondo ámbar), la traza de pico retenido deja de decaer y se mantiene en el nivel más alto observado para cada frecuencia. Desactívelo para reanudar el decaimiento normal. | Solo en el editor flotante |
| Familia de filtros | Cuadro combinado en la barra de encabezado del editor flotante. Selecciona la matemática de la cascada HP/LP: Butterworth (banda de paso maximalmente plana), Chebyshev (caída más pronunciada con 1 dB de rizado en la banda de paso), Bessel (fase lineal / caída más suave) o Elliptic (transición más pronunciada con rizado en ambas bandas). El valor predeterminado es Butterworth. Se aplica únicamente a los tipos de filtro HP y LP; las bandas de pico y shelving usan su propia topología fija de segundo orden independientemente. Se almacena como `ClientEqTxFilterFamily` / `ClientEqRxFilterFamily`. | Solo en el editor flotante |
| Reset | Botón de acción en la barra de encabezado del editor flotante. Restablece todas las bandas a la plantilla predeterminada de 10 bandas, restaura el número de bandas predeterminado y restablece la familia de filtros a Butterworth. Se guarda de inmediato. Información emergente: "Reset all bands to default values". | Solo en el editor flotante |
| Output Fader | Fader vertical combinado con medidor de nivel en el borde derecho del editor flotante. Arrástrelo para establecer la ganancia maestra post-EQ; la rueda de desplazamiento ajusta en pasos de 0,5 dB; haga doble clic para restablecer a 0 dB. Rango: -36 a +12 dB. La barra de nivel detrás del control muestra el pico post-EQ suavizado en tiempo real con el mismo gradiente verde-ámbar-rojo que el medidor de nivel Tube. Se almacena como `ClientEqTxMasterGain` / `ClientEqRxMasterGain`. | Solo en el editor flotante |

La edición de bandas requiere el editor flotante. Consulte [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en ambos lados](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).

## Consejos

- El applet es solo de visualización. Toda la edición de bandas — agregar, eliminar y ajustar — ocurre en el editor flotante "Aetherial Parametric EQ — TX", que se abre haciendo doble clic en la etapa TX EQ del widget CHAIN.
- Use la traza de pico retenido en el applet acoplado para identificar resonancias y picos molestos mientras ajusta otros controles. Abra el editor flotante y haga clic en Peak Hold para congelar la traza en su máximo actual antes de realizar un ajuste fino.
- Para flotar, extraer u ocultar el subcontenedor "Aetherial TX EQ", haga clic derecho en su barra de título.

## Solución de problemas

- **El subcontenedor "Aetherial TX EQ" no está visible** — El applet permanece oculto hasta que la etapa TX EQ esté habilitada. Habilítela desde el widget CHAIN o desde el editor flotante. Consulte [Omitir la etapa EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).
- **La superposición del analizador en tiempo real aparece inactiva** — No hay audio pasando por la ruta de TX. Debe haber audio de transmisión presente para que la superposición FFT funcione.
- **La traza de pico retenido no se mueve** — Peak Hold está habilitado en el editor flotante. Haga clic en Peak Hold nuevamente para reanudar el decaimiento normal.

## Relacionado

- [Descripción general de Aetherial Parametric EQ (TX / RX)](overview.md)
- [Inspeccionar la curva del EQ de RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Omitir la etapa EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en ambos lados](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Verificar que la curva sumada coincida con el objetivo deseado](verify-the-summed-curve-matches-your-mental-target.md)
