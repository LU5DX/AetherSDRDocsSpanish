# Descripción general del panel VFO

El panel VFO es un panel de control flotante, por slice (canal de recepción), anclado a la bandera del marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes de slice más utilizados — modo, preajustes de filtro, selección de antena, controles de audio, AGC, reducción de ruido, RIT/XIT y asignación DAX — sin abandonar la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Al menos un slice debe estar activo en el panadapter.

## Cómo funciona

Haga clic en la bandera del marcador VFO en la pantalla del espectro para cualquier slice. El panel aparece anclado a la izquierda del marcador y se desplaza automáticamente hacia la derecha si quedaría cortado por el borde de la ventana.

El panel está dividido en pestañas — **Mode**, **Audio**, **DSP**, **X/RIT** y **DAX** — más una fila de encabezado que siempre es visible. Los controles de la fila de encabezado se aplican independientemente de qué pestaña esté activa.

Cuando está contraído, el panel se reduce a una barra compacta que muestra solo la frecuencia. El ajuste con la rueda del ratón sigue funcionando en el modo contraído. Haga clic en cualquier parte de la barra contraída para expandirla de nuevo, o haga clic en el indicador TX para alternar la asignación del slice de transmisión.

### Fila de encabezado

La fila de encabezado se encuentra sobre las pestañas y siempre es visible.

| Control | Función |
|---|---|
| Botón de antena RX | Abre el menú de selección de antena para la antena de recepción de este slice. |
| Botón de antena TX | Abre el menú de selección de antena para la antena de transmisión de este slice. |
| Pantalla de frecuencia | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba un valor en MHz y presione Enter o Tab para aplicarlo. Gire la rueda del ratón sobre la pantalla de frecuencia para sintonizar según el paso actual. |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. |
| Indicador TX | Se muestra en rojo cuando este slice es el slice de transmisión activo. En modo contraído, haga clic en el indicador para alternar la asignación TX. |
| Indicador SPLIT | Se muestra en ámbar cuando la TX está asignada a un slice diferente al slice de recepción activo. |

### Pestaña Mode

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Selector de modo | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | — |
| Botones de preajuste de filtro | — | — | `FilterPresets` |

Haga clic derecho en un botón de preajuste de filtro para guardar el ancho de filtro actual en ese slot. Los bordes de filtro alto y bajo personalizados se pueden guardar por slot de la misma manera.

### Pestaña Audio

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Control deslizante de ganancia AF | 100 | 0–100 | — |
| Control deslizante Pan | 50 | 0–100 | — |
| Botón Mute | desactivado | — | — |
| Botón Squelch + control deslizante | desactivado | 0–100 | — |
| Selector AGC | FAST | FAST, MED, SLOW, OFF | — |

La posición central del control deslizante Pan (50) corresponde al centro estéreo. Haga doble clic en el control deslizante Pan para restablecerlo al centro. Los controles de audio reflejan el estado en tiempo real de la radio y no son persistidos por AetherSDR.

### Pestaña DSP

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF | desactivado | La disponibilidad de los botones depende de la serie de la radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo AetherDSP Settings para ese algoritmo. |

### Pestaña X/RIT

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botón RIT + etiqueta | desactivado | Activa la sintonía incremental del receptor. La etiqueta muestra el desplazamiento actual. La rueda del ratón ajusta en pasos de 10 Hz. |
| Botón XIT + etiqueta | desactivado | Activa la sintonía incremental del transmisor. La etiqueta muestra el desplazamiento actual. La rueda del ratón ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Selector de canal DAX | Off | Off, 1–8 | — |

### Controles de visualización

Estos controles afectan cómo aparece el slice en la pantalla del espectro. Se persisten individualmente por slice (donde `{N}` es el número de slice).

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Botón de grosor del marcador | 1 px | Off, 1 px, 3 px | `Slice{N}_MarkerWidth` |
| Botón de bordes de filtro | visible | visible / oculto | `Slice{N}_FilterEdgesHidden` |
| Botón de contraer | expandido | expandido / contraído | `SliceFlagCollapsed_{N}` |

Hacer clic en el indicador de slice en la fila de encabezado contrae el panel. Hacer clic en cualquier parte de la barra contraída lo expande.

## Consejos

- En modo contraído, gire la rueda del ratón en cualquier punto de la barra para sintonizar el slice según el paso actual.
- Los eventos de desplazamiento por inercia (inercial) en macOS se ignoran para evitar una sintonización no intencionada después de que finaliza un gesto del trackpad.
- El panel se desplaza automáticamente al lado derecho del marcador si mostrarlo a la izquierda lo cortaría en el borde de la ventana.

## Relacionados

- [Sintonice la radio escribiendo una frecuencia en el panel VFO](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Cambie el modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Aplique un preajuste de ancho de filtro desde el panel VFO](apply-a-filter-width-preset-from-the-vfo-panel.md)
- [Establezca un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)
- [Ajuste la ganancia AF y el pan desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Silencie el audio de un slice desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Active el squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
- [Active la reducción de ruido desde el panel VFO](enable-noise-reduction-from-the-vfo-panel.md)
- [Active el desplazamiento RIT o XIT desde el panel VFO](enable-rit-or-xit-offset-from-the-vfo-panel.md)
- [Asigne un canal DAX desde el panel VFO](assign-a-dax-channel-from-the-vfo-panel.md)
- [Cambie el grosor de la línea del marcador VFO](change-the-vfo-marker-line-thickness.md)
- [Oculte o muestre las líneas de borde del filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Contraiga el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
