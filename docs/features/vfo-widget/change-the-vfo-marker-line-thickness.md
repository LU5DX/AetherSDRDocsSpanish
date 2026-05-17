# Cambiar el grosor de la línea del marcador VFO

Utilice el botón de grosor del marcador para controlar la prominencia de la línea del marcador VFO en la visualización del espectro, o para ocultarla por completo. La configuración se guarda por slice.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO debe estar abierto para el slice que desea ajustar. Si no está visible, haga clic en la bandera del marcador VFO de ese slice en la visualización del espectro.

## Pasos

1. Abra el panel VFO del slice deseado haciendo clic en su bandera de marcador VFO en la visualización del espectro.
2. Localice el **Botón de grosor del marcador** en el panel VFO.
3. Haga clic en el botón para recorrer cíclicamente los valores disponibles: **Off**, **1 px** y **3 px**.
4. Deje de hacer clic cuando se muestre el grosor deseado. El marcador en la visualización del espectro se actualiza inmediatamente.

## Qué hace cada control

| Control                      | Valor predeterminado | Valores válidos                                            |
|------------------------------|----------------------|------------------------------------------------------------|
| Botón de grosor del marcador | 1 px                 | Off, 1 px, 3 px                                            |
| Botón ADSP (pestaña DSP)     | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de un conmutador DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo AetherDSP Settings no modal. |
| Botón AetherVoice (pestaña DSP) | Activa/desactiva la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

Cada clic avanza al siguiente valor en el ciclo: **Off** → **1 px** → **3 px** → **Off**. La configuración se conserva por slice, por lo que el slice 1 y el slice 2 pueden tener grosores diferentes.

## Consejos

- Configurar el marcador en **Off** oculta la línea vertical por completo. El panel VFO y la bandera permanecen visibles y funcionales.
- Si ejecuta varios slices en el mismo panadapter, aumentar un marcador a **3 px** puede ayudar a distinguirlo de los slices adyacentes.

## Cambios en la pestaña DSP en v0.9.8

La pestaña DSP en el panel VFO ahora muestra solo los botones de reducción de ruido proporcionados por la radio. Los siguientes botones se han eliminado de la pestaña DSP del panel VFO:

| Botón eliminado | Dónde encontrarlo ahora                     |
|-----------------|---------------------------------------------|
| NR2             | Menú de superposición del espectro o applet AetherDSP |
| RN2             | Menú de superposición del espectro o applet AetherDSP |
| BNR             | Menú de superposición del espectro o applet AetherDSP |
| NR4             | Menú de superposición del espectro o applet AetherDSP |
| MNR             | Menú de superposición del espectro o applet AetherDSP |
| DFNR            | Menú de superposición del espectro o applet AetherDSP |

Los botones restantes de la pestaña DSP están dispuestos en una cuadrícula de cuatro columnas:

| Fila | Col 0 | Col 1 | Col 2 | Col 3 |
|------|-------|-------|-------|-------|
| 0    | NR    | NB    | ANF   | APF   |
| 1    | NRL   | NRS   | RNN   | NRF   |
| 2    | ANFL  | ANFT  | ADSP  | AetherVoice (2 cols) |

El botón APF permanece oculto a menos que el slice esté en modo CW.

Aparecen dos nuevos botones de lanzamiento del lado del cliente en la fila 2 de la cuadrícula:
- **ADSP** — Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Este botón tiene el estilo de un conmutador DSP del lado de la radio pero no es seleccionable. Al hacer clic, abre y enfoca el diálogo AetherDSP Settings no modal.
- **AetherVoice** — Activa/desactiva la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8). Este botón ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira.

### Deslizador de nivel DSP

Una fila de deslizador de nivel compartido aparece debajo de la cuadrícula de botones DSP. El deslizador se reorienta automáticamente al botón DSP con nivel que se habilitó más recientemente. La etiqueta de la fila se actualiza para mostrar el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha del deslizador.

La fila siempre está presente en el diseño. Cuando no hay ningún DSP con nivel activo, o cuando solo RNN, ANFT o APF están encendidos, la fila se desvanece a transparente. Se vuelve completamente visible tan pronto como se activa un DSP con nivel.

El deslizador controla el nivel de estos objetivos:

| Etiqueta del objetivo | DSP controlado                   |
|------------------------|----------------------------------|
| NR                     | Nivel de reducción de ruido      |
| NB                     | Nivel de eliminador de ruido     |
| ANF                    | Nivel de filtro de muesca automático |
| NRL                    | Nivel de reducción de ruido (NRL) |
| NRS                    | Nivel de sustracción espectral   |
| NRF                    | Nivel de filtro de ruido espectral |
| ANFL                   | Nivel de filtro de muesca LMS    |

## Comportamiento del control de squelch

El botón y el deslizador de squelch en la pestaña Audio están deshabilitados en los modos digital, RTTY y CW. Los modos digital y RTTY envían audio a decodificadores externos a través de DAX, donde el squelch no tiene sentido y puede bloquear señales débiles FSK. La radio bloquea el squelch en un nivel fijo en modo CW y rechaza los cambios. Al cambiar a uno de estos modos mientras el squelch está habilitado, el squelch se desactiva automáticamente y el estado guardado se conserva en la radio para cuando vuelva a un modo de voz.

## Comportamiento de inicio del DSP (v0.9.8)

Cuando AetherSDR se conecta a la radio, cualquier DSP que estuviera habilitado en el perfil guardado de la radio ahora envía inmediatamente su nivel al deslizador de nivel DSP compartido. Anteriormente, el deslizador faltaba al inicio para estos DSP hasta que el usuario los activaba manualmente. Esta corrección asegura que el deslizador siempre esté presente y activo cuando un DSP con nivel ya está habilitado en la radio.

## Corrección de la etiqueta de ancho de filtro (v0.9.8)

La etiqueta de ancho de filtro en el panel VFO ahora utiliza una única fuente de verdad (`RxApplet::formatFilterWidth`) para generar su lectura. Esto corrige un desfase de 0,1 kHz que afectaba las lecturas en modo SSB y digital, y asegura que el panel VFO y el applet RX muestren valores de ancho de filtro idénticos.

## Mejoras en la selección de antena (v26.5.2.1)

Los botones de antena RX y TX ahora utilizan listas de antenas por slice cuando están disponibles, recurriendo a la lista de antenas global. El menú de antena TX excluye los puertos solo de RX verificando patrones de nomenclatura específicos.

### Selección de antena RX

1. Abra el panel VFO para el slice deseado.
2. Haga clic en el **botón de antena RX**. Se abre un menú que muestra las antenas de recepción disponibles.
3. Seleccione una antena del menú. El slice utiliza inmediatamente la antena seleccionada para recibir.

El menú muestra la lista de antenas de recepción por slice si está disponible. Cada entrada tiene una información sobre herramientas que muestra el identificador completo del puerto de antena.

### Selección de antena TX

1. Abra el panel VFO para el slice deseado.
2. Haga clic en el **botón de antena TX**. Se abre un menú que muestra las antenas que se pueden usar para transmitir.
3. Seleccione una antena del menú. El slice utiliza inmediatamente la antena seleccionada para transmitir.

El menú filtra los puertos de antena que comienzan con "RX" para evitar seleccionar puertos solo de RX para transmitir. Cada entrada tiene una información sobre herramientas que muestra el identificador completo del puerto de antena.

## Introducción de frecuencia en bandas XVTR (v26.5.2.1)

Al introducir frecuencias en bandas de transvertidor (XVTR), la frecuencia máxima admitida se ha incrementado de 450 MHz a 50 000 MHz. La lógica de inserción automática de decimales ahora solo se aplica a bandas de tres dígitos (100-999 MHz) cuando el valor introducido supera los 450 MHz. Para bandas superiores (1 000 MHz y más), los enteros simples se interpretan como MHz sin inserción de decimales.

## Soporte HTML para insignias de slice (v26.5.2.1)

La insignia de slice que muestra la letra del slice ahora puede representar texto enriquecido. Esto permite futuras mejoras donde se puedan usar caracteres no ASCII o texto con estilo para la identificación del slice.

## Resumen del panel VFO

El panel VFO es un panel de control flotante por slice anclado al marcador VFO en la visualización del espectro. Proporciona acceso rápido a las configuraciones por slice más utilizadas sin salir de la vista del espectro.

### Controles

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| Botón de antena RX | push_button | - | Abre el menú de selección de antena para la antena de recepción de este slice. |
| Botón de antena TX | push_button | - | Abre el menú de selección de antena para la antena de transmisión de este slice. |
| Visualización de frecuencia | indicator | - | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la introducción directa de frecuencia; escriba MHz y presione Enter o Tab. |
| Etiqueta de ancho de filtro | indicator | - | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. |
| Deslizador de ganancia AF (pestaña Audio) | slider | 100 | Establece el nivel de salida de audio para este slice. Rango 0-100. |
| Deslizador de paneo (pestaña Audio) | slider | 50 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. Rango 0-100. |
| Botón de silencio (pestaña Audio) | toggle_button | off | Silencia la salida de audio de este slice sin cambiar la configuración de ganancia AF. |
| Botón + deslizador de squelch (pestaña Audio) | toggle_button | off | Habilita el squelch para este slice. El deslizador adyacente establece el umbral. Rango 0-100. |
| Combo AGC (pestaña Audio) | combo_box | FAST | Establece la velocidad de ataque/liberación del AGC para este slice. Opciones: FAST, MED, SLOW, OFF. |
| Combo Mode (pestaña Mode) | combo_box | USB | Establece el modo de demodulación para este slice. Opciones: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY. |
| Botones de preajuste de filtro (pestaña Mode) | push_button | - | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | toggle_button | off | Habilita la sintonización incremental del receptor (RIT) o del transmisor (XIT). La rueda de desplazamiento ajusta en pasos de 10 Hz. |
| Combo de canal DAX (pestaña DAX) | combo_box | Off | Asigna un canal de audio DAX a este slice. Opciones: Off, 1-8. |
| Botón de grosor del marcador | push_button | 1 px | Recorre cíclicamente la línea del marcador VFO entre Off, 1 px y 3 px. |
| Botón de bordes de filtro | toggle_button | shown | Alterna las líneas de borde del filtro en la banda de paso del espectro. |
| Alternar colapso | toggle_button | expanded | Colapsa el panel VFO a una tira compacta solo de frecuencia. |

### Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Insignia TX | TX (rojo), oculta | Se muestra cuando este slice es el slice de transmisión activo. |
| Insignia SPLIT | SPLIT (ámbar), oculta | Se muestra cuando TX está asignado a un slice diferente al slice de recepción activo. |

## Relacionados

- [Ocultar o mostrar las líneas de borde del filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Colapsar el panel VFO a la vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Resumen del panel VFO](overview.md)
