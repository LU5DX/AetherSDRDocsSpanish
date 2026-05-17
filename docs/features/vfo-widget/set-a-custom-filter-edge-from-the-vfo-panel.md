# Establecer un borde de filtro personalizado desde el panel VFO

Los botones de preselección de filtro del panel VFO le permiten guardar y recuperar anchos de filtro rápidamente. Al hacer clic derecho en un botón de preselección, se abre un cuadro de diálogo donde puede establecer valores exactos de borde de filtro bajo y alto para esa ranura. Utilice esta opción cuando los anchos de preselección incorporados no se ajusten a sus necesidades operativas.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO debe estar abierto. Si no está visible, haga clic en la bandera del marcador VFO en la pantalla del espectro para la porción que desea ajustar.
- El panel VFO no debe estar colapsado. Si solo muestra una franja de frecuencia, haga clic en cualquier lugar del mismo para expandirlo.
- Abra la pestaña **Mode** dentro del panel VFO para que los botones de preselección de filtro estén visibles.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para abrir el panel VFO de la porción objetivo.
2. En el panel VFO, haga clic en la pestaña **Mode** para mostrar el selector de modo y los botones de preselección de filtro.
3. Haga clic derecho en el botón de preselección de filtro cuyos bordes desea personalizar. Aparece un menú contextual o un cuadro de diálogo.
4. Ingrese los valores de borde bajo y alto deseados en los campos proporcionados.
5. Confirme la entrada para guardar los bordes personalizados en esa ranura de preselección.

El botón de preselección ahora aplica sus bordes de filtro personalizados al hacer clic. Los valores se conservan en `FilterPresets`.

## Qué hace cada control

| Control                          | Comportamiento                                                                                                                                                                                                                                                                                                                                                   | Valor predeterminado                                                                                                         |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| Botón de antena RX              | Abre el menú de selección de antena para la antena receptora de esta porción. Ahora usa la lista de antenas por porción de la radio cuando está disponible; recurre a la lista global de antenas si está vacía. Cada elemento del menú muestra su nombre interno de antena como información sobre herramientas y sugerencia de estado. | —                                                                                                                           |
| Botón de antena TX              | Abre el menú de selección de antena para la antena transmisora de esta porción. Filtra automáticamente los puertos de antena solo de recepción. Usa `txAntennaOptions()` para determinar las antenas disponibles. Cada elemento del menú muestra su nombre interno de antena como información sobre herramientas y sugerencia de estado. | —                                                                                                                           |
| Pantalla de frecuencia          | Muestra la frecuencia actual de la porción. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. En bandas XVTR, acepta frecuencias de hasta 50000 MHz. Para 2m/70cm (rango de 100–999 MHz), un número entero simple como 1446 se convierte automáticamente a 144.6 MHz. En bandas de 23cm y microondas (≥1000 MHz), un número entero simple se trata directamente como MHz. | —                                                                                                                           |
| Etiqueta de ancho de filtro     | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode. Usa RxApplet::formatFilterWidth como única fuente de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modos SSB/digital (#2197, v0.9.8). | —                                                                                                                           |
| Insignia de porción             | Muestra la letra de la porción (p. ej., A, B) en una insignia de color. Ahora admite representación HTML para la letra de la porción (#2606). Haga clic para seleccionar esta porción.                                                                                                                                                                          | —                                                                                                                           |
| Deslizador de ganancia AF (pestaña Audio) | Establece el nivel de salida de audio para esta porción (0–100). No se conserva: refleja el estado vivo de la radio.                                                                                                                                                                                                                                             | 100                                                                                                                         |
| Deslizador de paneo (pestaña Audio) | Establece el paneo estéreo izquierdo/derecho para esta porción. 50 = centro.                                                                                                                                                                                                                                                                                        | 50                                                                                                                          |
| Botón de silencio (pestaña Audio) | Silencia la salida de audio para esta porción sin cambiar el ajuste de ganancia AF.                                                                                                                                                                                                                                                                                | desactivado                                                                                                                  |
| Botón + deslizador de squelch (pestaña Audio) | Activa el squelch para esta porción. El deslizador adyacente establece el umbral (0–100). El squelch se desactiva y se fuerza a desactivar cuando el modo de la porción es DIGU, DIGL, RTTY o cualquier modo CW, ya que no es significativo para audio digital/RTTY alimentado a través de DAX o para CW donde la radio bloquea el squelch (#2504). | desactivado |
| Combo de AGC (pestaña Audio)    | Establece la velocidad de ataque/liberación del AGC para esta porción: FAST, MED, SLOW u OFF.                                                                                                                                                                                                                                                                    | FAST                                                                                                                    |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Activa el algoritmo de reducción de ruido correspondiente para esta porción. La disponibilidad de los botones depende de la serie de radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo de configuración de AetherDSP para ese algoritmo. | desactivado |
| Botón ADSP (pestaña DSP)        | Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Es el mismo punto de entrada que el menú de configuración (v0.9.8). Tiene estilo similar a un conmutador DSP del lado de la radio pero no es seleccionable. Al hacer clic, abre y enfoca el cuadro de diálogo no modal de configuración de AetherDSP. | — |
| Botón AetherVoice (pestaña DSP) | Activa/desactiva el Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula de 4 columnas de DSP. Coincide con los puntos de entrada existentes del menú/cadena para el strip. | — |
| Combo de modo (pestaña Mode)    | Establece el modo de demodulación para esta porción: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY.                                                                                                                                                                                                                                                 | USB                                                                                                                    |
| Botones de preselección de filtro (pestaña Mode) | Aplica un ancho de filtro guardado al hacer clic. Haga clic derecho para guardar el ancho de filtro actual o establecer bordes bajo/alto personalizados para esa ranura. Se conserva en FilterPresets.                                                                                                                                                              | —                                                                                                                       |
| Botones RIT / XIT + etiquetas (pestaña X/RIT) | Activa la sintonización incremental del receptor (RIT) o transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz.                                                                                                                                                                                               | desactivado                                                                                                                     |
| Combo de canal DAX (pestaña DAX) | Asigna un canal de audio DAX a esta porción: Off o 1–8.                                                                                                                                                                                                                                                                                                            | Off                                                                                                                     |
| Botón de grosor del marcador    | Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Se conserva por porción.                                                                                                                                                                                                                                                                                  | 1 px                                                                                                                    |
| Botón de bordes de filtro       | Activa/desactiva las líneas de borde del filtro en la pantalla de banda pasante del espectro. Se conserva por porción.                                                                                                                                                                                                                                             | mostrado                                                                                                                   |
| Conmutador de colapso           | Colapsa el panel VFO a una franja compacta solo de frecuencia. Se conserva por porción.                                                                                                                                                                                                                                                                            | expandido                                                                                                                |

### Indicadores

| Etiqueta     | Estados               | Significado                                                                |
|--------------|-----------------------|----------------------------------------------------------------------------|
| Insignia TX  | TX (rojo) / oculto    | Se muestra cuando esta porción es la porción de transmisión activa.        |
| Insignia SPLIT | SPLIT (ámbar) / oculto | Se muestra cuando TX está asignada a una porción diferente a la porción de recepción activa. |

### Botones de la pestaña DSP

A partir de v0.9.7, la pestaña **DSP** muestra solo los botones de reducción de ruido proporcionados por la radio. Los algoritmos del lado del cliente (NR2, NR4, MNR, BNR, DFNR, RN2) se han movido al menú superpuesto del espectro y al applet de AetherDSP; actívelos/desactívelos allí.

Los botones disponibles en la pestaña DSP son:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Supresor de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de pico de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |
| ADSP | Abre el cuadro de diálogo de configuración de AetherDSP (algoritmos del lado del cliente) |
| AetherVoice | Abre el Aetherial Audio Channel Strip (conjunto unificado de DSP de TX/RX) |

#### Deslizador de nivel DSP

Cuando una o más funciones DSP del lado de la radio que admiten un control de nivel están activadas, aparece un deslizador de nivel compartido debajo de la cuadrícula de botones. La etiqueta y el valor del deslizador se actualizan para reflejar la función activada más recientemente. El deslizador siempre está presente en el diseño, pero se atenúa cuando ninguna función DSP compatible está activa. Arrastre el deslizador para establecer el nivel (0–100) para la función objetivo.

Funciones a las que el deslizador de nivel puede dirigirse: NR, NB, ANF, NRL, NRS, NRF, ANFL.

Funciones a las que el deslizador de nivel no se dirige: RNN, ANFT, APF.

## Consejos

- Para verificar los bordes de filtro activos en el espectro, confirme que el botón de bordes de filtro esté en su estado mostrado predeterminado. Si las líneas de borde están ocultas, presione el botón de bordes de filtro para hacerlas visibles nuevamente.
- Haga clic derecho en un botón de preselección para guardar el ancho de filtro *actual* en esa ranura como alternativa a escribir valores de borde manualmente. Úselo para una captura rápida de un filtro que ya ha ajustado.
- Para acceder a NR2, NR4, MNR, BNR, DFNR o RN2, haga clic derecho en la pantalla del espectro para abrir el menú superpuesto, o abra el applet AetherDSP.
- Los botones ADSP y AetherVoice se colocan en la cuadrícula de botones de la pestaña DSP junto con los conmutadores DSP del lado de la radio. No son seleccionables: al hacer clic en ADSP, se abre el cuadro de diálogo de configuración de AetherDSP, y al hacer clic en AetherVoice, se abre el Aetherial Audio Channel Strip.
- El squelch se desactiva automáticamente y se fuerza a desactivar cuando cambia a DIGU, DIGL, RTTY o cualquier modo CW. Para volver a activar el squelch, cambie a un modo de voz (USB, LSB, AM, SAM, FM, NFM, DFM).

## Relacionado

- [Apply a filter width preset from the VFO panel](apply-a-filter-width-preset-from-the-vfo-panel.md)
- [Hide or show filter edge lines on the spectrum](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Change mode from the VFO panel](change-mode-from-the-vfo-panel.md)
