# Descripción general del panel VFO

El panel VFO es un panel de control flotante por receptor, anclado a la bandera del marcador VFO en la visualización del espectro. Le brinda acceso rápido a los ajustes de receptor más utilizados (modo, preselecciones de filtro, selección de antena, controles de audio, AGC, reducción de ruido, RIT/XIT y asignación de DAX) sin tener que salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Al menos un receptor debe estar activo en el panadapter.

## Cómo funciona

Haga clic en la bandera del marcador VFO en la visualización del espectro para cualquier receptor. El panel aparece anclado a la izquierda del marcador y se voltea automáticamente hacia la derecha si colisionara con el borde de la ventana.

El panel está dividido en pestañas: **Mode**, **Audio**, **DSP**, **X/RIT** y **DAX**, además de una fila de encabezado que siempre está visible. Los controles en la fila de encabezado se aplican sin importar qué pestaña esté activa.

Cuando está colapsado, el panel se reduce a una tira compacta que solo muestra la frecuencia. El ajuste con la rueda del ratón aún funciona en modo colapsado. Haga clic en cualquier lugar de la tira colapsada para expandirla de nuevo, o haga clic en la insignia TX para alternar la asignación del receptor de transmisión.

### Fila de encabezado

La fila de encabezado se encuentra sobre las pestañas y siempre está visible.

| Control | Qué hace |
|---|---|
| Botón de antena RX | Abre el menú de selección de antena para la antena de recepción de este receptor. Los elementos del menú muestran las etiquetas proporcionadas por la radio junto con nombres abreviados entre paréntesis. |
| Botón de antena TX | Abre el menú de selección de antena para la antena de transmisión de este receptor. Los puertos de antena de solo recepción están excluidos. Los elementos del menú muestran las etiquetas proporcionadas por la radio junto con nombres abreviados entre paréntesis. |
| Visualización de frecuencia | Muestra la frecuencia actual del receptor. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba un valor en MHz y presione Enter o Tab para aplicarlo. La rueda del ratón sobre la visualización de frecuencia sintoniza según el tamaño de paso actual. Si el receptor está bloqueado, se muestra una superposición visual de BLOQUEADO y se bloquea el ajuste con la rueda del ratón. |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital (v0.9.8). |
| Insignia TX | Se muestra en rojo cuando este receptor es el receptor de transmisión activo. En modo colapsado, haga clic en la insignia para alternar la asignación TX. |
| Insignia SPLIT | Se muestra en ámbar cuando TX está asignado a un receptor diferente al receptor de recepción activo. |

### Pestaña Mode

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Modo combinado | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | — |
| Botones de preselección de filtro | — | — | `FilterPresets` |

Haga clic derecho en un botón de preselección de filtro para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro personalizados (bajo y alto) se pueden guardar por ranura de la misma manera.

Cuando se selecciona DIGU o DIGL en el modo combinado, aparece un contenedor de datos digitales en la pestaña. Este contenedor es más alto que el otro contenido de la pestaña. El panel VFO ahora informa solo el tamaño preferido de la pestaña actual, evitando que aparezca un espacio al volver a la pestaña Mode desde la pestaña DSP.

### Pestaña Audio

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Deslizador de ganancia AF | 100 | 0–100 | — |
| Deslizador de paneo | 50 | 0–100 | — |
| Botón de silencio | apagado | — | — |
| Botón + deslizador de silenciador | apagado | 0–100 | — |
| Modo AGC combinado | FAST | FAST, MED, SLOW, OFF | — |

La posición central (50) del deslizador de paneo es el centro estéreo. Haga doble clic en el deslizador de paneo para restablecerlo al centro. Los controles de audio reflejan el estado en vivo de la radio y no son persistidos por AetherSDR.

El silenciador está deshabilitado en modos digital, RTTY y CW. En modos digital y RTTY, el audio se alimenta a decodificadores externos a través de DAX, donde el silenciador podría bloquear señales FSK débiles. En modo CW, la radio fija el silenciador en un nivel fijo y rechaza los cambios. Al ingresar a uno de estos modos mientras el silenciador está habilitado, el silenciador se desactiva automáticamente y se restaura al salir de ese modo.

### Pestaña DSP

La pestaña DSP contiene botones para algoritmos de reducción de ruido y filtrado proporcionados directamente por la radio. Los módulos DSP del lado del cliente (NR2, NR4, MNR, BNR, DFNR y RN2) se pueden acceder desde el cuadro de diálogo de configuración de AetherDSP o desde la tira de canal de audio Aetherial.

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF | apagado | La disponibilidad de los botones depende de la serie y la versión de la radio. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo de configuración de AetherDSP para ese algoritmo. |
| Botón ADSP | — | Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). El mismo punto de entrada que el menú de configuración (v0.9.8). Tiene el estilo de un conmutador DSP del lado de la radio pero no es seleccionable. Al hacer clic, abre y enfoca el cuadro de diálogo de configuración de AetherDSP no modal. |
| Botón AetherVoice | — | Abre la tira de canal de audio Aetherial: el conjunto unificado de DSP de TX/RX (v0.9.8). Abarca 2 columnas en la cuadrícula de DSP de 4 columnas. |

#### Deslizador de nivel DSP

Un deslizador de nivel compartido aparece debajo de la cuadrícula de botones. Se dirige al botón DSP con nivel que se habilitó más recientemente: NR, NB, ANF, NRL, NRS, NRF o ANFL. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual. El valor numérico se muestra a la derecha.

La fila del deslizador permanece en el diseño en todo momento. Cuando ningún DSP con nivel está activo (o solo RNN, ANFT o APF están encendidos), la fila se atenúa y no responde a la interacción. Se vuelve completamente visible nuevamente tan pronto como se enciende un DSP con nivel.

En v0.9.8, el deslizador de nivel también se envía a la pila compartida cuando llega un cambio de estado de DSP con nivel desde la radio al inicio. Esto asegura que el deslizador aparezca para cualquier DSP que ya estuviera habilitado en el perfil guardado de la radio.

### Pestaña X/RIT

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botón + etiqueta RIT | apagado | Habilita la sintonización incremental del receptor. La etiqueta muestra el desplazamiento actual. La rueda del ratón ajusta en pasos de 10 Hz. |
| Botón + etiqueta XIT | apagado | Habilita la sintonización incremental del transmisor. La etiqueta muestra el desplazamiento actual. La rueda del ratón ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Canal DAX combinado | Off | Off, 1–8 | — |

### Controles de visualización

Estos controles afectan cómo aparece el receptor en la visualización del espectro. Se persisten individualmente por receptor (donde `{N}` es el número de receptor).

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Botón de grosor del marcador | 1 px | Off, 1 px, 3 px | `Slice{N}_MarkerWidth` |
| Botón de bordes de filtro | mostrado | mostrado / oculto | `Slice{N}_FilterEdgesHidden` |
| Alternancia de colapso | expandido | expandido / colapsado | `SliceFlagCollapsed_{N}` |

Al hacer clic en la insignia del receptor en la fila de encabezado, se colapsa el panel. Al hacer clic en cualquier lugar de la tira colapsada, se expande.

## Selección de antena

Los botones de antena RX y TX abren menús que muestran las etiquetas proporcionadas por la radio (como "ANT 1" o "RX ANT B") junto con nombres abreviados entre paréntesis cuando difieren. Los menús muestran:

- **Antena RX**: Todos los puertos de antena disponibles para recepción. Los elementos del menú incluyen información sobre herramientas y sugerencias en la barra de estado que muestran el nombre completo de la antena.
- **Antena TX**: Solo los puertos de antena adecuados para transmisión (los puertos de solo recepción están excluidos). Los elementos del menú incluyen información sobre herramientas y sugerencias en la barra de estado que muestran el nombre completo de la antena.

Ambos menús se completan desde la lista de antenas por receptor de la radio cuando está disponible, recurriendo a la lista global de antenas. Las asignaciones de antena se aplican de inmediato.

## Entrada de frecuencia

Haga clic en la visualización de frecuencia para comenzar la entrada directa. Se aplican las siguientes reglas:

- Escriba una frecuencia en MHz (por ejemplo, `14.200` o `14200`). Presione Enter o Tab para aplicarla.
- En bandas XVTR, se aceptan frecuencias de hasta 50000 MHz.
- En bandas entre 100-999 MHz (2m, 70cm), un número entero simple como `1446` se interpreta como `144.6`, `14696` como `146.96` y `144600` como `144.600`. Esta conveniencia no se aplica por encima de 1000 MHz (bandas de 23cm y microondas), donde un número entero simple representa la frecuencia directamente en MHz.
- Si ingresa explícitamente una frecuencia superior a 54 MHz (por ejemplo, `144.200`), el analizador la trata como una entrada válida en MHz y acepta frecuencias de hasta 50000 MHz, incluso si el receptor no está en una banda XVTR.

## Comportamiento del receptor bloqueado

Cuando un receptor está bloqueado:

- El botón de bloqueo muestra un icono de candado. Haga clic para desbloquear.
- El ajuste con la rueda del ratón está bloqueado. Si intenta sintonizar un receptor bloqueado, aparece una superposición visual de BLOQUEADO en la visualización de frecuencia y se cancela cualquier entrada directa de frecuencia en curso.
- La superposición de BLOQUEADO se elimina automáticamente cuando desbloquea el receptor.
- La entrada directa de frecuencia se evita mientras está bloqueado: al hacer clic en la visualización de frecuencia no se ingresa al modo de edición, y cualquier entrada directa activa se cancela de inmediato.

## Consejos

- En modo colapsado, la rueda del ratón en cualquier lugar sobre la tira sintoniza el receptor según el tamaño de paso actual.
- El ajuste con la rueda del ratón funciona en modo colapsado independientemente de si el receptor está bloqueado; si está bloqueado, la sintonización se bloquea y aparece la superposición de BLOQUEADO.
- Los eventos de desplazamiento por inercia en macOS se ignoran para evitar una sintonización no deseada después de que finaliza un gesto en el trackpad.
- El panel se voltea automáticamente al lado derecho del marcador si mostrarlo a la izquierda colisionara con el borde de la ventana.
- Los algoritmos de reducción de ruido del lado del cliente (NR2, NR4, MNR, BNR, DFNR, RN2) se acceden desde el cuadro de diálogo de configuración de AetherDSP (botón ADSP) o desde la tira de canal de audio Aetherial (botón AetherVoice), ambos en la pestaña DSP.
- El silenciador está deshabilitado en modos digital, RTTY y CW. El audio digital y RTTY se alimenta a decodificadores externos a través de canales DAX, y el silenciador podría bloquear señales FSK débiles. El modo CW fija el silenciador en un nivel fijo.

## Relacionados

- [Tune the radio by typing a frequency into the VFO panel](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Change mode from the VFO panel](change-mode-from-the-vfo-panel.md)
- [Apply a filter width preset from the VFO panel](apply-a-filter-width-preset-from-the-vfo-panel.md)
- [Set a custom filter edge from the VFO panel](set-a-custom-filter-edge-from-the-vfo-panel.md)
- [Adjust AF gain and pan from the VFO panel](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Mute audio for a slice from the VFO panel](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Enable squelch from the VFO panel](enable-squelch-from-the-vfo-panel.md)
- [Enable noise reduction from the VFO panel](enable-noise-reduction-from-the-vfo-panel.md)
- [Enable RIT or XIT offset from the VFO panel](enable-rit-or-xit-offset-from-the-vfo-panel.md)
- [Assign a DAX channel from the VFO panel](assign-a-dax-channel-from-the-vfo-panel.md)
- [Change the VFO marker line thickness](change-the-vfo-marker-line-thickness.md)
- [Hide or show filter edge lines on the spectrum](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Collapse the VFO panel to frequency-only view](collapse-the-vfo-panel-to-frequency-only-view.md)
- Lock a slice to prevent accidental tuning
