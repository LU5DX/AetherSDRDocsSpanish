# Cómo cambiar el modo desde el panel VFO

Utilice la pestaña Mode del panel VFO para cambiar el modo de demodulación de cualquier slice — por ejemplo, de USB a CW o FM — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO debe estar abierto. Si no está visible, haga clic en la bandera del marcador VFO en la pantalla del espectro para el slice que desea cambiar.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el slice deseado. Se abre el panel VFO, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el **Mode combo** y seleccione el modo deseado de la lista.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos |
|---|---|---|
| Mode combo | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY |
| Botones de presets de filtro | — | Presets guardados de ancho de filtro |
| Botón ADSP (pestaña DSP) | Abre el diálogo de configuración AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Diseñado como un conmutador de DSP del lado de la radio pero no es marcable. Al hacer clic, eleva y enfoca el diálogo AetherDSP Settings no modal. |
| Botón AetherVoice (pestaña DSP) | Alterna la Aetherial Audio Channel Strip — la suite unificada de DSP TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la strip. |
| Botón de antena RX | — | Abre el menú de selección de antena para la antena receptora de este slice. |
| Botón de antena TX | — | Abre el menú de selección de antena para la antena transmisora de este slice. |
| Pantalla de frecuencia | — | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba MHz y pulse Enter o Tab. |
| Etiqueta de ancho de filtro | — | Muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones de presets de filtro. Utiliza `RxApplet::formatFilterWidth`. |
| Deslizador AF Gain (pestaña Audio) | 100 | 0-100. Establece el nivel de salida de audio para este slice. |
| Deslizador Pan (pestaña Audio) | 50 | 0-100. Establece el balance estéreo izquierda/derecha para este slice. 50 = centro. |
| Botón Mute (pestaña Audio) | off | Alterna. Silencia la salida de audio de este slice sin cambiar el ajuste de ganancia AF. |
| Botón Squelch + deslizador (pestaña Audio) | off | 0-100. Activa el squelch para este slice. El deslizador adyacente establece el umbral. |
| Combo AGC (pestaña Audio) | FAST | FAST, MED, SLOW, OFF. Establece la velocidad de ataque/liberación del AGC para este slice. |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | off | Alterna. Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de los botones depende de la serie de la radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración AetherDSP para ese algoritmo. |
| Botón MN (pestaña DSP) | off | Alterna. Filtro de muesca manual. Se muestra solo en radios que lo admiten. |
| Botones RIT / XIT + etiquetas (pestaña X/RIT) | off | Alterna. Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La rueda del ratón ajusta en pasos de 10 Hz. |
| Combo de canal DAX (pestaña DAX) | Off | Off, 1-8. Asigna un canal de audio DAX a este slice. |
| Botón de grosor del marcador | 1 px | Off, 1 px, 3 px. Recorre el grosor de la línea del marcador VFO. Se conserva por slice. |
| Botón de bordes del filtro | shown | Alterna. Oculta o muestra las líneas de borde del filtro en la banda pasante del espectro. Se conserva por slice. |
| Alternador de contracción | expanded | Alterna. Contrae el panel VFO a una tira compacta de solo frecuencia. Se conserva por slice. |

**Mode combo** — establece el modo de demodulación del slice. Al seleccionar un nuevo modo, este se aplica inmediatamente en la radio.

**Botones de presets de filtro** — aparecen en la misma pestaña Mode. Cada botón aplica un ancho de filtro guardado. Haga clic derecho en un botón para guardar el ancho de filtro actual en esa ranura. Los presets se conservan en `FilterPresets`.

**Etiqueta de ancho de filtro** — muestra el ancho de banda actual del filtro. Haga clic en ella para recorrer los botones de presets de filtro de la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desfase de 0,1 kHz que afectaba a las lecturas en modos SSB/digitales (#2197, v0.9.8).

**Botón de antena RX** — abre un menú que lista las antenas receptoras disponibles. Los elementos del menú muestran etiquetas legibles para cada antena. La selección de antena se basa en la clave interna de antena, no en el texto mostrado. Si la radio proporciona una lista de antenas por slice, se utiliza esa lista en lugar de la lista global de antenas.

**Botón de antena TX** — abre un menú que lista las antenas transmisoras disponibles. El menú excluye automáticamente los puertos de solo RX (los que comienzan con "RX"). Los elementos del menú muestran etiquetas legibles para cada antena. La selección de antena se basa en la clave interna de antena, no en el texto mostrado. Si la radio proporciona una lista de antenas por slice, se utiliza esa lista en lugar de la lista global de antenas.

**Pantalla de frecuencia** — muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa de frecuencia. Escriba la frecuencia en MHz y pulse Enter o Tab.

- En bandas de transverter (frecuencia superior a 100 MHz), la lógica de entrada acepta frecuencias de hasta 50.000 MHz.
- Si introduce explícitamente una frecuencia superior a 54,0 MHz con formato MHz (por ejemplo, "145.000"), el analizador la trata como una entrada intencional en MHz y acepta frecuencias de hasta 50.000 MHz.
- Para bandas de tres dígitos (100-999 MHz), un entero simple de 4 o más dígitos inserta automáticamente un decimal después del tercer dígito (por ejemplo, 1446 se convierte en 144,6 MHz).
- En otras bandas, la frecuencia máxima introducida es 54,0 MHz. Los valores superiores a 54000 se tratan como Hz, y los valores entre 54 y 54000 se tratan como kHz.

## Navegación por la barra de pestañas (v26.6.3)

La barra de pestañas ahora utiliza controles `QPushButton` clicables con soporte de foco de teclado. Las etiquetas de las pestañas son navegables con el teclado mediante Tab y Shift+Tab.

- Pulse **Tab** para mover el foco al siguiente botón de pestaña, **Shift+Tab** para mover al anterior.
- Pulse **Enter** o **Space** para activar la pestaña enfocada.
- Un indicador de foco (subrayado) aparece en el botón de pestaña actualmente enfocado.

**Haga clic derecho en la pestaña Audio** (icono de altavoz) para alternar el silencio del slice actual directamente, sin cambiar a la pestaña Audio.

## Sintonización de frecuencia con la rueda del ratón (v26.6.3)

La dirección de la rueda del ratón para la sintonización de frecuencia ahora respeta el ajuste **Reverse mouse wheel** en `InteractionSettings`. Cuando está activado, desplazarse hacia arriba disminuye la frecuencia y desplazarse hacia abajo la aumenta. Este ajuste se aplica globalmente.

## Accesibilidad de la pantalla de frecuencia (v26.6.3)

La pantalla de frecuencia ahora proporciona eventos de accesibilidad (cambio de valor) cuando la frecuencia cambia, utilizando un temporizador de debounce para evitar un exceso de notificaciones. Los lectores de pantalla y las herramientas de accesibilidad reciben el texto actualizado de la frecuencia sin saturar el sistema de accesibilidad.

## Controles de la pestaña DSP

La pestaña DSP muestra botones para los algoritmos de reducción de ruido y filtrado proporcionados directamente por la radio, además de botones de lanzamiento del lado del cliente. Los siguientes botones están disponibles:

| Botón | Descripción |
|---|---|
| NR | Reducción de ruido |
| NB | Supresión de ruido (noise blanker) |
| ANF | Filtro de muesca automático |
| APF | Filtro de pico de audio (visible solo en modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro espectral de ruido |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |
| MN | Filtro de muesca manual (se muestra solo en radios que lo admiten) |
| NR2 | Abre el algoritmo NR2 en el diálogo de configuración AetherDSP (clic derecho) |
| NR4 | Abre el algoritmo NR4 en el diálogo de configuración AetherDSP (clic derecho) |
| MNR | Abre el algoritmo MNR en el diálogo de configuración AetherDSP (clic derecho) |
| DFNR | Abre el algoritmo DFNR en el diálogo de configuración AetherDSP (clic derecho) |
| BNR | Abre el algoritmo BNR en el diálogo de configuración AetherDSP (clic derecho) |
| RN2 | Abre el algoritmo RN2 en el diálogo de configuración AetherDSP (clic derecho) |
| ADSP | Abre el diálogo de configuración AetherDSP (mismo punto de entrada que el menú Settings) |
| AetherVoice | Alterna la Aetherial Audio Channel Strip — la suite unificada de DSP TX/RX |

Todos los botones del lado de la radio están desactivados por defecto y alternan el algoritmo correspondiente para el slice activo.

> **Nota:** Los módulos de reducción de ruido del lado del cliente NR2, NR4, MNR, BNR, DFNR y RN2 son accesibles mediante clic derecho en la pestaña DSP para abrir el diálogo de configuración AetherDSP, o desde el menú de superposición del espectro y el applet AetherDSP.

### Deslizador de nivel DSP

Cuando uno o más algoritmos DSP con nivel (NR, NB, ANF, NRL, NRS, NRF, ANFL o MN) están activos, aparece un deslizador de nivel debajo de la cuadrícula de botones DSP. La etiqueta del deslizador muestra qué algoritmo está dirigido actualmente — el DSP con nivel habilitado más recientemente. El valor numérico se muestra a la derecha del deslizador.

- Rango: 0-100.
- El deslizador se redirige automáticamente cuando activa un botón DSP con nivel diferente.
- Cuando no hay ningún DSP con nivel activo, o cuando solo RNN, ANFT o APF están activados, la fila del deslizador se atenúa. Permanece en el diseño en todo momento para evitar que la cuadrícula de botones se desplace.
- Al iniciar, cualquier DSP habilitado en el perfil guardado de la radio ahora muestra correctamente el deslizador de nivel sin necesidad de alternarlo manualmente (#startup-slider, v0.9.8).

### Comportamiento de la marca central del deslizador Pan (v26.6.1)

El deslizador Pan de la pestaña Audio ahora dibuja un degradado de relleno que se ancla desde el centro hacia afuera. Cuando el deslizador está en el punto medio (50), la ranura se rellena completamente con el color de fondo. Cuando se mueve hacia la izquierda o la derecha, el color de acento rellena la región entre el centro y la posición del mango. Un pequeño punto de marca central aparece en la ranura para indicar la posición neutra.

## Comportamiento del squelch según el modo

El botón y el deslizador de squelch en la pestaña Audio se desactivan automáticamente en ciertos modos donde el squelch no tiene sentido:

- **Modos digitales (DIGU, DIGL)** — El audio alimenta decodificadores externos mediante DAX. El squelch está desactivado.
- **Modo RTTY** — Al igual que los modos digitales, el audio alimenta decodificadores externos. El squelch está desactivado para evitar el bloqueo de señales FSK débiles (#2504, v26.5.1).
- **Modo CW** — La radio bloquea el squelch activado a un nivel fijo y rechaza los cambios. El squelch está desactivado.

Cuando el squelch está desactivado y estaba previamente habilitado, se apaga automáticamente para evitar un estado de squelch bloqueado. El indicador `m_savedSquelchOn` conserva el estado anterior para que pueda restaurarse al volver a un modo de voz.

## Comportamiento de slice bloqueado

Cuando un slice está bloqueado mediante el botón de bloqueo del panel VFO:

- Desplazar la rueda del ratón sobre el panel VFO no cambia la frecuencia. En su lugar, el estado de bloqueo se reconoce con retroalimentación visual.
- Se bloquea cualquier intento de iniciar la entrada directa de frecuencia en un slice bloqueado. Cualquier entrada directa en curso se cancela.
- La pantalla de frecuencia muestra una superposición de indicador de bloqueo.
- Desbloquear el slice elimina la superposición de bloqueo y restaura el comportamiento normal de sintonización.

## Comportamiento de la altura del panel VFO

El panel VFO ajusta dinámicamente su altura para coincidir con la pestaña actualmente visible. Cuando la pestaña DSP es más alta que la pestaña Mode (por ejemplo, cuando los controles de submodo digital están visibles en DIGU/DIGL), la altura del panel ahora coincide correctamente solo con la pestaña actual para evitar espacios no deseados.

## Tematización del panel VFO (v26.6.1)

El panel VFO ahora utiliza su propia superficie de tematización bajo el ámbito del contenedor `spectrum/vfo`. Esto permite que las anulaciones de tema se dirijan al panel VFO de forma independiente de la pantalla del espectro. El panel dibuja su fondo, medidor de señal y elementos de insignia utilizando tokens de `ThemeManager::color()`:

- `color.background.0`, `color.background.1`, `color.background.2`
- `color.text.primary`, `color.text.label`
- `color.accent`, `color.accent.bright`

Los botones ADSP y AetherVoice ahora utilizan colores tematizados para su estado presionado (`color.accent`) y fondo (`color.background.1`) en lugar de valores codificados.

## Sombra de elevación del panel VFO (v26.7.4)

El panel VFO ahora renderiza su sombra de elevación utilizando un widget separado `FlagShadow`. Esta superficie de sombra se actualiza independientemente del panel VFO principal para evitar volver a pintar toda la bandera cuando se actualiza el medidor de señal. La sombra utiliza un algoritmo de desenfoque de caja y se dibuja detr
