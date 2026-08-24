# Cambie el Grosor de la Línea del Marcador VFO

Use el botón de grosor del marcador para controlar cuán prominente aparece la línea del marcador VFO en la pantalla del espectro, o para ocultarla por completo. La configuración se guarda por slice.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO debe estar abierto para el slice que desea ajustar. Si no está visible, haga clic en la bandera del marcador VFO de ese slice en la pantalla del espectro.

## Pasos

1. Abra el panel VFO del slice objetivo haciendo clic en su bandera de marcador VFO en la pantalla del espectro.
2. Localice el **botón de grosor del marcador** en el panel VFO.
3. Haga clic en el botón para recorrer los valores disponibles: **Off**, **1 px** y **3 px**.
4. Deje de hacer clic cuando se muestre el grosor deseado. El marcador en la pantalla del espectro se actualiza inmediatamente.

## Qué hace cada control

| Control                      | Valor predeterminado                                                                                                                               | Valores válidos                                            |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| Botón de grosor del marcador      | 1 px                                                                                                                                  | Off, 1 px, 3 px                                         |
| Botón ADSP (pestaña DSP)        | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de un conmutador DSP del lado de la radio pero no marcable. Al hacer clic se eleva y enfoca el diálogo modeless de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP TX/RX (v0.9.8).                                                     | Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú / cadena para la tira.                 |

Cada clic avanza al siguiente valor en el ciclo: **Off** → **1 px** → **3 px** → **Off**. La configuración se conserva por slice, de modo que el slice 1 y el slice 2 pueden tener grosores diferentes.

## Consejos

- Configurar el marcador en **Off** oculta la línea vertical por completo. El panel VFO y la bandera permanecen visibles y funcionales.
- Si ejecuta varios slices en el mismo panadapter, aumentar un marcador a **3 px** puede ayudar a distinguirlo de los slices adyacentes.

## Cambios en la pestaña DSP en v0.9.8

La pestaña DSP en el panel VFO ahora muestra solo los botones de reducción de ruido suministrados por la radio. Los siguientes botones se han eliminado de la pestaña DSP del panel VFO:

| Botón eliminado | Dónde encontrarlo ahora |
|---|---|
| NR2 | Menú superpuesto del espectro o applet AetherDSP |
| RN2 | Menú superpuesto del espectro o applet AetherDSP |
| BNR | Menú superpuesto del espectro o applet AetherDSP |
| NR4 | Menú superpuesto del espectro o applet AetherDSP |
| MNR | Menú superpuesto del espectro o applet AetherDSP |
| DFNR | Menú superpuesto del espectro o applet AetherDSP |

Los botones restantes de la pestaña DSP están dispuestos en una cuadrícula de cuatro columnas:

| Fila | Col 0 | Col 1 | Col 2 | Col 3 |
|---|---|---|---|---|
| 0 | NR | NB | ANF | APF |
| 1 | NRL | NRS | RNN | NRF |
| 2 | ANFL | ANFT | MN | ADSP | 
| 3 | AetherVoice (2 col) | | | |

El botón APF permanece oculto a menos que el slice esté en modo CW. El botón MN (Manual Notch) se muestra solo en radios que declaran soporte de muesca manual.

Dos botones de lanzamiento del lado del cliente aparecen en la cuadrícula:
- **ADSP** — Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Este botón tiene el estilo de un conmutador DSP del lado de la radio pero no es marcable. Al hacer clic se eleva y enfoca el diálogo modeless de configuración de AetherDSP.
- **AetherVoice** — Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP TX/RX (v0.9.8). Este botón abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú / cadena para la tira.

### Control deslizante de nivel DSP

Una fila de control deslizante compartido aparece debajo de la cuadrícula de botones DSP. El control deslizante se redirige automáticamente al botón DSP con nivel habilitado más recientemente. La etiqueta de la fila se actualiza para mostrar el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha del control deslizante.

La fila está siempre presente en el diseño. Cuando no hay DSP con nivel activo — o cuando solo RNN, ANFT o APF está encendido — la fila se desvanece a transparente. Se vuelve completamente visible tan pronto como se enciende un DSP con nivel.

El control deslizante controla el nivel para estos objetivos:

| Etiqueta del objetivo | DSP controlado |
|---|---|
| NR | Nivel de reducción de ruido |
| NB | Nivel de supresor de ruido |
| ANF | Nivel de filtro de muesca automático |
| NRL | Nivel de reducción de ruido (NRL) |
| NRS | Nivel de sustracción espectral |
| NRF | Nivel de filtro de ruido espectral |
| ANFL | Nivel de filtro de muesca LMS |
| MN | Nivel de filtro de muesca manual |

## Comportamiento del control de squelch

El botón y el control deslizante de squelch en la pestaña Audio están deshabilitados en modos digital, RTTY y CW. Los modos digital y RTTY envían audio a decodificadores externos a través de DAX, donde el squelch no es significativo y puede bloquear señales FSK débiles. La radio bloquea el squelch encendido a un nivel fijo en modo CW y rechaza cambios. Al cambiar a uno de estos modos mientras el squelch está habilitado, el squelch se deshabilita automáticamente y el estado guardado se conserva en la radio para cuando vuelva a un modo de voz.

## Comportamiento de inicio de DSP (v0.9.8)

Cuando AetherSDR se conecta a la radio, cualquier DSP que estuviera habilitado en el perfil guardado de la radio ahora envía inmediatamente su nivel al control deslizante de nivel DSP compartido. Anteriormente, el control deslizante faltaba al iniciar para estos DSP hasta que el usuario los alternaba manualmente. Esta corrección garantiza que el control deslizante esté siempre presente y activo cuando un DSP con nivel ya está habilitado en la radio.

## Corrección de la etiqueta de ancho de filtro (v0.9.8)

La etiqueta de ancho de filtro en el panel VFO ahora usa una única fuente de verdad (`RxApplet::formatFilterWidth`) para generar su lectura. Esto corrige un desfase de 0.1 kHz que afectaba las lecturas en modos SSB y digital, y garantiza que el panel VFO y el applet RX muestren valores idénticos de ancho de filtro.

## Mejoras en la selección de antena (v26.5.2.1)

Los botones de antena RX y TX ahora usan listas de antenas por slice cuando están disponibles, recurriendo a la lista global de antenas. El menú de antena TX excluye los puertos solo de RX verificando patrones de nomenclatura específicos.

### Selección de antena RX

1. Abra el panel VFO del slice objetivo.
2. Haga clic en el **botón de antena RX**. Se abre un menú que muestra las antenas de recepción disponibles.
3. Seleccione una antena del menú. El slice usa inmediatamente la antena seleccionada para recepción.

El menú muestra la lista de antenas de recepción por slice si está disponible. Cada entrada tiene una información sobre herramientas que muestra el identificador completo del puerto de antena.

### Selección de antena TX

1. Abra el panel VFO del slice objetivo.
2. Haga clic en el **botón de antena TX**. Se abre un menú que muestra las antenas que se pueden usar para transmitir.
3. Seleccione una antena del menú. El slice usa inmediatamente la antena seleccionada para transmisión.

El menú filtra los puertos de antena que comienzan con "RX" para evitar seleccionar puertos solo de RX para transmisión. Cada entrada tiene una información sobre herramientas que muestra el identificador completo del puerto de antena.

## Mejoras en la entrada de frecuencia (v26.5.3)

### Comportamiento de entrada directa de frecuencia cuando el slice está bloqueado

Cuando un slice está bloqueado, intentar comenzar la entrada directa de frecuencia haciendo clic en la pantalla de frecuencia está bloqueado. El campo de entrada directa no aparece. Si una entrada directa ya está en progreso cuando el slice se bloquea, la entrada se cancela y la pantalla vuelve a mostrar la frecuencia bloqueada. Una superposición visual "LOCKED" se muestra centralmente a través del modelo del slice.

### Entrada de frecuencia en bandas XVTR (v26.5.2.1)

Al ingresar frecuencias en bandas de transvertidor (XVTR), la frecuencia máxima admitida se ha aumentado de 450 MHz a 50,000 MHz. La lógica automática de inserción decimal ahora solo se aplica a bandas de tres dígitos (100–999 MHz) cuando el valor ingresado supera 450 MHz. Para bandas superiores (1,000 MHz y más), los enteros sin decimales se interpretan como MHz sin inserción decimal.

### Entrada explícita en MHz en bandas HF (v26.5.3)

Al ingresar una frecuencia en bandas HF, ingresar un valor mayor que 54 MHz con un punto decimal explícito (por ejemplo, "144.200") ahora se interpreta como MHz en lugar de dividirse automáticamente por 1,000 (kHz) o 1,000,000 (Hz). Esto permite la entrada directa en MHz para frecuencias VHF/UHF incluso cuando no se está en una banda XVTR.

## Sintonización con rueda de desplazamiento en modo colapsado (v26.5.3)

En modo colapsado, la rueda de desplazamiento ahora sintoniza el slice incluso cuando el slice está bloqueado. Cuando se desplaza el slice bloqueado, se muestra una notificación visual "LOCKED" para indicar que la sintonización fue bloqueada. Anteriormente, el modo colapsado ignoraba los eventos de desplazamiento cuando el slice estaba bloqueado.

## Agregar spot con clic derecho en modo colapsado (v26.8.4)

Hacer clic derecho en la etiqueta de frecuencia en modo colapsado ahora abre correctamente el menú contextual **Add Spot**. Anteriormente, los clics pasaban al SpectrumWidget subyacente, que informaba la frecuencia ajustada al paso del cursor en lugar de la del VFO. La etiqueta de frecuencia colapsada ahora intercepta el evento, por lo que el spot siempre se agrega en la frecuencia del VFO.

## Corrección de altura de la pila de pestañas (v26.5.3)

El área de contenido de las pestañas del panel VFO ahora informa solo el tamaño preferido de la página de pestaña actual, en lugar del máximo de todas las páginas. Esto corrige un espacio de altura que ocurría cuando la pestaña DSP era más alta que la pestaña Mode (por ejemplo, cuando el contenedor de sub-modo digital estaba visible en modo DIGU o DIGL).

## Soporte HTML en la insignia de slice (v26.5.2.1)

La insignia de slice que muestra la letra del slice ahora puede representar texto enriquecido. Esto permite futuras mejoras donde se puedan usar caracteres no ASCII o texto con estilo para la identificación del slice.

## Visual de la marca central del control deslizante Pan (v26.6.1)

El control deslizante Pan en la pestaña Audio ahora llena su canal desde el centro hacia afuera en lugar de desde el borde izquierdo. Se dibuja un pequeño punto de marca central en el canal en la posición neutral (50) para que el operador pueda ver el punto medio de un vistazo.

Este cambio corrige la lectura visual del control de panorama L/R — la porción llena ahora representa con precisión la cantidad de panorama alejado del centro, coincidiendo con la expectativa del operador para controles anclados al centro.

## Descripción general del panel VFO

El panel VFO es un panel de control flotante por slice anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a las configuraciones por slice más utilizadas sin salir de la vista del espectro. El panel contiene pestañas para configuraciones de Audio, DSP, Mode, X/RIT y DAX, además de una tira de S-meter y controles de colapso.

### Tira de S-meter y sombra de la bandera VFO

La bandera del panel VFO (el panel flotante en sí) ahora incluye una superficie de sombra ligera separada del widget VFO principal. Esto significa que los repintados del S-meter en vivo no vuelven a desenfocar toda la bandera a la velocidad de animación. La sombra se renderiza usando un algoritmo de desenfoque de caja y se actualiza solo cuando cambia la geometría de la bandera.

Debajo de los controles con pestañas, cada panel VFO contiene una tira de S-meter. La tira de S-meter usa un widget de medidor inteligente que mantiene una relación de aspecto fija. La pila de pestañas del panel VFO reenvía la altura-por-ancho de la página actual, permitiendo que el S-meter impulse la altura de la tira cuando es la fila de pestaña activa.

### Insignias de slice

El panel VFO muestra insignias para indicar el estado del slice:

| Insignia | Estados | Significado |
|---|---|---|
| Insignia TX | TX (rojo), oculta | Se muestra cuando este slice es el slice de transmisión activo. |
| Insignia SPLIT | SPLIT (ámbar), oculta | Se muestra cuando TX está asignado a un slice diferente del slice de recepción activo. |

### Controles

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| Botón de antena RX | push_button | - | Abre el menú de selección de antena para la antena de recepción de este slice. |
| Botón de antena TX | push_button | - | Abre el menú de selección de antena para la antena de transmisión de este slice. |
| Pantalla de frecuencia | indicator | - | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. La entrada directa está bloqueada cuando el slice está bloqueado. Usa un widget `FreqLineEdit` para el campo de edición con texto de sugerencia "MHz (e.g. 14.225)". |
| Etiqueta de ancho de filtro | indicator | - | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode. Usa una única fuente de verdad (`RxApplet::formatFilterWidth`) para generar su lectura. |
| Control deslizante AF Gain (pestaña Audio) | slider | 100 | Establece el nivel de salida de audio para este slice. Rango 0-100. |
| Control deslizante Pan (pestaña Audio) | slider | 50 | Establece el panorama estéreo izquierdo/derecho para este slice. 50 = centro. Rango 0-100. El canal se llena desde el centro hacia afuera con un punto de marca central en la posición neutral. |
| Botón Mute (pestaña Audio) | toggle_button | off | Silencia la salida de audio para este slice sin cambiar la configuración de ganancia AF. Haga clic derecho en la etiqueta de la pesta
