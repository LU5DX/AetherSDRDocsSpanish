# Resumen del Panel VFO

El Panel VFO es un panel de control flotante por segmento, anclado a la bandera del marcador VFO en la pantalla del espectro. Le brinda acceso rápido a las configuraciones de segmento más utilizadas (modo, preajustes de filtro, selección de antena, controles de audio, AGC, reducción de ruido, RIT/XIT y asignación de DAX) sin tener que abandonar la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- Al menos un segmento debe estar activo en el panadaptador.

## Cómo funciona

Haga clic en la bandera del marcador VFO en la pantalla del espectro de cualquier segmento. El panel aparece anclado a la izquierda del marcador y se gira automáticamente hacia la derecha si quedara recortado por el borde de la ventana.

El panel está dividido en pestañas: **Mode**, **Audio**, **DSP**, **X/RIT** y **DAX**, además de una fila de encabezado que siempre está visible. Los controles en la fila de encabezado se aplican independientemente de la pestaña activa.

Cuando está contraído, el panel se reduce a una tira compacta que solo muestra la frecuencia. La sintonización con la rueda del ratón sigue funcionando en modo contraído. Haga clic en cualquier lugar de la tira contraída para expandirla nuevamente, o haga clic en la insignia TX para alternar la asignación del segmento de transmisión.

### Fila de encabezado

La fila de encabezado se encuentra encima de las pestañas y siempre está visible.

| Control | Función |
|---|---|
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de este segmento. |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de este segmento. |
| Pantalla de frecuencia | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba un valor en MHz y presione Enter o Tab para aplicarlo. La rueda del ratón sobre la pantalla de frecuencia sintoniza según el tamaño de paso actual. |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modo SSB/digital (v0.9.8). |
| Insignia TX | Se muestra en rojo cuando este segmento es el segmento de transmisión activo. En modo contraído, haga clic en la insignia para alternar la asignación TX. |
| Insignia SPLIT | Se muestra en ámbar cuando TX está asignado a un segmento diferente al segmento receptor activo. |

### Pestaña Mode

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Combo Mode | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | — |
| Botones de preajuste de filtro | — | — | `FilterPresets` |

Haga clic derecho en un botón de preajuste de filtro para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro personalizados (bajo y alto) se pueden guardar por ranura de la misma manera.

### Pestaña Audio

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Deslizador AF Gain | 100 | 0–100 | — |
| Deslizador Pan | 50 | 0–100 | — |
| Botón Mute | apagado | — | — |
| Botón + deslizador Squelch | apagado | 0–100 | — |
| Combo AGC | FAST | FAST, MED, SLOW, OFF | — |

La posición central del deslizador Pan (50) es el centro estéreo. Haga doble clic en el deslizador Pan para restablecerlo al centro. Los controles de audio reflejan el estado en vivo del radio y no son persistidos por AetherSDR.

### Pestaña DSP

La pestaña DSP contiene botones para algoritmos de reducción de ruido y filtrado proporcionados directamente por el radio. Los módulos DSP del lado del cliente (NR2, NR4, MNR, BNR, DFNR y RN2) se pueden acceder desde el diálogo de Configuración de AetherDSP o desde la Tira de Canales de Audio de Aetherial.

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botones NR / NB / ANF / APF / NRL / NRS / RNN / NRF / ANFL / ANFT | apagado | La disponibilidad de los botones depende de la serie del radio y la compilación. APF solo es visible en modo CW. |
| Botón ADSP | — | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). El mismo punto de entrada que el menú Settings (v0.9.8). Tiene el estilo de un conmutador DSP del lado del radio pero no es seleccionable. Al hacer clic, abre y enfoca el diálogo de Configuración de AetherDSP no modal. |
| Botón AetherVoice | — | Abre la Tira de Canales de Audio de Aetherial, el conjunto unificado de DSP de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

#### Deslizador de nivel DSP

Un deslizador de nivel compartido aparece debajo de la cuadrícula de botones. Se dirige al botón DSP con nivel que se haya habilitado más recientemente: NR, NB, ANF, NRL, NRS, NRF o ANFL. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual. El valor numérico se muestra a la derecha.

La fila del deslizador permanece en el diseño en todo momento. Cuando ningún DSP con nivel está activo (o solo RNN, ANFT o APF están encendidos), la fila se atenúa y no responde a la interacción. Se vuelve completamente visible tan pronto como se enciende un DSP con nivel.

En v0.9.8, el deslizador de nivel también se envía a la pila compartida cuando llega un cambio de estado de DSP con nivel desde el radio al iniciarse. Esto asegura que el deslizador aparezca para cualquier DSP que ya estuviera habilitado en el perfil guardado del radio.

### Pestaña X/RIT

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botón RIT + etiqueta | apagado | Activa la sintonización incremental del receptor. La etiqueta muestra el desfase actual. La rueda del ratón ajusta en pasos de 10 Hz. |
| Botón XIT + etiqueta | apagado | Activa la sintonización incremental del transmisor. La etiqueta muestra el desfase actual. La rueda del ratón ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Combo de canal DAX | Off | Off, 1–8 | — |

### Controles de visualización

Estos controles afectan la forma en que el segmento aparece en la pantalla del espectro. Se persisten individualmente por segmento (donde `{N}` es el número de segmento).

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Botón de grosor del marcador | 1 px | Off, 1 px, 3 px | `Slice{N}_MarkerWidth` |
| Botón de bordes de filtro | mostrados | mostrados / ocultos | `Slice{N}_FilterEdgesHidden` |
| Alternar contracción | expandido | expandido / contraído | `SliceFlagCollapsed_{N}` |

Al hacer clic en la insignia del segmento en la fila de encabezado, se contrae el panel. Al hacer clic en cualquier lugar de la tira contraída, se expande.

## Consejos

- En modo contraído, la rueda del ratón en cualquier lugar de la tira sintoniza el segmento según el tamaño de paso actual.
- Los eventos de desplazamiento con inercia (momentum) en macOS se ignoran para evitar sintonizaciones no deseadas después de que finaliza un gesto en el panel táctil.
- El panel se gira automáticamente al lado derecho del marcador si mostrarlo a la izquierda lo recortara en el borde de la ventana.
- Los algoritmos de reducción de ruido del lado del cliente (NR2, NR4, MNR, BNR, DFNR, RN2) se acceden desde el diálogo de Configuración de AetherDSP (botón ADSP) o desde la Tira de Canales de Audio de Aetherial (botón AetherVoice), ambos en la pestaña DSP.

## Relacionados

- [Sintonice el radio escribiendo una frecuencia en el panel VFO](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Cambie el modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Aplique un preajuste de ancho de filtro desde el panel VFO](apply-a-filter-width-preset-from-the-vfo-panel.md)
- [Establezca un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)
- [Ajuste la ganancia AF y el paneo desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Silencie el audio de un segmento desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Active el squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
- [Active la reducción de ruido desde el panel VFO](enable-noise-reduction-from-the-vfo-panel.md)
- [Active el desfase RIT o XIT desde el panel VFO](enable-rit-or-xit-offset-from-the-vfo-panel.md)
- [Asigne un canal DAX desde el panel VFO](assign-a-dax-channel-from-the-vfo-panel.md)
- [Cambie el grosor de la línea del marcador VFO](change-the-vfo-marker-line-thickness.md)
- [Oculte o muestre las líneas de borde del filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Contraiga el panel VFO a la vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
