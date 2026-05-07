# Establecer un borde de filtro personalizado desde el panel VFO

Los botones preestablecidos de filtro del panel VFO le permiten guardar y recuperar anchos de filtro rápidamente. Al hacer clic derecho en un botón preestablecido, se abre un diálogo donde puede establecer valores exactos de borde bajo y alto del filtro para esa ranura. Utilice esta función cuando los anchos preestablecidos incorporados no se ajusten a sus necesidades operativas.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO debe estar abierto. Si no está visible, haga clic en la bandera marcadora VFO en la visualización del espectro para la franja que desea ajustar.
- El panel VFO no debe estar colapsado. Si solo muestra una tira de frecuencia, haga clic en cualquier parte para expandirlo.
- Abra la pestaña **Mode** dentro del panel VFO para que los botones preestablecidos de filtro estén visibles.

## Pasos

1. Haga clic en la bandera marcadora VFO en la visualización del espectro para abrir el panel VFO de la franja objetivo.
2. En el panel VFO, haga clic en la pestaña **Mode** para mostrar el selector de modo y los botones preestablecidos de filtro.
3. Haga clic derecho en el botón preestablecido de filtro cuyos bordes desea personalizar. Aparecerá un menú contextual o diálogo.
4. Ingrese los valores deseados de borde bajo y borde alto en los campos proporcionados.
5. Confirme la entrada para guardar los bordes personalizados en esa ranura preestablecida.

El botón preestablecido ahora aplicará sus bordes de filtro personalizados al hacer clic. Los valores se conservan en `FilterPresets`.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de esta franja. | — |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de esta franja. | — |
| Visualización de frecuencia | Muestra la frecuencia actual de la franja. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. | — |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. Usa RxApplet::formatFilterWidth como fuente única de verdad, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). | — |
| Deslizador AF Gain (pestaña Audio) | Establece el nivel de salida de audio para esta franja (0–100). No se conserva; refleja el estado en vivo de la radio. | 100 |
| Deslizador Pan (pestaña Audio) | Establece la panorámica estéreo izquierda/derecha para esta franja. 50 = centro. | 50 |
| Botón Mute (pestaña Audio) | Silencia la salida de audio de esta franja sin cambiar la configuración de ganancia AF. | off |
| Botón + deslizador Squelch (pestaña Audio) | Activa el squelch para esta franja. El deslizador adyacente establece el umbral (0–100). | off |
| Combo AGC (pestaña Audio) | Establece la velocidad de ataque/liberación del AGC para esta franja: FAST, MED, SLOW u OFF. | FAST |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Activa el algoritmo de reducción de ruido correspondiente para esta franja. La disponibilidad del botón depende de la serie de la radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. | off |
| Botón ADSP (pestaña DSP) | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Estilizado como un conmutador DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. | — |
| Botón AetherVoice (pestaña DSP) | Activa/desactiva el Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. | — |
| Combo Mode (pestaña Mode) | Establece el modo de demodulación para esta franja: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY. | USB |
| Botones preestablecidos de filtro (pestaña Mode) | Aplica un ancho de filtro guardado al hacer clic. Haga clic derecho para guardar el ancho de filtro actual o establecer bordes inferiores/superiores personalizados para esa ranura. Se conservan en FilterPresets. | — |
| Botones y etiquetas RIT / XIT (pestaña X/RIT) | Activa la sintonización incremental del receptor (RIT) o transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. | off |
| Combo de canal DAX (pestaña DAX) | Asigna un canal de audio DAX a esta franja: Off o 1–8. | Off |
| Botón de grosor del marcador | Cambia la línea del marcador VFO entre Off, 1 px y 3 px. Se conserva por franja. | 1 px |
| Botón de bordes de filtro | Activa/desactiva las líneas de borde de filtro en la visualización de la banda pasante del espectro. Se conserva por franja. | mostrado |
| Conmutador de colapso | Colapsa el panel VFO a una tira compacta solo de frecuencia. Se conserva por franja. | expandido |

### Indicadores

| Etiqueta | Estados | Significado |
|---|---|---|
| Insignia TX | TX (rojo) / oculto | Se muestra cuando esta franja es la franja transmisora activa. |
| Insignia SPLIT | SPLIT (ámbar) / oculto | Se muestra cuando TX está asignada a una franja diferente a la franja receptora activa. |

### Botones de la pestaña DSP

A partir de la v0.9.7, la pestaña **DSP** muestra solo los botones de reducción de ruido proporcionados por la radio. Los algoritmos del lado del cliente (NR2, NR4, MNR, BNR, DFNR, RN2) se han movido al menú superpuesto del espectro y al applet AetherDSP; actívelos desde allí.

Los botones disponibles en la pestaña DSP son:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Eliminador de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de pico de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |
| ADSP | Abre el diálogo de configuración de AetherDSP (algoritmos del lado del cliente) |
| AetherVoice | Abre el Aetherial Audio Channel Strip (conjunto unificado de DSP de TX/RX) |

#### Deslizador de nivel DSP

Cuando una o más funciones DSP del lado de la radio que admiten control de nivel están activadas, aparece un deslizador de nivel compartido debajo de la cuadrícula de botones. La etiqueta y el valor del deslizador se actualizan para reflejar la función activada más recientemente. El deslizador siempre está presente en el diseño pero se atenúa cuando ninguna función DSP compatible está activa. Arrastre el deslizador para establecer el nivel (0–100) para la función objetivo.

Funciones a las que el deslizador de nivel puede apuntar: NR, NB, ANF, NRL, NRS, NRF, ANFL.

Funciones que no apuntan al deslizador de nivel: RNN, ANFT, APF.

## Consejos

- Para verificar los bordes de filtro activos en el espectro, confirme que el botón de bordes de filtro esté en su estado mostrado predeterminado. Si las líneas de borde están ocultas, presione el botón de bordes de filtro para hacerlas visibles nuevamente.
- Haga clic derecho en un botón preestablecido para guardar el ancho de filtro *actual* en esa ranura como alternativa a escribir los valores de borde manualmente. Utilice esto para una captura rápida de un filtro que ya haya ajustado.
- Para acceder a NR2, NR4, MNR, BNR, DFNR o RN2, haga clic derecho en la visualización del espectro para abrir el menú superpuesto, o abra el applet AetherDSP.
- Los botones ADSP y AetherVoice se colocan en la cuadrícula de botones de la pestaña DSP junto a los conmutadores DSP del lado de la radio. No son seleccionables: al hacer clic en ADSP se abre el diálogo de configuración de AetherDSP, y al hacer clic en AetherVoice se abre el Aetherial Audio Channel Strip.

## Relacionado

- [Apply a filter width preset from the VFO panel](apply-a-filter-width-preset-from-the-vfo-panel.md)
- [Hide or show filter edge lines on the spectrum](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Change mode from the VFO panel](change-mode-from-the-vfo-panel.md)
