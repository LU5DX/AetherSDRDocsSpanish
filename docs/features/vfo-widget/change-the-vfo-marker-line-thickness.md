# Cambiar el Grosor de la Línea del Marcador VFO

Utilice el botón de grosor del marcador para controlar la prominencia de la línea del marcador VFO en la pantalla del espectro, o para ocultarla por completo. La configuración se guarda por slice.

## Antes de empezar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El panel VFO debe estar abierto para el slice que desea ajustar. Si no está visible, haga clic en la bandera del marcador VFO de ese slice en la pantalla del espectro.

## Pasos

1. Abra el panel VFO para el slice objetivo haciendo clic en su bandera del marcador VFO en la pantalla del espectro.
2. Localice el **Botón de grosor del marcador** en el panel VFO.
3. Haga clic en el botón para recorrer los valores disponibles: **Off**, **1 px** y **3 px**.
4. Deje de hacer clic cuando se muestre el grosor deseado. El marcador en la pantalla del espectro se actualiza inmediatamente.

## Qué hace cada control

| Control                      | Predeterminado | Valores válidos                               |
|------------------------------|----------------|-----------------------------------------------|
| Botón de grosor del marcador | 1 px           | Off, 1 px, 3 px                               |
| Botón ADSP (pestaña DSP)     | Abre el cuadro de diálogo AetherDSP Settings (NR2/NR4/DFNR/RN2/BNR/MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de conmutador DSP del lado del radio pero no seleccionable. Al hacer clic, abre y enfoca el cuadro de diálogo no modal AetherDSP Settings. |
| Botón AetherVoice (pestaña DSP) | Activa o desactiva la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

Cada clic avanza al siguiente valor en el ciclo: **Off** → **1 px** → **3 px** → **Off**. La configuración se conserva por slice, por lo que el slice 1 y el slice 2 pueden tener grosores diferentes.

## Consejos

- Establecer el marcador en **Off** oculta la línea vertical por completo. El panel VFO y la bandera permanecen visibles y funcionales.
- Si utiliza varios slices en el mismo panadapter, aumentar un marcador a **3 px** puede ayudar a distinguirlo de los slices adyacentes.

## Cambios en la pestaña DSP en v0.9.8

La pestaña DSP en el panel VFO ahora muestra solo los botones de reducción de ruido suministrados por el radio. Los siguientes botones se han eliminado de la pestaña DSP del panel VFO:

| Botón eliminado | Dónde encontrarlo ahora                           |
|-----------------|---------------------------------------------------|
| NR2             | Menú superpuesto del espectro o applet AetherDSP  |
| RN2             | Menú superpuesto del espectro o applet AetherDSP  |
| BNR             | Menú superpuesto del espectro o applet AetherDSP  |
| NR4             | Menú superpuesto del espectro o applet AetherDSP  |
| MNR             | Menú superpuesto del espectro o applet AetherDSP  |
| DFNR            | Menú superpuesto del espectro o applet AetherDSP  |

Los botones restantes de la pestaña DSP están organizados en una cuadrícula de cuatro columnas:

| Fila | Col 0 | Col 1 | Col 2 | Col 3 |
|------|-------|-------|-------|-------|
| 0    | NR    | NB    | ANF   | APF   |
| 1    | NRL   | NRS   | RNN   | NRF   |
| 2    | ANFL  | ANFT  | ADSP  | AetherVoice (2 cols) |

El botón APF permanece oculto a menos que el slice esté en modo CW.

Aparecen dos nuevos botones de inicio del lado del cliente en la fila 2 de la cuadrícula:
- **ADSP** — Abre el cuadro de diálogo AetherDSP Settings (NR2/NR4/DFNR/RN2/BNR/MNR del lado del cliente). Este botón tiene el estilo de un conmutador DSP del lado del radio, pero no es seleccionable. Al hacer clic, abre y enfoca el cuadro de diálogo no modal AetherDSP Settings.
- **AetherVoice** — Activa o desactiva la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8). Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira.

### Control deslizante de nivel DSP

Una fila de control deslizante de nivel compartido aparece debajo de la cuadrícula de botones DSP. El control deslizante se reorienta automáticamente al botón DSP con nivel que se haya habilitado más recientemente. La etiqueta de la fila se actualiza para mostrar el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha del control deslizante.

La fila siempre está presente en el diseño. Cuando ningún DSP con nivel está activo, o cuando solo RNN, ANFT o APF están activados, la fila se desvanece a transparente. Se vuelve completamente visible tan pronto como se activa un DSP con nivel.

El control deslizante controla el nivel para estos objetivos:

| Etiqueta del objetivo | DSP controlado                               |
|-----------------------|-----------------------------------------------|
| NR                    | Nivel de reducción de ruido                   |
| NB                    | Nivel del eliminador de ruido                 |
| ANF                   | Nivel del filtro de muesca automático         |
| NRL                   | Nivel de reducción de ruido (NRL)             |
| NRS                   | Nivel de sustracción espectral                |
| NRF                   | Nivel del filtro de ruido espectral           |
| ANFL                  | Nivel del filtro de muesca LMS               |

## Comportamiento del control de squelch

El botón y el control deslizante de squelch en la pestaña Audio están deshabilitados en los modos digital, RTTY y CW. Los modos digital y RTTY envían audio a decodificadores externos a través de DAX, donde el squelch no tiene sentido y puede bloquear señales FSK débiles. El radio bloquea el squelch activado en un nivel fijo en el modo CW y rechaza los cambios. Al cambiar a uno de estos modos mientras el squelch está habilitado, este se deshabilita automáticamente y el estado guardado se conserva en el radio para cuando vuelva a un modo de voz.

## Comportamiento de inicio de DSP (v0.9.8)

Cuando AetherSDR se conecta al radio, cualquier DSP que estuviera habilitado en el perfil guardado del radio ahora envía inmediatamente su nivel al control deslizante de nivel DSP compartido. Anteriormente, el control deslizante faltaba al inicio para estos DSP hasta que el usuario los activaba manualmente. Esta corrección garantiza que el control deslizante esté siempre presente y activo cuando un DSP con nivel ya está habilitado en el radio.

## Corrección de la etiqueta de ancho de filtro (v0.9.8)

La etiqueta de ancho de filtro en el panel VFO ahora utiliza una única fuente de verdad (`RxApplet::formatFilterWidth`) para generar su lectura. Esto corrige un desfase de 0,1 kHz que afectaba las lecturas en los modos SSB y digital, y garantiza que el panel VFO y el applet RX muestren valores de ancho de filtro idénticos.

## Mejoras en la selección de antena (v26.5.2.1)

Los botones de antena RX y TX ahora utilizan listas de antenas por slice cuando están disponibles, recurriendo a la lista de antenas global. El menú de antena TX excluye los puertos solo de RX verificando patrones de nombres específicos.

### Selección de antena RX

1. Abra el panel VFO para el slice objetivo.
2. Haga clic en el **botón de antena RX**. Se abre un menú que muestra las antenas de recepción disponibles.
3. Seleccione una antena del menú. El slice utiliza inmediatamente la antena seleccionada para la recepción.

El menú muestra la lista de antenas de recepción por slice si está disponible. Cada entrada tiene una información sobre herramientas que muestra el identificador completo del puerto de antena.

### Selección de antena TX

1. Abra el panel VFO para el slice objetivo.
2. Haga clic en el **botón de antena TX**. Se abre un menú que muestra las antenas que se pueden usar para transmitir.
3. Seleccione una antena del menú. El slice utiliza inmediatamente la antena seleccionada para la transmisión.

El menú filtra los puertos de antena que comienzan con "RX" para evitar seleccionar puertos solo de RX para la transmisión. Cada entrada tiene una información sobre herramientas que muestra el identificador completo del puerto de antena.

## Mejoras en la entrada de frecuencia (v26.5.3)

### Comportamiento de entrada directa de frecuencia cuando el slice está bloqueado

Cuando un slice está bloqueado, se bloquea el intento de iniciar la entrada directa de frecuencia haciendo clic en la pantalla de frecuencia. El campo de entrada directa no aparece. Si una entrada directa ya está en progreso cuando se bloquea el slice, la entrada se cancela y la pantalla vuelve a mostrar la frecuencia bloqueada. Se muestra una superposición visual "LOCKED" de forma centralizada a través del modelo del slice.

### Entrada de frecuencia en bandas XVTR (v26.5.2.1)

Al introducir frecuencias en bandas de transvertedor (XVTR), la frecuencia máxima compatible se ha incrementado de 450 MHz a 50.000 MHz. La lógica de inserción decimal automática ahora solo se aplica a bandas de tres dígitos (100–999 MHz) cuando el valor introducido supera los 450 MHz. Para bandas superiores (1.000 MHz y más), los números enteros se interpretan como MHz sin inserción decimal.

### Entrada explícita de MHz en bandas HF (v26.5.3)

Al introducir una frecuencia en bandas HF, un valor superior a 54 MHz con un punto decimal explícito (por ejemplo, "144.200") ahora se interpreta como MHz en lugar de dividirse automáticamente por 1.000 (kHz) o 1.000.000 (Hz). Esto permite la entrada directa de MHz para frecuencias VHF/UHF incluso cuando no se está en una banda XVTR.

## Sintonización con rueda de desplazamiento en modo contraído (v26.5.3)

En el modo contraído, la rueda de desplazamiento ahora sintoniza el slice incluso cuando el slice está bloqueado. Cuando se desplaza el slice bloqueado, se muestra una notificación visual "LOCKED" para indicar que la sintonización fue bloqueada. Anteriormente, el modo contraído ignoraba los eventos de desplazamiento cuando el slice estaba bloqueado.

## Corrección de altura de la pila de pestañas (v26.5.3)

El área de contenido de pestañas del panel VFO ahora informa solo el tamaño preferido de la página de pestaña actual, en lugar del máximo de todas las páginas. Esto corrige un espacio de altura que ocurría cuando la pestaña DSP era más alta que la pestaña Mode (por ejemplo, cuando el contenedor de submodo digital estaba visible en el modo DIGU o DIGL).

## Soporte HTML en la insignia del slice (v26.5.2.1)

La insignia del slice que muestra la letra del slice ahora puede representar texto enriquecido. Esto permite futuras mejoras donde se puedan usar caracteres no ASCII o texto con estilo para la identificación del slice.

## Indicador visual del punto central del control deslizante Pan (v26.6.1)

El control deslizante Pan en la pestaña Audio ahora llena su ranura desde el centro hacia afuera en lugar de desde el borde izquierdo. Se pinta un pequeño punto de marca central en la ranura en la posición neutral (50) para que el operador pueda ver el punto medio de un vistazo.

Este cambio corrige la lectura visual del control de paneo L/R — la porción llena ahora representa con precisión la cantidad de paneo desde el centro, coincidiendo con la expectativa del operador para los controles anclados al centro.

## Descripción general del panel VFO

El panel VFO es un panel de control flotante por slice anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a las configuraciones por slice más utilizadas sin salir de la vista del espectro. El panel contiene pestañas para configuraciones de Audio, DSP, Mode, X/RIT y DAX, además de una tira del S-meter y controles de contracción.

### Sombra de la bandera VFO y tira del S-meter

La bandera del panel VFO (el propio panel flotante) ahora incluye una superficie de sombra ligera que está separada del widget VFO principal. Esto significa que las repintadas en vivo del S-meter no vuelven a desenfocar toda la bandera a la velocidad de animación. La sombra se representa mediante un algoritmo de desenfoque de caja y solo se actualiza cuando la geometría de la bandera cambia.

Debajo de los controles con pestañas, cada panel VFO contiene una tira del S-meter. La tira del S-meter utiliza un widget de medidor inteligente que mantiene una relación de aspecto fija. La pila de pestañas del panel VFO reenvía la altura en función del ancho desde la página actual, lo que permite que el S-meter impulse la altura de la tira cuando es la fila de pestañas activa.

### Insignias del slice

El panel VFO muestra insignias para indicar el estado del slice:

| Insignia    | Estados                | Significado                                                  |
|-------------|------------------------|--------------------------------------------------------------|
| Insignia TX | TX (rojo), oculto      | Se muestra cuando este slice es el slice de transmisión activo. |
| Insignia SPLIT | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un slice diferente al slice de recepción activo. |

### Controles

| Control                           | Tipo                 | Predeterminado | Comportamiento                                               |
|------------------------------------|----------------------|----------------|--------------------------------------------------------------|
| Botón de antena RX                 | botón pulsador       | -              | Abre el menú de selección de antena para la antena de recepción de este slice. |
| Botón de antena TX                 | botón pulsador       | -              | Abre el menú de selección de antena para la antena de transmisión de este slice. |
| Pantalla de frecuencia             | indicador            | -              | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. La entrada directa se bloquea cuando el slice está bloqueado. Utiliza un widget `FreqLineEdit` para el campo de edición con el texto de sugerencia "MHz (e.g. 14.225)". |
| Etiqueta de ancho de filtro         | indicador            | -              | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos del filtro en la pestaña Mode. Utiliza una única fuente de verdad (`RxApplet::formatFilterWidth`) para generar su lectura. |
| Control deslizante de ganancia AF (pestaña Audio) | control deslizante | 100            | Establece el nivel de salida de audio para este slice. Rango 0-100. |
| Control deslizante Pan (pestaña Audio) | control deslizante | 50             | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. Rango 0-100. La ranura se llena desde el centro hacia afuera con un punto de marca central en la posición neutral. |
| Botón de silencio (pestaña Audio)    | botón de conmutación | off            | Silencia la salida de audio de este slice sin cambiar la configuración de ganancia AF. Haga clic derecho en la etiqueta de la pestaña Audio para activar/desactivar el silencio directamente. |
| Botón y control deslizante de squelch (pestaña Audio) | bot
