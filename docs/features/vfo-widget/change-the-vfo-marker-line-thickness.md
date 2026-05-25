# Cambiar el Grosor de la Línea del Marcador de VFO

Utilice el botón de grosor del marcador para controlar la prominencia de la línea del marcador de VFO en la pantalla del espectro, o para ocultarla por completo. La configuración se guarda por slice.

## Antes de empezar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO debe estar abierto para el slice que desea ajustar. Si no está visible, haga clic en la bandera del marcador de VFO para ese slice en la pantalla del espectro.

## Pasos

1. Abra el panel VFO para el slice objetivo haciendo clic en su bandera del marcador de VFO en la pantalla del espectro.
2. Localice el **botón de grosor del marcador** en el panel VFO.
3. Haga clic en el botón para recorrer cíclicamente los valores disponibles: **Off**, **1 px** y **3 px**.
4. Deje de hacer clic cuando se muestre el grosor deseado. El marcador en la pantalla del espectro se actualiza inmediatamente.

## Qué hace cada control

| Control                      | Default                                                                                                                               | Valores válidos                                            |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| Botón de grosor del marcador      | 1 px                                                                                                                                  | Off, 1 px, 3 px                                         |
| Botón ADSP (pestaña DSP)        | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene el estilo de un conmutador DSP del lado de la radio pero no es marcable. Al hacer clic, abre y enfoca el diálogo no modal de Configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Alterna la Tira de Canal de Audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8).                                                     | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú / cadena para la tira.                 |

Cada clic avanza al siguiente valor en el ciclo: **Off** → **1 px** → **3 px** → **Off**. La configuración se conserva por slice, por lo que el slice 1 y el slice 2 pueden tener grosores diferentes.

## Consejos

- Configurar el marcador en **Off** oculta la línea vertical por completo. El panel VFO y la bandera permanecen visibles y funcionales.
- Si ejecuta varios slices en el mismo panadapter, aumentar un marcador a **3 px** puede ayudar a distinguirlo de los slices adyacentes.

## Cambios en la pestaña DSP en v0.9.8

La pestaña DSP en el panel VFO ahora muestra solo los botones de reducción de ruido proporcionados por la radio. Los siguientes botones se han eliminado de la pestaña DSP del panel VFO:

| Botón eliminado | Dónde encontrarlo ahora |
|---|---|
| NR2 | Menú superpuesto del espectro o applet AetherDSP |
| RN2 | Menú superpuesto del espectro o applet AetherDSP |
| BNR | Menú superpuesto del espectro o applet AetherDSP |
| NR4 | Menú superpuesto del espectro o applet AetherDSP |
| MNR | Menú superpuesto del espectro o applet AetherDSP |
| DFNR | Menú superpuesto del espectro o applet AetherDSP |

Los botones restantes de la pestaña DSP están organizados en una cuadrícula de cuatro columnas:

| Fila | Col 0 | Col 1 | Col 2 | Col 3 |
|---|---|---|---|---|
| 0 | NR | NB | ANF | APF |
| 1 | NRL | NRS | RNN | NRF |
| 2 | ANFL | ANFT | ADSP | AetherVoice (2 cols) |

El botón APF permanece oculto a menos que el slice esté en un modo CW.

Aparecen dos nuevos botones de lanzador del lado del cliente en la fila 2 de la cuadrícula:
- **ADSP** — Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Este botón tiene el estilo de un conmutador DSP del lado de la radio pero no es marcable. Al hacer clic, abre y enfoca el diálogo no modal de Configuración de AetherDSP.
- **AetherVoice** — Alterna la Tira de Canal de Audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8). Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú / cadena para la tira.

### Deslizador de nivel DSP

Aparece una fila de deslizador de nivel compartido debajo de la cuadrícula de botones DSP. El deslizador se reorienta automáticamente al botón DSP con nivel que se haya habilitado más recientemente. La etiqueta de la fila se actualiza para mostrar el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha del deslizador.

La fila está siempre presente en el diseño. Cuando ningún DSP con nivel está activo — o cuando solo RNN, ANFT o APF están encendidos — la fila se desvanece a transparente. Se vuelve completamente visible tan pronto como se enciende un DSP con nivel.

El deslizador controla el nivel para estos objetivos:

| Etiqueta del objetivo | DSP controlado |
|---|---|
| NR | Nivel de reducción de ruido |
| NB | Nivel de eliminador de ruido |
| ANF | Nivel de filtro de muesca automático |
| NRL | Nivel de reducción de ruido (NRL) |
| NRS | Nivel de sustracción espectral |
| NRF | Nivel de filtro de ruido espectral |
| ANFL | Nivel de filtro de muesca LMS |

## Comportamiento del control de squelch

El botón y el deslizador de squelch en la pestaña Audio están deshabilitados en modos digital, RTTY y CW. Los modos digital y RTTY envían audio a decodificadores externos a través de DAX, donde el squelch no tiene sentido y puede bloquear señales FSK débiles. La radio bloquea el squelch en un nivel fijo en modo CW y rechaza los cambios. Al cambiar a uno de estos modos mientras el squelch está habilitado, el squelch se deshabilita automáticamente y el estado guardado se conserva en la radio para cuando vuelva a un modo de voz.

## Comportamiento de inicio de DSP (v0.9.8)

Cuando AetherSDR se conecta a la radio, cualquier DSP que estuviera habilitado en el perfil guardado de la radio ahora envía inmediatamente su nivel al deslizador de nivel DSP compartido. Anteriormente, el deslizador faltaba al iniciar para estos DSP hasta que el usuario los alternaba manualmente. Esta corrección asegura que el deslizador esté siempre presente y activo cuando un DSP con nivel ya está habilitado en la radio.

## Corrección de la etiqueta de ancho de filtro (v0.9.8)

La etiqueta de ancho de filtro en el panel VFO ahora utiliza una única fuente de verdad (`RxApplet::formatFilterWidth`) para generar su lectura. Esto corrige un desfase de 0,1 kHz que afectaba las lecturas en modos SSB y digital, y asegura que el panel VFO y el applet RX muestren valores de ancho de filtro idénticos.

## Mejoras en la selección de antena (v26.5.2.1)

Los botones de antena RX y TX ahora utilizan listas de antenas por slice cuando están disponibles, volviendo a la lista global de antenas en caso contrario. El menú de antena TX excluye los puertos solo de RX verificando patrones de nomenclatura específicos.

### Selección de antena RX

1. Abra el panel VFO para el slice objetivo.
2. Haga clic en el **botón de antena RX**. Se abre un menú que muestra las antenas de recepción disponibles.
3. Seleccione una antena del menú. El slice utiliza inmediatamente la antena seleccionada para la recepción.

El menú muestra la lista de antenas de recepción por slice si está disponible. Cada entrada tiene un tooltip que muestra el identificador completo del puerto de antena.

### Selección de antena TX

1. Abra el panel VFO para el slice objetivo.
2. Haga clic en el **botón de antena TX**. Se abre un menú que muestra las antenas que se pueden usar para transmitir.
3. Seleccione una antena del menú. El slice utiliza inmediatamente la antena seleccionada para la transmisión.

El menú filtra los puertos de antena que comienzan con "RX" para evitar seleccionar puertos solo de RX para la transmisión. Cada entrada tiene un tooltip que muestra el identificador completo del puerto de antena.

## Mejoras en la entrada de frecuencia (v26.5.3)

### Comportamiento de entrada directa de frecuencia cuando el slice está bloqueado

Cuando un slice está bloqueado, se bloquea el intento de comenzar la entrada directa de frecuencia haciendo clic en la pantalla de frecuencia. El campo de entrada directa no aparece. Si ya hay una entrada directa en curso cuando el slice se bloquea, la entrada se cancela y la pantalla vuelve a mostrar la frecuencia bloqueada. Se muestra una superposición visual "LOCKED" de forma centralizada a través del modelo del slice.

### Entrada de frecuencia en bandas XVTR (v26.5.2.1)

Al introducir frecuencias en bandas de transvertidor (XVTR), la frecuencia máxima admitida se ha incrementado de 450 MHz a 50 000 MHz. La lógica de inserción decimal automática ahora solo se aplica a bandas de tres dígitos (100-999 MHz) cuando el valor ingresado supera los 450 MHz. Para bandas superiores (1000 MHz y más), los números enteros se interpretan como MHz sin inserción decimal.

### Entrada explícita de MHz en bandas HF (v26.5.3)

Al introducir una frecuencia en bandas HF, un valor superior a 54 MHz con un punto decimal explícito (por ejemplo, "144.200") ahora se interpreta como MHz en lugar de dividirse automáticamente por 1000 (kHz) o 1 000 000 (Hz). Esto permite la entrada directa de MHz para frecuencias VHF/UHF incluso cuando no se está en una banda XVTR.

## Sintonización con la rueda del ratón en modo colapsado (v26.5.3)

En modo colapsado, la rueda del ratón ahora sintoniza el slice incluso cuando el slice está bloqueado. Cuando se desplaza el slice bloqueado, se muestra una notificación visual "LOCKED" para indicar que la sintonización fue bloqueada. Anteriormente, el modo colapsado ignoraba los eventos de desplazamiento cuando el slice estaba bloqueado.

## Corrección de altura de la pila de pestañas (v26.5.3)

El área de contenido de las pestañas del panel VFO ahora informa solo el tamaño preferido de la página de pestaña actual, en lugar del máximo de todas las páginas. Esto corrige un espacio de altura que ocurría cuando la pestaña DSP era más alta que la pestaña Mode (por ejemplo, cuando el contenedor de submodo digital era visible en modo DIGU o DIGL).

## Soporte HTML para la insignia de slice (v26.5.2.1)

La insignia de slice que muestra la letra del slice ahora puede renderizar texto enriquecido. Esto permite futuras mejoras donde se puedan utilizar caracteres no ASCII o texto con estilo para la identificación del slice.

## Descripción general del panel VFO

El panel VFO es un panel de control flotante por slice anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a las configuraciones por slice más utilizadas sin salir de la vista del espectro.

### Controles

| Control | Tipo | Default | Comportamiento |
|---|---|---|---|
| Botón de antena RX | push_button | - | Abre el menú de selección de antena para la antena de recepción de este slice. |
| Botón de antena TX | push_button | - | Abre el menú de selección de antena para la antena de transmisión de este slice. |
| Pantalla de frecuencia | indicator | - | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. La entrada directa se bloquea cuando el slice está bloqueado. |
| Etiqueta de ancho de filtro | indicator | - | Muestra el ancho de banda del filtro actual. Haga clic para recorrer cíclicamente los botones de preajuste de filtro en la pestaña Mode. |
| Deslizador de ganancia AF (pestaña Audio) | slider | 100 | Establece el nivel de salida de audio para este slice. Rango 0-100. |
| Deslizador de paneo (pestaña Audio) | slider | 50 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. Rango 0-100. |
| Botón de silencio (pestaña Audio) | toggle_button | off | Silencia la salida de audio para este slice sin cambiar la configuración de ganancia AF. |
| Botón + deslizador de squelch (pestaña Audio) | toggle_button | off | Habilita el squelch para este slice. El deslizador adyacente establece el umbral. Rango 0-100. |
| Combo AGC (pestaña Audio) | combo_box | FAST | Establece la velocidad de ataque/liberación del AGC para este slice. Opciones: FAST, MED, SLOW, OFF. |
| Combo de modo (pestaña Mode) | combo_box | USB | Establece el modo de demodulación para este slice. Opciones: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY. |
| Botones de preajuste de filtro (pestaña Mode) | push_button | - | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | toggle_button | off | Habilita la sintonización incremental del receptor (RIT) o transmisor (XIT). La rueda del ratón ajusta en pasos de 10 Hz. |
| Combo de canal DAX (pestaña DAX) | combo_box | Off | Asigna un canal de audio DAX a este slice. Opciones: Off, 1-8. |
| Botón de grosor del marcador | push_button | 1 px | Recorre cíclicamente la línea del marcador VFO entre Off, 1 px y 3 px. |
| Botón de bordes de filtro | toggle_button | shown | Alterna las líneas de borde del filtro en la banda pasante del espectro. |
| Alternar colapso | toggle_button | expanded | Colapsa el panel VFO a una tira compacta solo de frecuencia. |

### Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Insignia TX | TX (rojo), oculto | Se muestra cuando este slice es el slice de transmisión activo. |
| Insignia SPLIT | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un slice diferente del slice de recepción activo. |

## Relacionados

- [Ocultar o mostrar las líneas de borde del filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Colapsar el panel VFO a la vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Descripción general del panel VFO](overview.md)
