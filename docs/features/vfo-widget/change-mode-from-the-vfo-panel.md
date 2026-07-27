# Cambiar el modo desde el panel del VFO

Use la pestaña Modo del panel del VFO para cambiar el modo de demodulación de cualquier slice — por ejemplo, de USB a CW o FM — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel del VFO requiere una conexión activa con la radio.
- El panel del VFO debe estar abierto. Si no está visible, haga clic en la bandera del marcador del VFO en la pantalla del espectro para el slice que desea cambiar.

## Pasos

1. Haga clic en la bandera del marcador del VFO en la pantalla del espectro para el slice deseado. El panel del VFO se abre, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Modo** dentro del panel del VFO.
3. Haga clic en el **combo Modo** y seleccione el modo deseado de la lista.

## Qué hace cada control

| Control                      | Valor predeterminado                                                                                                                 | Valores válidos                                                                                                             |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| Combo Modo                   | USB                                                                                                                                  | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY                                                                 |
| Botones de preselección de filtro | —                                                                                                                                 | Preselecciones guardadas de ancho de filtro                                                                                 |
| Botón ADSP (pestaña DSP)     | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Configuración (v0.9.8). | Tiene estilo de conmutador de DSP del lado de la radio pero no es seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de Configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Activa/desactiva la Tira de Canales de Audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8).                              | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Botón de antena RX           | —                                                                                                                                     | Abre el menú de selección de antena para la antena receptora de este slice.                                                 |
| Botón de antena TX           | —                                                                                                                                     | Abre el menú de selección de antena para la antena transmisora de este slice.                                               |
| Visualización de frecuencia  | —                                                                                                                                     | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar a introducir la frecuencia directamente; escriba MHz y pulse Enter o Tabulador.           |
| Etiqueta de ancho de filtro  | —                                                                                                                                     | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro. Usa RxApplet::formatFilterWidth.                |
| Deslizador de Ganancia AF (pestaña Audio) | 100                                                                                                                          | 0-100. Define el nivel de salida de audio para este slice.                                                                  |
| Deslizador de Panorámica (pestaña Audio) | 50                                                                                                                           | 0-100. Define la panorámica estéreo izquierda/derecha para este slice. 50 = centro.                                          |
| Botón de Silencio (pestaña Audio) | desactivado                                                                                                                   | Alternar. Silencia la salida de audio para este slice sin cambiar el ajuste de ganancia AF.                                 |
| Botón de Squelch + deslizador (pestaña Audio) | desactivado                                                                                                              | 0-100. Activa el squelch para este slice. El deslizador adyacente define el umbral.                                           |
| Combo AGC (pestaña Audio)    | FAST                                                                                                                                  | FAST, MED, SLOW, OFF. Define la velocidad de ataque/liberación del AGC para este slice.                                      |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | desactivado | Alternar. Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad del botón depende de la serie de radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo. |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | desactivado                                                                                                                   | Alternar. Activa la sintonización incremental del receptor (RIT) o transmisor (XIT). La rueda del ratón ajusta en pasos de 10 Hz. |
| Combo de canal DAX (pestaña DAX) | Desactivado                                                                                                                    | Desactivado, 1-8. Asigna un canal de audio DAX a este slice.                                                                 |
| Botón de grosor del marcador | 1 px                                                                                                                                  | Desactivado, 1 px, 3 px. Cambia el grosor de la línea del marcador VFO. Se conserva por slice.                              |
| Botón de bordes del filtro   | mostrado                                                                                                                             | Alternar. Muestra u oculta las líneas de borde del filtro en la banda de paso del espectro. Se conserva por slice.          |
| Alternar colapso             | expandido                                                                                                                            | Alternar. Colapsa el panel del VFO a una tira compacta solo de frecuencia. Se conserva por slice.                            |

**Combo Modo** — define el modo de demodulación para el slice. Seleccionar un nuevo modo surte efecto inmediatamente en la radio.

**Botones de preselección de filtro** — aparecen en la misma pestaña Modo. Cada botón aplica un ancho de filtro guardado. Haga clic derecho en un botón para guardar el ancho de filtro actual en esa ranura. Las preselecciones se conservan en `FilterPresets`.

**Etiqueta de ancho de filtro** — muestra el ancho de banda del filtro actual. Haga clic en ella para recorrer los botones de preselección de filtro en la pestaña Modo. Usa `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas de modo SSB/digital (#2197, v0.9.8).

**Botón de antena RX** — abre un menú que lista las antenas receptoras disponibles. Los elementos del menú muestran etiquetas legibles para cada antena. La selección de antena se basa en la clave interna de la antena, no en el texto mostrado. Si la radio proporciona una lista de antenas por slice, se usa esa lista en lugar de la lista global de antenas.

**Botón de antena TX** — abre un menú que lista las antenas transmisoras disponibles. El menú excluye automáticamente los puertos de antena solo de RX (aquellos que comienzan con "RX"). Los elementos del menú muestran etiquetas legibles para cada antena. La selección de antena se basa en la clave interna de la antena, no en el texto mostrado. Si la radio proporciona una lista de antenas por slice, se usa esa lista en lugar de la lista global de antenas.

**Visualización de frecuencia** — muestra la frecuencia actual del slice. Haga clic una vez para comenzar a introducir la frecuencia directamente. Escriba la frecuencia en MHz y pulse Enter o Tabulador.

- En bandas de transverter (frecuencia por encima de 100 MHz), la lógica de entrada acepta frecuencias de hasta 50 000 MHz.
- Si introduce explícitamente una frecuencia superior a 54,0 MHz con formato MHz (p. ej., "145.000"), el analizador la trata como una entrada intencionada en MHz y acepta frecuencias de hasta 50 000 MHz.
- Para bandas de tres dígitos (100-999 MHz), un número entero de 4 o más dígitos inserta automáticamente un decimal después del tercer dígito (p. ej., 1446 se convierte en 144,6 MHz).
- En otras bandas, la frecuencia máxima introducida es 54,0 MHz. Los valores superiores a 54000 se tratan como Hz, y los valores entre 54 y 54000 se tratan como kHz.

## Navegación por pestañas (v26.6.3)

La barra de pestañas ahora usa controles `QPushButton` en los que se puede hacer clic y que admiten enfoque por teclado. Se puede navegar por las etiquetas de las pestañas mediante Tab y Mayús+Tab.

- Pulse **Tab** para mover el enfoque al siguiente botón de pestaña, **Mayús+Tab** para moverlo al anterior.
- Pulse **Enter** o **Espacio** para activar la pestaña enfocada.
- Un indicador de enfoque (subrayado) aparece en el botón de la pestaña actualmente enfocada.

**Haga clic derecho en la pestaña Audio** (icono de altavoz) para silenciar o reactivar el slice actual directamente, sin cambiar a la pestaña Audio.

## Sintonización con la rueda del ratón (v26.6.3)

La dirección de la rueda del ratón para la sintonización de frecuencia ahora respeta el ajuste **Invertir rueda del ratón** en `InteractionSettings`. Cuando está activado, desplazarse hacia arriba disminuye la frecuencia y desplazarse hacia abajo la aumenta. Este ajuste se aplica globalmente.

## Accesibilidad en la visualización de frecuencia (v26.6.3)

La visualización de frecuencia ahora proporciona eventos de accesibilidad (cambio de valor) cuando la frecuencia cambia, utilizando un temporizador con supresión de rebotes para evitar saturación. Los lectores de pantalla y las herramientas de accesibilidad reciben el texto de frecuencia actualizado sin inundar el sistema de accesibilidad.

## Controles de la pestaña DSP

La pestaña DSP muestra botones para algoritmos de reducción de ruido y filtrado proporcionados directamente por la radio, además de botones de lanzamiento del lado del cliente. Los siguientes botones están disponibles:

| Botón | Descripción |
|---|---|
| NR | Reducción de ruido |
| NB | Supresor de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de pico de audio (visible solo en modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro espectral de ruido |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |
| NR2 | Abre el algoritmo NR2 en el diálogo de Configuración de AetherDSP (clic derecho) |
| NR4 | Abre el algoritmo NR4 en el diálogo de Configuración de AetherDSP (clic derecho) |
| MNR | Abre el algoritmo MNR en el diálogo de Configuración de AetherDSP (clic derecho) |
| DFNR | Abre el algoritmo DFNR en el diálogo de Configuración de AetherDSP (clic derecho) |
| BNR | Abre el algoritmo BNR en el diálogo de Configuración de AetherDSP (clic derecho) |
| RN2 | Abre el algoritmo RN2 en el diálogo de Configuración de AetherDSP (clic derecho) |
| ADSP | Abre el diálogo de Configuración de AetherDSP (mismo punto de entrada que el menú Configuración) |
| AetherVoice | Activa/desactiva la Tira de Canales de Audio Aetherial — el conjunto unificado de DSP de TX/RX |

Todos los botones del lado de la radio están desactivados por defecto y activan o desactivan el algoritmo correspondiente para el slice activo.

> **Nota:** Los módulos de reducción de ruido del lado del cliente NR2, NR4, MNR, BNR, DFNR y RN2 son accesibles mediante clic derecho en la pestaña DSP para abrir el diálogo de Configuración de AetherDSP, o desde el menú superpuesto del espectro y el applet de AetherDSP.

### Deslizador de nivel de DSP

Cuando uno o más algoritmos de DSP con nivel (NR, NB, ANF, NRL, NRS, NRF o ANFL) están activos, aparece un deslizador de nivel debajo de la cuadrícula de botones DSP. La etiqueta del deslizador muestra qué algoritmo está siendo apuntado actualmente: el DSP con nivel habilitado más recientemente. El valor numérico se muestra a la derecha del deslizador.

- Rango: 0-100.
- El deslizador se reorienta automáticamente cuando habilita un botón de DSP con nivel diferente.
- Cuando no hay ningún DSP con nivel activo, o cuando solo RNN, ANFT o APF están encendidos, la fila del deslizador se atenúa. Permanece en el diseño en todo momento para evitar que la cuadrícula de botones se desplace.
- Al iniciar, cualquier DSP habilitado en el perfil guardado de la radio ahora muestra correctamente el deslizador de nivel sin necesidad de activarlo manualmente (#startup-slider, v0.9.8).

### Comportamiento de la marca central del deslizador de panorámica (v26.6.1)

El deslizador de panorámica en la pestaña Audio now pinta un degradado de relleno que se ancla desde el centro hacia afuera. Cuando el deslizador está en el punto medio (50), la ranura está completamente llena con el color de fondo. Cuando se mueve a la izquierda o a la derecha, el color de acento llena la región entre el centro y la posición del control. Aparece un pequeño punto de marca central en la ranura para indicar la posición neutral.

## Comportamiento del squelch por modo

El botón de squelch y el deslizador en la pestaña Audio se deshabilitan automáticamente en ciertos modos donde el squelch no es significativo:

- **Modos digitales (DIGU, DIGL)** — El audio se envía a decodificadores externos a través de DAX. El squelch está deshabilitado.
- **Modo RTTY** — Al igual que los modos digitales, el audio se envía a decodificadores externos. El squelch está deshabilitado para evitar bloquear señales FSK débiles (#2504, v26.5.1).
- **Modo CW** — La radio bloquea el squelch en un nivel fijo y rechaza los cambios. El squelch está deshabilitado.

Cuando el squelch está deshabilitado y estaba activado previamente, se desactiva automáticamente para evitar un estado de squelch atascado. El indicador `m_savedSquelchOn` preserva el estado anterior para que pueda restaurarse al volver a un modo de voz.

## Comportamiento del slice bloqueado

Cuando un slice está bloqueado mediante el botón de bloqueo en el panel del VFO:

- Desplazar la rueda del ratón sobre el panel del VFO no cambia la frecuencia. En cambio, el estado de bloqueo se reconoce con retroalimentación visual.
- Se bloquea cualquier intento de comenzar a introducir la frecuencia directamente en un slice bloqueado. Cualquier entrada directa en curso se cancela.
- La visualización de frecuencia muestra un indicador de superposición de bloqueo.
- Desbloquear el slice elimina la superposición de bloqueo y restaura el comportamiento normal de sintonización.

## Comportamiento de la altura del panel del VFO

El panel del VFO ajusta dinámicamente su altura para coincidir con la pestaña actualmente visible. Cuando la pestaña DSP es más alta que la pestaña Modo (por ejemplo, cuando los controles de submodo digital son visibles en DIGU/DIGL), la altura del panel ahora coincide correctamente solo con la pestaña actual para evitar espacios no deseados.

## Tematización del panel del VFO (v26.6.1)

El panel del VFO now usa su propia superficie de tematización bajo el ámbito del contenedor `spectrum/vfo`. Esto permite que las anulaciones de tema apunten al panel del VFO de forma independiente de la visualización del espectro. El panel pinta su fondo, medidor de señal y elementos de distintivo usando los tokens de `ThemeManager::color()`:

- `color.background.0`, `color.background.1`, `color.background.2`
- `color.text.primary`, `color.text.label`
- `color.accent`, `color.accent.bright
