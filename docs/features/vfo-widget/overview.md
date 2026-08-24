# Descripción general del panel VFO

El panel VFO es un panel de control flotante por slice, anclado a la bandera del marcador VFO en la pantalla del espectro. Le brinda acceso rápido a los ajustes de slice más utilizados — modo, presets de filtro, selección de antena, controles de audio, AGC, reducción de ruido, RIT/XIT y asignación DAX — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Al menos un slice debe estar activo en el panadapter.

## Cómo funciona

Haga clic en la bandera del marcador VFO en la pantalla del espectro para cualquier slice. El panel aparece anclado a la izquierda del marcador y se voltea automáticamente hacia la derecha si fuera recortado por el borde de la ventana.

El panel está dividido en pestañas — **Mode**, **Audio**, **DSP**, **X/RIT** y **DAX** — más una fila de encabezado que siempre está visible. Los controles de la fila de encabezado se aplican independientemente de qué pestaña esté activa.

Cuando está colapsado, el panel se reduce a una franja compacta de solo frecuencia. La sintonización con la rueda del ratón sigue funcionando en modo colapsado. Haga clic en cualquier lugar de la franja colapsada para expandirla nuevamente, o haga clic en la insignia TX para alternar la asignación del slice de transmisión.

El panel utiliza un ámbito de contenedor temático (`spectrum/vfo`) para su tematización. Al hacer clic en un control del panel durante el modo Inspector se muestran los valores de token correspondientes.

La bandera VFO ahora incluye una sombra de elevación renderizada por un widget hermano ligero `FlagShadow`. La sombra se mantiene separada del panel VFO principal para que las repintadas del medidor en vivo no vuelvan a desenfocar toda la bandera a la velocidad de animación.

### Fila de encabezado

La fila de encabezado se encuentra sobre las pestañas y siempre está visible.

| Control | Qué hace |
|---|---|
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de este slice. Los elementos del menú muestran las etiquetas proporcionadas por la radio junto con nombres abreviados entre paréntesis. |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de este slice. Los puertos de antena solo-RX quedan excluidos. Los elementos del menú muestran las etiquetas proporcionadas por la radio junto con nombres abreviados entre paréntesis. |
| Pantalla de frecuencia | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba un valor en MHz y presione Enter o Tab para aplicarlo. La rueda del ratón sobre la pantalla de frecuencia sintoniza según el tamaño de paso actual. Si el slice está bloqueado, se muestra una superposición visual LOCKED y se bloquea la sintonización con la rueda del ratón. |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preset de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modos SSB/digitales (#2197, v0.9.8). |
| Insignia TX | Se muestra en rojo cuando este slice es el slice de transmisión activo. En modo colapsado, haga clic en la insignia para alternar la asignación TX. |
| Insignia SPLIT | Se muestra en ámbar cuando TX está asignado a un slice diferente del slice receptor activo. Desde v26.6.3, la insignia utiliza un estilo de opacidad mejorado para mayor visibilidad — blanco con alfa 120 en estado normal, alfa 180 al pasar el cursor. |

### Botones de pestaña

La fila de pestañas proporciona botones para Mode, Audio, DSP, X/RIT y DAX. Desde v26.6.3:

- Los botones de pestaña ahora son instancias de `QPushButton` en lugar de `QLabel`, lo que los hace enfocables mediante teclado.
- Presione **Tab** para enfocar los botones de pestaña. Use las teclas de flecha o **Enter** para cambiar de pestaña.
- La pestaña activa muestra un borde inferior verde azulado. Los botones de pestaña no tienen contorno de enfoque visible.
- **Clic derecho** en el botón de la pestaña Audio para alternar el silencio del slice actual directamente.

La pila de pestañas ahora reenvía `heightForWidth` de cada página, de modo que las páginas que mantienen una relación de aspecto (como `SmartMtrWidget`) impulsan correctamente la altura de la franja. Las páginas sin `heightForWidth` (el espaciador del medidor S) no se ven afectadas.

En v26.8.4, el índice de la pestaña DAX se rastrea internamente, y los separadores de pestaña se almacenan como una lista para que puedan recibir estilo u ocultarse de manera consistente con los botones de pestaña.

### Pestaña Mode

| Control | Predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Combo de modo | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | — |
| Botones de preset de filtro | — | — | `FilterPresets` |

Haga clic derecho en un botón de preset de filtro para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro personalizados bajo y alto se pueden guardar por ranura de la misma manera.

Cuando se selecciona DIGU o DIGL en el combo de modo, aparece un contenedor de datos digitales en la pestaña. Este contenedor es más alto que el otro contenido de la pestaña. El panel VFO ahora informa solo el tamaño preferido de la pestaña actual, evitando que aparezca un espacio al volver a la pestaña Mode desde la pestaña DSP.

**Tonos en modo FM**: En modos FM, NFM y DFM, la pestaña Mode muestra controles de tono adicionales (codificación y decodificación CTCSS/DCS). Estos controles están ocultos en modo DSTR y en todos los modos no-FM. Los controles de tono están controlados por un helper dedicado `hasFmToneControls`, que separa la verificación de la familia FM de la verificación más amplia del modo RF utilizada para otros fines.

### Pestaña Audio

| Control | Predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Deslizador de ganancia AF | 100 | 0–100 | — |
| Deslizador de paneo | 50 (centro) | 0–100 | — |
| Botón de silencio | apagado | — | — |
| Botón + deslizador de squelch | apagado | 0–100 | — |
| Combo AGC | FAST | FAST, MED, SLOW, OFF | — |

La posición central del deslizador de paneo (50) es el centro estéreo. Haga doble clic en el deslizador de paneo para restablecerlo al centro. Los controles de audio reflejan el estado en vivo de la radio y no son persistidos por AetherSDR.

El deslizador de paneo utiliza una implementación CenterMarkSlider. El relleno se ancla desde el centro hacia afuera, de modo que el relleno de la ranura se extiende desde la posición central hasta la posición del controlador. Se dibuja un pequeño punto de marca central en la ranura para mostrar la posición neutral de un vistazo. El color de relleno utiliza el token `color.accent` del tema, y el área sin rellenar utiliza `color.background.1`.

El squelch está deshabilitado en modos digitales, RTTY y CW. En modos digitales y RTTY, el audio alimenta decodificadores externos a través de DAX, donde el squelch bloquearía señales FSK débiles. En modo CW, la radio bloquea el squelch activado a un nivel fijo y rechaza cambios. Al entrar en uno de estos modos mientras el squelch está habilitado, el squelch se apaga automáticamente y se restaura al salir de ese modo.

En v26.8.4, los cambios de estado del squelch ahora llaman a `setManualSquelch()` en el slice. Esta es la API dedicada para cambios de squelch locales impulsados por el operador y mantiene el modelo sincronizado con las posiciones del deslizador y el botón.

### Pestaña DSP

La pestaña DSP contiene botones para reducción de ruido y algoritmos de filtrado proporcionados directamente por la radio. Los módulos DSP del lado del cliente (NR2, NR4, MNR, BNR, DFNR y RN2) se pueden acceder desde el diálogo de configuración de AetherDSP o desde la tira de canal de audio Aetherial.

| Control | Predeterminado | Notas |
|---|---|---|
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF | apagado | La disponibilidad de los botones depende de la serie y compilación de la radio. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |
| Botón MN | apagado | Filtro de muesca manual. Disponible solo cuando la radio informa soporte `hasManualNotch`. Oculto en caso contrario. |
| Botón ADSP | — | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Tiene estilo de conmutador DSP del lado de la radio pero no es marcable. Al hacer clic, eleva y enfoca el diálogo de configuración de AetherDSP no modal. El estilo del botón utiliza tokens del tema (`color.background.1` para fondo y borde, `color.accent` para el estado presionado). |
| Botón AetherVoice | — | Abre la tira de canal de audio Aetherial — la suite DSP unificada TX/RX (v0.9.8). Abarca 2 columnas en la cuadrícula DSP de 4 columnas. |

En v26.8.4, los botones de conmutación DSP tienen valores de `objectName` estables con la forma `dsp<Etiqueta>Btn` (por ejemplo, `dspANFBtn`). Esto proporciona una dirección de automatización confiable independiente del texto del nombre accesible, de modo que las herramientas de scripting y certificación puedan apuntar a estos conmutadores sin depender de una redacción que pueda cambiar.

#### Deslizador de nivel DSP

Un deslizador de nivel compartido aparece debajo de la cuadrícula de botones. Apunta al botón DSP con nivel que se habilitó más recientemente — NR, NB, ANF, NRL, NRS, NRF, ANFL o MN. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual. El valor numérico se muestra a la derecha.

La fila del deslizador permanece en el diseño en todo momento. Cuando no hay DSP con nivel activo (o solo RNN, ANFT o APF están activados), la fila se desvanece y no responde a la interacción. Se vuelve completamente visible nuevamente tan pronto como se activa un DSP con nivel.

En v0.9.8, el deslizador de nivel también se empuja a la pila compartida cuando llega un cambio de estado de DSP con nivel desde la radio al inicio. Esto garantiza que el deslizador aparezca para cualquier DSP que ya estuviera habilitado en el perfil guardado de la radio.

En v26.8.4, el deslizador apunta al nivel MN (muesca manual) cuando se selecciona el botón MN, manteniendo el nivel MN ajustable a través del mismo mecanismo de deslizador compartido.

### Pestaña X/RIT

| Control | Predeterminado | Notas |
|---|---|---|
| Botón + etiqueta RIT | apagado | Habilita la sintonización incremental del receptor. La etiqueta muestra el desfase actual. La rueda del ratón ajusta en pasos de 10 Hz. |
| Botón + etiqueta XIT | apagado | Habilita la sintonización incremental del transmisor. La etiqueta muestra el desfase actual. La rueda del ratón ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Combo de canal DAX | Off | Off, 1–8 | — |

### Controles de visualización

Estos controles afectan cómo se muestra el slice en la pantalla del espectro. Se persisten individualmente por slice (donde `{N}` es el número de slice).

| Control | Predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Botón de grosor de marcador | 1 px | Off, 1 px, 3 px | `Slice{N}_MarkerWidth` |
| Botón de bordes de filtro | mostrado | mostrado / oculto | `Slice{N}_FilterEdgesHidden` |
| Alternar colapso | expandido | expandido / colapsado | `SliceFlagCollapsed_{N}` |

Al hacer clic en la insignia del slice en la fila de encabezado se colapsa el panel. Al hacer clic en cualquier lugar de la franja colapsada se expande.

En v26.8.4, la etiqueta de frecuencia colapsada participa en la cadena de filtros de eventos. Esto garantiza que las acciones de clic derecho (como Add Spot) en la franja colapsada apunten a la frecuencia propia del VFO en lugar de pasar al widget del espectro subyacente, que de otro modo informaría la frecuencia del cursor ajustada al paso (#4455).

## Selección de antena

Los botones de antena RX y TX abren menús que muestran las etiquetas proporcionadas por la radio (como "ANT 1" o "RX ANT B") junto con nombres abreviados entre paréntesis cuando difieren. Los menús muestran:

- **Antena RX**: Todos los puertos de antena disponibles para recepción. Los elementos del menú incluyen tooltips y sugerencias en la barra de estado que muestran el nombre completo de la antena.
- **Antena TX**: Solo los puertos de antena adecuados para transmisión (los puertos solo-RX quedan excluidos). Los elementos del menú incluyen tooltips y sugerencias en la barra de estado que muestran el nombre completo de la antena.

Ambos menús se completan desde la lista de antenas por slice de la radio cuando está disponible, con respaldo a la lista de antenas global. Las asignaciones de antena se aplican inmediatamente.

## Entrada de frecuencia

Haga clic en la pantalla de frecuencia para comenzar la entrada directa. Se aplican las siguientes reglas:

- Escriba una frecuencia en MHz (p. ej., `14.200` o `14200`). Presione Enter o Tab para aplicarla.
- En bandas XVTR, se aceptan frecuencias de hasta 50000 MHz.
- En bandas entre 100-999 MHz (2m, 70cm), un entero simple como `1446` se interpreta como `144.6`, `14696` como `146.96`, y `144600` como `144.600`. Esta conveniencia no se aplica por encima de 1000 MHz (bandas de 23cm y microondas), donde un entero simple representa la frecuencia en MHz directamente.
- Si ingresa explícitamente una frecuencia superior a 54 MHz (p. ej., `144.200`), el analizador la trata como una entrada válida en MHz y acepta frecuencias de hasta 50000 MHz, incluso si el slice no está en una banda XVTR.

Desde v26.6.3, el campo de entrada de frecuencia utiliza un widget `FreqLineEdit` con texto de sugerencia "MHz (e.g. 14.225)" que se muestra cuando el campo está vacío.

## Comportamiento del slice bloqueado

Cuando un slice está bloqueado:

- El botón de bloqueo muestra un icono de candado
