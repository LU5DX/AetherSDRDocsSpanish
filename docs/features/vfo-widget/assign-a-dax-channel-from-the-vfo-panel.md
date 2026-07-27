# Referencia del Panel VFO

El panel VFO es un panel de control flotante por porción anclado al marcador VFO en la visualización del espectro. Proporciona acceso rápido a las configuraciones más utilizadas por porción — modo, preajustes de filtro, selección de antena, ganancia de AF, paneo, silenciador, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. Se colapsa a una tira compacta que solo muestra la frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa al radio.
- El puente de audio DAX debe estar en ejecución. Si no lo está, actívelo mediante `Settings > Autostart DAX with AetherSDR` y reinicie AetherSDR, o inícielo manualmente.
- El panel VFO para la porción objetivo debe estar abierto y expandido. Si está colapsado a la tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Abrir el panel VFO

Haga clic en la bandera del marcador VFO en la visualización del espectro de la porción que desea configurar. El panel VFO se abre, anclado a la izquierda del marcador.

## Controles del panel VFO

| Control | Ubicación | Predeterminado | Valores válidos | Comportamiento |
|---|---|---|---|---|
| Botón de antena RX | Encabezado | — | — | Abre el menú de selección de antena para la antena receptora de esta porción. |
| Botón de antena TX | Encabezado | — | — | Abre el menú de selección de antena para la antena transmisora de esta porción. |
| Visualización de frecuencia | Encabezado | — | — | Muestra la frecuencia actual de la porción. Haga clic una vez para iniciar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro | Encabezado | — | — | Muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. |
| Alternar colapso | Encabezado | expandido | — | Colapsa el panel VFO a una tira compacta de solo frecuencia. Se mantiene por porción como `SliceFlagCollapsed_{N}`. |
| Botón de grosor del marcador | Encabezado | 1 px | Off, 1 px, 3 px | Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Se mantiene por porción como `Slice{N}_MarkerWidth`. |
| Botón de bordes del filtro | Encabezado | mostrado | — | Alterna las líneas de borde del filtro en la banda de paso del espectro. Se mantiene por porción como `Slice{N}_FilterEdgesHidden`. |
| Deslizador de ganancia AF | Pestaña Audio | 100 | 0–100 | Establece el nivel de salida de audio para esta porción. No se mantiene — refleja el estado en vivo del radio. |
| Deslizador de paneo | Pestaña Audio | 50 | 0–100 | Establece el paneo estéreo izquierda/derecha para esta porción. 50 = centro. |
| Botón de silencio | Pestaña Audio | off | — | Silencia la salida de audio para esta porción sin cambiar la configuración de ganancia AF. |
| Botón + deslizador de silenciador | Pestaña Audio | off | 0–100 | Activa el silenciador para esta porción. El deslizador adyacente establece el umbral. |
| Combo AGC | Pestaña Audio | FAST | FAST, MED, SLOW, OFF | Establece la velocidad de ataque/liberación del AGC para esta porción. |
| Combo de modo | Pestaña Mode | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | Establece el modo de demodulación para esta porción. |
| Botones de preajuste de filtro | Pestaña Mode | — | — | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se mantiene en `FilterPresets`. |
| Botones + etiquetas RIT/XIT | Pestaña X/RIT | off | — | Activa la sintonización incremental del receptor (RIT) o transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. |
| Combo de canal DAX | Pestaña DAX | Off | Off, 1–8 | Asigna un canal de audio DAX a esta porción. |
| Botones DSP | Pestaña DSP | off | — | Activa el algoritmo de reducción de ruido correspondiente para esta porción. La disponibilidad de botones depende de la serie del radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo AetherDSP Settings para ese algoritmo. |
| Botón ADSP | Pestaña DSP | — | — | Abre el cuadro de diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Con estilo de alternancia DSP del lado del radio pero no seleccionable. Al hacer clic, eleva y enfoca el cuadro de diálogo AetherDSP Settings no modal. |
| Botón AetherVoice | Pestaña DSP | — | — | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Distintivo TX | TX (rojo), oculto | Se muestra cuando esta porción es la porción de transmisión activa. |
| Distintivo SPLIT | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a una porción diferente a la porción receptora activa. |

## Asignación de un canal DAX

1. Haga clic en la pestaña **DAX** dentro del panel VFO.
2. Haga clic en el **combo de canal DAX** y seleccione un canal de la lista desplegable.
3. Para deshabilitar el enrutamiento DAX para esta porción, seleccione **Off**.

El combo de canal DAX asigna un canal de audio DAX a la porción actual. Seleccionar un canal numerado enruta el audio recibido de la porción a ese canal DAX. Seleccionar **Off** elimina la asignación. Esta configuración refleja el estado en vivo del radio y AetherSDR no la mantiene localmente.

## Comportamiento del silenciador por modo

El botón y el deslizador del silenciador se deshabilitan automáticamente en modos donde el silenciador no es relevante o no es compatible:

- **El silenciador está deshabilitado** en modos **Digital**, **RTTY** y **CW**.
  - **Digital / RTTY**: El audio alimenta decodificadores externos a través de DAX; el silenciador no es relevante y puede bloquear señales FSK débiles.
  - **CW**: El radio bloquea el silenciador activado a un nivel fijo y rechaza cambios.
- Si el silenciador estaba activado al cambiar a uno de estos modos, el radio lo desactiva automáticamente. El estado guardado del silenciador se conserva y se restaurará si vuelve a un modo compatible.

## Controles de la pestaña DSP

La pestaña DSP en el panel VFO contiene botones de reducción de ruido proporcionados por el radio y dos botones lanzadores del lado del cliente.

### Botones DSP del lado del radio

Los siguientes botones DSP del lado del radio aparecen en la cuadrícula de la pestaña DSP:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Eliminador de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de pico de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

### Botones lanzadores del lado del cliente

Dos botones lanzadores del lado del cliente aparecen al final de la cuadrícula DSP:

| Botón | Comportamiento |
|---|---|
| **ADSP** | Abre el cuadro de diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Con estilo de alternancia DSP del lado del radio pero no seleccionable. Al hacer clic, eleva y enfoca el cuadro de diálogo AetherDSP Settings no modal. |
| **AetherVoice** | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

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

Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo AetherDSP Settings para ese algoritmo.

### Deslizador de nivel DSP

Aparece una fila de deslizador de nivel compartida debajo de la cuadrícula de botones. El deslizador ajusta la intensidad del botón DSP nivelado que se encendió más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

El rango del deslizador es 0–100. Cuando no hay DSP nivelado activo — o solo RNN, ANFT o APF está encendido — la fila del deslizador se atenúa y no responde a la entrada. La fila permanece en su lugar en todo momento; no desplaza la cuadrícula de botones cuando cambia su objetivo.

Algoritmos que admiten el deslizador de nivel: NR, NB, ANF, NRL, NRS, NRF, ANFL.

Cuando un algoritmo DSP nivelado se activa desde el perfil guardado del radio al iniciar, el deslizador de nivel se completa automáticamente sin necesidad de una alternancia manual.

## Etiqueta de ancho de filtro

La etiqueta de ancho de filtro muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. La etiqueta usa `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital.

## Menús de antena RX y TX

El **botón de antena RX** abre un menú para seleccionar la antena receptora de esta porción. El **botón de antena TX** abre un menú para seleccionar la antena transmisora. Estos menús utilizan la lista de antenas proporcionada por el radio para la porción cuando está disponible, recurriendo a la lista de antenas global. Las opciones de antena TX excluyen automáticamente los puertos de solo RX. Cada elemento del menú muestra su nombre de antena sin procesar como información sobre herramientas.

## Controles del marcador

El **botón de grosor del marcador** recorre la línea del marcador VFO entre Off, 1 px y 3 px. La configuración se mantiene por porción como `Slice{N}_MarkerWidth`.

El **botón de bordes del filtro** alterna las líneas de borde del filtro en la banda de paso del espectro. La configuración se mantiene por porción como `Slice{N}_FilterEdgesHidden`.

## Alternar colapso

La **alternancia de colapso** colapsa el panel VFO a una tira compacta de solo frecuencia. La configuración se mantiene por porción como `SliceFlagCollapsed_{N}`.

## Distintivo de porción

El distintivo de porción muestra la letra de la porción. El distintivo admite formato de texto enriquecido, permitiendo caracteres especiales.

## Entrada de frecuencia

Haga clic en la visualización de frecuencia para iniciar la entrada directa de frecuencia. Escriba la frecuencia en MHz y presione Enter o Tab.

- En bandas XVTR, el rango de frecuencia se extiende a 50000.0 MHz.
- Para bandas de 2m/70cm (rango 100-999 MHz), un número entero simple como 1446 se interpreta automáticamente como 144.6 MHz insertando un decimal después del tercer dígito.
- Para bandas de 23cm y microondas, un número entero simple representa MHz directamente.
- Cuando ingresa explícitamente una frecuencia superior a 54 MHz (por ejemplo, escribiendo "144.225"), el analizador la trata correctamente como MHz incluso sin una porción XVTR, permitiendo la entrada directa en VHF/UHF.

Si intenta una entrada directa de frecuencia mientras el VFO está bloqueado, la entrada se cancela y se muestra la superposición BLOQUEADO en lugar de aceptar la nueva frecuencia. La sintonización con la rueda de desplazamiento en un VFO bloqueado activa la misma retroalimentación — el modelo de porción notifica `tuneBlockedByLock`, que cancela cualquier entrada de frecuencia en curso y vuelve a pintar el indicador BLOQUEADO.

El campo de entrada de frecuencia utiliza un widget `FreqLineEdit` personalizado. El texto de sugerencia muestra "MHz (ej. 14.225)". La visualización de frecuencia también proporciona anuncios de accesibilidad cuando la frecuencia cambia, asegurando la compatibilidad con lectores de pantalla.

## Comportamiento de bloqueo del VFO

El **botón de bloqueo del VFO** alterna el estado bloqueado del VFO. Cuando está bloqueado:
- La sintonización con la rueda de desplazamiento está bloqueada — el modelo de porción muestra retroalimentación a través de `tuneBlockedByLock`.
- La entrada directa de frecuencia se cancela al intentar iniciarla o durante una entrada activa.
- La visualización de frecuencia muestra una superposición BLOQUEADO (símbolo 🔒) en lugar del valor de frecuencia durante los intentos de entrada directa.

Desbloquear elimina la superposición BLOQUEADO de forma centralizada en SliceModel.

## Diseño de pestañas

La pila de pestañas del panel VFO informa solo el tamaño preferido de la pestaña actual. Esto corrige un espacio visual dentro de la pestaña Mode cuando la pestaña DSP es más alta (debido a que el digContainer está visible en modos DIGU/DIGL). El contenido de la pestaña ya no asigna altura en exceso del máximo de todas las páginas.

### Navegación de pestañas

Las pestañas del panel VFO están implementadas como widgets `QPushButton` en lugar de widgets `QLabel`. Este cambio proporciona soporte adecuado para el enfoque del teclado:

- Cada botón de pestaña se puede enfocar mediante la tecla Tab (política `Qt::TabFocus`).
- Las pestañas enfocadas muestran un contorno de borde inferior sutil usando el color de la etiqueta de la pestaña.
- **Haga clic derecho en la pestaña del altavoz (primera pestaña)** para alternar el estado de silencio de audio directamente — un acceso directo
