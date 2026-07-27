# Descripción general del Panel VFO

El Panel VFO es un panel de control flotante por segmento (slice) anclado al marcador VFO en la pantalla del espectro. Le brinda acceso rápido a las configuraciones de segmento más utilizadas (modo, ajustes preestablecidos de filtro, selección de antena, controles de audio, AGC, reducción de ruido, RIT/XIT y asignación DAX) sin necesidad de salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Al menos un segmento debe estar activo en el panadaptador.

## Cómo funciona

Haga clic en el marcador VFO en la pantalla del espectro para cualquier segmento. El panel aparece anclado a la izquierda del marcador y se voltea automáticamente hacia la derecha si quedara recortado por el borde de la ventana.

El panel está dividido en pestañas — **Mode**, **Audio**, **DSP**, **X/RIT** y **DAX** — además de una fila de encabezado que siempre está visible. Los controles en la fila de encabezado se aplican independientemente de qué pestaña esté activa.

Cuando está contraído, el panel se reduce a una tira compacta que solo muestra la frecuencia. El ajuste con la rueda del ratón aún funciona en modo contraído. Haga clic en cualquier parte de la tira contraída para expandirla nuevamente, o haga clic en la insignia TX para alternar la asignación del segmento de transmisión.

El panel utiliza un ámbito contenedor temático (`spectrum/vfo`) para su tematización. Hacer clic en un control del panel durante el modo Inspector muestra los valores de token correspondientes.

El marcador VFO ahora incluye una sombra de elevación renderizada por un widget `FlagShadow` hermano ligero. La sombra se mantiene separada del panel VFO principal para que las repintadas del medidor en vivo no vuelvan a desenfocar todo el marcador a la velocidad de animación.

### Fila de encabezado

La fila de encabezado se encuentra sobre las pestañas y siempre está visible.

| Control | Qué hace |
|---|---|
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de este segmento. Los elementos del menú muestran las etiquetas proporcionadas por la radio junto con nombres abreviados entre paréntesis. |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de este segmento. Los puertos de antena solo RX están excluidos. Los elementos del menú muestran las etiquetas proporcionadas por la radio junto con nombres abreviados entre paréntesis. |
| Visualización de frecuencia | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba un valor en MHz y presione Enter o Tab para aplicarlo. La rueda del ratón sobre la visualización de frecuencia sintoniza según el tamaño de paso actual. Si el segmento está bloqueado, se muestra una superposición visual de LOCKED y se bloquea el ajuste con la rueda del ratón. |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer cíclicamente los botones de ajustes preestablecidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como la única fuente de verdad, corrigiendo un desfase de 0,1 kHz que afectaba las lecturas en modo SSB/digital (v0.9.8). |
| Insignia TX | Se muestra en rojo cuando este segmento es el segmento de transmisión activo. En modo contraído, haga clic en la insignia para alternar la asignación TX. |
| Insignia SPLIT | Se muestra en ámbar cuando TX está asignado a un segmento diferente al segmento receptor activo. Desde v26.6.3, la insignia utiliza un estilo de opacidad mejorado para una mejor visibilidad: blanco con alfa 120 en estado normal, alfa 180 al pasar el ratón. |

### Botones de pestaña

La fila de pestañas proporciona botones para Mode, Audio, DSP, X/RIT y DAX. Desde v26.6.3:

- Los botones de pestaña ahora son instancias de `QPushButton` en lugar de `QLabel`, lo que los hace enfocables por teclado.
- Presione **Tab** para enfocar los botones de pestaña. Use las teclas de flecha o **Enter** para cambiar de pestaña.
- La pestaña activa muestra un borde inferior color verde azulado. Los botones de pestaña no tienen un contorno de enfoque visible.
- **Haga clic derecho** en el botón de la pestaña Audio para silenciar el segmento actual directamente.

La pila de pestañas ahora reenvía `heightForWidth` desde cada página, por lo que las páginas que mantienen una relación de aspecto (como `SmartMtrWidget`) impulsan correctamente la altura de la tira. Las páginas sin `heightForWidth` (el espaciador del S-meter) no se ven afectadas.

### Pestaña Mode

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Menú desplegable de modo | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | — |
| Botones de ajuste preestablecido de filtro | — | — | `FilterPresets` |

Haga clic derecho en un botón de ajuste preestablecido de filtro para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro bajo y alto personalizados se pueden guardar por ranura de la misma manera.

Cuando se selecciona DIGU o DIGL en el menú desplegable de modo, aparece un contenedor de datos digitales en la pestaña. Este contenedor es más alto que el otro contenido de la pestaña. El Panel VFO ahora informa solo el tamaño preferido de la pestaña actual, evitando que aparezca un espacio al volver a la pestaña Mode desde la pestaña DSP.

### Pestaña Audio

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Deslizador de ganancia AF | 100 | 0–100 | — |
| Deslizador de balance (Pan) | 50 (centro) | 0–100 | — |
| Botón de silencio (Mute) | desactivado | — | — |
| Botón + deslizador de squelch | desactivado | 0–100 | — |
| Menú desplegable de AGC | FAST | FAST, MED, SLOW, OFF | — |

La posición central del deslizador de balance (50) es el centro estéreo. Haga doble clic en el deslizador de balance para restablecerlo al centro. Los controles de audio reflejan el estado en vivo de la radio y no son persistidos por AetherSDR.

El deslizador de balance utiliza una implementación CenterMarkSlider. El relleno se ancla desde el centro hacia afuera, por lo que el relleno de la ranura se extiende desde la posición central hasta la posición del control deslizante. Se pinta un pequeño punto de marca central en la ranura para mostrar la posición neutra de un vistazo. El color de relleno utiliza el token `color.accent` del tema, y el área no rellena utiliza `color.background.1`.

El squelch está desactivado en modos digital, RTTY y CW. En modos digital y RTTY, el audio alimenta decodificadores externos a través de DAX, donde el squelch enmascararía señales FSK débiles. En modo CW, la radio bloquea el squelch en un nivel fijo y rechaza los cambios. Al ingresar a uno de estos modos mientras el squelch está activado, el squelch se desactiva automáticamente y se restaura al salir de ese modo.

### Pestaña DSP

La pestaña DSP contiene botones para algoritmos de reducción de ruido y filtrado proporcionados directamente por la radio. Los módulos DSP del lado del cliente (NR2, NR4, MNR, BNR, DFNR y RN2) se pueden acceder desde el cuadro de diálogo de Configuración de AetherDSP o desde la Tira de Canal de Audio Aetherial.

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF | desactivado | La disponibilidad de los botones depende de la serie de radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo de Configuración de AetherDSP para ese algoritmo. |
| Botón ADSP | — | Abre el cuadro de diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). El mismo punto de entrada que el menú de Configuración (v0.9.8). Tiene el estilo de un conmutador DSP del lado de la radio pero no es seleccionable. Al hacer clic, abre y enfoca el cuadro de diálogo modeless de Configuración de AetherDSP. El estilo del botón utiliza tokens del tema (`color.background.1` para el fondo y borde, `color.accent` para el estado presionado). |
| Botón AetherVoice | — | Abre la Tira de Canal de Audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

#### Deslizador de nivel DSP

Un deslizador de nivel compartido aparece debajo de la cuadrícula de botones. Se dirige al botón DSP con nivel que se habilitó más recientemente: NR, NB, ANF, NRL, NRS, NRF o ANFL. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual. El valor numérico se muestra a la derecha.

La fila del deslizador permanece en el diseño en todo momento. Cuando no hay ningún DSP con nivel activo (o solo RNN, ANFT o APF están activados), la fila se atenúa y no responde a la interacción. Se vuelve completamente visible nuevamente tan pronto como se activa un DSP con nivel.

En v0.9.8, el deslizador de nivel también se envía a la pila compartida cuando llega un cambio de estado de DSP con nivel desde la radio al inicio. Esto asegura que el deslizador aparezca para cualquier DSP que ya estuviera habilitado en el perfil guardado de la radio.

### Pestaña X/RIT

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botón RIT + etiqueta | desactivado | Habilita la sintonización incremental del receptor. La etiqueta muestra el desfase actual. La rueda del ratón ajusta en pasos de 10 Hz. |
| Botón XIT + etiqueta | desactivado | Habilita la sintonización incremental del transmisor. La etiqueta muestra el desfase actual. La rueda del ratón ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Menú desplegable de canal DAX | Off | Off, 1–8 | — |

### Controles de visualización

Estos controles afectan cómo aparece el segmento en la pantalla del espectro. Se persisten individualmente por segmento (donde `{N}` es el número de segmento).

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Botón de grosor del marcador | 1 px | Off, 1 px, 3 px | `Slice{N}_MarkerWidth` |
| Botón de bordes de filtro | mostrado | mostrado / oculto | `Slice{N}_FilterEdgesHidden` |
| Alternar contracción | expandido | expandido / contraído | `SliceFlagCollapsed_{N}` |

Haga clic en la insignia del segmento en la fila de encabezado para contraer el panel. Haga clic en cualquier parte de la tira contraída para expandirla.

## Selección de antena

Los botones de antena RX y TX abren menús que muestran las etiquetas proporcionadas por la radio (como "ANT 1" o "RX ANT B") junto con nombres abreviados entre paréntesis cuando difieren. Los menús muestran:

- **Antena RX**: Todos los puertos de antena disponibles para recepción. Los elementos del menú incluyen información sobre herramientas y sugerencias en la barra de estado que muestran el nombre completo de la antena.
- **Antena TX**: Solo los puertos de antena adecuados para transmisión (los puertos solo RX están excluidos). Los elementos del menú incluyen información sobre herramientas y sugerencias en la barra de estado que muestran el nombre completo de la antena.

Ambos menús se completan desde la lista de antenas por segmento de la radio cuando está disponible, recurriendo a la lista de antenas global. Las asignaciones de antena se aplican de inmediato.

## Entrada de frecuencia

Haga clic en la visualización de frecuencia para comenzar la entrada directa. Se aplican las siguientes reglas:

- Escriba una frecuencia en MHz (p. ej., `14.200` o `14200`). Presione Enter o Tab para aplicarla.
- En bandas XVTR, se aceptan frecuencias de hasta 50000 MHz.
- En bandas entre 100-999 MHz (2m, 70cm), un número entero simple como `1446` se interpreta como `144.6`, `14696` como `146.96` y `144600` como `144.600`. Esta conveniencia no se aplica por encima de 1000 MHz (bandas de 23cm y microondas), donde un número entero simple representa la frecuencia en MHz directamente.
- Si ingresa explícitamente una frecuencia superior a 54 MHz (p. ej., `144.200`), el analizador la trata como una entrada válida en MHz y acepta frecuencias de hasta 50000 MHz, incluso si el segmento no está en una banda XVTR.

Desde v26.6.3, el campo de entrada de frecuencia utiliza un widget `FreqLineEdit` con texto de sugerencia "MHz (e.g. 14.225)" que se muestra cuando el campo está vacío.

## Comportamiento del segmento bloqueado

Cuando un segmento está bloqueado:

- El botón de bloqueo muestra un icono de candado. Haga clic para desbloquear.
- El ajuste con la rueda del ratón está bloqueado. Si intenta sintonizar un segmento bloqueado, aparece una superposición visual de LOCKED en la visualización de frecuencia y cualquier entrada directa de frecuencia en curso se cancela.
- La superposición LOCKED se borra automáticamente cuando desbloquea el segmento.
- La entrada directa de frecuencia se impide mientras está bloqueado: hacer clic en la visualización de frecuencia no ingresa al modo de edición, y cualquier entrada directa activa se cancela de inmediato.

## Ajuste con la rueda del ratón

Desde v26.6.3, el ajuste con la rueda del ratón respeta la configuración `InteractionSettings::reverseMouseWheel`. Cuando el desplazamiento inverso del ratón está habilitado, girar hacia arriba ahora disminuye la frecuencia y girar hacia abajo la aumenta. Esto se aplica a todas las interacciones con la rueda del ratón en el panel VFO, incluida la visualización de frecuencia y el modo contraído.

Accesibilidad: Desde v26.6.3, la etiqueta de frecuencia dispara `QAccessibleValueChangeEvent` cuando la frecuencia cambia, lo que garantiza que los lectores de pantalla anuncien el nuevo valor de frecuencia. La actualización de accesibilidad tiene una tasa limitada para evitar anuncios excesivos.

## Soporte de tematización e Inspector

El Panel VFO utiliza tokens de tema para su apariencia visual. En v26.6.1, los siguientes tokens de tema se declaran para la cobertura del modo Inspector:

- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

Estos tokens son utilizados por llamadas raw de QPainter que pintan el fondo del panel, el medidor de señal
