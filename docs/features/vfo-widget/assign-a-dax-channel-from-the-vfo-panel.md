# Referencia del Panel VFO

El panel VFO es un panel de control flotante por slice anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes por slice más utilizados — modo, presets de filtro, selección de antena, ganancia AF, balance, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. Se colapsa en una tira compacta de solo frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión de radio activa.
- El puente de audio DAX debe estar en ejecución. Si no lo está, actívelo mediante `Settings > Autostart DAX with AetherSDR` y reinicie AetherSDR, o inícielo manualmente.
- El panel VFO del slice objetivo debe estar abierto y expandido. Si está colapsado en la tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Abrir el panel VFO

Haga clic en la bandera del marcador VFO en la pantalla del espectro para el slice que desea configurar. El panel VFO se abre, anclado a la izquierda del marcador.

## Controles del panel VFO

| Control | Ubicación | Predeterminado | Valores válidos | Comportamiento |
|---|---|---|---|---|
| Botón de antena RX | Encabezado | — | — | Abre el menú de selección de antena para la antena receptora de este slice. |
| Botón de antena TX | Encabezado | — | — | Abre el menú de selección de antena para la antena transmisora de este slice. |
| Pantalla de frecuencia | Encabezado | — | — | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro | Encabezado | — | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preset de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modos SSB/digitales (#2197, v0.9.8). |
| Alternancia de colapso | Encabezado | expandido | — | Colapsa el panel VFO a una tira compacta de solo frecuencia. Se persiste por slice como `SliceFlagCollapsed_{N}`. Clic derecho → Add Spot también funciona en modo colapsado. |
| Botón de grosor del marcador | Encabezado | 1 px | Off, 1 px, 3 px | Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Se persiste por slice como `Slice{N}_MarkerWidth`. |
| Botón de bordes del filtro | Encabezado | mostrado | — | Alterna las líneas de borde del filtro en la banda de paso del espectro. Se persiste por slice como `Slice{N}_FilterEdgesHidden`. |
| Deslizador de ganancia AF | Pestaña Audio | 100 | 0–100 | Establece el nivel de salida de audio para este slice. No se persiste — refleja el estado en vivo del radio. |
| Deslizador de balance | Pestaña Audio | 50 | 0–100 | Establece el balance estéreo izquierda/derecha para este slice. 50 = centro. |
| Botón de silencio | Pestaña Audio | apagado | — | Silencia la salida de audio para este slice sin cambiar el ajuste de ganancia AF. |
| Botón + deslizador de squelch | Pestaña Audio | apagado | 0–100 | Activa el squelch para este slice. El deslizador adyacente establece el umbral. |
| Combinación AGC | Pestaña Audio | FAST | FAST, MED, SLOW, OFF | Establece la velocidad de ataque/liberación del AGC para este slice. |
| Combinación de modo | Pestaña Mode | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para este slice. |
| Botones de preset de filtro | Pestaña Mode | — | — | Aplica un preset de ancho de filtro guardado. Clic derecho para guardar el ancho de filtro actual en esa ranura. Se persiste en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |
| Botones + etiquetas RIT / XIT | Pestaña X/RIT | apagado | — | Activa el ajuste incremental de sintonización del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desfase actual; la rueda del ratón ajusta en pasos de 10 Hz. |
| Combinación de canal DAX | Pestaña DAX | Off | Off, 1–8 | Asigna un canal de audio DAX a este slice. |
| Botones DSP | Pestaña DSP | apagado | — | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de botones depende de la serie del radio y la compilación. Clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de AetherDSP Settings para ese algoritmo. |
| Botón ADSP | Pestaña DSP | — | — | Abre el diálogo de AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Con estilo de alternancia DSP del lado del radio pero no seleccionable. El clic eleva y enfoca el diálogo no modal de AetherDSP Settings. |
| Botón AetherVoice | Pestaña DSP | — | — | Alterna la Aetherial Audio Channel Strip — la suite unificada de DSP TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Insignia TX | TX (rojo), oculto | Se muestra cuando este slice es el slice transmisor activo. |
| Insignia SPLIT | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un slice diferente del slice receptor activo. |

## Asignación de un canal DAX

1. Haga clic en la pestaña **DAX** dentro del panel VFO.
2. Haga clic en la **combinación de canal DAX** y seleccione un canal de la lista desplegable.
3. Para desactivar el enrutamiento DAX para este slice, seleccione **Off**.

La combinación de canal DAX asigna un canal de audio DAX al slice actual. Seleccionar un canal numerado enruta el audio recibido del slice a ese canal DAX. Seleccionar **Off** elimina la asignación. Este ajuste refleja el estado en vivo del radio y no se persiste localmente en AetherSDR.

## Comportamiento del squelch por modo

El botón y deslizador de squelch se desactivan automáticamente en modos donde el squelch no es significativo o no está soportado:

- **El squelch está desactivado** en modos **Digital**, **RTTY** y **CW**.
  - **Digital / RTTY**: El audio se alimenta a decodificadores externos mediante DAX; el squelch no es significativo y puede bloquear señales FSK débiles.
  - **CW**: El radio bloquea el squelch activado a un nivel fijo y rechaza cambios.
- Si el squelch estaba activado al cambiar a uno de estos modos, el radio lo desactiva automáticamente. El estado guardado del squelch se conserva y se restaurará si vuelve a un modo compatible.

## Controles de la pestaña DSP

La pestaña DSP en el panel VFO contiene botones de reducción de ruido proporcionados por el radio y dos botones de lanzamiento del lado del cliente.

### Botones DSP del lado del radio

Los siguientes botones DSP del lado del radio aparecen en la cuadrícula de la pestaña DSP:

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
| MN | Filtro de muesca manual (solo se muestra en radios que lo soportan) |

### Botones de lanzamiento del lado del cliente

Dos botones de lanzamiento del lado del cliente aparecen al final de la cuadrícula DSP:

| Botón | Comportamiento |
|---|---|
| **ADSP** | Abre el diálogo de AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Con estilo de alternancia DSP del lado del radio pero no seleccionable. El clic eleva y enfoca el diálogo no modal de AetherDSP Settings. |
| **AetherVoice** | Alterna la Aetherial Audio Channel Strip — la suite unificada de DSP TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

### Alternancias de reducción de ruido del lado del cliente

Los siguientes botones de reducción de ruido del lado del cliente aparecen en la pestaña DSP cuando están habilitados por la serie del radio y la compilación:

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

Clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de AetherDSP Settings para ese algoritmo.

### Deslizador de nivel DSP

Una fila compartida de deslizador de nivel aparece debajo de la cuadrícula de botones. El deslizador ajusta la intensidad del botón DSP con nivel que se activó más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

El rango del deslizador es 0–100. Cuando ningún DSP con nivel está activo — o cuando solo RNN, ANFT o APF están activados — la fila del deslizador se atenúa y no responde a la entrada. La fila permanece en su lugar en todo momento; no desplaza la cuadrícula de botones cuando su objetivo cambia.

Algoritmos que soportan el deslizador de nivel: NR, NB, ANF, NRL, NRS, NRF, ANFL, MN.

Cuando un algoritmo DSP con nivel se activa desde el perfil guardado del radio al iniciar, el deslizador de nivel se rellena automáticamente sin requerir una alternancia manual.

## Etiqueta de ancho de filtro

La etiqueta de ancho de filtro muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preset de filtro en la pestaña Mode. La etiqueta utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modos SSB/digitales (#2197, v0.9.8).

## Menús de antena RX y TX

El **botón de antena RX** abre un menú para seleccionar la antena receptora de este slice. El **botón de antena TX** abre un menú para seleccionar la antena transmisora. Estos menús utilizan la lista de antenas proporcionada por el radio del slice cuando está disponible, recurriendo a la lista global de antenas. Las opciones de antena TX excluyen automáticamente los puertos de solo RX. Cada elemento del menú muestra su nombre de antena original como tooltip.

## Controles del marcador

El **botón de grosor del marcador** recorre la línea del marcador VFO entre Off, 1 px y 3 px. El ajuste se persiste por slice como `Slice{N}_MarkerWidth`.

El **botón de bordes del filtro** alterna las líneas de borde del filtro en la banda de paso del espectro. El ajuste se persiste por slice como `Slice{N}_FilterEdgesHidden`.

## Alternancia de colapso

La **alternancia de colapso** colapsa el panel VFO a una tira compacta de solo frecuencia. El ajuste se persiste por slice como `SliceFlagCollapsed_{N}`.

Clic derecho → Add Spot también funciona en modo colapsado. La etiqueta de frecuencia colapsada instala un filtro de eventos para garantizar que los clics sean manejados por el panel VFO, no por el widget del espectro subyacente, de modo que la frecuencia ajustada al paso del cursor nunca se informe en lugar de la del VFO (#4455).

## Insignia del slice

La insignia del slice muestra la letra del slice. La insignia soporta formato de texto enriquecido, permitiendo caracteres especiales.

## Entrada de frecuencia

Haga clic en la pantalla de frecuencia para comenzar la entrada directa de frecuencia. Escriba la frecuencia en MHz y presione Enter o Tab.

- En bandas XVTR, el rango de frecuencia se extiende a 50000.0 MHz.
- Para bandas de 2m/70cm (rango de 100–999 MHz), un entero simple como 1446 se interpreta automáticamente como 144.6 MHz insertando un decimal después del tercer dígito.
- Para bandas de 23cm y microondas, un entero simple representa MHz directamente.
- Cuando ingresa explícitamente una frecuencia por encima de 54 MHz (por ejemplo, escribiendo "144.225"), el analizador la trata correctamente como MHz incluso sin un slice XVTR, permitiendo la entrada directa de VHF/UHF.

Si intenta una entrada directa de frecuencia mientras el VFO está bloqueado, la entrada se cancela y se muestra la superposición LOCKED en lugar de aceptar la nueva frecuencia. La sintonización con la rueda del ratón en un VFO bloqueado activa la misma retroalimentación — el modelo del slice notifica `tuneBlockedByLock`, que cancela cualquier entrada de frecuencia en curso y redibuja el indicador LOCKED.

El campo de entrada de frecuencia utiliza un widget personalizado `FreqLineEdit`. El texto de sugerencia dice "MHz (e.g. 14.225)". La pantalla de frecuencia también proporciona anuncios de accesibilidad cuando la frecuencia cambia, garantizando la compatibilidad con lectores de pantalla.

## Comportamiento de bloqueo del VFO

El **botón Lock VFO** alterna el estado bloqueado del VFO. Cuando está bloqueado:
- La sintonización con la rueda del ratón está bloqueada — el modelo del slice muestra retroalimentación mediante `tuneBlockedByLock`.
- La entrada directa de frecuencia se cancela al intentar comenzar o durante una entrada activa.
- La pantalla de frecuencia muestra una superposición LOCKED (símbolo 🔒) en lugar del valor de frecuencia durante los intentos de entrada directa.

Desbloquear limpia la superposición LOCKED de forma centralizada en el SliceModel.

## Diseño de pestañas

La pila de pestañas del panel VFO informa solo el tamaño preferido de la pestaña actual. Esto corrige un espacio visual dentro de la pestaña Mode cuando la pestaña DSP es más alta (debido al digContainer visible en modos DIGU/DIGL). El
