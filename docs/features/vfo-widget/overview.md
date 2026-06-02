# Resumen del Panel VFO

El Panel VFO es un panel de control flotante por segmento (slice), anclado a la bandera del marcador VFO en la pantalla del espectro. Le brinda acceso rápido a los ajustes de segmento más utilizados — modo, preajustes de filtro, selección de antena, controles de audio, AGC, reducción de ruido, RIT/XIT y asignación de DAX — sin tener que salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- Al menos un segmento debe estar activo en el panadapter.

## Cómo funciona

Haga clic en la bandera del marcador VFO en la pantalla del espectro para cualquier segmento. El panel aparece anclado a la izquierda del marcador y se voltea automáticamente hacia la derecha si quedara recortado por el borde de la ventana.

El panel está dividido en pestañas — **Mode**, **Audio**, **DSP**, **X/RIT** y **DAX** — más una fila de encabezado que siempre está visible. Los controles en la fila de encabezado se aplican independientemente de qué pestaña esté activa.

Cuando está colapsado, el panel se reduce a una tira compacta que solo muestra la frecuencia. El ajuste con la rueda del ratón sigue funcionando en modo colapsado. Haga clic en cualquier parte de la tira colapsada para expandirla de nuevo, o haga clic en la insignia TX para alternar la asignación del segmento de transmisión.

El panel utiliza un ámbito de contenedor temático (`spectrum/vfo`) para su apariencia. Al hacer clic en un control del panel durante el modo Inspector, se muestran los valores de token relevantes.

### Fila de encabezado

La fila de encabezado se encuentra sobre las pestañas y siempre está visible.

| Control | Qué hace |
|---|---|
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de este segmento. Los elementos del menú muestran las etiquetas proporcionadas por el radio junto con nombres abreviados entre paréntesis. |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de este segmento. Los puertos de antena solo RX están excluidos. Los elementos del menú muestran las etiquetas proporcionadas por el radio junto con nombres abreviados entre paréntesis. |
| Visualización de frecuencia | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba un valor en MHz y presione Enter o Tab para aplicarlo. La rueda del ratón sobre la visualización de frecuencia sintoniza según el tamaño de paso actual. Si el segmento está bloqueado, se muestra una superposición visual de LOCKED y se bloquea el ajuste con la rueda del ratón. |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (v0.9.8). |
| Insignia TX | Se muestra en rojo cuando este segmento es el segmento de transmisión activo. En modo colapsado, haga clic en la insignia para alternar la asignación TX. |
| Insignia SPLIT | Se muestra en ámbar cuando TX está asignado a un segmento diferente al segmento receptor activo. |

### Pestaña Mode

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Combo Mode | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | — |
| Botones de preajuste de filtro | — | — | `FilterPresets` |

Haga clic derecho en un botón de preajuste de filtro para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro bajo y alto personalizados se pueden guardar por ranura de la misma manera.

Cuando se selecciona DIGU o DIGL en el combo Mode, aparece un contenedor de datos digitales en la pestaña. Este contenedor es más alto que el otro contenido de la pestaña. El Panel VFO ahora informa solo el tamaño preferido de la pestaña actual, evitando que aparezca un espacio al cambiar de nuevo a la pestaña Mode desde la pestaña DSP.

### Pestaña Audio

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Deslizador AF Gain | 100 | 0–100 | — |
| Deslizador Pan | 50 (centro) | 0–100 | — |
| Botón Mute | desactivado | — | — |
| Botón + deslizador Squelch | desactivado | 0–100 | — |
| Combo AGC | FAST | FAST, MED, SLOW, OFF | — |

La posición central del deslizador Pan (50) es el centro estéreo. Haga doble clic en el deslizador Pan para reiniciarlo al centro. Los controles de audio reflejan el estado en vivo del radio y no son persistidos por AetherSDR.

El deslizador Pan utiliza una implementación CenterMarkSlider. El relleno se ancla desde el centro hacia afuera, por lo que el relleno de la ranura se extiende desde la posición central hasta la posición del control. Se pinta un pequeño punto de marca central en la ranura para mostrar la posición neutral de un vistazo. El color de relleno utiliza el token `color.accent` del tema, y el área sin rellenar utiliza `color.background.1`.

El squelch está desactivado en modos digital, RTTY y CW. En modos digital y RTTY, el audio alimenta decodificadores externos a través de DAX, donde el squelch podría bloquear señales FSK débiles. En modo CW, el radio bloquea el squelch en un nivel fijo y rechaza los cambios. Al ingresar a uno de estos modos mientras el squelch está activado, el squelch se apaga automáticamente y se restaura al salir de ese modo.

### Pestaña DSP

La pestaña DSP contiene botones para algoritmos de reducción de ruido y filtrado proporcionados directamente por el radio. Los módulos DSP del lado del cliente (NR2, NR4, MNR, BNR, DFNR y RN2) se pueden acceder desde el diálogo de Ajustes de AetherDSP o desde la Tira de Canal de Audio Aetherial.

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF | desactivado | La disponibilidad de los botones depende de la serie y versión del radio. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Ajustes de AetherDSP para ese algoritmo. |
| Botón ADSP | — | Abre el diálogo de Ajustes de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). El mismo punto de entrada que el menú de Ajustes (v0.9.8). Tiene el estilo de una palanca DSP del lado del radio pero no es seleccionable. Al hacer clic, abre y enfoca el diálogo modal de Ajustes de AetherDSP. El estilo del botón utiliza tokens de tema (`color.background.1` para fondo y borde, `color.accent` para el estado presionado). |
| Botón AetherVoice | — | Abre la Tira de Canal de Audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

#### Deslizador de nivel DSP

Un deslizador de nivel compartido aparece debajo de la cuadrícula de botones. Apunta al botón DSP con nivel que se habilitó más recientemente: NR, NB, ANF, NRL, NRS, NRF o ANFL. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual. El valor numérico se muestra a la derecha.

La fila del deslizador permanece en el diseño en todo momento. Cuando no hay ningún DSP con nivel activo (o solo RNN, ANFT o APF están encendidos), la fila se atenúa y no responde a la interacción. Se vuelve completamente visible tan pronto como se enciende un DSP con nivel.

En v0.9.8, el deslizador de nivel también se envía a la pila compartida cuando llega un cambio de estado de DSP con nivel desde el radio al iniciar. Esto asegura que el deslizador aparezca para cualquier DSP que ya estuviera habilitado en el perfil guardado del radio.

### Pestaña X/RIT

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botón + etiqueta RIT | desactivado | Habilita la sintonización incremental del receptor. La etiqueta muestra el desplazamiento actual. La rueda del ratón ajusta en pasos de 10 Hz. |
| Botón + etiqueta XIT | desactivado | Habilita la sintonización incremental del transmisor. La etiqueta muestra el desplazamiento actual. La rueda del ratón ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Combo canal DAX | Off | Off, 1–8 | — |

### Controles de visualización

Estos controles afectan cómo aparece el segmento en la pantalla del espectro. Se persisten individualmente por segmento (donde `{N}` es el número de segmento).

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Botón de grosor del marcador | 1 px | Off, 1 px, 3 px | `Slice{N}_MarkerWidth` |
| Botón de bordes de filtro | mostrado | mostrado / oculto | `Slice{N}_FilterEdgesHidden` |
| Alternar colapso | expandido | expandido / colapsado | `SliceFlagCollapsed_{N}` |

Al hacer clic en la insignia del segmento en la fila de encabezado, se colapsa el panel. Al hacer clic en cualquier parte de la tira colapsada, se expande.

## Selección de antena

Los botones de antena RX y TX abren menús que muestran las etiquetas proporcionadas por el radio (como "ANT 1" o "RX ANT B") junto con nombres abreviados entre paréntesis cuando difieren. Los menús muestran:

- **Antena RX**: Todos los puertos de antena disponibles para recepción. Los elementos del menú incluyen información sobre herramientas y sugerencias en la barra de estado que muestran el nombre completo de la antena.
- **Antena TX**: Solo los puertos de antena adecuados para transmisión (los puertos solo RX están excluidos). Los elementos del menú incluyen información sobre herramientas y sugerencias en la barra de estado que muestran el nombre completo de la antena.

Ambos menús se completan a partir de la lista de antenas por segmento del radio cuando esté disponible, recurriendo a la lista global de antenas. Las asignaciones de antena se aplican de inmediato.

## Entrada de frecuencia

Haga clic en la visualización de frecuencia para comenzar la entrada directa. Se aplican las siguientes reglas:

- Escriba una frecuencia en MHz (p. ej., `14.200` o `14200`). Presione Enter o Tab para aplicarla.
- En bandas XVTR, se aceptan frecuencias de hasta 50000 MHz.
- En bandas entre 100-999 MHz (2m, 70cm), un número entero simple como `1446` se interpreta como `144.6`, `14696` como `146.96` y `144600` como `144.600`. Esta conveniencia no se aplica por encima de 1000 MHz (bandas de 23cm y microondas), donde un número entero simple representa la frecuencia en MHz directamente.
- Si ingresa explícitamente una frecuencia superior a 54 MHz (p. ej., `144.200`), el analizador la trata como una entrada válida en MHz y acepta frecuencias de hasta 50000 MHz, incluso si el segmento no está en una banda XVTR.

## Comportamiento del segmento bloqueado

Cuando un segmento está bloqueado:

- El botón de bloqueo muestra un ícono de candado. Haga clic para desbloquear.
- El ajuste con la rueda del ratón está bloqueado. Si intenta sintonizar un segmento bloqueado, aparece una superposición visual de LOCKED en la visualización de frecuencia y cualquier entrada directa de frecuencia en curso se cancela.
- La superposición de LOCKED se borra automáticamente cuando desbloquea el segmento.
- La entrada directa de frecuencia está impedida mientras está bloqueado — al hacer clic en la visualización de frecuencia no se ingresa al modo de edición, y cualquier entrada directa activa se cancela de inmediato.

## Soporte de temas e Inspector

El Panel VFO utiliza tokens de tema para su apariencia visual. En v26.6.1, se declaran los siguientes tokens de tema para la cobertura del modo Inspector:

- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

Estos tokens son utilizados por llamadas QPainter sin procesar que pintan el fondo del panel, el medidor de señal y otros elementos dibujados personalizados. Al usar el Inspector, al hacer clic en la bandera VFO, la insignida de indicativo o la superficie de la tira del medidor de señal, se muestran estos tokens en la lista de aciertos.

El botón ADSP y otros botones pulsadores en el panel utilizan un estilo consciente del tema a través de applyStyleSheet, con `{{color.background.1}}` para el fondo y `{{color.accent}}` para el estado presionado.

## Consejos

- En modo colapsado, la rueda del ratón en cualquier lugar de la tira sintoniza el segmento según el tamaño de paso actual.
- El ajuste con la rueda del ratón funciona en modo colapsado independientemente de si el segmento está bloqueado — si está bloqueado, la sintonización se bloquea y aparece la superposición de LOCKED.
- Los eventos de desplazamiento con momento (inercia) en macOS se ignoran para evitar una sintonización no deseada después de que finaliza un gesto en el trackpad.
- El panel se voltea al lado derecho del marcador automáticamente si mostrarlo a la izquierda lo recortaría en el borde de la ventana.
- Los algoritmos de reducción de ruido del lado del cliente (NR2, NR4, MNR, BNR, DFNR, RN2) se acceden desde el diálogo de Ajustes de AetherDSP (botón ADSP) o desde la Tira de Canal de Audio Aetherial (botón AetherVoice), ambos en la pestaña DSP.
- El squelch está desactivado en modos digital, RTTY y CW. El audio digital y RTTY alimenta decodificadores externos a través de canales DAX, y el squelch podría bloquear señales FSK débiles. El modo CW bloquea el squelch en un nivel fijo.
- El relleno del deslizador Pan se ancla desde el centro hacia afuera con colores conscientes del tema. Haga doble clic para reiniciar al centro.

## Relacionados

- [Sintonice el radio escribiendo una frecuencia en el panel VFO](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Cambie el modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Aplique un preajuste de ancho de filtro desde el panel VFO](apply-a-filter-width-preset-from-the-vfo-panel.md)
- [Establezca un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)
- [Ajuste la ganancia AF y el paneo desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Silencie el audio de un segmento desde el panel V
