# Silenciar el audio de un slice desde el panel VFO

Silencie la salida de audio de un solo slice sin modificar su valor de ganancia AF. Utilice esta función cuando desee suprimir un slice temporalmente y restaurar su volumen anterior con un solo clic.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO para el slice objetivo debe estar abierto. Si está contraído a una tira solo de frecuencia, haga clic en cualquier parte del mismo para expandirlo primero.

## Pasos

1. Haga clic en el marcador VFO en la pantalla de espectro correspondiente al slice que desea silenciar. El panel VFO se abre anclado al marcador.
2. Haga clic en **Audio** para seleccionar la pestaña Audio dentro del panel VFO.
3. Haga clic en **Mute**. El botón se activa y la salida de audio del slice se detiene. El valor del deslizador de ganancia AF no cambia.
4. Para restaurar el audio, haga clic en **Mute** nuevamente. El botón se desactiva y el audio se reanuda al nivel de ganancia AF anterior.

## Función de cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Notas |
|---------|------|---------------------|----------------|-------|
| Botón de antena RX | Botón pulsador | — | Abre el menú de selección de antena para la antena receptora de este slice. | |
| Botón de antena TX | Botón pulsador | — | Abre el menú de selección de antena para la antena transmisora de este slice. | |
| Indicador de frecuencia | Indicador | — | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la introducción directa de frecuencia; escriba los MHz y presione Enter o Tab. | |
| Etiqueta de ancho de filtro | Indicador | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer cíclicamente los botones preestablecidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad. | Corrige un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Deslizador de ganancia AF (pestaña Audio) | Deslizador | 100 | Establece el nivel de salida de audio para este slice. | No se persiste; refleja el estado en vivo de la radio. |
| Deslizador de paneo (pestaña Audio) | Deslizador | 50 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. | |
| Botón Mute (pestaña Audio) | Botón de alternancia | Desactivado | Silencia la salida de audio de este slice sin modificar el valor de ganancia AF. | |
| Botón + deslizador de squelch (pestaña Audio) | Botón de alternancia | Desactivado | Activa el squelch para este slice. El deslizador adyacente establece el umbral. | |
| Combinación AGC (pestaña Audio) | Cuadro combinado | FAST | Establece la velocidad de ataque/liberación del AGC para este slice. | |
| Botón NR (pestaña DSP) | Botón de alternancia | Desactivado | Activa el algoritmo de reducción de ruido del lado de la radio. | |
| Botón NB (pestaña DSP) | Botón de alternancia | Desactivado | Activa el eliminador de ruido (noise blanker). | |
| Botón ANF (pestaña DSP) | Botón de alternancia | Desactivado | Activa el filtro de muesca automático. | |
| Botón APF (pestaña DSP) | Botón de alternancia | Desactivado | Activa el filtro de énfasis de audio (solo modo CW). | |
| Botón NRL (pestaña DSP) | Botón de alternancia | Desactivado | Activa el nivel de reducción de ruido. | |
| Botón NRS (pestaña DSP) | Botón de alternancia | Desactivado | Activa la sustracción espectral. | |
| Botón RNN (pestaña DSP) | Botón de alternancia | Desactivado | Activa la reducción de ruido RNN. | |
| Botón NRF (pestaña DSP) | Botón de alternancia | Desactivado | Activa el filtro de ruido espectral. | |
| Botón ANFL (pestaña DSP) | Botón de alternancia | Desactivado | Activa el filtro de muesca LMS. | |
| Botón ANFT (pestaña DSP) | Botón de alternancia | Desactivado | Activa el filtro de muesca FFT. | |
| Botón ADSP (pestaña DSP) | Botón pulsador | — | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene el estilo de una alternancia DSP del lado de la radio pero no es verificable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Botón pulsador | — | Alterna el Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para el strip. |
| Combinación Mode (pestaña Mode) | Cuadro combinado | USB | Establece el modo de demodulación para este slice. | |
| Botones preestablecidos de filtro (pestaña Mode) | Botón pulsador | — | Aplica un ancho de filtro preestablecido guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. | Se persiste en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |
| Botones RIT / XIT + etiquetas (pestaña X/RIT) | Botón de alternancia | Desactivado | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. | |
| Combinación de canal DAX (pestaña DAX) | Cuadro combinado | Desactivado | Asigna un canal de audio DAX a este slice. | |
| Botón de grosor del marcador | Botón pulsador | 1 px | Recorre cíclicamente la línea del marcador VFO entre Desactivado, 1 px y 3 px. | Se persiste por slice en `Slice{N}_MarkerWidth`. |
| Botón de bordes de filtro | Botón de alternancia | Mostrado | Alterna las líneas de borde del filtro en la banda de paso del espectro. | Se persiste por slice en `Slice{N}_FilterEdgesHidden`. |
| Alternancia de contracción | Botón de alternancia | Expandido | Contrae el panel VFO a una tira compacta solo de frecuencia. | Se persiste por slice en `SliceFlagCollapsed_{N}`. |

## Cambios en la pestaña DSP en v0.9.7 (refinados en v0.9.8)

La pestaña DSP ahora muestra solo los algoritmos de reducción de ruido proporcionados por la radio. Los botones para NR2, RN2, BNR, NR4, MNR y DFNR se han eliminado del panel VFO. Esos algoritmos son módulos del lado del cliente; acceda a ellos a través del menú superpuesto del espectro o del applet de AetherDSP.

Los botones presentes en la pestaña DSP son:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Eliminador de ruido (noise blanker) |
| ANF | Filtro de muesca automático |
| APF | Filtro de énfasis de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

Una fila compartida de **Nivel DSP** aparece debajo de la cuadrícula de botones. Contiene un deslizador y una lectura numérica. El deslizador se reorienta automáticamente al algoritmo DSP con nivel que se haya activado más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). Cuando ningún algoritmo DSP con nivel está activo, o cuando solo RNN, ANFT o APF están encendidos, la fila se atenúa y la interacción con el deslizador no tiene efecto. La fila permanece en el diseño en todo momento; no desplaza la cuadrícula de botones cuando se atenúa o aparece.

Algoritmos que admiten un nivel a través de este deslizador: NR, NB, ANF, NRL, NRS, NRF, ANFL.

**Nota:** En v0.9.8, el deslizador de nivel DSP ahora aparece al inicio para cualquier algoritmo DSP que estuviera activado en el perfil guardado de la radio. Anteriormente, no aparecía hasta que el usuario alternaba manualmente el botón DSP.

## Consejos

- Silenciar un slice no restablece el deslizador de ganancia AF. Al reactivar el audio, este regresa al mismo nivel que tenía antes.
- Si desea silenciar un slice de forma permanente en lugar de temporal, arrastre el deslizador de ganancia AF a 0.
- Para acceder a NR2, RN2, BNR, NR4, MNR o DFNR, haga clic derecho en la pantalla de espectro para abrir el menú superpuesto, o abra el applet de AetherDSP.
- Los botones ADSP y AetherVoice en la pestaña DSP son lanzadores del lado del cliente. Tienen el estilo de alternancias DSP del lado de la radio pero no son verificables.
- Use el botón **ADSP** para abrir el diálogo de configuración de AetherDSP para los algoritmos de reducción de ruido del lado del cliente.
- Use el botón **AetherVoice** para abrir el Aetherial Audio Channel Strip para el DSP unificado de TX/RX.

## Relacionado

- [Adjust AF gain and pan from the VFO panel](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Enable squelch from the VFO panel](enable-squelch-from-the-vfo-panel.md)
- [Collapse the VFO panel to frequency-only view](collapse-the-vfo-panel-to-frequency-only-view.md)
