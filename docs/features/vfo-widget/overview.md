# Resumen del Panel VFO

El Panel VFO es un panel de control flotante por segmento (slice), anclado a la bandera del marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes de segmento más utilizados — modo, preajustes de filtro, selección de antena, controles de audio, AGC, reducción de ruido, RIT/XIT y asignación de DAX — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- Al menos un segmento debe estar activo en el panadaptador.

## Cómo funciona

Haga clic en la bandera del marcador VFO en la pantalla del espectro para cualquier segmento. El panel aparece anclado a la izquierda del marcador y se voltea automáticamente hacia la derecha si se saliera por el borde de la ventana.

El panel está dividido en pestañas — **Mode**, **Audio**, **DSP**, **X/RIT** y **DAX** — más una fila de encabezado que siempre está visible. Los controles en la fila de encabezado se aplican independientemente de qué pestaña esté activa.

Cuando está colapsado, el panel se reduce a una tira compacta que solo muestra la frecuencia. El sintonizador de rueda de desplazamiento aún funciona en modo colapsado. Haga clic en cualquier lugar de la tira colapsada para expandirla de nuevo, o haga clic en la insignia TX para alternar la asignación del segmento de transmisión.

### Fila de encabezado

La fila de encabezado se encuentra sobre las pestañas y siempre está visible.

| Control | Qué hace |
|---|---|
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de este segmento. Los elementos del menú muestran las etiquetas proporcionadas por el radio junto con nombres abreviados entre paréntesis. |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de este segmento. Los puertos de antena solo de RX están excluidos. Los elementos del menú muestran las etiquetas proporcionadas por el radio junto con nombres abreviados entre paréntesis. |
| Visualización de frecuencia | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba un valor en MHz y presione Enter o Tab para aplicarlo. La rueda de desplazamiento sobre la visualización de frecuencia sintoniza según el tamaño de paso actual. |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer cíclicamente los botones de preajuste de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como la única fuente de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (v0.9.8). |
| Insignia TX | Se muestra en rojo cuando este segmento es el segmento de transmisión activo. En modo colapsado, haga clic en la insignia para alternar la asignación TX. |
| Insignia SPLIT | Se muestra en ámbar cuando TX está asignado a un segmento diferente al segmento receptor activo. |

### Pestaña Mode (Modo)

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
| Botón Mute | desactivado | — | — |
| Botón + deslizador Squelch | desactivado | 0–100 | — |
| Combo AGC | FAST | FAST, MED, SLOW, OFF | — |

La posición central del deslizador Pan (50) es el centro estéreo. Haga doble clic en el deslizador Pan para restablecerlo al centro. Los controles de audio reflejan el estado en vivo del radio y no son persistidos por AetherSDR.

El squelch está deshabilitado en modos digital, RTTY y CW. En modos digital y RTTY, el audio alimenta decodificadores externos a través de DAX, donde el squelch podría enmascarar señales FSK débiles. En modo CW, el radio bloquea el squelch activado a un nivel fijo y rechaza cambios. Al entrar en uno de estos modos mientras el squelch está activado, se desactiva automáticamente y se restaura al salir de ese modo.

### Pestaña DSP

La pestaña DSP contiene botones para algoritmos de reducción de ruido y filtrado suministrados directamente por el radio. Los módulos DSP del lado del cliente (NR2, NR4, MNR, BNR, DFNR y RN2) se pueden acceder desde el diálogo de Configuración de AetherDSP o desde la Tira de Canales de Audio Aetherial.

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botones NR / NB / ANF / APF / NRL / NRS / RNN / NRF / ANFL / ANFT | desactivado | La disponibilidad de los botones depende de la serie y versión del radio. APF solo es visible en modo CW. |
| Botón ADSP | — | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). El mismo punto de entrada que el menú Settings (v0.9.8). Estilo como un conmutador DSP del lado del radio pero no marcable. Haga clic para abrir y enfocar el diálogo de Configuración de AetherDSP no modal. |
| Botón AetherVoice | — | Abre la Tira de Canales de Audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

#### Deslizador de nivel DSP

Un deslizador de nivel compartido aparece debajo de la cuadrícula de botones. Apunta al botón DSP con nivel que se habilitó más recientemente: NR, NB, ANF, NRL, NRS, NRF o ANFL. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual. El valor numérico se muestra a la derecha.

La fila del deslizador permanece en el diseño en todo momento. Cuando no hay ningún DSP con nivel activo (o solo están activados RNN, ANFT o APF), la fila se atenúa y no responde a la interacción. Se vuelve completamente visible tan pronto como se activa un DSP con nivel.

En v0.9.8, el deslizador de nivel también se envía a la pila compartida cuando llega un cambio de estado de DSP con nivel desde el radio al inicio. Esto asegura que el deslizador aparezca para cualquier DSP que ya estuviera habilitado en el perfil guardado del radio.

### Pestaña X/RIT

| Control | Valor predeterminado | Notas |
|---|---|---|
| Botón RIT + etiqueta | desactivado | Habilita la sintonización incremental del receptor. La etiqueta muestra el desplazamiento actual. La rueda de desplazamiento ajusta en pasos de 10 Hz. |
| Botón XIT + etiqueta | desactivado | Habilita la sintonización incremental del transmisor. La etiqueta muestra el desplazamiento actual. La rueda de desplazamiento ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Combo de canal DAX | Off | Off, 1–8 | — |

### Controles de visualización

Estos controles afectan cómo se muestra el segmento en la pantalla del espectro. Se persisten individualmente por segmento (donde `{N}` es el número de segmento).

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Botón de grosor del marcador | 1 px | Off, 1 px, 3 px | `Slice{N}_MarkerWidth` |
| Botón de bordes del filtro | mostrado | mostrado / oculto | `Slice{N}_FilterEdgesHidden` |
| Alternar colapso | expandido | expandido / colapsado | `SliceFlagCollapsed_{N}` |

Haga clic en la insignia del segmento en la fila de encabezado para colapsar el panel. Haga clic en cualquier lugar de la tira colapsada para expandirlo.

## Selección de antena

Los botones de antena RX y TX abren menús que muestran las etiquetas proporcionadas por el radio (como "ANT 1" o "RX ANT B") junto con nombres abreviados entre paréntesis cuando son diferentes. Los menús muestran:

- **Antena RX**: Todos los puertos de antena disponibles para recepción. Los elementos del menú incluyen información sobre herramientas e indicaciones en la barra de estado que muestran el nombre completo de la antena.
- **Antena TX**: Solo los puertos de antena adecuados para transmisión (los puertos solo de RX están excluidos). Los elementos del menú incluyen información sobre herramientas e indicaciones en la barra de estado que muestran el nombre completo de la antena.

Ambos menús se completan desde la lista de antenas por segmento del radio cuando está disponible, recurriendo a la lista global de antenas. Las asignaciones de antena se aplican de inmediato.

## Entrada de frecuencia

Haga clic en la visualización de frecuencia para comenzar la entrada directa. Se aplican las siguientes reglas:

- Escriba una frecuencia en MHz (por ejemplo, `14.200` o `14200`). Presione Enter o Tab para aplicarla.
- En bandas XVTR, se aceptan frecuencias de hasta 50000 MHz.
- En bandas entre 100-999 MHz (2m, 70cm), un número entero simple como `1446` se interpreta como `144.6`, `14696` como `146.96`, y `144600` como `144.600`. Esta conveniencia no se aplica por encima de 1000 MHz (bandas de 23cm y microondas), donde un número entero simple representa la frecuencia en MHz directamente.

## Consejos

- En modo colapsado, la rueda de desplazamiento en cualquier lugar de la tira sintoniza el segmento según el tamaño de paso actual.
- Los eventos de desplazamiento por inercia (momentum) en macOS se ignoran para evitar sintonizaciones no deseadas después de que un gesto del trackpad finalice.
- El panel se voltea al lado derecho del marcador automáticamente si mostrarlo a la izquierda lo recortaría en el borde de la ventana.
- Los algoritmos de reducción de ruido del lado del cliente (NR2, NR4, MNR, BNR, DFNR, RN2) se acceden desde el diálogo de Configuración de AetherDSP (botón ADSP) o desde la Tira de Canales de Audio Aetherial (botón AetherVoice), ambos en la pestaña DSP.
- El squelch está deshabilitado en modos digital, RTTY y CW. El audio digital y RTTY alimenta decodificadores externos a través de canales DAX, y el squelch podría enmascarar señales FSK débiles. El modo CW bloquea el squelch activado a un nivel fijo.

## Relacionado

- [Sintonice el radio escribiendo una frecuencia en el panel VFO](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Cambie el modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Aplique un preajuste de ancho de filtro desde el panel VFO](apply-a-filter-width-preset-from-the-vfo-panel.md)
- [Establezca un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)
- [Ajuste la ganancia AF y el paneo desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Silencie el audio de un segmento desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Active el squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
- [Active la reducción de ruido desde el panel VFO](enable-noise-reduction-from-the-vfo-panel.md)
- [Active el desplazamiento RIT o XIT desde el panel VFO](enable-rit-or-xit-offset-from-the-vfo-panel.md)
- [Asigne un canal DAX desde el panel VFO](assign-a-dax-channel-from-the-vfo-panel.md)
- [Cambie el grosor de la línea del marcador VFO](change-the-vfo-marker-line-thickness.md)
- [Oculte o muestre las líneas de borde del filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Colapse el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
