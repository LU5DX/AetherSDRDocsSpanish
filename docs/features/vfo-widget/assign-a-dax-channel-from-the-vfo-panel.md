# Asignar un canal DAX desde el panel VFO

DAX (Digital Audio Exchange) enruta el audio recibido de un slice a un canal de audio con nombre en su computadora. Utilice este procedimiento para asignar o cambiar el canal DAX de cualquier slice directamente desde su panel VFO.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El puente de audio DAX debe estar en ejecución. Si no lo está, actívelo mediante `Settings > Autostart DAX with AetherSDR` y reinicie AetherSDR, o inícielo manualmente.
- El panel VFO del slice objetivo debe estar abierto y expandido. Si está colapsado a la tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en la bandera del marcador VFO en la visualización del espectro para el slice que desea configurar. Se abrirá el panel VFO, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **DAX** dentro del panel VFO.
3. Haga clic en el **combo de canales DAX** y seleccione un canal de la lista desplegable.
4. Para deshabilitar el enrutamiento DAX para este slice, seleccione **Off**.

## Qué hace cada control

| Control                      | Valor predeterminado                                                                                                                 | Valores válidos                                                                                                          |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Combo de canales DAX         | Off                                                                                                                                  | Off, 1–8                                                                                                                 |
| Botón ADSP (pestaña DSP)     | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Estilizado como un conmutador DSP del lado de la radio pero no marcable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Abre la tira de canales de audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8).                                     | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |                                                              |

El combo de canales DAX asigna un canal de audio DAX al slice actual. Seleccionar un canal numerado enruta el audio recibido del slice a ese canal DAX. Seleccionar **Off** elimina la asignación. Esta configuración refleja el estado en vivo de la radio y no se conserva localmente por AetherSDR.

## Comportamiento del squelch por modo

El botón y el deslizador del squelch se deshabilitan automáticamente en modos donde el squelch no es significativo o no es compatible. A partir de v26.5.1:

- **El squelch está deshabilitado** en los modos **Digital**, **RTTY** y **CW**.
  - **Digital / RTTY**: El audio se envía a decodificadores externos a través de DAX; el squelch no es significativo y puede cerrar señales FSK débiles (incidencia #2504).
  - **CW**: La radio bloquea el squelch activado a un nivel fijo y rechaza los cambios.
- Si el squelch estaba habilitado al cambiar a uno de estos modos, la radio lo apaga automáticamente. El estado guardado del squelch se conserva y se restaurará si vuelve a cambiar a un modo compatible.

## Controles de la pestaña DSP

La pestaña DSP en el panel VFO contiene botones de reducción de ruido proporcionados por la radio y dos botones de lanzamiento del lado del cliente.

### Botones DSP del lado de la radio

Los siguientes botones DSP del lado de la radio aparecen en la cuadrícula de la pestaña DSP:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Supresor de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de pico de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

### Botones de lanzamiento del lado del cliente

Dos botones de lanzamiento del lado del cliente aparecen al final de la cuadrícula DSP:

| Botón | Comportamiento |
|---|---|
| **ADSP** | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Estilizado como un conmutador DSP del lado de la radio pero no marcable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| **AetherVoice** | Activa/desactiva la tira de canales de audio Aetherial — el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

### Conmutadores de reducción de ruido del lado del cliente

Los siguientes botones de reducción de ruido del lado del cliente aparecen en la pestaña DSP cuando están habilitados por la serie de radio y la compilación:

| Botón | Algoritmo |
|---|---|
| NR2 | Algoritmo de reducción de ruido del lado del cliente 2 |
| NR4 | Algoritmo de reducción de ruido del lado del cliente 4 |
| RN2 | Algoritmo de reducción de ruido del lado del cliente RN2 |
| MNR | Algoritmo de reducción de ruido del lado del cliente MNR |
| DFNR | Algoritmo de reducción de ruido del lado del cliente DFNR |
| BNR | Algoritmo de reducción de ruido del lado del cliente BNR |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |

Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo.

### Deslizador de nivel DSP

Una fila compartida de deslizador de nivel aparece debajo de la cuadrícula de botones. El deslizador ajusta la intensidad del botón DSP con nivel que se encendió más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

El rango del deslizador es 0–100. Cuando ningún DSP con nivel está activo, o cuando solo RNN, ANFT o APF está encendido, la fila del deslizador está atenuada y no responde a la entrada. La fila permanece en su lugar en todo momento; no desplaza la cuadrícula de botones cuando cambia su objetivo.

Algoritmos que admiten el deslizador de nivel: NR, NB, ANF, NRL, NRS, NRF, ANFL.

A partir de v0.9.8, cuando un algoritmo DSP con nivel está habilitado desde el perfil guardado de la radio al inicio, el deslizador de nivel se completa automáticamente sin necesidad de un conmutación manual.

### Etiqueta de ancho de filtro

La etiqueta de ancho de filtro muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. A partir de v0.9.8, esta etiqueta utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modo SSB/digital.

### Menús de antena RX y TX

El **botón de antena RX** abre un menú para seleccionar la antena de recepción para este slice. El **botón de antena TX** abre un menú para seleccionar la antena de transmisión. A partir de v26.5.2, estos menús utilizan la lista de antenas proporcionada por la radio para el slice cuando está disponible, recurriendo a la lista global de antenas. Las opciones de antena TX excluyen automáticamente los puertos de antena solo RX. Cada elemento del menú muestra su nombre de antena sin procesar como información sobre herramientas.

### Controles del marcador

El **botón de grosor del marcador** recorre la línea del marcador VFO entre Off, 1 px y 3 px. La configuración se conserva por slice como `Slice{N}_MarkerWidth`.

El **botón de bordes del filtro** activa o desactiva las líneas de borde del filtro en la banda de paso del espectro. La configuración se conserva por slice como `Slice{N}_FilterEdgesHidden`.

### Conmutador de colapso

El **conmutador de colapso** colapsa el panel VFO a una tira compacta de solo frecuencia. La configuración se conserva por slice como `SliceFlagCollapsed_{N}`.

### Insignia del slice

La insignia del slice muestra la letra del slice. A partir de v26.5.2, la insignia admite formato de texto enriquecido, permitiendo caracteres especiales (incidencia #2606).

### Entrada de frecuencia

Haga clic en la pantalla de frecuencia para comenzar la entrada directa de frecuencia. Escriba la frecuencia en MHz y presione Enter o Tab. A partir de v26.5.2, en bandas XVTR el rango de frecuencia se extiende a 50000.0 MHz. Para bandas de 2m/70cm (rango 100-999 MHz), un número entero simple como 1446 se interpreta automáticamente como 144.6 MHz insertando un decimal después del tercer dígito. Para bandas de 23cm y microondas, un número entero simple representa MHz directamente.

## Consejos

- Cada canal DAX solo se puede asignar a un slice a la vez. Si asigna un canal que ya está en uso por otro slice, la radio moverá la asignación.
- Si el panel VFO quedaría recortado por el borde de la ventana, se voltea automáticamente al lado derecho del marcador.
- Para acceder a NR2, RN2, NR4, MNR, BNR o DFNR, haga clic derecho en la visualización del espectro para abrir el menú superpuesto, o abra el applet AetherDSP.

## Solución de problemas

- **El combo de canales DAX no tiene efecto / el audio no aparece en el anfitrión** — Confirme que el puente de audio DAX esté en ejecución. Verifique `Settings > Autostart DAX with AetherSDR`. En sistemas macOS y PipeWire, el puente debe estar activo para que los canales DAX aparezcan como dispositivos de audio.
- **La pestaña DAX no es visible** — El panel VFO puede estar colapsado. Haga clic en la tira colapsada para expandirla, luego seleccione la pestaña DAX.
- **El deslizador de nivel DSP está atenuado** — Ningún algoritmo DSP con nivel está activo actualmente, o solo RNN, ANFT o APF está habilitado. Active NR, NB, ANF, NRL, NRS, NRF o ANFL para activar el deslizador.
- **El deslizador de nivel DSP falta al inicio** — Si un algoritmo DSP con nivel estaba habilitado en el perfil guardado de la radio, el deslizador ahora se completa automáticamente. Si aún parece faltar, desactive y vuelva a activar el algoritmo.
- **El botón de squelch está deshabilitado** — Está en modo Digital, RTTY o CW. El squelch no está disponible en estos modos (digital y RTTY enrutan el audio a través de DAX; CW tiene squelch fijo bloqueado por la radio). Cambie a un modo compatible como USB o AM para habilitar los controles de squelch.

## Relacionados

- [Resumen del panel VFO](overview.md)
- [Ajustar la ganancia AF y el paneo desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Silenciar el audio de un slice desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Colapsar el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
