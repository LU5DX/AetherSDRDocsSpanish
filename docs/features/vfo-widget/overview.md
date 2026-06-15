# Panel de VFO: descripción general

El Panel de VFO es un panel de control flotante por segmento, anclado a la marca indicadora de VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes de segmento más utilizados — modo, preajustes de filtro, selección de antena, controles de audio, AGC, reducción de ruido, RIT/XIT y asignación de DAX — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Al menos un segmento debe estar activo en el panadapter.

## Cómo funciona

Haga clic en la marca indicadora de VFO en la pantalla del espectro para cualquier segmento. El panel aparece anclado a la izquierda de la marca y se voltea automáticamente a la derecha si quedara recortado por el borde de la ventana.

El panel está dividido en pestañas: **Mode**, **Audio**, **DSP**, **X/RIT** y **DAX**, más una fila de encabezado que siempre está visible. Los controles de la fila de encabezado se aplican independientemente de la pestaña activa.

Cuando está contraído, el panel se reduce a una tira compacta que solo muestra la frecuencia. El sintonizador con la rueda del ratón sigue funcionando en modo contraído. Haga clic en cualquier parte de la tira contraída para expandirla de nuevo, o haga clic en la insignia de TX para alternar la asignación del segmento de transmisión.

El panel utiliza un alcance de contenedor temático (`spectrum/vfo`) para su tematización. Hacer clic en un control del panel durante el modo Inspector muestra los valores de token correspondientes.

### Fila de encabezado

La fila de encabezado se encuentra sobre las pestañas y siempre está visible.

| Control | Función |
|---|---|
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de este segmento. Los elementos del menú muestran las etiquetas proporcionadas por la radio junto con nombres abreviados entre paréntesis. |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de este segmento. Los puertos de antena solo de RX están excluidos. Los elementos del menú muestran las etiquetas proporcionadas por la radio junto con nombres abreviados entre paréntesis. |
| Pantalla de frecuencia | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba un valor en MHz y presione Enter o Tab para aplicarlo. La rueda del ratón sobre la pantalla de frecuencia sintoniza según el tamaño de paso actual. Si el segmento está bloqueado, se muestra una superposición visual de BLOQUEADO y se bloquea la sintonización con la rueda del ratón. |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (v0.9.8). |
| Insignia de TX | Se muestra en rojo cuando este segmento es el segmento de transmisión activo. En modo contraído, haga clic en la insignia para alternar la asignación de TX. |
| Insignia de SPLIT | Se muestra en ámbar cuando TX está asignado a un segmento diferente al segmento receptor activo. A partir de v26.6.3, la insignia utiliza un estilo de opacidad mejorado para una mejor visibilidad: blanco con alfa 120 en estado normal, alfa 180 al pasar el ratón. |

### Botones de pestaña

La fila de pestañas proporciona botones para Mode, Audio, DSP, X/RIT y DAX. A partir de v26.6.3:

- Los botones de pestaña ahora son instancias de `QPushButton` en lugar de `QLabel`, lo que los hace enfocables mediante teclado.
- Presione **Tab** para enfocar los botones de pestaña. Use las teclas de flecha o **Enter** para cambiar de pestaña.
- La pestaña activa muestra un borde inferior en color verde azulado. Los botones de pestaña no tienen un contorno de enfoque visible.
- **Haga clic derecho** en el botón de la pestaña Audio para alternar la función de silencio del segmento actual directamente.

### Pestaña Mode

| Control | Predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Combinación de modo | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | — |
| Botones de preajuste de filtro | — | — | `FilterPresets` |

Haga clic derecho en un botón de preajuste de filtro para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro inferior y superior personalizados se pueden guardar por ranura de la misma manera.

Cuando se selecciona DIGU o DIGL en la combinación de modo, aparece un contenedor de datos digitales en la pestaña. Este contenedor es más alto que el otro contenido de la pestaña. El Panel de VFO ahora informa solo el tamaño preferido de la pestaña actual, evitando que aparezca un espacio al volver a la pestaña Mode desde la pestaña DSP.

### Pestaña Audio

| Control | Predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Control deslizante de ganancia AF | 100 | 0–100 | — |
| Control deslizante de balance | 50 (centro) | 0–100 | — |
| Botón de silencio | desactivado | — | — |
| Botón + control deslizante de silenciador | desactivado | 0–100 | — |
| Combinación de AGC | FAST | FAST, MED, SLOW, OFF | — |

La posición central del control deslizante de balance (50) es el centro estéreo. Haga doble clic en el control deslizante de balance para restablecerlo al centro. Los controles de audio reflejan el estado en vivo de la radio y no son persistidos por AetherSDR.

El control deslizante de balance utiliza una implementación de CenterMarkSlider. El relleno se ancla desde el centro hacia afuera, por lo que el relleno de la ranura se extiende desde la posición central hasta la posición del control. Se dibuja un pequeño punto de marca central en la ranura para mostrar la posición neutral de un vistazo. El color de relleno utiliza el token `color.accent` del tema, y el área sin rellenar utiliza `color.background.1`.

El silenciador está deshabilitado en modos digital, RTTY y CW. En modos digital y RTTY, el audio alimenta decodificadores externos a través de DAX, donde el silenciador podría bloquear señales FSK débiles. En modo CW, la radio fija el silenciador en un nivel fijo y rechaza los cambios. Al ingresar a uno de estos modos mientras el silenciador está habilitado, el silenciador se desactiva automáticamente y se restaura al salir de ese modo.

### Pestaña DSP

La pestaña DSP contiene botones para algoritmos de reducción de ruido y filtrado proporcionados directamente por la radio. Los módulos DSP del lado del cliente (NR2, NR4, MNR, BNR, DFNR y RN2) se pueden acceder desde el diálogo de configuración de AetherDSP o desde la tira de canal de audio de Aetherial.

| Control | Predeterminado | Notas |
|---|---|---|
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF | desactivado | La disponibilidad de los botones depende de la serie y la versión de la radio. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |
| Botón ADSP | — | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú de configuración (v0.9.8). Estilizado como un conmutador de DSP del lado de la radio, pero no seleccionable. Al hacer clic, abre y enfoca el diálogo de configuración de AetherDSP no modal. El estilo del botón utiliza tokens de tema (`color.background.1` para fondo y borde, `color.accent` para estado presionado). |
| Botón AetherVoice | — | Abre la tira de canal de audio de Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula de DSP de 4 columnas. |

#### Control deslizante de nivel DSP

Un control deslizante de nivel compartido aparece debajo de la cuadrícula de botones. Apunta al botón DSP con nivel que se haya habilitado más recientemente: NR, NB, ANF, NRL, NRS, NRF o ANFL. La etiqueta a la izquierda del control deslizante muestra el nombre del objetivo actual. El valor numérico se muestra a la derecha.

La fila del control deslizante permanece en el diseño en todo momento. Cuando no hay ningún DSP con nivel activo (o solo están activos RNN, ANFT o APF), la fila se desvanece y no responde a la interacción. Se vuelve completamente visible tan pronto como se activa un DSP con nivel.

En v0.9.8, el control deslizante de nivel también se envía a la pila compartida cuando llega un cambio de estado de DSP con nivel desde la radio al iniciar. Esto asegura que el control deslizante aparezca para cualquier DSP que ya estuviera habilitado en el perfil guardado de la radio.

### Pestaña X/RIT

| Control | Predeterminado | Notas |
|---|---|---|
| Botón + etiqueta de RIT | desactivado | Habilita la sintonización incremental del receptor. La etiqueta muestra el desplazamiento actual. La rueda del ratón ajusta en pasos de 10 Hz. |
| Botón + etiqueta de XIT | desactivado | Habilita la sintonización incremental del transmisor. La etiqueta muestra el desplazamiento actual. La rueda del ratón ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Combinación de canal DAX | Off | Off, 1–8 | — |

### Controles de pantalla

Estos controles afectan la apariencia del segmento en la pantalla del espectro. Se persisten individualmente por segmento (donde `{N}` es el número de segmento).

| Control | Predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Botón de grosor de marca | 1 px | Off, 1 px, 3 px | `Slice{N}_MarkerWidth` |
| Botón de bordes de filtro | mostrado | mostrado / oculto | `Slice{N}_FilterEdgesHidden` |
| Alternancia de contracción | expandido | expandido / contraído | `SliceFlagCollapsed_{N}` |

Haga clic en la insignia del segmento en la fila de encabezado para contraer el panel. Haga clic en cualquier parte de la tira contraída para expandirlo.

## Selección de antena

Los botones de antena RX y TX abren menús que muestran las etiquetas proporcionadas por la radio (como "ANT 1" o "RX ANT B") junto con nombres abreviados entre paréntesis cuando difieren. Los menús muestran:

- **Antena RX**: Todos los puertos de antena disponibles para recepción. Los elementos del menú incluyen información sobre herramientas y sugerencias en la barra de estado que muestran el nombre completo de la antena.
- **Antena TX**: Solo los puertos de antena adecuados para transmisión (los puertos solo de RX están excluidos). Los elementos del menú incluyen información sobre herramientas y sugerencias en la barra de estado que muestran el nombre completo de la antena.

Ambos menús se completan desde la lista de antenas por segmento de la radio cuando está disponible, recurriendo a la lista de antenas global. Las asignaciones de antena se aplican inmediatamente.

## Entrada de frecuencia

Haga clic en la pantalla de frecuencia para comenzar la entrada directa. Se aplican las siguientes reglas:

- Escriba una frecuencia en MHz (por ejemplo, `14.200` o `14200`). Presione Enter o Tab para aplicarla.
- En bandas XVTR, se aceptan frecuencias de hasta 50000 MHz.
- En bandas entre 100-999 MHz (2m, 70cm), un número entero como `1446` se interpreta como `144.6`, `14696` como `146.96`, y `144600` como `144.600`. Esta conveniencia no se aplica por encima de 1000 MHz (bandas de 23cm y microondas), donde un número entero representa la frecuencia en MHz directamente.
- Si ingresa explícitamente una frecuencia superior a 54 MHz (por ejemplo, `144.200`), el analizador la trata como una entrada válida en MHz y acepta frecuencias de hasta 50000 MHz, incluso si el segmento no está en una banda XVTR.

A partir de v26.6.3, el campo de entrada de frecuencia utiliza un widget `FreqLineEdit` con texto de sugerencia "MHz (e.g. 14.225)" que se muestra cuando el campo está vacío.

## Comportamiento del segmento bloqueado

Cuando un segmento está bloqueado:

- El botón de bloqueo muestra un icono de candado. Haga clic para desbloquear.
- La sintonización con la rueda del ratón está bloqueada. Si intenta sintonizar un segmento bloqueado, aparece una superposición visual de BLOQUEADO en la pantalla de frecuencia y se cancela cualquier entrada directa de frecuencia en curso.
- La superposición de BLOQUEADO se elimina automáticamente cuando desbloquea el segmento.
- La entrada directa de frecuencia se evita mientras está bloqueado: al hacer clic en la pantalla de frecuencia no se ingresa al modo de edición, y cualquier entrada directa activa se cancela inmediatamente.

## Sintonización con la rueda del ratón

A partir de v26.6.3, la sintonización con la rueda del ratón respeta la configuración `InteractionSettings::reverseMouseWheel`. Cuando la rueda del ratón inversa está habilitada, el desplazamiento hacia arriba disminuye la frecuencia y el desplazamiento hacia abajo la aumenta. Esto se aplica a todas las interacciones de desplazamiento en el panel de VFO, incluida la pantalla de frecuencia y el modo contraído.

Accesibilidad: A partir de v26.6.3, la etiqueta de frecuencia activa `QAccessibleValueChangeEvent` cuando la frecuencia cambia, lo que garantiza que los lectores de pantalla anuncien el nuevo valor de frecuencia. La actualización de accesibilidad tiene una velocidad limitada para evitar anuncios excesivos.

## Soporte de tematización e Inspector

El Panel de VFO utiliza tokens de tema para su apariencia visual. En v26.6.1, se declaran los siguientes tokens de tema para la cobertura del modo Inspector:

- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

Estos tokens son utilizados por llamadas QPainter sin formato que pintan el fondo del panel, el indicador de señal y otros elementos dibujados personalizados. Al usar el Inspector, al hacer clic en la marca de VFO, la insignia de indicativo o la superficie de la tira del indicador de señal, estos tokens aparecen en la lista de resultados.

El botón ADSP y otros botones del panel utilizan un estilo basado en temas a través de applyStyleSheet, con `{{color.background.1}}` para el fondo y `{{color.accent}}` para el estado presionado.

## Consejos

- En modo contraído, la rueda del ratón en cualquier lugar de la tira sintoniza el segmento según el tamaño de paso actual.
- La sintonización con la rueda del ratón funciona en modo contra
