# Aplicar un ancho de filtro predefinido desde el panel VFO

Los botones de ajustes predefinidos de filtro le permiten cambiar el ancho del filtro de recepción de un slice con un solo clic. Úselos para moverse rápidamente entre anchos de banda comunes — por ejemplo, entre un filtro SSB ancho de 3 kHz y un filtro CW estrecho de 500 Hz — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO del slice objetivo debe estar abierto y expandido. Si está colapsado a una tira que solo muestra la frecuencia, haga clic en cualquier parte de él para expandirlo primero.

## Pasos

1. Haga clic en la marca del indicador VFO en la pantalla del espectro para el slice que desea ajustar. El panel VFO se abre, anclado a la izquierda de la marca.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el botón de ajuste predefinido de filtro que corresponda al ancho de banda que desea. La radio aplica inmediatamente ese ancho de filtro al slice.

Para guardar el ancho de filtro actual en una ranura de ajuste predefinido:

1. Ajuste el filtro al ancho de banda que desea guardar (consulte [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)).
2. Haga clic derecho en la ranura del botón de ajuste predefinido que desea sobrescribir.
3. El ancho de filtro actual se guarda en esa ranura.

## Qué hace cada control

| Control                          | Comportamiento                                                                                                                                                                                                                                        | Valor predeterminado                                                                                                   |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Botón de antena RX               | Abre un menú de selección de antena para la antena receptora de este slice. Utiliza la lista de antenas específica del slice cuando está disponible. Los elementos del menú muestran información sobre herramientas y sugerencia de estado.                | —                                                                                                                      |
| Botón de antena TX               | Abre un menú de selección de antena para la antena transmisora de este slice. Filtra automáticamente los puertos de antena solo de recepción. Los elementos del menú muestran información sobre herramientas y sugerencia de estado.                      | —                                                                                                                      |
| Visualización de frecuencia      | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. La entrada directa está bloqueada cuando el slice está bloqueado.                                            | —                                                                                                                      |
| Etiqueta de ancho de filtro      | Muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones de ajustes predefinidos de filtro en la pestaña Mode. Utiliza RxApplet::formatFilterWidth como fuente única de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8).                |                                                                                                                        |
| Deslizador de ganancia AF (pestaña Audio) | Establece el nivel de salida de audio para este slice (0-100).                                                                                                                                                                                           | 100                                                                                                                    |
| Deslizador Pan (pestaña Audio)   | Establece la panoramización estéreo izquierda/derecha para este slice (0-100). 50 = centro. El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central en la ranura que muestra la posición neutra.                     | 50                                                                                                                     |
| Botón de silencio (pestaña Audio) | Silencia la salida de audio de este slice sin cambiar la configuración de ganancia AF. Haga clic derecho en el botón de la pestaña Audio para alternar el silencio directamente.                                                                          | desactivado                                                                                                            |
| Botón + deslizador de squelch (pestaña Audio) | Habilita el squelch para este slice. El deslizador adyacente establece el umbral (0-100). Deshabilitado para RTTY y modos digitales (DIGU, DIGL).                                                                                                          | desactivado                                                                                                            |
| Combinación AGC (pestaña Audio)  | Establece la velocidad de ataque/liberación del AGC para este slice. Opciones: FAST, MED, SLOW, OFF.                                                                                                                                                   | FAST                                                                                                                   |
| Botones NR / NB / ANF / APF / NRL / NRS / RNN / NRF / ANFL / ANFT (pestaña DSP) | Habilita el algoritmo de reducción de ruido o filtrado del lado de la radio correspondiente para este slice. APF solo es visible en modo CW.                                                                                             | desactivado                                                                                                            |
| Deslizador de nivel DSP (pestaña DSP) | Establece el nivel de procesamiento para el algoritmo DSP nivelado activado más recientemente. La etiqueta a la izquierda identifica el objetivo actual. Se activa automáticamente al inicio si el perfil guardado de la radio tiene un DSP nivelado habilitado. Oculto (atenuado) cuando no hay ningún algoritmo nivelado activo. | —                                                                                                                      |
| Botón ADSP (pestaña DSP)         | Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Botón pulsador no verificable. Al hacer clic, eleva y enfoca el cuadro de diálogo no modal.                                           | —                                                                                                                      |
| Botón AetherVoice (pestaña DSP)  | Abre el Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX. Botón pulsador no verificable. Abarca 2 columnas en la cuadrícula DSP de 4 columnas.                                                                                     | —                                                                                                                      |
| Combinación Mode (pestaña Mode)  | Establece el modo de demodulación para este slice. Opciones: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY.                                                                                                                               | USB                                                                                                                    |
| Botones de ajustes predefinidos de filtro (pestaña Mode) | Cada botón aplica un ajuste predefinido de ancho de filtro guardado al slice. Haga clic izquierdo para aplicar; haga clic derecho para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro bajo y alto personalizados se pueden almacenar por ranura mediante clic derecho. | —                                                                                                                      |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Habilita la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desfase actual; la rueda de desplazamiento ajusta en pasos de 10 Hz.                                                                             | desactivado                                                                                                            |
| Combinación de canal DAX (pestaña DAX) | Asigna un canal de audio DAX a este slice. Opciones: Off, 1-8.                                                                                                                                                                                          | Off                                                                                                                    |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Habilita el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad del botón depende de la serie de la radio y la compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo de configuración de AetherDSP para ese algoritmo. | desactivado                                                                                                            |
| Botón ADSP (pestaña DSP)         | Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Tiene el estilo de un conmutador DSP del lado de la radio pero no es verificable. Al hacer clic, eleva y enfoca el cuadro de diálogo no modal de configuración de AetherDSP. | —                                                                                                                      |
| Botón AetherVoice (pestaña DSP)  | Alterna el Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX (v0.9.8). Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira.                                    | —                                                                                                                      |
| Botón de grosor de marca         | Recorre la línea de marca VFO entre Off, 1 px y 3 px. Se conserva por slice.                                                                                                                                                                           | 1 px                                                                                                                   |
| Botón de bordes de filtro        | Alterna las líneas de borde del filtro en la banda pasante del espectro. Se conserva por slice.                                                                                                                                                         | mostrado                                                                                                               |
| Alternar colapso                 | Colapsa el panel VFO a una tira compacta que solo muestra la frecuencia. Se conserva por slice.                                                                                                                                                        | expandido                                                                                                              |

## Diseño de la pestaña DSP (v26.7.4)

La pestaña **DSP** ahora muestra los botones de reducción de ruido y filtrado del lado de la radio dispuestos en una cuadrícula de cuatro columnas, seguidos por los botones de lanzamiento ADSP y AetherVoice. La cuadrícula ahora incluye botones de reducción de ruido adicionales que anteriormente estaban disponibles en el cuadro de diálogo de configuración de AetherDSP.

| Posición | Botón |
|---|---|
| Fila 1, col 1 | NR |
| Fila 1, col 2 | NR2 |
| Fila 1, col 3 | NR4 |
| Fila 1, col 4 | MNR |
| Fila 2, col 1 | DFNR |
| Fila 2, col 2 | BNR |
| Fila 2, col 3 | RN2 |
| Fila 2, col 4 | RNN |
| Fila 3, col 1 | NRL |
| Fila 3, col 2 | NRS |
| Fila 3, col 3 | NRF |
| Fila 3, col 4 | MNR (duplicado) |
| Fila 4, col 1 | ADSP |
| Fila 4, cols 2–3 | AetherVoice |

**Nota**: El diseño de la pestaña DSP se ha actualizado en v26.7.4. Los siguientes botones se han eliminado de la cuadrícula de la pestaña DSP: NB, ANF, APF, ANFL, ANFT. Ahora están disponibles desde el panel frontal de la radio o el menú superpuesto del espectro.

Los siguientes módulos DSP del lado del cliente se han añadido como botones de alternancia en la cuadrícula de la pestaña DSP: **NR2**, **RN2**, **BNR**, **NR4**, **MNR**, **DFNR**. Haga clic derecho en cualquiera de estos botones para abrir el cuadro de diálogo de configuración de AetherDSP para ese algoritmo específico.

Una fila compartida de **deslizador de nivel DSP** aparece debajo de la cuadrícula de botones. El deslizador se reorienta automáticamente al último botón DSP nivelado que se encendió. En v26.7.4, cuando llega un cambio de estado de nivel DSP desde la radio (por ejemplo, cuando el perfil guardado de la radio tiene NR habilitado al inicio), el deslizador aparece inmediatamente sin necesidad de re-alternar manualmente. Su etiqueta muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor a la derecha del deslizador muestra el nivel actual numéricamente. Cuando no hay ningún algoritmo DSP nivelado activo — o cuando solo RNN, ANFT o APF están encendidos — la fila del deslizador está presente en el diseño pero visualmente atenuada. Hacer clic en ella mientras está atenuada no tiene efecto.

## Cambios en los botones de pestaña (v26.6.3)

Las etiquetas de las pestañas del panel VFO (Audio, DSP, Mode, X/RIT, DAX) se han cambiado de widgets `QLabel` a `QPushButton`. Este cambio proporciona:

- **Accesibilidad del teclado**: Los botones de las pestañas ahora son accesibles mediante la tecla Tab. Presione Tab para navegar entre pestañas y presione Enter o Espacio para activar la pestaña enfocada.
- **Indicador de enfoque**: El botón de pestaña enfocado muestra un anillo de enfoque visible (borde inferior) utilizando el color de texto de la etiqueta del tema (`#6880a0`), haciendo visible la navegación por teclado.
- **Clic derecho en la pestaña Audio**: Haga clic derecho en el botón de la pestaña **Audio** para alternar el estado de silencio directamente, sin necesidad de abrir la pestaña Audio y hacer clic en el botón Mute.

## Dirección de desplazamiento de frecuencia (v26.6.3)

La dirección de desplazamiento de la rueda del ratón para la sintonización de frecuencia en el panel VFO ahora respeta la configuración **Reverse mouse wheel** que se encuentra en `Settings > Interaction`. Cuando esta configuración está habilitada, desplazar la rueda del ratón hacia arriba disminuye la frecuencia y desplazarla hacia abajo la aumenta. Anteriormente, la dirección de desplazamiento siempre era fija independientemente de esta configuración.

## Cambios en el comportamiento del Squelch (v26.5.1)

El control de squelch en la pestaña **Audio** ahora está deshabilitado para RTTY y modos digitales, además del modo CW. Esto evita que el squelch enmascare señales FSK débiles que se envían a decodificadores externos a través de DAX (#2504).

Cuando cambia un slice a modo DIGU, DIGL o RTTY:

- El botón y el deslizador de Squelch se deshabilitan.
- Si el squelch estaba activo, se desactiva automáticamente. El estado anterior se guarda internamente y se restaura si vuelve a un modo de voz.

Esto coincide con el comportamiento existente para el modo CW, donde la radio bloquea el squelch activado en un nivel fijo y rechaza los cambios del usuario.

## Cambios en la selección de antena (v26.5.2.1)

Los botones **RX antenna** y **TX antenna** ahora utilizan menús mejorados:

- El menú de antena RX utiliza `rxAntennaList()` del slice cuando está disponible, recurriendo a la lista global de antenas para compatibilidad con versiones anteriores.
- El menú de antena TX filtra inteligentemente los puertos de antena solo de recepción verificando prefijos "RX", prefijos "ANT", prefijos "TX" o "XVTR" como tokens de respaldo.
- Los elementos del menú ahora almacenan el identificador de la antena como datos, permitiendo la selección por nombre interno en lugar de etiqueta mostrada.
- Cada elemento del menú incluye información sobre herramientas y sugerencia de estado que muestran el identificador de la antena.

## Mejoras en la entrada de frecuencia (v26.5.2.1)

La lógica de entrada de frecuencia se ha actualizado para manejar mejor las bandas de transvertidor (XVTR):

- La frecuencia máxima de XVTR se ha incrementado de 450 MHz a 50000 MHz para soportar bandas de microondas.
- El análisis de conveniencia de "banda de tres dígitos" (insertar un decimal después del tercer dígito para números enteros simples como 1446 → 144.6 MHz) ahora solo se activa cuando la frecuencia del slice está entre 100 MHz y 999 MHz. Para las bandas de 23 cm y microondas (por encima de 1000 MHz), un número entero simple como 1296 se trata como 1296 MHz directamente.

## Mejoras en la entrada de frecuencia (v26.5.3)

La lógica de entrada de frecuencia ahora utiliza la clase de utilidad `FrequencyEntryParser` para un análisis consistente en toda la aplicación:

- La entrada explícita de MHz (escribir una frecuencia mayor de 54 MHz) ahora también se reconoce en bandas de HF, permitiendo la entrada directa de MHz sin estar en una banda XVTR.
- El método `normalizedMhzText()` maneja formatos de múltiples puntos como "14.225.000" eliminando los puntos posteriores al primero, asegurando un análisis consistente.
- La entrada directa de frecuencia está bloqueada cuando el slice está bloqueado. Intentar ingresar
