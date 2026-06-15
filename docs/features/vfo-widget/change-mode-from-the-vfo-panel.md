# Cambiar el modo desde el panel VFO

Utilice la pestaña Mode del panel VFO para cambiar el modo de demodulación de cualquier slice — por ejemplo, de USB a CW o FM — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión de radio activa.
- El panel VFO debe estar abierto. Si no está visible, haga clic en la bandera del marcador VFO en la pantalla del espectro para el slice que desea cambiar.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro del slice de destino. Se abre el panel VFO, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el **Mode combo** y seleccione el modo deseado de la lista.

## Qué hace cada control

| Control                      | Valor predeterminado                                                                                                                 | Valores válidos                                                                                                            |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Mode combo                   | USB                                                                                                                                  | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY                                                                |
| Botones de preselección de filtro | —                                                                                                                               | Preselecciones de ancho de filtro guardadas                                                                                |
| Botón ADSP (pestaña DSP)     | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de alternancia DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo AetherDSP Settings no modal. |
| Botón AetherVoice (pestaña DSP) | Activa o desactiva el Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX (v0.9.8).                              | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú / cadena para el strip. |
| Botón de antena RX           | —                                                                                                                                    | Abre el menú de selección de antena para la antena receptora de este slice.                                               |
| Botón de antena TX           | —                                                                                                                                    | Abre el menú de selección de antena para la antena transmisora de este slice.                                              |
| Visualización de frecuencia  | —                                                                                                                                    | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro  | —                                                                                                                                    | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro. Usa RxApplet::formatFilterWidth. |
| Deslizador de ganancia AF (pestaña Audio) | 100                                                                                                                          | 0-100. Establece el nivel de salida de audio para este slice.                                                              |
| Deslizador Pan (pestaña Audio) | 50                                                                                                                                   | 0-100. Establece la panorámica estéreo izquierda/derecha para este slice. 50 = centro.                                      |
| Botón Mute (pestaña Audio)   | desactivado                                                                                                                           | Alternancia. Silencia la salida de audio para este slice sin cambiar el ajuste de ganancia AF.                             |
| Botón + deslizador Squelch (pestaña Audio) | desactivado                                                                                                              | 0-100. Activa el squelch para este slice. El deslizador adyacente establece el umbral.                                      |
| Combo AGC (pestaña Audio)    | FAST                                                                                                                                 | FAST, MED, SLOW, OFF. Establece la velocidad de ataque/reposo del AGC para este slice.                                     |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | desactivado                                                                                                              | Alternancia. Activa la sintonización incremental del receptor (RIT) o transmisor (XIT). La rueda del ratón ajusta en pasos de 10 Hz. |
| Combo de canal DAX (pestaña DAX) | Off                                                                                                                                  | Off, 1-8. Asigna un canal de audio DAX a este slice.                                                                       |
| Botón de grosor del marcador | 1 px                                                                                                                                 | Off, 1 px, 3 px. Recorre el grosor de la línea del marcador VFO. Se conserva por slice.                                    |
| Botón de bordes del filtro   | mostrado                                                                                                                            | Alternancia. Oculta o muestra las líneas de borde del filtro en la banda pasante del espectro. Se conserva por slice.      |
| Alternancia de colapso       | expandido                                                                                                                           | Alternancia. Colapsa el panel VFO a una tira compacta solo de frecuencia. Se conserva por slice.                           |

**Mode combo** — establece el modo de demodulación para el slice. Seleccionar un nuevo modo tiene efecto inmediato en la radio.

**Botones de preselección de filtro** — aparecen en la misma pestaña Mode. Cada botón aplica un ancho de filtro guardado. Haga clic derecho en un botón para guardar el ancho de filtro actual en esa ranura. Las preselecciones se conservan en `FilterPresets`.

**Etiqueta de ancho de filtro** — muestra el ancho de banda del filtro actual. Haga clic en ella para recorrer los botones de preselección de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8).

**Botón de antena RX** — abre un menú que lista las antenas receptoras disponibles. Los elementos del menú muestran etiquetas legibles para cada antena. La selección de antena se basa en la clave interna de la antena, no en el texto mostrado. Si la radio proporciona una lista de antenas por slice, se usa esa lista en lugar de la lista global de antenas.

**Botón de antena TX** — abre un menú que lista las antenas transmisoras disponibles. El menú excluye automáticamente los puertos de antena solo RX (aquellos que comienzan con "RX"). Los elementos del menú muestran etiquetas legibles para cada antena. La selección de antena se basa en la clave interna de la antena, no en el texto mostrado. Si la radio proporciona una lista de antenas por slice, se usa esa lista en lugar de la lista global de antenas.

**Visualización de frecuencia** — muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa de frecuencia. Escriba la frecuencia en MHz y presione Enter o Tab.

- En bandas de transverter (frecuencia por encima de 100 MHz), la lógica de entrada acepta frecuencias de hasta 50 000 MHz.
- Si ingresa explícitamente una frecuencia por encima de 54.0 MHz con formato MHz (ej., "145.000"), el analizador la trata como una entrada intencional en MHz y acepta frecuencias de hasta 50 000 MHz.
- Para bandas de tres dígitos (100-999 MHz), un número entero simple de 4 o más dígitos inserta automáticamente un decimal después del tercer dígito (ej., 1446 se convierte en 144.6 MHz).
- En otras bandas, la frecuencia máxima ingresada es 54.0 MHz. Los valores superiores a 54000 se tratan como Hz, y los valores entre 54 y 54000 se tratan como kHz.

## Navegación por la barra de pestañas (v26.6.3)

La barra de pestañas ahora usa controles `QPushButton` en los que se puede hacer clic y con soporte de enfoque por teclado. Las etiquetas de las pestañas se pueden navegar con el teclado mediante Tab y Shift+Tab.

- Presione **Tab** para mover el enfoque al siguiente botón de pestaña, **Shift+Tab** para moverse al anterior.
- Presione **Enter** o **Space** para activar la pestaña enfocada.
- Un indicador de enfoque (subrayado) aparece en el botón de pestaña actualmente enfocado.

**Haga clic derecho en la pestaña Audio** (icono de altavoz) para alternar la función de silencio (mute) del slice actual directamente, sin cambiar a la pestaña Audio.

## Sintonización de frecuencia con la rueda del ratón (v26.6.3)

La dirección de la rueda del ratón para la sintonización de frecuencia ahora respeta la configuración **Reverse mouse wheel** en `InteractionSettings`. Cuando está activada, desplazarse hacia arriba disminuye la frecuencia y desplazarse hacia abajo la aumenta. Esta configuración se aplica globalmente.

## Accesibilidad de la visualización de frecuencia (v26.6.3)

La visualización de frecuencia ahora proporciona eventos de accesibilidad (cambio de valor) cuando la frecuencia cambia, utilizando un temporizador con supresión de rebotes para evitar saturación. Los lectores de pantalla y las herramientas de accesibilidad reciben el texto de frecuencia actualizado sin inundar el sistema de accesibilidad.

## Controles de la pestaña DSP

La pestaña DSP muestra botones para algoritmos de reducción de ruido y filtrado suministrados directamente por la radio, además de botones de lanzamiento del lado del cliente. Los siguientes botones están disponibles:

| Botón    | Descripción |
|----------|-------------|
| NR       | Reducción de ruido |
| NB       | Supresor de ruido |
| ANF      | Filtro de muesca automático |
| APF      | Filtro de pico de audio (visible solo en modo CW) |
| NRL      | Nivel de reducción de ruido |
| NRS      | Sustracción espectral |
| RNN      | Reducción de ruido RNN |
| NRF      | Filtro de ruido espectral |
| ANFL     | Filtro de muesca LMS |
| ANFT     | Filtro de muesca FFT |
| NR2      | Abre el algoritmo NR2 en el diálogo AetherDSP Settings (clic derecho) |
| NR4      | Abre el algoritmo NR4 en el diálogo AetherDSP Settings (clic derecho) |
| MNR      | Abre el algoritmo MNR en el diálogo AetherDSP Settings (clic derecho) |
| DFNR     | Abre el algoritmo DFNR en el diálogo AetherDSP Settings (clic derecho) |
| BNR      | Abre el algoritmo BNR en el diálogo AetherDSP Settings (clic derecho) |
| RN2      | Abre el algoritmo RN2 en el diálogo AetherDSP Settings (clic derecho) |
| ADSP     | Abre el diálogo AetherDSP Settings (mismo punto de entrada que el menú Settings) |
| AetherVoice | Activa o desactiva el Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX |

Todos los botones del lado de la radio están desactivados por defecto y activan o desactivan el algoritmo correspondiente para el slice activo.

> **Nota:** Los módulos de reducción de ruido del lado del cliente NR2, NR4, MNR, BNR, DFNR y RN2 son accesibles mediante clic derecho en la pestaña DSP para abrir el diálogo AetherDSP Settings, o desde el menú de superposición del espectro y el applet AetherDSP.

### Deslizador de nivel DSP

Cuando uno o más algoritmos DSP con nivel (NR, NB, ANF, NRL, NRS, NRF o ANFL) están activos, aparece un deslizador de nivel debajo de la cuadrícula de botones DSP. La etiqueta del deslizador muestra qué algoritmo está siendo objetivo actualmente — el DSP con nivel habilitado más recientemente. El valor numérico se muestra a la derecha del deslizador.

- Rango: 0–100.
- El deslizador se reorienta automáticamente cuando habilita un botón DSP con nivel diferente.
- Cuando no hay ningún DSP con nivel activo, o cuando solo RNN, ANFT o APF están encendidos, la fila del deslizador se atenúa. Permanece en el diseño en todo momento para evitar que la cuadrícula de botones se desplace.
- Al iniciar, cualquier DSP habilitado en el perfil guardado de la radio ahora muestra correctamente el deslizador de nivel sin necesidad de alternancia manual (#startup-slider, v0.9.8).

### Comportamiento de la marca central del deslizador Pan (v26.6.1)

El deslizador Pan en la pestaña Audio ahora dibuja un degradado de relleno que se ancla desde el centro hacia afuera. Cuando el deslizador está en el punto medio (50), la ranura está completamente llena con el color de fondo. Cuando se mueve hacia la izquierda o la derecha, el color de acento llena la región entre el centro y la posición del control. Aparece un pequeño punto de marca central en la ranura para indicar la posición neutral.

## Comportamiento del squelch por modo

El botón y el deslizador de squelch en la pestaña Audio se desactivan automáticamente en ciertos modos donde el squelch no es significativo:

- **Modos digitales (DIGU, DIGL)** — El audio alimenta decodificadores externos a través de DAX. El squelch está desactivado.
- **Modo RTTY** — Al igual que los modos digitales, el audio alimenta decodificadores externos. El squelch está desactivado para evitar el bloqueo de señales FSK débiles (#2504, v26.5.1).
- **Modo CW** — La radio bloquea el squelch en un nivel fijo y rechaza los cambios. El squelch está desactivado.

Cuando el squelch está desactivado y estaba previamente habilitado, se apaga automáticamente para evitar un estado de squelch atascado. El indicador `m_savedSquelchOn` preserva el estado anterior para que pueda restaurarse al volver a un modo de voz.

## Comportamiento del slice bloqueado

Cuando un slice está bloqueado usando el botón de bloqueo en el panel VFO:

- Desplazar la rueda del ratón sobre el panel VFO no cambia la frecuencia. En su lugar, el estado de bloqueo se reconoce con una retroalimentación visual.
- Se bloquea cualquier intento de iniciar la entrada directa de frecuencia en un slice bloqueado. Cualquier entrada directa en curso se cancela.
- La visualización de frecuencia muestra una superposición de indicador de bloqueo.
- Desbloquear el slice elimina la superposición de bloqueo y restaura el comportamiento normal de sintonización.

## Comportamiento de la altura del panel VFO

El panel VFO ajusta dinámicamente su altura para coincidir con la pestaña actualmente visible. Cuando la pestaña DSP es más alta que la pestaña Mode (por ejemplo, cuando los controles de submodo digital son visibles en DIGU/DIGL), la altura del panel ahora coincide correctamente solo con la pestaña actual para evitar espacios no deseados.

## Tematización del panel VFO (v26.6.1)

El panel VFO ahora usa su propia superficie de tematización bajo el ámbito del contenedor `spectrum/vfo`. Esto permite que las anulaciones de tema se dirijan al panel VFO de forma independiente de la pantalla del espectro. El panel pinta su fondo, medidor de señal y elementos de insignia utilizando tokens de `ThemeManager::color()`:

- `color.background.0`, `color.background.1`, `color.background.2`
- `color.text.primary`, `color.text.label`
- `color.accent`, `color.accent.bright`

Los botones ADSP y AetherVoice ahora usan colores temáticos para su estado presionado (`color.accent`) y fondo (`color.background.1`) en lugar de valores codificados.

## Consejos

- Cambiar de modo puede alterar la banda pasante del filtro activo. Verifique la etiqueta de ancho de filtro en la fila del encabezado después de cambiar de modo y aplique una preselección de filtro si es necesario.
- La etiqueta de ancho de filtro en el encabezado del panel VFO muestra el ancho de banda actual. Haga clic en ella para recorrer los botones de preselección de filtro en la pestaña Mode.
- Para acceder a NR2, NR4, MNR, BNR, DFNR o RN2, haga clic derecho en el botón de la pestaña DSP para
