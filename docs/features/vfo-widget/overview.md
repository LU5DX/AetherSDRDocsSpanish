# Descripción general del panel VFO

El panel VFO es un panel de control flotante por segmento, anclado a la bandera del marcador VFO en la pantalla del espectro. Le brinda acceso rápido a las configuraciones de segmento más utilizadas (modo, preconfiguraciones de filtro, selección de antena, controles de audio, AGC, reducción de ruido, RIT/XIT y asignación de DAX) sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Al menos un segmento debe estar activo en el panadapter.

## Cómo funciona

Haga clic en la bandera del marcador VFO en la pantalla del espectro para cualquier segmento. El panel aparece anclado a la izquierda del marcador y se voltea automáticamente hacia la derecha si quedara recortado por el borde de la ventana.

El panel está dividido en pestañas — **Mode**, **Audio**, **DSP**, **X/RIT** y **DAX** — más una fila de encabezado que siempre está visible. Los controles en la fila de encabezado se aplican independientemente de qué pestaña esté activa.

Cuando está colapsado, el panel se reduce a una tira compacta que solo muestra la frecuencia. El ajuste con la rueda del ratón sigue funcionando en modo colapsado. Haga clic en cualquier lugar de la tira colapsada para expandirla de nuevo, o haga clic en la insignia TX para alternar la asignación del segmento de transmisión.

### Fila de encabezado

La fila de encabezado se encuentra sobre las pestañas y siempre está visible.

| Control | Qué hace |
|---|---|
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de este segmento. |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de este segmento. |
| Visualización de frecuencia | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba un valor en MHz y presione Enter o Tab para aplicarlo. La rueda del ratón sobre la visualización de frecuencia sintoniza según el tamaño de paso actual. |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer cíclicamente los botones de preconfiguración de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (v0.9.8). |
| Insignia TX | Se muestra en rojo cuando este segmento es el segmento de transmisión activo. En modo colapsado, haga clic en la insignia para alternar la asignación TX. |
| Insignia SPLIT | Se muestra en ámbar cuando TX está asignado a un segmento diferente al segmento receptor activo. |

### Pestaña Mode

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Combo Mode | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | — |
| Botones de preconfiguración de filtro | — | — | `FilterPresets` |

Haga clic derecho en un botón de preconfiguración de filtro para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro personalizados inferior y superior se pueden guardar por ranura de la misma manera.

### Pestaña Audio

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Deslizador AF Gain | 100 | 0–100 | — |
| Deslizador Pan | 50 | 0–100 | — |
| Botón Mute | off | — | — |
| Botón + deslizador Squelch | off | 0–100 | — |
| Combo AGC | FAST | FAST, MED, SLOW, OFF | — |

La posición central del deslizador Pan (50) es el centro estéreo. Haga doble clic en el deslizador Pan para restablecerlo al centro. Los controles de audio reflejan el estado en vivo de la radio y no son persistidos por AetherSDR.

El squelch está deshabilitado en modos digital, RTTY y CW. En modos digital y RTTY, el audio alimenta decodificadores externos a través de DAX, donde el squelch podría bloquear señales FSK débiles. En modo CW, la radio fija el squelch en un nivel fijo y rechaza los cambios. Al ingresar a uno de estos modos mientras el squelch está habilitado, el squelch se desactiva automáticamente y se restaura al salir de ese modo.

### Pestaña DSP

La pestaña DSP contiene botones para algoritmos de reducción de ruido y filtrado suministrados directamente por la radio. Los módulos DSP del lado del cliente (NR2, NR4, MNR, BNR, DFNR y RN2) se pueden acceder desde el diálogo AetherDSP Settings o desde la tira de canal de audio Aetherial Audio Channel Strip.

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botones NR / NB / ANF / APF / NRL / NRS / RNN / NRF / ANFL / ANFT | off | La disponibilidad de los botones depende de la serie y la versión de la radio. APF solo es visible en modo CW. |
| Botón ADSP | — | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). El mismo punto de entrada que el menú Settings (v0.9.8). Con estilo de alternancia DSP del lado de la radio pero no marcable. Al hacer clic, levanta y enfoca el diálogo AetherDSP Settings no modal. |
| Botón AetherVoice | — | Abre la tira de canal de audio Aetherial Audio Channel Strip, el conjunto unificado de DSP TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

#### Deslizador de nivel DSP

Un deslizador de nivel compartido aparece debajo de la cuadrícula de botones. Apunta al botón DSP con nivel que se haya habilitado más recientemente: NR, NB, ANF, NRL, NRS, NRF o ANFL. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual. El valor numérico se muestra a la derecha.

La fila del deslizador permanece en el diseño en todo momento. Cuando no hay ningún DSP con nivel activo (o solo RNN, ANFT o APF están encendidos), la fila se atenúa y no responde a la interacción. Se vuelve completamente visible tan pronto como se enciende un DSP con nivel.

En v0.9.8, el deslizador de nivel también se envía a la pila compartida cuando llega un cambio de estado de DSP con nivel desde la radio al inicio. Esto asegura que el deslizador aparezca para cualquier DSP que ya estuviera habilitado en el perfil guardado de la radio.

### Pestaña X/RIT

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botón + etiqueta RIT | off | Habilita la sintonización incremental del receptor. La etiqueta muestra el desplazamiento actual. La rueda del ratón ajusta en pasos de 10 Hz. |
| Botón + etiqueta XIT | off | Habilita la sintonización incremental del transmisor. La etiqueta muestra el desplazamiento actual. La rueda del ratón ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Combo de canal DAX | Off | Off, 1–8 | — |

### Controles de visualización

Estos controles afectan cómo se muestra el segmento en la pantalla del espectro. Se persisten individualmente por segmento (donde `{N}` es el número de segmento).

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Botón de grosor del marcador | 1 px | Off, 1 px, 3 px | `Slice{N}_MarkerWidth` |
| Botón de bordes de filtro | shown | shown / hidden | `Slice{N}_FilterEdgesHidden` |
| Alternancia de colapso | expanded | expanded / collapsed | `SliceFlagCollapsed_{N}` |

Al hacer clic en la insignia del segmento en la fila de encabezado, el panel se colapsa. Al hacer clic en cualquier lugar de la tira colapsada, se expande.

## Consejos

- En modo colapsado, la rueda del ratón en cualquier lugar de la tira sintoniza el segmento según el tamaño de paso actual.
- Los eventos de desplazamiento con momento (inercial) en macOS se ignoran para evitar una sintonización no deseada después de que termine un gesto con el trackpad.
- El panel se voltea automáticamente al lado derecho del marcador si mostrarlo a la izquierda quedara recortado en el borde de la ventana.
- Los algoritmos de reducción de ruido del lado del cliente (NR2, NR4, MNR, BNR, DFNR, RN2) se acceden desde el diálogo AetherDSP Settings (botón ADSP) o desde la tira de canal de audio Aetherial Audio Channel Strip (botón AetherVoice), ambos en la pestaña DSP.
- El squelch está deshabilitado en modos digital, RTTY y CW. El audio digital y RTTY alimenta decodificadores externos a través de canales DAX, y el squelch podría bloquear señales FSK débiles. El modo CW fija el squelch en un nivel fijo.

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
