# Aplicar un ancho de filtro preestablecido desde el panel VFO

Los botones de filtros preestablecidos le permiten cambiar el ancho del filtro de recepción para una franja con un solo clic. Úselos para moverse rápidamente entre anchos de banda comunes, por ejemplo, entre un filtro SSB ancho de 3 kHz y un filtro CW estrecho de 500 Hz, sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO de la franja objetivo debe estar abierto y expandido. Si está colapsado a una tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo primero.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para la franja que desea ajustar. Se abre el panel VFO, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el botón de filtro preestablecido que corresponde al ancho de banda que desea. La radio aplica inmediatamente ese ancho de filtro a la franja.

Para guardar el ancho de filtro actual en una ranura preestablecida:

1. Ajuste el filtro al ancho de banda que desea guardar (consulte [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)).
2. Haga clic derecho en la ranura del botón preestablecido que desea sobrescribir.
3. El ancho de filtro actual se guarda en esa ranura.

## Qué hace cada control

| Control                          | Comportamiento                                                                                                                                                                                                                                                                                     | Valor predeterminado                                                                                                        |
|----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| Botón de antena RX               | Abre un menú de selección de antena para la antena receptora de esta franja. Usa la lista de antenas específica de la franja cuando está disponible. Los elementos del menú muestran información sobre herramientas y sugerencia de estado.                                                         | —                                                                                                                           |
| Botón de antena TX               | Abre un menú de selección de antena para la antena transmisora de esta franja. Filtra automáticamente los puertos de antena solo RX. Los elementos del menú muestran información sobre herramientas y sugerencia de estado.                                                                         | —                                                                                                                           |
| Visualización de frecuencia      | Muestra la frecuencia actual de la franja. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. La entrada directa está bloqueada cuando la franja está bloqueada.                                                                                 | —                                                                                                                           |
| Etiqueta de ancho de filtro      | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de filtros preestablecidos en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como única fuente de información, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas de modo SSB/digital (#2197, v0.9.8). |                                                                                                                             |
| Deslizador de ganancia AF (pestaña Audio) | Establece el nivel de salida de audio para esta franja (0-100).                                                                                                                                                                                                                                      | 100                                                                                                                         |
| Deslizador de paneo (pestaña Audio) | Establece el paneo estéreo izquierdo/derecho para esta franja (0-100). 50 = centro. El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central en la ranura que muestra la posición neutra.                                                                      | 50                                                                                                                          |
| Botón de silencio (pestaña Audio)  | Silencia la salida de audio para esta franja sin cambiar el ajuste de ganancia AF. Haga clic derecho en el botón de la pestaña Audio para alternar el silencio directamente.                                                                                                                         | desactivado                                                                                                                 |
| Botón + deslizador de squelch (pestaña Audio) | Activa el squelch para esta franja. El deslizador adyacente establece el umbral (0-100). Deshabilitado para RTTY y modos digitales (DIGU, DIGL).                                                                                                                                                   | desactivado                                                                                                                 |
| Combo AGC (pestaña Audio)        | Establece la velocidad de ataque/liberación del AGC para esta franja. Opciones: FAST, MED, SLOW, OFF.                                                                                                                                                                                              | FAST                                                                                                                       |
| Botones NR / NB / ANF / APF / NRL / NRS / RNN / NRF / ANFL / ANFT (pestaña DSP) | Activa el algoritmo correspondiente de reducción de ruido o filtrado del lado de la radio para esta franja. APF es visible solo en modo CW.                                                                                                                                                         | desactivado                                                                                                                 |
| Deslizador de nivel DSP (pestaña DSP) | Establece el nivel de procesamiento para el algoritmo DSP nivelado activado más recientemente. La etiqueta a la izquierda identifica el objetivo actual. Se activa automáticamente al inicio si el perfil guardado de la radio tiene un DSP nivelado activado. Oculto (atenuado) cuando no hay ningún algoritmo nivelado activo. | —                                                                                                                           |
| Botón ADSP (pestaña DSP)         | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Botón pulsador no verificable. Al hacer clic, eleva y enfoca el diálogo no modal.                                                                                                         | —                                                                                                                           |
| Botón AetherVoice (pestaña DSP)  | Abre el Canal de Audio Aetherial — el conjunto unificado de DSP de TX/RX. Botón pulsador no verificable. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas.                                                                                                                                     | —                                                                                                                           |
| Combo Mode (pestaña Mode)        | Establece el modo de demodulación para esta franja. Opciones: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY.                                                                                                                                                                       | USB                                                                                                                        |
| Botones de filtros preestablecidos (pestaña Mode) | Cada botón aplica un ancho de filtro preestablecido guardado a la franja. Clic izquierdo para aplicar; clic derecho para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro bajo y alto personalizados se pueden almacenar por ranura mediante clic derecho.                      | —                                                                                                                           |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz.                                                                                                                       | desactivado                                                                                                                 |
| Combo de canal DAX (pestaña DAX) | Asigna un canal de audio DAX a esta franja. Opciones: Off, 1-8.                                                                                                                                                                                                                                   | Off                                                                                                                        |
| Botón de grosor del marcador     | Cicla la línea del marcador VFO entre Off (desactivado), 1 px y 3 px. Se conserva por franja.                                                                                                                                                                                                      | 1 px                                                                                                                       |
| Botón de bordes del filtro       | Alterna las líneas de borde del filtro en la banda de paso del espectro. Se conserva por franja.                                                                                                                                                                                                    | mostrado                                                                                                                   |
| Alternancia de colapso           | Colapsa el panel VFO a una tira compacta de solo frecuencia. Se conserva por franja.                                                                                                                                                                                                               | expandido                                                                                                                  |

## Diseño de la pestaña DSP (v0.9.8)

La pestaña **DSP** muestra los botones de reducción de ruido y filtrado del lado de la radio dispuestos en una cuadrícula de cuatro columnas, seguida de los botones de lanzamiento ADSP y AetherVoice:

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

Una fila compartida del **deslizador de nivel DSP** aparece debajo de la cuadrícula de botones. El deslizador se reorienta automáticamente al botón DSP nivelado que se haya activado más recientemente. En v0.9.8, cuando llega un cambio de estado del nivel DSP desde la radio (por ejemplo, cuando el perfil guardado de la radio tiene NR activado al inicio), el deslizador aparece inmediatamente sin necesidad de re-activar manualmente. Su etiqueta muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor a la derecha del deslizador muestra el nivel actual numéricamente. Cuando ningún algoritmo DSP nivelado está activo, o solo RNN, ANFT o APF están encendidos, la fila del deslizador está presente en el diseño pero visualmente atenuada. Hacer clic en ella mientras está atenuada no tiene efecto.

Los siguientes módulos DSP del lado del cliente se han eliminado de la pestaña DSP del panel VFO en v0.9.8: **NR2**, **RN2**, **BNR**, **NR4**, **MNR**, **DFNR**. Actívelos desde el menú de superposición del espectro o desde el applet AetherDSP.

## Cambios en los botones de pestaña (v26.6.3)

Las etiquetas de las pestañas del panel VFO (Audio, DSP, Mode, X/RIT, DAX) se han cambiado de widgets `QLabel` a `QPushButton`. Este cambio proporciona:

- **Accesibilidad del teclado**: Los botones de pestaña ahora son accesibles mediante la tecla Tab. Presione Tab para navegar entre pestañas y presione Enter o Espacio para activar la pestaña enfocada.
- **Indicador de enfoque**: El botón de pestaña enfocado muestra un anillo de enfoque visible (borde inferior) usando el color de texto de la etiqueta del tema (`#6880a0`), haciendo visible la navegación por teclado.
- **Clic derecho en la pestaña Audio**: Haga clic derecho en el botón de la pestaña **Audio** para alternar el estado de silencio directamente, sin necesidad de abrir la pestaña Audio y hacer clic en el botón Mute.

## Dirección de desplazamiento de frecuencia (v26.6.3)

La dirección de desplazamiento de la rueda del ratón para la sintonización de frecuencia en el panel VFO ahora respeta la configuración **Reverse mouse wheel** que se encuentra en `Settings > Interaction`. Cuando esta configuración está activada, desplazar la rueda del ratón hacia arriba disminuye la frecuencia y desplazarla hacia abajo la aumenta. Anteriormente, la dirección de desplazamiento siempre era fija independientemente de esta configuración.

## Cambios en el comportamiento del squelch (v26.5.1)

El control de squelch en la pestaña **Audio** ahora está deshabilitado para RTTY y modos digitales, además del modo CW. Esto evita que el squelch bloquee señales FSK débiles que se envían a decodificadores externos a través de DAX (#2504).

Cuando cambia una franja a modo DIGU, DIGL o RTTY:

- El botón y el deslizador de Squelch se deshabilitan.
- Si el squelch estaba activo, se desactiva automáticamente. El estado anterior se guarda internamente y se restaura si vuelve a cambiar a un modo de voz.

Esto coincide con el comportamiento existente para el modo CW, donde la radio bloquea el squelch en un nivel fijo y rechaza los cambios del usuario.

## Cambios en la selección de antena (v26.5.2.1)

Los botones **RX antenna** y **TX antenna** ahora usan menús mejorados:

- El menú de antena RX usa `rxAntennaList()` de la franja cuando está disponible, recurriendo a la lista de antenas global para compatibilidad heredada.
- El menú de antena TX filtra inteligentemente los puertos de antena solo RX, verificando prefijos "RX", prefijos "ANT", prefijos "TX" o "XVTR" como tokens de respaldo.
- Los elementos del menú ahora almacenan el identificador de la antena como datos, permitiendo la selección por nombre interno en lugar de por etiqueta mostrada.
- Cada elemento del menú incluye información sobre herramientas y sugerencia de estado que muestran el identificador de la antena.

## Mejoras en la entrada de frecuencia (v26.5.2.1)

La lógica de entrada de frecuencia se ha actualizado para manejar mejor las bandas de transvertor (XVTR):

- La frecuencia máxima de XVTR se ha incrementado de 450 MHz a 50000 MHz para soportar bandas de microondas.
- El análisis de conveniencia de "tres dígitos de banda" (insertar un decimal después del tercer dígito para enteros simples como 1446 → 144,6 MHz) ahora solo se activa cuando la frecuencia de la franja está entre 100 MHz y 999 MHz. Para bandas de 23 cm y microondas (por encima de 1000 MHz), un entero simple como 1296 se trata directamente como 1296 MHz.

## Mejoras en la entrada de frecuencia (v26.5.3)

La lógica de entrada de frecuencia ahora usa la clase de utilidad `FrequencyEntryParser` para un análisis consistente en toda la aplicación:

- La entrada explícita de MHz (escribir una frecuencia mayor de 54 MHz) ahora se reconoce también en bandas HF, permitiendo la entrada directa de MHz sin estar en una banda XVTR.
- El método `normalizedMhzText()` maneja formatos con múltiples puntos como "14.225.000" eliminando los puntos después del primero, asegurando un análisis consistente.
- La entrada directa de frecuencia está bloqueada cuando la franja está bloqueada. Intentar ingresar una frecuencia mientras está bloqueada no produce ninguna acción.

## Renderizado de la insignia de franja (v26.5.2.1)

La insignia de letra de la franja ahora se renderiza como Texto Enriquecido Qt (`Qt::RichText`), corrigiendo un problema donde ciertas letras de franja se mostraban incorrectamente (#2606). El estilo de la insignia permanece igual.

## Mejoras visuales del deslizador de paneo (v26.6.1)

El **deslizador de paneo** en la pestaña **Audio** ahora pinta su relleno desde el centro hacia afuera, con un pequeño punto de marca central en la ranura. Esto hace que la posición neutra (50%) sea visible de un vistazo, y la dirección del relleno coincide con las expectativas del operador para un control de balance izquierdo/derecho.

Anteriormente, el relleno del deslizador se pintaba desde el borde izquierdo hasta la posición del mango, lo cual era engañoso para un control anclado al centro donde el cero significativo es el punto medio. El nuevo renderizado usa la clase `CenterMarkSlider` que sobrepinta el relleno de subpágina predeterminado de Qt: borra la mitad no deseada de la subpágina con el color de fondo de la ranura, luego agrega el relleno deseado del centro al mango en el color de acento.

## Actualización del tema (v26.6.1)

El panel VFO ahora usa el sistema de temas para todos los elementos visuales:

- El contenedor del panel VFO está registrado bajo el ámbito de tema `spectrum/vfo`, permitiendo que los archivos de tema apunten a estilos específicos del VFO por separado de la pantalla del espectro.
- Las clases `CenterMarkSlider` y `MiniBadgeButton` usan tokens de color de `ThemeManager` (`color.background.1`, `color.accent`, etc.) para sus operaciones de pintura personalizadas.
- La hoja de estilo del botón MiniBadge usa el método `applyStyleSheet()` con variables de plantilla de tema
