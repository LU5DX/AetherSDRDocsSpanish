# Cambiar modo desde el panel VFO

Use la pestaña Modo del panel VFO para cambiar el modo de demodulación de cualquier slice — por ejemplo, de USB a CW o FM — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO debe estar abierto. Si no es visible, haga clic en la bandera del marcador VFO en la pantalla del espectro para el slice que desea cambiar.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el slice objetivo. Se abre el panel VFO, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el **Mode combo** y seleccione el modo deseado de la lista.

## Función de cada control

| Control                      | Valor predeterminado                                                                                                                 | Valores válidos                                                                                                            |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Mode combo                   | USB                                                                                                                                  | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY                                                               |
| Filter preset buttons        | —                                                                                                                                    | Presets guardados de ancho de filtro                                                                                       |
| ADSP button (pestaña DSP)    | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene el estilo de un conmutador de DSP del lado de la radio pero no es marcable. Al hacer clic, abre y enfoca el diálogo AetherDSP Settings no modal. |
| AetherVoice button (pestaña DSP) | Activa/desactiva Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX (v0.9.8).                                     | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada del menú/chain existentes para el canal. |
| RX antenna button            | —                                                                                                                                    | Abre el menú de selección de antena para la antena receptora de este slice.                                                |
| TX antenna button            | —                                                                                                                                    | Abre el menú de selección de antena para la antena transmisora de este slice.                                              |
| Frequency display            | —                                                                                                                                    | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Filter width label           | —                                                                                                                                    | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preset de filtro. Usa `RxApplet::formatFilterWidth`. |
| AF Gain slider (pestaña Audio) | 100                                                                                                                                  | 0-100. Establece el nivel de salida de audio para este slice.                                                              |
| Pan slider (pestaña Audio)   | 50                                                                                                                                   | 0-100. Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro.                                          |
| Mute button (pestaña Audio)  | off                                                                                                                                  | Conmutador. Silencia la salida de audio de este slice sin cambiar el ajuste de ganancia AF.                                 |
| Squelch button + slider (pestaña Audio) | off                                                                                                                           | 0-100. Activa el squelch para este slice. El deslizador adyacente establece el umbral.                                      |
| AGC combo (pestaña Audio)    | FAST                                                                                                                                 | FAST, MED, SLOW, OFF. Establece la velocidad de ataque/soltura del AGC para este slice.                                    |
| RIT / XIT buttons + labels (pestaña X/RIT) | off                                                                                                                           | Conmutador. Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La rueda del ratón ajusta en pasos de 10 Hz. |
| DAX channel combo (pestaña DAX) | Off                                                                                                                                  | Off, 1-8. Asigna un canal de audio DAX a este slice.                                                                       |
| Marker thickness button      | 1 px                                                                                                                                 | Off, 1 px, 3 px. Recorre el grosor de la línea del marcador VFO. Se conserva por slice.                                    |
| Filter edges button          | shown                                                                                                                                | Conmutador. Muestra u oculta las líneas de borde del filtro en la banda pasante del espectro. Se conserva por slice.       |
| Collapse toggle              | expanded                                                                                                                             | Conmutador. Colapsa el panel VFO a una franja compacta solo con la frecuencia. Se conserva por slice.                      |

**Mode combo** — establece el modo de demodulación para el slice. Al seleccionar un nuevo modo, el cambio se aplica inmediatamente en la radio.

**Filter preset buttons** — aparecen en la misma pestaña Mode. Cada botón aplica un ancho de filtro guardado. Haga clic derecho en un botón para guardar el ancho de filtro actual en esa ranura. Los presets se guardan en `FilterPresets`.

**Filter width label** — muestra el ancho de banda del filtro actual. Haga clic en él para recorrer los botones de preset de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modos SSB/digitales (#2197, v0.9.8).

## Controles de la pestaña DSP

La pestaña DSP muestra botones para algoritmos de reducción de ruido y filtrado suministrados directamente por la radio, además de botones de inicio del lado cliente. Están disponibles los siguientes botones:

| Botón | Descripción |
|---|---|
| NR | Reducción de ruido |
| NB | Eliminador de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de pico de audio (visible solo en modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |
| NR2 | Abre el algoritmo NR2 en el diálogo AetherDSP Settings (clic derecho) |
| NR4 | Abre el algoritmo NR4 en el diálogo AetherDSP Settings (clic derecho) |
| MNR | Abre el algoritmo MNR en el diálogo AetherDSP Settings (clic derecho) |
| DFNR | Abre el algoritmo DFNR en el diálogo AetherDSP Settings (clic derecho) |
| BNR | Abre el algoritmo BNR en el diálogo AetherDSP Settings (clic derecho) |
| RN2 | Abre el algoritmo RN2 en el diálogo AetherDSP Settings (clic derecho) |
| ADSP | Abre el diálogo AetherDSP Settings (mismo punto de entrada que el menú Settings) |
| AetherVoice | Activa/desactiva Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX |

Todos los botones del lado de la radio están desactivados por defecto y activan o desactivan el algoritmo correspondiente para el slice activo.

> **Nota:** Los módulos de reducción de ruido del lado cliente NR2, NR4, MNR, BNR, DFNR y RN2 son accesibles mediante clic derecho en la pestaña DSP para abrir el diálogo AetherDSP Settings, o desde el menú superpuesto del espectro y el applet AetherDSP.

### Deslizador de nivel DSP

Cuando uno o más algoritmos DSP con nivel (NR, NB, ANF, NRL, NRS, NRF o ANFL) están activos, aparece un deslizador de nivel debajo de la cuadrícula de botones DSP. La etiqueta del deslizador muestra qué algoritmo está siendo ajustado actualmente — el DSP con nivel habilitado más recientemente. El valor numérico se muestra a la derecha del deslizador.

- Rango: 0–100.
- El deslizador se reorienta automáticamente cuando habilita un botón DSP con nivel diferente.
- Cuando no hay ningún DSP con nivel activo, o cuando solo RNN, ANFT o APF están encendidos, la fila del deslizador se atenúa. Permanece en el diseño en todo momento para evitar que la cuadrícula de botones se desplace.
- Al iniciar, cualquier DSP habilitado en el perfil guardado de la radio ahora muestra correctamente el deslizador de nivel sin necesidad de conmutación manual (#startup-slider, v0.9.8).

## Comportamiento del squelch por modo

El botón y deslizador de squelch en la pestaña Audio se deshabilitan automáticamente en ciertos modos donde el squelch no es relevante:

- **Modos digitales (DIGU, DIGL)** — El audio alimenta decodificadores externos a través de DAX. El squelch está deshabilitado.
- **Modo RTTY** — Al igual que los modos digitales, el audio alimenta decodificadores externos. El squelch está deshabilitado para evitar el bloqueo de señales FSK débiles (#2504, v26.5.1).
- **Modo CW** — La radio bloquea el squelch encendido a un nivel fijo y rechaza los cambios. El squelch está deshabilitado.

Cuando el squelch está deshabilitado y estaba previamente habilitado, se apaga automáticamente para evitar un estado de squelch atascado. El indicador `m_savedSquelchOn` conserva el estado anterior para que pueda restaurarse al volver a un modo de voz.

## Consejos

- Cambiar de modo puede alterar la banda pasante activa del filtro. Verifique la etiqueta de ancho de filtro en la fila de encabezado después de cambiar de modo y aplique un preset de filtro si es necesario.
- La etiqueta de ancho de filtro en el encabezado del panel VFO muestra el ancho de banda actual. Haga clic en ella para recorrer los botones de preset de filtro en la pestaña Mode.
- Para acceder a NR2, NR4, MNR, BNR, DFNR o RN2, haga clic derecho en el botón de la pestaña DSP para ese algoritmo, o haga clic derecho en la pantalla del espectro y abra el menú superpuesto, o abra el applet AetherDSP.
- Los botones de grosor del marcador y bordes del filtro se conservan por slice en las claves de configuración `Slice{N}_MarkerWidth` y `Slice{N}_FilterEdgesHidden`.
- Presione el conmutador de colapso junto a la visualización de frecuencia para reducir el panel a una franja compacta solo con la frecuencia. El estado se conserva por slice.

## Relacionado

- [Aplicar un preset de ancho de filtro desde el panel VFO](apply-a-filter-width-preset-from-the-vfo-panel.md)
- [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)
- [Resumen del panel VFO](overview.md)
