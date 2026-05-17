# Silenciar el audio de un segmento desde el panel VFO

Silencie la salida de audio de un segmento individual sin cambiar su ajuste de Ganancia AF. Utilícelo cuando desee suprimir un segmento temporalmente y restaurar su volumen anterior con un solo clic.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO del segmento objetivo debe estar abierto. Si está colapsado a una tira de solo frecuencia, haga clic en cualquier lugar del mismo para expandirlo primero.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla de espectro del segmento que desea silenciar. El panel VFO se abre anclado al marcador.
2. Haga clic en **Audio** para seleccionar la pestaña Audio dentro del panel VFO.
3. Haga clic en **Mute**. El botón se activa y la salida de audio del segmento se detiene. El valor del deslizador de Ganancia AF no cambia.
4. Para restaurar el audio, haga clic en **Mute** nuevamente. El botón se desactiva y el audio se reanuda al nivel de Ganancia AF anterior.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Notas |
|---------|------|---------------------|----------------|-------|
| Botón de antena RX | Botón pulsador | — | Abre el menú de selección de antena para la antena receptora de este segmento. El menú usa `rxAntennaList()` si está disponible; de lo contrario, recurre a la lista completa de antenas. Cada acción establece la antena mediante `data()`. | |
| Botón de antena TX | Botón pulsador | — | Abre el menú de selección de antena para la antena transmisora de este segmento. El menú se construye a partir de `txAntennaOptions()`, que filtra los puertos solo de RX. Cada acción establece la antena mediante `data()`. | |
| Indicador de frecuencia | Indicador | — | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. En bandas XVTR, la entrada de números enteros inserta un decimal después del tercer dígito para bandas de 2m/70cm (rango 100-999 MHz). Para bandas de 23cm y microondas, los números enteros se tratan como valores completos de MHz. | |
| Etiqueta de ancho de filtro | Indicador | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de ajustes preestablecidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad. | Corrige un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| Deslizador de Ganancia AF (pestaña Audio) | Deslizador | 100 | Establece el nivel de salida de audio para este segmento. | No se persiste: refleja el estado en vivo de la radio. |
| Deslizador de Pan (pestaña Audio) | Deslizador | 50 | Establece el paneo estéreo izquierdo/derecho para este segmento. 50 = centro. | |
| Botón Mute (pestaña Audio) | Botón de alternancia | Off | Silencia la salida de audio de este segmento sin cambiar el ajuste de ganancia AF. | |
| Botón + deslizador de Squelch (pestaña Audio) | Botón de alternancia | Off | Activa el squelch para este segmento. El deslizador adyacente establece el umbral. | El squelch está desactivado en modos digital, RTTY y CW. En modos digital y RTTY, el audio alimenta decodificadores externos a través de DAX y el squelch no tiene sentido; también bloquea señales FSK débiles. En modo CW, la radio bloquea el squelch activado a un nivel fijo y rechaza los cambios. |
| Combo AGC (pestaña Audio) | Cuadro combinado | FAST | Establece la velocidad de ataque/liberación del AGC para este segmento. | |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Botón de alternancia | Off | Activa el algoritmo de reducción de ruido correspondiente para este segmento. La disponibilidad del botón depende de la serie de radio y la compilación. | Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |
| Botón ADSP (pestaña DSP) | Botón pulsador | — | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene el estilo de una alternancia DSP del lado de la radio, pero no es marcable. Al hacer clic, abre y enfoca el diálogo de configuración de AetherDSP no modal. |
| Botón AetherVoice (pestaña DSP) | Botón pulsador | — | Alterna la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8). | Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para el strip. |
| Combo Mode (pestaña Mode) | Cuadro combinado | USB | Establece el modo de demodulación para este segmento. | |
| Botones de ajustes preestablecidos de filtro (pestaña Mode) | Botón pulsador | — | Aplica un ajuste preestablecido de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. | Se persiste en `FilterPresets`. Los bordes lo/hi personalizados se pueden establecer por ranura mediante clic derecho. |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Botón de alternancia | Off | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. | |
| Combo de canal DAX (pestaña DAX) | Cuadro combinado | Off | Asigna un canal de audio DAX a este segmento. | |
| Botón de grosor del marcador | Botón pulsador | 1 px | Alterna la línea del marcador VFO entre Off, 1 px y 3 px. | Se persiste por segmento en `Slice{N}_MarkerWidth`. |
| Botón de bordes del filtro | Botón de alternancia | Mostrado | Alterna las líneas de borde del filtro en la banda pasante del espectro. | Se persiste por segmento en `Slice{N}_FilterEdgesHidden`. |
| Alternancia de colapso | Botón de alternancia | Expandido | Colapsa el panel VFO a una tira compacta de solo frecuencia. | Se persiste por segmento en `SliceFlagCollapsed_{N}`. |

## Cambios en la pestaña DSP en v0.9.7 (refinados en v0.9.8)

La pestaña DSP ahora muestra solo los algoritmos de reducción de ruido proporcionados por la radio. Los botones para NR2, RN2, BNR, NR4, MNR y DFNR se han eliminado del panel VFO. Esos algoritmos son módulos del lado del cliente; acceda a ellos a través del menú superpuesto del espectro o del applet AetherDSP.

Los botones presentes en la pestaña DSP son:

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

Una fila compartida **DSP Level** aparece debajo de la cuadrícula de botones. Contiene un deslizador y una lectura numérica. El deslizador se reorienta automáticamente al algoritmo DSP nivelado que se haya activado más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). Cuando ningún algoritmo DSP nivelado está activo, o solo RNN, ANFT o APF lo está, la fila se desvanece y la interacción con el deslizador no tiene efecto. La fila permanece en el diseño en todo momento; no desplaza la cuadrícula de botones cuando aparece o desaparece.

Algoritmos que admiten un nivel a través de este deslizador: NR, NB, ANF, NRL, NRS, NRF, ANFL.

**Nota:** En v0.9.8, el deslizador de nivel DSP ahora aparece al inicio para cualquier algoritmo DSP que estuviera habilitado en el perfil guardado de la radio. Anteriormente, faltaba hasta que el usuario alternaba manualmente el botón DSP.

## Comportamiento del squelch por modo

El botón y el deslizador de squelch se desactivan automáticamente en ciertos modos:

- **Modos digitales (DIGU, DIGL):** El squelch está desactivado porque el audio alimenta decodificadores externos a través de DAX; el squelch no tiene sentido y bloquea señales FSK débiles.
- **RTTY:** El squelch está desactivado por las mismas razones que en los modos digitales, resolviendo un problema donde el squelch bloqueaba señales FSK débiles (#2504).
- **CW:** El squelch está desactivado porque la radio bloquea el squelch activado a un nivel fijo y rechaza los cambios.

Cuando el squelch está desactivado y estaba previamente activado, el sistema apaga automáticamente el squelch para el segmento y guarda su estado. Cuando cambie de nuevo a un modo de voz, el squelch puede restaurarse.

## Consejos

- Silenciar un segmento no restablece el deslizador de Ganancia AF. Cuando reactive el sonido, el audio regresa al mismo nivel que tenía antes.
- Si desea silenciar un segmento de forma permanente en lugar de temporal, arrastre el deslizador de Ganancia AF a 0.
- Para acceder a NR2, RN2, BNR, NR4, MNR o DFNR, haga clic derecho en la pantalla de espectro para abrir el menú superpuesto, o abra el applet AetherDSP.
- Los botones ADSP y AetherVoice en la pestaña DSP son lanzadores del lado del cliente. Tienen el estilo de alternancias DSP del lado de la radio, pero no son marcables.
- Use el botón **ADSP** para abrir el diálogo de configuración de AetherDSP para algoritmos de reducción de ruido del lado del cliente.
- Use el botón **AetherVoice** para abrir la Aetherial Audio Channel Strip para DSP unificado de TX/RX.
- El squelch se desactiva automáticamente en modos digital, RTTY y CW. Si cambia a uno de estos modos mientras el squelch está activado, el sistema lo apagará y guardará su estado para restaurarlo cuando regrese a un modo de voz.
- La insignia del segmento ahora admite formato de texto enriquecido para la letra del segmento (#2606), lo que permite la representación HTML adecuada en la etiqueta de la insignia.

## Relacionado

- [Ajustar ganancia AF y paneo desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Activar squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
- [Colapsar el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
