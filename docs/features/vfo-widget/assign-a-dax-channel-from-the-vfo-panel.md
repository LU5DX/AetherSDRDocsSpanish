# Asignar un canal DAX desde el panel VFO

DAX (Digital Audio Exchange) enruta el audio recibido de un slice a un canal de audio con nombre en su computadora. Utilice este procedimiento para asignar o cambiar el canal DAX de cualquier slice directamente desde su panel VFO.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El puente de audio DAX debe estar en ejecución. Si no lo está, actívelo mediante `Settings > Autostart DAX with AetherSDR` y reinicie AetherSDR, o inícielo manualmente.
- El panel VFO del slice objetivo debe estar abierto y expandido. Si está colapsado a la tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora VFO en la visualización del espectro para el slice que desea configurar. Se abre el panel VFO, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **DAX** dentro del panel VFO.
3. Haga clic en el **combo de canal DAX** y seleccione un canal de la lista desplegable.
4. Para deshabilitar el enrutamiento DAX para este slice, seleccione **Off**.

## Función de cada control

| Control                         | Valor predeterminado                                                                                                                      | Valores válidos                                                                                                            |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Combo de canal DAX              | Off                                                                                                                                       | Off, 1–8                                                                                                                   |
| Botón ADSP (pestaña DSP)        | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de alternancia DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Abre la tira de canales de audio Aetherial — el conjunto unificado DSP de TX/RX (v0.9.8).                                                | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

El combo de canal DAX asigna un canal de audio DAX al slice actual. Al seleccionar un canal numerado, se enruta el audio recibido del slice a ese canal DAX. Al seleccionar **Off** se elimina la asignación. Esta configuración refleja el estado activo de la radio y AetherSDR no la conserva localmente.

## Comportamiento del squelch por modo

El botón y el deslizador de squelch se deshabilitan automáticamente en modos donde el squelch no es significativo o no es compatible. A partir de v26.5.1:

- **El squelch está deshabilitado** en los modos **Digital**, **RTTY** y **CW**.
  - **Digital / RTTY**: El audio alimenta decodificadores externos a través de DAX; el squelch no es significativo y puede bloquear señales FSK débiles (incidencia #2504).
  - **CW**: La radio bloquea el squelch activado a un nivel fijo y rechaza los cambios.
- Si el squelch estaba activado al cambiar a uno de estos modos, la radio lo desactiva automáticamente. El estado guardado del squelch se conserva y se restaurará si vuelve a un modo compatible.

## Controles de la pestaña DSP

La pestaña DSP en el panel VFO contiene botones de reducción de ruido proporcionados por la radio y dos botones de lanzador del lado del cliente.

### Botones DSP del lado de la radio

Los siguientes botones DSP del lado de la radio aparecen en la cuadrícula de la pestaña DSP:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Supresor de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de énfasis de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

### Botones de lanzador del lado del cliente

Dos botones de lanzador del lado del cliente aparecen al final de la cuadrícula DSP:

| Botón | Comportamiento |
|---|---|
| **ADSP** | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Con estilo de alternancia DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| **AetherVoice** | Alterna la tira de canales de audio Aetherial — el conjunto unificado DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

### Alternancias de reducción de ruido del lado del cliente

Los siguientes botones de reducción de ruido del lado del cliente aparecen en la pestaña DSP cuando están habilitados según la serie y la compilación de la radio:

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

Una fila de deslizador de nivel compartida aparece debajo de la cuadrícula de botones. El deslizador ajusta la intensidad del botón DSP con nivel que se encendió más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

El rango del deslizador es 0–100. Cuando no hay ningún DSP con nivel activo — o solo RNN, ANFT o APF está encendido — la fila del deslizador se atenúa y no responde a la entrada. La fila permanece en su lugar en todo momento; no desplaza la cuadrícula de botones cuando cambia su objetivo.

Algoritmos compatibles con el deslizador de nivel: NR, NB, ANF, NRL, NRS, NRF, ANFL.

A partir de v0.9.8, cuando un algoritmo DSP con nivel se habilita desde el perfil guardado de la radio al inicio, el deslizador de nivel se completa automáticamente sin necesidad de una alternancia manual.

### Etiqueta de ancho de filtro

La etiqueta de ancho de filtro muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. A partir de v0.9.8, esta etiqueta utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas de modo SSB/digital.

### Menús de antena RX y TX

El **botón de antena RX** abre un menú para seleccionar la antena de recepción para este slice. El **botón de antena TX** abre un menú para seleccionar la antena de transmisión. A partir de v26.5.2, estos menús utilizan la lista de antenas proporcionada por la radio del slice cuando está disponible, recurriendo a la lista de antenas global. Las opciones de antena TX excluyen automáticamente los puertos de antena solo RX. Cada elemento del menú muestra el nombre de la antena sin procesar como información sobre herramientas.

### Controles de marcador

El **botón de grosor de marcador** recorre la línea del marcador VFO a través de Off, 1 px y 3 px. La configuración se conserva por slice como `Slice{N}_MarkerWidth`.

El **botón de bordes de filtro** alterna las líneas de borde del filtro en la banda pasante del espectro. La configuración se conserva por slice como `Slice{N}_FilterEdgesHidden`.

### Alternancia de colapso

La **alternancia de colapso** colapsa el panel VFO a una tira compacta de solo frecuencia. La configuración se conserva por slice como `SliceFlagCollapsed_{N}`.

### Insignia del slice

La insignia del slice muestra la letra del slice. A partir de v26.5.2, la insignia admite formato de texto enriquecido, permitiendo caracteres especiales (incidencia #2606).

### Ingreso de frecuencia

Haga clic en la visualización de frecuencia para comenzar el ingreso directo de frecuencia. Escriba la frecuencia en MHz y presione Enter o Tab. A partir de v26.5.2, en bandas XVTR el rango de frecuencia se extiende a 50000,0 MHz. Para bandas de 2m/70cm (rango de 100-999 MHz), un número entero simple como 1446 se interpreta automáticamente como 144,6 MHz insertando un decimal después del tercer dígito. Para bandas de 23cm y microondas, un número entero simple representa MHz directamente.

A partir de v26.5.3, el análisis del ingreso de frecuencia se mejora con manejo consciente del contexto. Cuando ingresa explícitamente una frecuencia superior a 54 MHz (por ejemplo, escribiendo "144.225"), el analizador la trata correctamente como MHz incluso sin un slice XVTR, permitiendo el ingreso directo de VHF/UHF. La función `FrequencyEntryParser::normalizedMhzText` normaliza formatos de entrada como "14.225.000" eliminando puntos adicionales. La función `FrequencyEntryParser::isExplicitMhzEntry` detecta cuando ha escrito un valor en MHz explícitamente. En bandas XVTR, la convención de banda de 3 dígitos (número entero simple como 1446 = 144,6 MHz) sigue funcionando.

Si intenta un ingreso directo de frecuencia mientras el VFO está bloqueado, el ingreso se cancela y se muestra la superposición LOCKED en lugar de aceptar la nueva frecuencia (incidencia #2983). La visualización de frecuencia también indica cuando la sintonía está bloqueada por el bloqueo. La sintonía con rueda de desplazamiento en un VFO bloqueado activa la misma retroalimentación — el modelo del slice notifica `tuneBlockedByLock`, lo que cancela cualquier ingreso de frecuencia en curso y vuelve a dibujar el indicador LOCKED.

### Comportamiento del bloqueo VFO

El **botón Lock VFO** alterna el estado de bloqueo del VFO. Cuando está bloqueado:
- La sintonía con rueda de desplazamiento está bloqueada — el modelo del slice muestra retroalimentación a través de `tuneBlockedByLock`.
- El ingreso directo de frecuencia se cancela al intentar iniciarlo o durante un ingreso activo.
- La visualización de frecuencia muestra una superposición LOCKED (símbolo 🔒) en lugar del valor de frecuencia durante los intentos de ingreso directo.

Desbloquear elimina la superposición LOCKED de forma centralizada en el SliceModel (incidencia #2983).

### Mejora en el diseño de pestañas

A partir de v26.5.3, la pila de pestañas del panel VFO utiliza un widget `TabStack` personalizado que informa solo el tamaño preferido de la pestaña actual. Esto corrige un espacio visual dentro de la pestaña Mode cuando la pestaña DSP es más alta (debido a que el digContainer es visible en modos DIGU/DIGL). El contenido de la pestaña ya no asigna en exceso la altura del máximo de todas las páginas.

### Tematización de deslizadores (v26.6.1)

A partir de v26.6.1, el panel VFO utiliza un estilo de deslizadores tematizado en toda su extensión. El deslizador Pan se pinta con relleno anclado al centro: la sección de la ranura desde el control deslizante hasta el punto medio se rellena con el color de acento, mientras que el lado opuesto utiliza el color de fondo. Esto hace que la posición central (neutra) sea inmediatamente visible. El control deslizante es dibujado por el estilo Qt predeterminado.

Todos los demás deslizadores (AF Gain, umbral de squelch, nivel DSP) siguen las mismas reglas de tematización. El estilo está impulsado por el tema de color activo en lugar de colores codificados.

### Tematización del panel VFO (v26.6.1)

A partir de v26.6.1, el panel VFO utiliza un ámbito de contenedor de tematización dedicado `spectrum/vfo`. Esto asegura que los clics del inspector en la superficie del panel VFO (incluyendo la insignia de frecuencia, la insignia de indicativo y el medidor de señal) se resuelvan en tokens de tema específicos del VFO en lugar de recurrir al ámbito del espectro. El panel VFO declara los siguientes tokens de tema para cobertura del inspector:

- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

Estos tokens se pintan directamente mediante llamadas `QPainter` y se muestran correctamente en el modo de inspección.

## Consejos

- Cada canal DAX se puede asignar a un solo slice a la vez. Si asigna un canal que ya está en uso por otro slice, la radio moverá la asignación.
- Si el panel VFO se recortaría por el borde de la ventana, se voltea automáticamente al lado derecho del marcador.
- Para acceder a NR2, RN2, NR4, MNR, BNR o DFNR, haga clic derecho en la visualización del espectro para abrir el menú superpuesto, o abra el applet AetherDSP.

## Solución de problemas

- **El combo de canal DAX no tiene efecto / el audio no aparece en el host** — Confirme que el puente de audio DAX está en ejecución. Verifique `Settings > Autostart DAX with AetherSDR`. En sistemas macOS y PipeWire, el puente debe estar activo para que los canales DAX aparezcan como dispositivos de audio.
- **La pestaña DAX no es visible** — El panel VFO puede estar colapsado. Haga clic en la tira colapsada para expandirla, luego seleccione la pestaña DAX.
- **El deslizador de nivel DSP está atenuado** — Ningún algoritmo DSP con nivel está activo actualmente, o solo RNN, ANFT o APF está habilitado. Active NR, NB, ANF, NRL, NRS, NRF o ANFL para activar el deslizador.
- **El deslizador de nivel DSP falta al inicio** — Si un algoritmo DSP con nivel estaba habilitado en el perfil guardado de la radio, el deslizador ahora se completa automáticamente. Si aún parece faltar, desactive y active el algoritmo nuevamente.
- **El botón de squelch está deshabilitado** — Está en modo Digital, RTTY o CW. El squelch no está disponible en estos modos (digital y RTTY enrutan el audio a través de DAX; CW tiene squelch fijo bloqueado por la radio). Cambie a un modo compatible como USB o AM para habilitar los controles de squelch.
- **El ingreso de frecuencia no acepta frecuencias VHF/UHF** — A partir de v26.5.3, escriba la frecuencia explícitamente en formato MHz (por ejemplo, "144.225") y el
