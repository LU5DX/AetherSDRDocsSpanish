# Ajustar la ganancia de AF y la panorámica desde el panel VFO

Utilice la pestaña Audio en el panel VFO para configurar el nivel de salida de audio y la posición de panorámica estéreo de cualquier slice de recepción de forma independiente de los demás slices.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa con el radio.
- El panel VFO del slice de destino debe estar abierto. Si está colapsado a una tira solo de frecuencia, haga clic en cualquier lugar de la tira colapsada para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora VFO en la pantalla del espectro para el slice que desea ajustar. El panel VFO se abre anclado al marcador.
2. Haga clic en la pestaña **Audio** dentro del panel VFO.
3. Para configurar el nivel de salida de audio, arrastre el **control deslizante AF Gain** hacia la izquierda o la derecha. El valor predeterminado es 100; el rango válido es 0–100.
4. Para configurar la posición estéreo, arrastre el **control deslizante Pan** hacia la izquierda o la derecha. El valor predeterminado es 50 (centro); el rango válido es 0–100. Un valor inferior a 50 mueve el audio hacia el canal izquierdo; superior a 50 hacia el derecho.

## Función de cada control

| Control | Predeterminado | Rango |
|---|---|---|
| Control deslizante AF Gain (pestaña Audio) | 100 | 0–100 |
| Control deslizante Pan (pestaña Audio) | 50 | 0–100 |
| Botón Mute (pestaña Audio) | desactivado | — |
| Botón + control deslizante Squelch (pestaña Audio) | desactivado | 0–100 |
| Combo AGC (pestaña Audio) | FAST | FAST \| MED \| SLOW \| OFF |
| Botón ADSP (pestaña DSP) | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de alternancia DSP del lado del radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal AetherDSP Settings. |
| Botón AetherVoice (pestaña DSP) | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

## Consejos

- Haga doble clic en cualquier control deslizante para restablecerlo a su valor predeterminado: 100 para AF Gain, 50 para Pan.
- La ganancia AF es por slice. Ajustar un slice no afecta a ningún otro slice.
- Para silenciar un slice sin mover el control deslizante AF Gain, use el **botón Mute** en la pestaña Audio en su lugar. Silenciar no cambia el valor de ganancia almacenado.

## Cambio en la etiqueta del ancho de filtro en v0.9.8

La etiqueta del ancho de filtro ahora usa `RxApplet::formatFilterWidth` como su única fuente de referencia. Esto corrige un desplazamiento de 0.1 kHz que anteriormente afectaba las lecturas en modo SSB y digital (#2197, v0.9.8). La etiqueta ahora se mantiene sincronizada con la lectura del filtro en el applet RX.

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP en el panel VFO ahora solo muestra los algoritmos de reducción de ruido proporcionados por el radio. Los algoritmos del lado del cliente que anteriormente estaban disponibles como botones en esta pestaña — NR2, RN2, NR4, MNR, BNR y DFNR — se han eliminado del panel VFO. Para habilitar esos algoritmos, use el menú superpuesto del espectro o el applet AetherDSP.

Los botones que permanecen en la pestaña DSP son:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Cancelador de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de realce de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

### Botón ADSP (v0.9.8)

La pestaña DSP ahora incluye un **botón ADSP** que abre el diálogo AetherDSP Settings. Este botón proporciona el mismo punto de entrada que el menú Settings. Tiene el estilo de una alternancia DSP del lado del radio pero no es seleccionable. Haga clic en él para abrir y enfocar el diálogo no modal AetherDSP Settings.

### Botón AetherVoice (v0.9.8)

La pestaña DSP también incluye un **botón AetherVoice** que alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP TX/RX. Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas y coincide con los puntos de entrada existentes del menú y la cadena para la tira.

### Control deslizante de nivel DSP

Ahora aparece un control deslizante de nivel compartido debajo de la cuadrícula de botones DSP. El control deslizante se redirige automáticamente al algoritmo DSP con nivel que se haya habilitado más recientemente. La etiqueta a la izquierda del control deslizante muestra el nombre del algoritmo actualmente dirigido, y el valor numérico se muestra a la derecha.

Cambio importante en v0.9.8: El control deslizante de nivel DSP ahora aparece correctamente al inicio para cualquier DSP que estuviera habilitado en el perfil guardado del radio. Anteriormente, el control deslizante faltaba hasta que se alternaba manualmente el algoritmo (#startup-slider). Esto afecta a NB, NR, ANF, NRL, NRS, NRF y ANFL.

La fila del control deslizante permanece dispuesta en todo momento. Cuando no hay ningún algoritmo con nivel activo — o cuando solo RNN, ANFT o APF está encendido — la fila del control deslizante se atenúa y no responde a los clics.

| Control | Rango | Comportamiento |
|---|---|---|
| Control deslizante de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP con nivel habilitado más recientemente. Se redirige automáticamente al cambiar de algoritmo. Oculto (atenuado) cuando no hay ningún algoritmo con nivel activo. |

## Relacionado

- [Silenciar audio para un slice desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Habilitar squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
- [Colapsar el panel VFO a vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Resumen del panel VFO](overview.md)
