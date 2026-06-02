# Aplicar un ancho de filtro predefinido desde el panel VFO

Los botones de preselección de filtro le permiten cambiar el ancho del filtro de recepción de un segmento con un solo clic. Úselos para moverse rápidamente entre anchos de banda comunes — por ejemplo, entre un filtro SSB ancho de 3 kHz y un filtro CW estrecho de 500 Hz — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO del segmento objetivo debe estar abierto y expandido. Si está contraído a una tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo primero.

## Pasos

1. Haga clic en la bandera marcadora VFO en la pantalla del espectro para el segmento que desea ajustar. El panel VFO se abre, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el botón de preselección de filtro que corresponde al ancho de banda que desea. La radio aplica inmediatamente ese ancho de filtro al segmento.

Para guardar el ancho de filtro actual en una ranura de preselección:

1. Ajuste el filtro al ancho de banda que desea guardar (consulte [Configurar un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)).
2. Haga clic con el botón derecho en la ranura del botón de preselección que desea sobrescribir.
3. El ancho de filtro actual se guarda en esa ranura.

## Qué hace cada control

| Control                          | Comportamiento                                                                                                                                                                                                                                       | Valor predeterminado                                                                                                                 |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| Botón de antena RX               | Abre un menú de selección de antena para la antena receptora de este segmento. Usa la lista de antenas específica del segmento cuando está disponible. Los elementos del menú muestran información sobre herramientas y sugerencia de estado.             | —                                                                                                                                    |
| Botón de antena TX               | Abre un menú de selección de antena para la antena transmisora de este segmento. Filtra automáticamente los puertos de antena solo RX. Los elementos del menú muestran información sobre herramientas y sugerencia de estado.                            | —                                                                                                                                    |
| Pantalla de frecuencia           | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. La entrada directa está bloqueada cuando el segmento está bloqueado.                                    | —                                                                                                                                    |
| Etiqueta de ancho de filtro      | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode. Usa RxApplet::formatFilterWidth como fuente única de verdad, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |                                                                                                                                      |
| Deslizador de ganancia AF (pestaña Audio) | Establece el nivel de salida de audio para este segmento (0-100).                                                                                                                                                                                       | 100                                                                                                                                  |
| Deslizador de paneo (pestaña Audio)      | Establece el paneo estéreo izquierda/derecha para este segmento (0-100). 50 = centro. El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central en la ranura que muestra la posición neutra.                          | 50                                                                                                                                   |
| Botón de silencio (pestaña Audio)        | Silencia la salida de audio para este segmento sin cambiar la configuración de ganancia AF.                                                                                                                                                            | desactivado                                                                                                                          |
| Botón de squelch + deslizador (pestaña Audio) | Activa el squelch para este segmento. El deslizador adyacente establece el umbral (0-100). Deshabilitado para RTTY y modos digitales (DIGU, DIGL).                                                                                                      | desactivado                                                                                                                          |
| Combinación AGC (pestaña Audio)           | Establece la velocidad de ataque/soltura del AGC para este segmento. Opciones: FAST, MED, SLOW, OFF.                                                                                                                                                   | FAST                                                                                                                                 |
| Botones NR / NB / ANF / APF / NRL / NRS / RNN / NRF / ANFL / ANFT (pestaña DSP) | Activa el algoritmo correspondiente de reducción de ruido o filtrado del lado de la radio para este segmento. APF es visible solo en modo CW.                                                                                                             | desactivado                                                                                                                          |
| Deslizador de nivel DSP (pestaña DSP)         | Establece el nivel de procesamiento para el algoritmo DSP nivelado activado más recientemente. La etiqueta a la izquierda identifica el objetivo actual. Se activa automáticamente al inicio si el perfil guardado de la radio tiene un DSP nivelado activado. Oculto (atenuado) cuando no hay ningún algoritmo nivelado activo. | —                                                                                                                                    |
| Botón ADSP (pestaña DSP)                     | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Botón pulsador no verificable. Al hacer clic, eleva y enfoca el diálogo no modal.                                                               | —                                                                                                                                    |
| Botón AetherVoice (pestaña DSP)              | Abre el Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX. Botón pulsador no verificable. Abarca 2 columnas en la cuadrícula DSP de 4 columnas.                                                                                     | —                                                                                                                                    |
| Combinación Mode (pestaña Mode)              | Establece el modo de demodulación para este segmento. Opciones: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY.                                                                                                                           | USB                                                                                                                                  |
| Botones de preselección de filtro (pestaña Mode) | Cada botón aplica una preselección de ancho de filtro guardada al segmento. Haga clic izquierdo para aplicar; haga clic derecho para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro inferior y superior personalizados se pueden almacenar por ranura mediante clic derecho. | —                                                                                                                                    |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz.                                                                      | desactivado                                                                                                                          |
| Combinación de canal DAX (pestaña DAX)         | Asigna un canal de audio DAX a este segmento. Opciones: Off, 1-8.                                                                                                                                                                                     | Off                                                                                                                                  |
| Botón de grosor del marcador                  | Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Persiste por segmento.                                                                                                                                                                    | 1 px                                                                                                                                 |
| Botón de bordes de filtro                     | Alterna las líneas de borde del filtro en la banda pasante del espectro. Persiste por segmento.                                                                                                                                                       | mostrado                                                                                                                            |
| Alternancia de contracción                    | Contrae el panel VFO a una tira compacta de solo frecuencia. Persiste por segmento.                                                                                                                                                                | expandido                                                                                                                           |

## Cambios en la pestaña DSP en v0.9.8

La pestaña **DSP** ahora muestra solo los botones de reducción de ruido del lado de la radio. Los siguientes botones se han eliminado de la pestaña DSP del panel VFO:

- **NR2**
- **RN2**
- **BNR**
- **NR4**
- **MNR**
- **DFNR**

Estos módulos DSP del lado del cliente ahora son accesibles a través del menú de superposición del espectro y el applet AetherDSP. Actívelos allí en lugar de desde el panel VFO.

Los botones que permanecen en la pestaña DSP están dispuestos en una cuadrícula de cuatro columnas, seguidos de los botones de lanzamiento ADSP y AetherVoice:

| Posición | Botón |
|---|---|
| Fila 1, col 1 | NR |
| Fila 1, col 2 | NB |
| Fila 1, col 3 | ANF |
| Fila 1, col 4 | APF (visible solo en modo CW) |
| Fila 2, col 1 | NRL |
| Fila 2, col 2 | NRS |
| Fila 2, col 3 | RNN |
| Fila 2, col 4 | NRF |
| Fila 3, col 1 | ANFL |
| Fila 3, col 2 | ANFT |
| Fila 4, col 1 | ADSP |
| Fila 4, cols 2–3 | AetherVoice |

Una fila compartida de **deslizador de nivel DSP** aparece debajo de la cuadrícula de botones. El deslizador se redirige automáticamente al botón DSP nivelado que se encendió más recientemente. En v0.9.8, cuando llega un cambio de estado de nivel DSP desde la radio (por ejemplo, cuando el perfil guardado de la radio tiene NR activado al inicio), el deslizador aparece inmediatamente sin requerir una reactivación manual. Su etiqueta muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor a la derecha del deslizador muestra el nivel actual numéricamente. Cuando no hay ningún algoritmo DSP nivelado activo — o cuando solo RNN, ANFT o APF están encendidos — la fila del deslizador está presente en el diseño pero visualmente atenuada. Hacer clic en ella mientras está atenuada no tiene efecto.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Botones NR / NB / ANF / APF / NRL / NRS / RNN / NRF / ANFL / ANFT (pestaña DSP) | Activa el algoritmo correspondiente de reducción de ruido o filtrado del lado de la radio para este segmento. APF es visible solo en modo CW. | desactivado | — |
| Deslizador de nivel DSP (pestaña DSP) | Establece el nivel de procesamiento para el algoritmo DSP nivelado activado más recientemente. La etiqueta a la izquierda identifica el objetivo actual. Se activa automáticamente al inicio si el perfil guardado de la radio tiene un DSP nivelado activado. Oculto (atenuado) cuando no hay ningún algoritmo nivelado activo. | — | — |
| Botón ADSP (pestaña DSP) | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Botón pulsador no verificable. | — | — |
| Botón AetherVoice (pestaña DSP) | Abre el Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX. Botón pulsador no verificable. Abarca 2 columnas en la cuadrícula DSP de 4 columnas. | — | — |

## Cambios en el comportamiento del squelch (v26.5.1)

El control de squelch en la pestaña **Audio** ahora está deshabilitado para RTTY y modos digitales, además del modo CW. Esto evita que el squelch enmascare señales FSK débiles que se envían a decodificadores externos a través de DAX (#2504).

Cuando cambia un segmento a modo DIGU, DIGL o RTTY:

- El botón y el deslizador de Squelch se deshabilitan.
- Si el squelch estaba activo, se apaga automáticamente. El estado anterior se guarda internamente y se restaura si vuelve a un modo de voz.

Esto coincide con el comportamiento existente para el modo CW, donde la radio bloquea el squelch encendido a un nivel fijo y rechaza los cambios del usuario.

## Cambios en la selección de antena (v26.5.2.1)

Los botones de **antena RX** y **antena TX** ahora utilizan menús mejorados:

- El menú de antena RX usa `rxAntennaList()` del segmento cuando está disponible, recurriendo a la lista global de antenas para compatibilidad con versiones anteriores.
- El menú de antena TX filtra inteligentemente los puertos de antena solo RX verificando prefijos "RX", prefijos "ANT", prefijos "TX" o "XVTR" como tokens de respaldo.
- Los elementos del menú ahora almacenan el identificador de la antena como datos, permitiendo la selección por nombre interno en lugar de etiqueta mostrada.
- Cada elemento del menú incluye información sobre herramientas y sugerencia de estado que muestran el identificador de la antena.

## Mejoras en la entrada de frecuencia (v26.5.2.1)

La lógica de entrada de frecuencia se ha actualizado para manejar mejor las bandas de transvertidor (XVTR):

- La frecuencia máxima de XVTR se ha incrementado de 450 MHz a 50000 MHz para soportar bandas de microondas.
- El análisis de conveniencia de "banda de tres dígitos" (insertar un decimal después del tercer dígito para enteros simples como 1446 → 144.6 MHz) ahora solo se activa cuando la frecuencia del segmento está entre 100 MHz y 999 MHz. Para bandas de 23 cm y microondas (por encima de 1000 MHz), un entero simple como 1296 se trata directamente como 1296 MHz.

## Mejoras en la entrada de frecuencia (v26.5.3)

La lógica de entrada de frecuencia ahora usa la clase de utilidad `FrequencyEntryParser` para un análisis consistente en toda la aplicación:

- La entrada explícita en MHz (escribir una frecuencia mayor a 54 MHz) ahora también se reconoce en bandas HF, permitiendo la entrada directa en MHz sin estar en una banda XVTR.
- El método `normalizedMhzText()` maneja formatos con múltiples puntos como "14.225.000" eliminando los puntos después del primero, asegurando un análisis consistente.
- La entrada directa de frecuencia está bloqueada cuando el segmento está bloqueado. Intentar ingresar una frecuencia mientras está bloqueado no produce ninguna acción.

## Renderizado de la insignia del segmento (v26.5.2.1)

La insignia de la letra del segmento ahora se renderiza como Qt Rich Text (`Qt::RichText`), corrigiendo un problema donde ciertas letras de segmento se mostraban incorrectamente (#2606). El estilo de la insignia permanece igual.

## Mejoras visuales del deslizador de paneo (v26.6.1)

El **deslizador de paneo** en la pestaña **Audio** ahora pinta su relleno desde el centro hacia afuera, con un pequeño punto de marca central en la ranura. Esto hace que la posición neutral (50%) sea visible de un vistazo, y la dirección del relleno coincide con las expectativas del operador para un control de balance izquierda/derecha.

Anteriormente, el relleno del deslizador se pintaba desde el borde izquierdo hasta la posición del control, lo cual era engañoso para un control anclado al centro donde el cero significativo es el punto medio. El nuevo renderizado usa la clase `CenterMarkSlider` que sobrescribe el relleno de subpágina predeterminado de Qt: borra la mitad no deseada de la subpágina con el color de fondo de la ranura, luego agrega el relleno deseado del centro al control en el color de acento.

## Actualización del tema (v26.6.1)

El panel VFO ahora usa el sistema de temas para todos los elementos visuales:

- El contenedor del panel VFO está registrado bajo el ámbito de tema `spectrum/vfo`, permitiendo que los archivos de tema apunten a estilos específicos del VFO por separado de la pantalla del espectro.
- Las clases `CenterMarkSlider` y `MiniBadgeButton` usan tokens de color de `ThemeManager` (`color.background.1`, `color.accent`, etc.) para sus operaciones de pintado personalizadas.
- La hoja de estilo del botón MiniBadge usa el método `applyStyleSheet()` con variables de plantilla del tema (por ejemplo, `{{color.background.1}}`, `{{color.accent}}`) en lugar de colores hexadecimales codificados.
- La herramienta Inspector (clic en modo Inspeccionar) en el panel VFO ahora muestra los tokens de tema que
