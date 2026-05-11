# Ajustar la ganancia de AF y la panorámica desde el panel VFO

Use la pestaña Audio en el panel VFO para configurar el nivel de salida de audio y la posición de panorámica estéreo de cualquier segmento de recepción de forma independiente de otros segmentos.

## Antes de empezar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa al radio.
- El panel VFO del segmento destino debe estar abierto. Si está colapsado a una tira solo de frecuencia, haga clic en cualquier lugar de la tira colapsada para expandirlo.

## Pasos

1. Haga clic en la bandera del marcador VFO en la visualización del espectro del segmento que desea ajustar. Se abre el panel VFO anclado al marcador.
2. Haga clic en la pestaña **Audio** dentro del panel VFO.
3. Para configurar el nivel de salida de audio, arrastre el **deslizador AF Gain** hacia la izquierda o la derecha. El valor predeterminado es 100; el rango válido es 0–100.
4. Para configurar la posición estéreo, arrastre el **deslizador Pan** hacia la izquierda o la derecha. El valor predeterminado es 50 (centro); el rango válido es 0–100. Un valor por debajo de 50 desplaza el audio hacia el canal izquierdo; por encima de 50 hacia el derecho.

## Qué hace cada control

| Control | Predeterminado | Rango |
|---|---|---|
| Deslizador AF Gain (pestaña Audio) | 100 | 0–100 |
| Deslizador Pan (pestaña Audio) | 50 | 0–100 |
| Botón Mute (pestaña Audio) | desactivado | — |
| Botón + deslizador Squelch (pestaña Audio) | desactivado | 0–100 |
| Combobox AGC (pestaña Audio) | FAST | FAST \| MED \| SLOW \| OFF |
| Botón ADSP (pestaña DSP) | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de conmutador DSP del lado del radio pero no marcable. Al hacer clic, abre y enfoca el diálogo no modal AetherDSP Settings. |
| Botón AetherVoice (pestaña DSP) | Conmuta la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

## Consejos

- Al hacer doble clic en cualquier deslizador, se restablece a su valor predeterminado: 100 para AF Gain, 50 para Pan.
- La ganancia de AF es por segmento. Ajustar un segmento no afecta a ningún otro segmento.
- Para silenciar un segmento sin mover el deslizador AF Gain, use el **botón Mute** en la pestaña Audio en su lugar. Silenciar no cambia el valor de ganancia almacenado.

## Cambio en la etiqueta de ancho de filtro en v0.9.8

La etiqueta de ancho de filtro ahora usa `RxApplet::formatFilterWidth` como única fuente de información. Esto corrige un desplazamiento de 0.1 kHz que antes afectaba las lecturas en modo SSB y digital (#2197, v0.9.8). La etiqueta ahora se mantiene sincronizada con la lectura del filtro en el applet RX.

## Comportamiento del squelch para modo RTTY (v26.5.1)

El botón y el deslizador de squelch ahora están deshabilitados en modo RTTY, además de los modos digital y CW. Esto evita que el squelch bloquee señales FSK débiles cuando el audio alimenta decodificadores externos a través de DAX (#2504).

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP en el panel VFO ahora solo muestra los algoritmos de reducción de ruido proporcionados por el radio. Los algoritmos del lado cliente que antes eran accesibles como botones en esta pestaña — NR2, RN2, NR4, MNR, BNR y DFNR — se han movido fuera del panel VFO. Para habilitar esos algoritmos, use el menú superpuesto del espectro o el applet AetherDSP.

Los botones que permanecen en la pestaña DSP son:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Borrador de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de énfasis de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

### Botón ADSP (v0.9.8)

La pestaña DSP ahora incluye un **botón ADSP** que abre el diálogo AetherDSP Settings. Este botón proporciona el mismo punto de entrada que el menú Settings. Tiene el estilo de un conmutador DSP del lado del radio pero no es marcable. Haga clic en él para abrir y enfocar el diálogo no modal AetherDSP Settings.

### Botón AetherVoice (v0.9.8)

La pestaña DSP también incluye un **botón AetherVoice** que conmuta la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX. Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas y coincide con los puntos de entrada existentes del menú y la cadena para la tira.

### Deslizador de nivel DSP

Ahora aparece un deslizador de nivel compartido debajo de la cuadrícula de botones DSP. El deslizador se redirige automáticamente al algoritmo DSP con nivel que se haya habilitado más recientemente. La etiqueta a la izquierda del deslizador muestra el nombre del algoritmo actualmente seleccionado, y el valor numérico se muestra a la derecha.

Cambio importante en v0.9.8: El deslizador de nivel DSP ahora aparece correctamente al iniciar para cualquier DSP que estuviera habilitado en el perfil guardado del radio. Anteriormente, el deslizador faltaba hasta que se conmutaba manualmente el algoritmo (#startup-slider). Esto afecta a NB, NR, ANF, NRL, NRS, NRF y ANFL.

La fila del deslizador permanece siempre presente. Cuando no hay ningún algoritmo con nivel activo — o cuando solo RNN, ANFT o APF están encendidos — la fila del deslizador se atenúa y no responde a los clics.

| Control | Rango | Comportamiento |
|---|---|---|
| Deslizador de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP con nivel habilitado más recientemente. Se redirige automáticamente al cambiar de algoritmos. Oculto (atenuado) cuando no hay ningún algoritmo con nivel activo. |

## Relacionado

- [Silenciar audio de un segmento desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Habilitar squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
- [Colapsar el panel VFO a vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Descripción general del panel VFO](overview.md)
