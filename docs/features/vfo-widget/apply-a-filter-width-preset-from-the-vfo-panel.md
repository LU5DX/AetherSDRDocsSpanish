# Aplicar un ancho de filtro preestablecido desde el panel VFO

Los botones de ajustes preestablecidos de filtro le permiten cambiar el ancho del filtro de recepción de un slice con un solo clic. Úselos para moverse rápidamente entre anchos de banda comunes — por ejemplo, entre un filtro SSB ancho de 3 kHz y un filtro CW estrecho de 500 Hz — sin salir de la vista de espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión de radio activa.
- El panel VFO del slice objetivo debe estar abierto y expandido. Si está colapsado a una franja de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo primero.

## Pasos

1. Haga clic en el marcador VFO en la pantalla de espectro del slice que desea ajustar. Se abre el panel VFO, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el botón de ajuste preestablecido de filtro que corresponda al ancho de banda deseado. La radio aplica inmediatamente ese ancho de filtro al slice.

Para guardar el ancho de filtro actual en una ranura preestablecida:

1. Configure el filtro al ancho de banda que desea guardar (consulte [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)).
2. Haga clic derecho en la ranura del botón preestablecido que desea sobrescribir.
3. El ancho de filtro actual se guarda en esa ranura.

## Qué hace cada control

| Control                          | Comportamiento                                                                                                                                                                                                                                       | Predeterminado                                                                                                                 |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Botón RX antenna                | Abre un menú de selección de antena para la antena receptora de este slice. Utiliza la lista de antenas específica del slice cuando está disponible. Los elementos del menú muestran información sobre herramientas y sugerencia de estado.                                                                                | —                                                                                                                       |
| Botón TX antenna                | Abre un menú de selección de antena para la antena transmisora de este slice. Filtra automáticamente los puertos de antena solo de recepción. Los elementos del menú muestran información sobre herramientas y sugerencia de estado.                                                                               | —                                                                                                                       |
| Pantalla de frecuencia                | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. La entrada directa se bloquea cuando el slice está bloqueado.                                                                                 | —                                                                                                                       |
| Etiqueta de ancho de filtro               | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de ajustes preestablecidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas de modo SSB/digital (#2197, v0.9.8). |                                                                                                                         |
| Deslizador AF Gain (pestaña Audio)       | Establece el nivel de salida de audio para este slice (0-100).                                                                                                                                                                                              | 100                                                                                                                     |
| Deslizador Pan (pestaña Audio)           | Establece el paneo estéreo izquierdo/derecho para este slice (0-100). 50 = centro. El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central en la ranura que muestra la posición neutral.                                                              | 50                                                                                                                      |
| Botón Mute (pestaña Audio)          | Silencia la salida de audio de este slice sin cambiar el ajuste de ganancia AF. Haga clic derecho en el botón de la pestaña Audio para alternar el silencio directamente.                                                                                                                 | off                                                                                                                     |
| Botón y deslizador Squelch (pestaña Audio) | Activa el squelch para este slice. El deslizador adyacente establece el umbral (0-100). Deshabilitado para modos RTTY y digitales (DIGU, DIGL).                                                                                                                 | off                                                                                                                     |
| Combinación AGC (pestaña Audio)            | Establece la velocidad de ataque/liberación del AGC para este slice. Opciones: FAST, MED, SLOW, OFF.                                                                                                                                                                | FAST                                                                                                                     |
| Botones NR / NB / ANF / APF / NRL / NRS / RNN / NRF / ANFL / ANFT (pestaña DSP) | Activa el algoritmo correspondiente de reducción de ruido o filtrado del lado de la radio para este slice. APF solo es visible en modo CW.                                                                                           | off                                                                                                                     |
| Botón MN (pestaña DSP)              | Activa el filtro de muesca manual para este slice. Solo se muestra en radios que admiten filtrado de muesca manual.                                                                                                                                       | off                                                                                                                     |
| Deslizador DSP level (pestaña DSP)       | Establece el nivel de procesamiento para el algoritmo DSP nivelado activado más recientemente. La etiqueta a la izquierda identifica el objetivo actual. Se activa automáticamente al inicio si el perfil guardado de la radio tiene un DSP nivelado habilitado. Oculto (atenuado) cuando no hay ningún algoritmo nivelado activo. | —                                                                                                                       |
| Botón ADSP (pestaña DSP)            | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Botón pulsador no marcable. Al hacer clic, eleva y enfoca el diálogo no modal.                                                                                   | —                                                                                                                       |
| Botón AetherVoice (pestaña DSP)     | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP TX/RX. Botón pulsador no marcable. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas.                                                                                                      | —                                                                                                                       |
| Combinación Mode (pestaña Mode)            | Establece el modo de demodulación para este slice. Opciones: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY.                                                                                                                                 | USB                                                                                                                     |
| Botones de ajustes preestablecidos de filtro (pestaña Mode) | Cada botón aplica un ancho de filtro guardado al slice. Clic izquierdo para aplicar; clic derecho para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro personalizados bajo y alto se pueden almacenar por ranura mediante clic derecho.                          | —                                                                                                                       |
| Botones y etiquetas RIT / XIT (pestaña X/RIT) | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desfase actual; la rueda del ratón ajusta en pasos de 10 Hz.                                                                                                       | off                                                                                                                     |
| Combinación DAX channel (pestaña DAX)      | Asigna un canal de audio DAX a este slice. Opciones: Off, 1-8.                                                                                                                                                                                   | Off                                                                                                                     |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad del botón depende de la serie de radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. | off                                                                                                                     |
| Botón ADSP (pestaña DSP)            | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Con estilo de alternancia de DSP del lado de la radio pero no marcable. Al hacer clic, eleva y enfoca el diálogo no modal de configuración de AetherDSP. | —                                                                                                                       |
| Botón AetherVoice (pestaña DSP)     | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú / cadena para la tira. | —                                                                                                                       |
| Botón de grosor del marcador          | Recorre la línea del marcador VFO por Off, 1 px y 3 px. Se conserva por slice.                                                                                                                                                                    | 1 px                                                                                                                    |
| Botón de bordes de filtro              | Alterna las líneas de borde del filtro en la banda de paso del espectro. Se conserva por slice.                                                                                                                                                                    | mostrado                                                                                                                   |
| Alternancia de colapso                  | Colapsa el panel VFO a una franja compacta de solo frecuencia. Se conserva por slice.                                                                                                                                                                 | expandido                                                                                                                |

## Diseño de la pestaña DSP (v26.8.4)

La pestaña **DSP** ahora muestra botones de reducción de ruido y filtrado del lado de la radio dispuestos en una cuadrícula de cuatro columnas, seguidos de los botones de lanzamiento ADSP y AetherVoice. La cuadrícula incluye todos los botones de reducción de ruido que antes estaban disponibles en el diálogo de configuración de AetherDSP, más un botón de filtro de muesca manual en radios que lo admiten.

| Posición | Botón |
|---|---|
| Fila 1, col 1 | NR |
| Fila 1, col 2 | NR2 |
| Fila 1, col 3 | NR4 |
| Fila 1, col 4 | MNR |
| Fila 2, col 1 | DFNR |
| Fila 2, col 2 | BNR |
| Fila 2, col 3 | RN2 |
| Fila 2, col 4 | RNN |
| Fila 3, col 1 | NRL |
| Fila 3, col 2 | NRS |
| Fila 3, col 3 | NRF |
| Fila 3, col 4 | ANFL |
| Fila 4, col 1 | ANFT |
| Fila 4, col 2 | MN (solo en radios que admiten muesca manual) |
| Fila 4, col 3 | (vacío) |
| Fila 4, col 4 | (vacío) |
| Fila 5, col 1 | ADSP |
| Fila 5, cols 2–3 | AetherVoice |

**Nota**: El diseño de la pestaña DSP se ha actualizado en v26.8.4. Los siguientes botones se han eliminado de la cuadrícula de la pestaña DSP: NB, ANF, APF. Ahora están disponibles desde el panel frontal de la radio o el menú superpuesto del espectro.

Los siguientes módulos DSP del lado del cliente están disponibles como botones de alternancia en la cuadrícula de la pestaña DSP: **NR2**, **RN2**, **BNR**, **NR4**, **MNR**, **DFNR**. Haga clic derecho en cualquiera de estos botones para abrir el diálogo de configuración de AetherDSP para ese algoritmo específico.

Una fila compartida de **deslizador DSP level** aparece debajo de la cuadrícula de botones. El deslizador se redirige automáticamente al botón DSP nivelado que se activó más recientemente. Cuando llega un cambio de estado de nivel DSP desde la radio (por ejemplo, cuando el perfil guardado de la radio tiene NR habilitado al inicio), el deslizador aparece inmediatamente sin necesidad de alternar manualmente. Su etiqueta muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor a la derecha del deslizador muestra el nivel actual numéricamente. Cuando no hay ningún algoritmo DSP nivelado activo — o cuando solo RNN, ANFT o APF están activados — la fila del deslizador está presente en el diseño pero visualmente atenuada. Hacer clic en ella mientras está atenuada no tiene efecto.

## Identificadores de automatización de botones DSP (v26.8.4)

Cada botón de alternancia DSP en la cuadrícula ahora lleva un nombre de objeto estable (`dspNRBtn`, `dspNR2Btn`, `dspANFLBtn`, etc.) que el puente de automatización puede direccionar directamente. Esto complementa los nombres accesibles existentes utilizados por los lectores de pantalla. Los scripts de automatización deben usar estos nombres de objeto en lugar de etiquetas en prosa, que pueden cambiar si alguna vez se ajusta el texto de los botones.

## Consistencia del control de squelch (v26.8.4)

Los controles de squelch en la pestaña **Audio** ahora llaman a `setManualSquelch()` de manera consistente para los ajustes manuales de squelch. Este cambio interno garantiza que el comportamiento del squelch coincida con la API de squelch manual del lado de la radio, proporcionando un comportamiento más predecible en todos los tipos de slice y modos de recepción externos.

## Corrección de entrada de spot en modo colapsado (v26.8.4)

Hacer clic derecho en la pantalla de frecuencia mientras el panel VFO está colapsado ahora abre correctamente el menú contextual **Add Spot** en la propia frecuencia del VFO. Anteriormente, los clics pasaban al widget de espectro subyacente, que informaba la frecuencia ajustada por paso del cursor en lugar de la del VFO. Esta corrección también se aplica a otras interacciones en modo colapsado que dependen de la etiqueta de frecuencia.

## Cambios en los botones de pestaña (v26.6.3)

Las etiquetas de pestaña del panel VFO (Audio, DSP, Mode, X/RIT, DAX) se han cambiado de widgets `QLabel` a `QPushButton`. Este cambio proporciona:

- **Accesibilidad de teclado**: los botones de pestaña ahora son accesibles mediante la tecla Tab. Presione Tab para navegar entre pestañas y presione Enter o Espacio para activar la pestaña enfocada.
- **Indicador de enfoque**: el botón de pestaña enfocado muestra un anillo de enfoque visible (borde inferior) usando el color de texto de etiqueta del tema (`#6880a0`), haciendo visible la navegación por teclado.
- **Clic derecho en la pestaña Audio**: haga clic derecho en el botón de la pestaña **Audio** para alternar el estado de silencio directamente, sin necesidad de abrir la pestaña Audio y hacer clic en el botón Mute.

## Dirección del desplazamiento de frecuencia (v26.6.3)

La dirección del desplazamiento de la rueda del ratón para la sintonización de frecuencia en el panel VFO ahora respeta el ajuste **Reverse mouse wheel** que se encuentra en `Settings > Interaction`. Cuando este ajuste está habilitado, desplazar la rueda del ratón hacia arriba disminuye la frecuencia y desplazarla hacia abajo la aumenta. Anteriormente, la dirección del desplazamiento estaba siempre fija independientemente de este ajuste.

## Cambios en el comportamiento del squelch (v26.5.1)

El control de squelch en la pestaña **Audio** ahora está deshabilitado para modos RTTY y digitales, además del modo CW. Esto evita que el squelch bloquee señales FSK débiles que se alimentan a decodificadores externos a través de DAX (#2504).

Cuando cambia un slice a modo DIGU, DIGL o RTTY:

- El botón y el deslizador Squelch se deshabilitan.
- Si el squelch estaba activo, se apaga automáticamente. El estado anterior se guarda internamente y se restaura si vuelve a un modo de voz.

Esto coincide con el comportamiento existente para el modo CW, donde la radio bloquea el squelch activado a un nivel fijo y rechaza cambios del usuario.

## Cambios en la selección de antena (v26.5.2.1)

Los botones **RX antenna** y **TX antenna** ahora usan menús mejorados:

- El menú de antena RX usa la `rxAntennaList()` del slice cuando está disponible, recurriendo a la lista de antenas global para compatibilidad heredada.
- El menú de antena TX filtra inteligentemente los puertos de antena solo de recepción verificando prefijos "RX", prefijos "ANT", prefijos "TX" o "XVTR" como tokens de respaldo.
- Los elementos del men
