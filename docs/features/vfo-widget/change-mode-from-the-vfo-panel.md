# Cambiar el modo desde el panel VFO

Use la pestaña Modo del panel VFO para cambiar el modo de demodulación de cualquier slice — por ejemplo, de USB a CW o FM — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO debe estar abierto. Si no está visible, haga clic en la bandera del marcador VFO en la pantalla del espectro para el slice que desea cambiar.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el slice objetivo. El panel VFO se abre, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el **Mode combo** y seleccione el modo deseado de la lista.

## Función de cada control

| Control                        | Valor predeterminado                                                                                                                    | Valores válidos                                                                                                          |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Mode combo                     | USB                                                                                                                                     | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY                                                              |
| Botones de preajuste de filtro | —                                                                                                                                       | Preajustes guardados de ancho de filtro                                                                                  |
| Botón ADSP (pestaña DSP)       | Abre el cuadro de diálogo de AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de un conmutador DSP del lado de la radio pero no marcable. Al hacer clic, levanta y enfoca el cuadro de diálogo no modal AetherDSP Settings. |
| Botón AetherVoice (pestaña DSP)| Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX (v0.9.8).                                               | Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú / cadena para la tira.                  |
| Botón de antena RX             | —                                                                                                                                       | Abre el menú de selección de antena para la antena receptora de este slice.                                              |
| Botón de antena TX             | —                                                                                                                                       | Abre el menú de selección de antena para la antena transmisora de este slice.                                            |
| Pantalla de frecuencia         | —                                                                                                                                       | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba en MHz y presione Enter o Tab.        |
| Etiqueta de ancho de filtro    | —                                                                                                                                       | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro. Utiliza RxApplet::formatFilterWidth.        |
| Deslizador AF Gain (pestaña Audio) | 100                                                                                                                                     | 0-100. Establece el nivel de salida de audio para este slice.                                                             |
| Deslizador Pan (pestaña Audio) | 50                                                                                                                                      | 0-100. Establece la panorámica estéreo izquierda/derecha para este slice. 50 = centro.                                    |
| Botón Mute (pestaña Audio)     | off                                                                                                                                     | Alternar. Silencia la salida de audio para este slice sin cambiar la configuración de ganancia AF.                       |
| Botón + deslizador Squelch (pestaña Audio) | off                                                                                                                          | 0-100. Activa el squelch para este slice. El deslizador adyacente establece el umbral.                                   |
| Combo AGC (pestaña Audio)      | FAST                                                                                                                                    | FAST, MED, SLOW, OFF. Establece la velocidad de ataque/liberación del AGC para este slice.                                |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | off                                                                                                                          | Alternar. Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La rueda del ratón ajusta en pasos de 10 Hz. |
| Combo de canal DAX (pestaña DAX) | Off                                                                                                                                     | Off, 1-8. Asigna un canal de audio DAX a este slice.                                                                     |
| Botón de grosor del marcador   | 1 px                                                                                                                                    | Off, 1 px, 3 px. Recorre el grosor de la línea del marcador VFO. Se conserva por slice.                                 |
| Botón de bordes del filtro     | shown                                                                                                                                   | Alternar. Oculta o muestra las líneas de borde del filtro en la banda pasante del espectro. Se conserva por slice.       |
| Alternar colapso               | expandido                                                                                                                               | Alternar. Colapsa el panel VFO a una tira compacta solo de frecuencia. Se conserva por slice.                            |

**Mode combo** — establece el modo de demodulación para el slice. Al seleccionar un nuevo modo, el cambio se aplica inmediatamente en la radio.

**Botones de preajuste de filtro** — aparecen en la misma pestaña Mode. Cada botón aplica un ancho de filtro guardado. Haga clic derecho en un botón para guardar el ancho de filtro actual en esa ranura. Los preajustes se conservan en `FilterPresets`.

**Etiqueta de ancho de filtro** — muestra el ancho de banda del filtro actual. Haga clic en ella para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como la única fuente de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas de modo SSB/digital (#2197, v0.9.8).

**Botón de antena RX** — abre un menú que enumera las antenas receptoras disponibles. Los elementos del menú muestran etiquetas legibles para cada antena. La selección de antena se basa en la clave de antena interna, no en el texto mostrado. Si la radio proporciona una lista de antenas por slice, se usa esa lista en lugar de la lista global de antenas.

**Botón de antena TX** — abre un menú que enumera las antenas transmisoras disponibles. El menú excluye automáticamente los puertos de antena solo RX (aquellos que comienzan con "RX"). Los elementos del menú muestran etiquetas legibles para cada antena. La selección de antena se basa en la clave de antena interna, no en el texto mostrado. Si la radio proporciona una lista de antenas por slice, se usa esa lista en lugar de la lista global de antenas.

**Pantalla de frecuencia** — muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa de frecuencia. Escriba la frecuencia en MHz y presione Enter o Tab. En bandas de transverter (frecuencia superior a 100 MHz), la lógica de entrada acepta frecuencias de hasta 50 000 MHz. Para bandas de tres dígitos (100-999 MHz), un número entero de 4 o más dígitos inserta automáticamente un decimal después del tercer dígito (por ejemplo, 1446 se convierte en 144.6 MHz). En otras bandas, la frecuencia máxima ingresada es 54.0 MHz.

## Controles de la pestaña DSP

La pestaña DSP muestra botones para algoritmos de reducción de ruido y filtrado suministrados directamente por la radio, además de botones de inicio del lado del cliente. Los siguientes botones están disponibles:

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
| NR2 | Abre el algoritmo NR2 en el cuadro de diálogo AetherDSP Settings (clic derecho) |
| NR4 | Abre el algoritmo NR4 en el cuadro de diálogo AetherDSP Settings (clic derecho) |
| MNR | Abre el algoritmo MNR en el cuadro de diálogo AetherDSP Settings (clic derecho) |
| DFNR | Abre el algoritmo DFNR en el cuadro de diálogo AetherDSP Settings (clic derecho) |
| BNR | Abre el algoritmo BNR en el cuadro de diálogo AetherDSP Settings (clic derecho) |
| RN2 | Abre el algoritmo RN2 en el cuadro de diálogo AetherDSP Settings (clic derecho) |
| ADSP | Abre el cuadro de diálogo AetherDSP Settings (mismo punto de entrada que el menú Settings) |
| AetherVoice | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX |

Todos los botones del lado de la radio están desactivados de forma predeterminada y activan o desactivan el algoritmo correspondiente para el slice activo.

> **Nota:** Los módulos de reducción de ruido del lado del cliente NR2, NR4, MNR, BNR, DFNR y RN2 son accesibles mediante clic derecho en la pestaña DSP para abrir el cuadro de diálogo AetherDSP Settings, o desde el menú superpuesto del espectro y el applet AetherDSP.

### Deslizador de nivel DSP

Cuando uno o más algoritmos DSP con nivel (NR, NB, ANF, NRL, NRS, NRF o ANFL) están activos, aparece un deslizador de nivel debajo de la cuadrícula de botones DSP. La etiqueta del deslizador muestra qué algoritmo está siendo apuntado actualmente — el DSP con nivel habilitado más recientemente. El valor numérico se muestra a la derecha del deslizador.

- Rango: 0–100.
- El deslizador se reorienta automáticamente cuando habilita un botón DSP con nivel diferente.
- Cuando no hay ningún DSP con nivel activo, o cuando solo RNN, ANFT o APF están encendidos, la fila del deslizador se atenúa. Permanece en el diseño en todo momento para evitar que la cuadrícula de botones se desplace.
- Al iniciar, cualquier DSP habilitado en el perfil guardado de la radio ahora muestra correctamente el deslizador de nivel sin necesidad de alternarlo manualmente (#startup-slider, v0.9.8).

## Comportamiento del squelch por modo

El botón y el deslizador de squelch en la pestaña Audio se deshabilitan automáticamente en ciertos modos donde el squelch no es significativo:

- **Modos digitales (DIGU, DIGL)** — El audio alimenta decodificadores externos a través de DAX. El squelch está deshabilitado.
- **Modo RTTY** — Al igual que los modos digitales, el audio alimenta decodificadores externos. El squelch está deshabilitado para evitar el bloqueo de señales FSK débiles (#2504, v26.5.1).
- **Modo CW** — La radio bloquea el squelch activado a un nivel fijo y rechaza cambios. El squelch está deshabilitado.

Cuando el squelch está deshabilitado y estaba previamente activado, se desactiva automáticamente para evitar un estado de squelch atascado. El indicador `m_savedSquelchOn` preserva el estado anterior para que pueda restaurarse al volver a un modo de voz.

## Consejos

- Cambiar de modo puede alterar la banda pasante del filtro activo. Verifique la etiqueta de ancho de filtro en la fila del encabezado después de cambiar de modo y aplique un preajuste de filtro si es necesario.
- La etiqueta de ancho de filtro en el encabezado del panel VFO muestra el ancho de banda actual. Haga clic en ella para recorrer los botones de preajuste de filtro en la pestaña Mode.
- Para acceder a NR2, NR4, MNR, BNR, DFNR o RN2, haga clic derecho en el botón de la pestaña DSP para ese algoritmo, o haga clic derecho en la pantalla del espectro y abra el menú superpuesto, o abra el applet AetherDSP.
- El grosor del marcador y los botones de bordes del filtro se conservan por slice en las claves de configuración `Slice{N}_MarkerWidth` y `Slice{N}_FilterEdgesHidden`.
- Presione el alternador de colapso junto a la pantalla de frecuencia para reducir el panel a una tira compacta solo de frecuencia. El estado se conserva por slice.

## Relacionado

- [Aplicar un preajuste de ancho de filtro desde el panel VFO](apply-a-filter-width-preset-from-the-vfo-panel.md)
- [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)
- [Visión general del panel VFO](overview.md)
