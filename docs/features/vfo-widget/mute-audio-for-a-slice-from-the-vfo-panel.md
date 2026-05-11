# Silenciar el audio de un slice desde el panel VFO

Silencie la salida de audio de un slice individual sin cambiar su configuración de ganancia AF. Utilice esto cuando desee suprimir un slice temporalmente y restaurar su volumen anterior con un solo clic.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO para el slice objetivo debe estar abierto. Si está colapsado a una tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo primero.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el slice que desea silenciar. El panel VFO se abre anclado al marcador.
2. Haga clic en **Audio** para seleccionar la pestaña Audio dentro del panel VFO.
3. Haga clic en **Mute**. El botón se activa y la salida de audio del slice se detiene. El valor del deslizador de ganancia AF no cambia.
4. Para restaurar el audio, haga clic en **Mute** nuevamente. El botón se desactiva y el audio se reanuda en el nivel de ganancia AF anterior.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Notas |
|---------|------|---------------------|---------------|-------|
| Botón de antena RX | Botón pulsador | — | Abre el menú de selección de antena para la antena receptora de este slice. | |
| Botón de antena TX | Botón pulsador | — | Abre el menú de selección de antena para la antena transmisora de este slice. | |
| Pantalla de frecuencia | Indicador | — | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. | |
| Etiqueta de ancho de filtro | Indicador | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad. | Corrige un desplazamiento de 0,1 kHz que afectaba las lecturas en modos SSB/digitales (#2197, v0.9.8). |
| Deslizador de ganancia AF (pestaña Audio) | Deslizador | 100 | Establece el nivel de salida de audio para este slice. | No se conserva: refleja el estado activo de la radio. |
| Deslizador de paneo (pestaña Audio) | Deslizador | 50 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. | |
| Botón Mute (pestaña Audio) | Botón de alternancia | Desactivado | Silencia la salida de audio de este slice sin cambiar la configuración de ganancia AF. | |
| Botón + deslizador de Squelch (pestaña Audio) | Botón de alternancia | Desactivado | Activa el squelch para este slice. El deslizador adyacente establece el umbral. | El squelch está deshabilitado en modos digital, RTTY y CW. En modos digital y RTTY, el audio alimenta decodificadores externos a través de DAX y el squelch no es significativo: también bloquea señales FSK débiles. En modo CW, la radio bloquea el squelch en un nivel fijo y rechaza los cambios. |
| Combo AGC (pestaña Audio) | Cuadro combinado | FAST | Establece la velocidad de ataque/liberación del AGC para este slice. | |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Botón de alternancia | Desactivado | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de botones depende de la serie de radio y la compilación. | Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo de Configuración de AetherDSP para ese algoritmo. |
| Botón ADSP (pestaña DSP) | Botón pulsador | — | Abre el cuadro de diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene estilo de alternancia DSP del lado de la radio pero no se puede marcar. Al hacer clic, abre y enfoca el cuadro de diálogo no modal de Configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Botón pulsador | — | Alterna la Aetherial Audio Channel Strip: el conjunto unificado de DSP TX/RX (v0.9.8). | Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Combo Mode (pestaña Mode) | Cuadro combinado | USB | Establece el modo de demodulación para este slice. | |
| Botones de preajuste de filtro (pestaña Mode) | Botón pulsador | — | Aplica un preajuste guardado de ancho de filtro. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. | Se conserva en `FilterPresets`. Los bordes lo/hi personalizados se pueden establecer por ranura mediante clic derecho. |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Botón de alternancia | Desactivado | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. | |
| Combo de canal DAX (pestaña DAX) | Cuadro combinado | Desactivado | Asigna un canal de audio DAX a este slice. | |
| Botón de grosor del marcador | Botón pulsador | 1 px | Recorre la línea del marcador VFO entre Desactivado, 1 px y 3 px. | Se conserva por slice en `Slice{N}_MarkerWidth`. |
| Botón de bordes del filtro | Botón de alternancia | Mostrado | Alterna las líneas de borde del filtro en la banda pasante del espectro. | Se conserva por slice en `Slice{N}_FilterEdgesHidden`. |
| Botón de colapso | Botón de alternancia | Expandido | Colapsa el panel VFO a una tira compacta de solo frecuencia. | Se conserva por slice en `SliceFlagCollapsed_{N}`. |

## Cambios en la pestaña DSP en v0.9.7 (refinados en v0.9.8)

La pestaña DSP ahora muestra solo los algoritmos de reducción de ruido suministrados por la radio. Los botones para NR2, RN2, BNR, NR4, MNR y DFNR se han eliminado del panel VFO. Esos algoritmos son módulos del lado del cliente; acceda a ellos a través del menú superpuesto del espectro o del applet AetherDSP.

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

Una fila compartida de **Nivel DSP** aparece debajo de la cuadrícula de botones. Contiene un deslizador y una lectura numérica. El deslizador se reorienta automáticamente al algoritmo DSP nivelado que se haya habilitado más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). Cuando ningún algoritmo DSP nivelado está activo, o solo RNN, ANFT o APF está encendido, la fila se atenúa y la interacción con el deslizador no tiene efecto. La fila permanece en el diseño en todo momento; no desplaza la cuadrícula de botones cuando se atenúa o aparece.

Algoritmos que admiten un nivel a través de este deslizador: NR, NB, ANF, NRL, NRS, NRF, ANFL.

**Nota:** En v0.9.8, el deslizador de nivel DSP ahora aparece al inicio para cualquier algoritmo DSP que estuviera habilitado en el perfil guardado de la radio. Anteriormente, faltaba hasta que el usuario alternaba manualmente el botón DSP.

## Comportamiento del squelch por modo

El botón y deslizador de squelch se deshabilitan automáticamente en ciertos modos:

- **Modos digitales (DIGU, DIGL):** El squelch está deshabilitado porque el audio alimenta decodificadores externos a través de DAX; el squelch no es significativo y bloquea señales FSK débiles.
- **RTTY:** El squelch está deshabilitado por las mismas razones que los modos digitales, resolviendo un problema donde el squelch bloqueaba señales FSK débiles (#2504).
- **CW:** El squelch está deshabilitado porque la radio bloquea el squelch en un nivel fijo y rechaza los cambios.

Cuando el squelch está deshabilitado y estaba previamente activado, el sistema apaga automáticamente el squelch para el slice y guarda su estado. Cuando vuelva a un modo de voz, el squelch puede restaurarse.

## Consejos

- Silenciar un slice no restablece el deslizador de ganancia AF. Cuando lo reactive, el audio regresa al mismo nivel que tenía antes.
- Si desea silenciar un slice de forma permanente en lugar de temporal, arrastre el deslizador de ganancia AF a 0.
- Para acceder a NR2, RN2, BNR, NR4, MNR o DFNR, haga clic derecho en la pantalla del espectro para abrir el menú superpuesto, o abra el applet AetherDSP.
- Los botones ADSP y AetherVoice en la pestaña DSP son lanzadores del lado del cliente. Tienen estilo de alternativas DSP del lado de la radio pero no se pueden marcar.
- Use el botón **ADSP** para abrir el cuadro de diálogo de Configuración de AetherDSP para algoritmos de reducción de ruido del lado del cliente.
- Use el botón **AetherVoice** para abrir la Aetherial Audio Channel Strip para DSP TX/RX unificado.
- El squelch se deshabilita automáticamente en modos digital, RTTY y CW. Si cambia a uno de estos modos mientras el squelch está activado, el sistema lo apagará y guardará su estado para restaurarlo cuando regrese a un modo de voz.

## Relacionado

- [Ajustar ganancia AF y paneo desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Activar squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
- [Colapsar el panel VFO a vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
