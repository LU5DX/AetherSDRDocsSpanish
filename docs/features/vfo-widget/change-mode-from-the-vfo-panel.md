# Cambiar el modo desde el panel VFO

Use la pestaña Mode del panel VFO para cambiar el modo de demodulación de cualquier slice — por ejemplo, de USB a CW o FM — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa a la radio.
- El panel VFO debe estar abierto. Si no está visible, haga clic en la bandera del marcador VFO en la pantalla del espectro para el slice que desea cambiar.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el slice de destino. Se abre el panel VFO, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el **Mode combo** y seleccione el modo deseado de la lista.

## Función de cada control

| Control                      | Valor predeterminado                                                                                                                 | Valores válidos                                                                                                           |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Mode combo                   | USB                                                                                                                                  | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY                                                               |
| Botones de preselección de filtro | —                                                                                                                              | Preselecciones guardadas de anchura de filtro                                                                              |
| Botón ADSP (pestaña DSP)     | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene estilo de conmutador DSP del lado de la radio pero no es seleccionable. Al hacer clic, abre y enfoca el diálogo de configuración de AetherDSP no modal. |
| Botón AetherVoice (pestaña DSP) | Activa y desactiva el Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8).                              | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/chain para el strip. |
| Botón RX antenna             | —                                                                                                                                    | Abre el menú de selección de antena para la antena receptora de este slice.                                               |
| Botón TX antenna             | —                                                                                                                                    | Abre el menú de selección de antena para la antena transmisora de este slice.                                              |
| Pantalla de frecuencia       | —                                                                                                                                    | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de anchura de filtro | —                                                                                                                                  | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro. Usa `RxApplet::formatFilterWidth`. |
| Deslizador AF Gain (pestaña Audio) | 100                                                                                                                            | 0-100. Establece el nivel de salida de audio para este slice.                                                              |
| Deslizador Pan (pestaña Audio) | 50                                                                                                                               | 0-100. Establece la panorámica estéreo izquierda/derecha para este slice. 50 = centro.                                     |
| Botón Mute (pestaña Audio)   | off                                                                                                                                  | Conmutador. Silencia la salida de audio para este slice sin cambiar el ajuste de ganancia AF.                              |
| Botón Squelch + deslizador (pestaña Audio) | off                                                                                                                          | 0-100. Activa el squelch para este slice. El deslizador adyacente establece el umbral.                                     |
| Combo AGC (pestaña Audio)    | FAST                                                                                                                                 | FAST, MED, SLOW, OFF. Establece la velocidad de ataque/liberación del AGC para este slice.                                 |
| Botones RIT / XIT + etiquetas (pestaña X/RIT) | off                                                                                                                         | Conmutador. Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La rueda del ratón ajusta en pasos de 10 Hz. |
| Combo DAX channel (pestaña DAX) | Off                                                                                                                             | Off, 1-8. Asigna un canal de audio DAX a este slice.                                                                      |
| Botón de grosor del marcador | 1 px                                                                                                                                 | Off, 1 px, 3 px. Recorre el grosor de la línea del marcador VFO. Se conserva por slice.                                   |
| Botón de bordes del filtro   | mostrado                                                                                                                            | Conmutador. Oculta o muestra las líneas de borde del filtro en la banda de paso del espectro. Se conserva por slice.       |
| Conmutador de contracción    | expandido                                                                                                                           | Conmutador. Contrae el panel VFO a una tira compacta solo de frecuencia. Se conserva por slice.                            |

**Mode combo** — establece el modo de demodulación para el slice. Al seleccionar un modo nuevo, el cambio se aplica de inmediato en la radio.

**Botones de preselección de filtro** — aparecen en la misma pestaña Mode. Cada botón aplica una anchura de filtro guardada. Haga clic con el botón derecho en un botón para guardar la anchura de filtro actual en esa ranura. Las preselecciones se conservan en `FilterPresets`.

**Etiqueta de anchura de filtro** — muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desfase de 0,1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8).

## Controles de la pestaña DSP

La pestaña DSP muestra botones para los algoritmos de reducción de ruido y filtrado proporcionados directamente por la radio, además de botones de inicio del lado del cliente. Los siguientes botones están disponibles:

| Botón | Descripción |
|---|---|
| NR | Reducción de ruido |
| NB | Supresor de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de pico de audio (visible solo en modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |
| NR2 | Abre el algoritmo NR2 en el diálogo de configuración de AetherDSP (clic derecho) |
| NR4 | Abre el algoritmo NR4 en el diálogo de configuración de AetherDSP (clic derecho) |
| MNR | Abre el algoritmo MNR en el diálogo de configuración de AetherDSP (clic derecho) |
| DFNR | Abre el algoritmo DFNR en el diálogo de configuración de AetherDSP (clic derecho) |
| BNR | Abre el algoritmo BNR en el diálogo de configuración de AetherDSP (clic derecho) |
| RN2 | Abre el algoritmo RN2 en el diálogo de configuración de AetherDSP (clic derecho) |
| ADSP | Abre el diálogo de configuración de AetherDSP (mismo punto de entrada que el menú Settings) |
| AetherVoice | Activa y desactiva el Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX |

Todos los botones del lado de la radio están desactivados por defecto y activan o desactivan el algoritmo correspondiente para el slice activo.

> **Nota:** Los módulos de reducción de ruido del lado del cliente NR2, NR4, MNR, BNR, DFNR y RN2 son accesibles mediante clic derecho en la pestaña DSP para abrir el diálogo de configuración de AetherDSP, o desde el menú superpuesto del espectro y el applet AetherDSP.

### Deslizador de nivel DSP

Cuando uno o más algoritmos DSP con nivel (NR, NB, ANF, NRL, NRS, NRF o ANFL) están activos, aparece un deslizador de nivel debajo de la cuadrícula de botones DSP. La etiqueta del deslizador muestra qué algoritmo está seleccionado actualmente — el DSP con nivel habilitado más recientemente. El valor numérico se muestra a la derecha del deslizador.

- Rango: 0–100.
- El deslizador se reorienta automáticamente cuando habilita un botón DSP con nivel diferente.
- Cuando no hay ningún DSP con nivel activo, o cuando solo RNN, ANFT o APF están encendidos, la fila del deslizador se atenúa. Permanece en el diseño en todo momento para evitar que la cuadrícula de botones se desplace.
- Al iniciar, cualquier DSP habilitado en el perfil guardado de la radio ahora muestra correctamente el deslizador de nivel sin necesidad de activarlo manualmente (#startup-slider, v0.9.8).

## Consejos

- Cambiar de modo puede alterar la banda de paso activa del filtro. Verifique la etiqueta de anchura de filtro en la fila de encabezado después de cambiar de modo y aplique una preselección de filtro si es necesario.
- La etiqueta de anchura de filtro en el encabezado del panel VFO muestra el ancho de banda actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode.
- Para acceder a NR2, NR4, MNR, BNR, DFNR o RN2, haga clic derecho en el botón de la pestaña DSP correspondiente a ese algoritmo, o haga clic derecho en la pantalla del espectro y abra el menú superpuesto, o abra el applet AetherDSP.
- Los botones de grosor del marcador y bordes del filtro se conservan por slice en las claves de configuración `Slice{N}_MarkerWidth` y `Slice{N}_FilterEdgesHidden`.
- Presione el conmutador de contracción junto a la pantalla de frecuencia para reducir el panel a una tira compacta solo de frecuencia. El estado se conserva por slice.

## Relacionados

- [Aplicar una preselección de anchura de filtro desde el panel VFO](apply-a-filter-width-preset-from-the-vfo-panel.md)
- [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)
- [Descripción general del panel VFO](overview.md)
