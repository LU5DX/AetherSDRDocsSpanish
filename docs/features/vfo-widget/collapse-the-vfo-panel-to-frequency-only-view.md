# Contraer el panel VFO a una vista solo de frecuencia

Cuando el espacio en la pantalla es limitado, puede contraer el panel VFO a una tira compacta que muestra solo la frecuencia de la porción. El estado contraído se guarda por cada porción, de modo que persiste entre sesiones.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO de la porción debe estar abierto. Si no es visible, haga clic en el marcador de la porción en la pantalla del espectro para esa porción.

## Pasos

1. Localice la insignia de la porción en el área del encabezado del panel VFO. La insignia muestra el identificador de la porción (por ejemplo, **A** o **B**).
2. Haga clic en la insignia de la porción. El panel se contrae a una tira compacta que solo muestra la frecuencia.
3. Para restaurar el panel completo, haga clic en cualquier lugar de la tira contraída.

## Función de cada control

| Control | Valor predeterminado | Ajuste persistente |
|---|---|---|
| Alternar contraer | Expandido | `SliceFlagCollapsed_{N}` |
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de esta porción. Utiliza la `rxAntennaList` de la porción cuando está disponible; de lo contrario, recurre a la lista de antenas de la radio. | Ninguno |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de esta porción. Filtra los puertos de antena solo RX. Utiliza la `txAntennaList` de la porción cuando está disponible. | Ninguno |
| Pantalla de frecuencia | Muestra la frecuencia actual de la porción. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. | Ninguno |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para alternar entre los botones preestablecidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de información, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). | Ninguno |
| Insignia de la porción | Muestra la letra de la porción. Haga clic para contraer el panel. Muestra texto con formato HTML (#2606). | Ninguno |
| Deslizador AF Gain (pestaña Audio) | 100 | Ninguno — refleja el estado en vivo de la radio. |
| Deslizador Pan (pestaña Audio) | 50 | Ninguno |
| Botón Mute (pestaña Audio) | Apagado | Ninguno |
| Botón y deslizador Squelch (pestaña Audio) | Apagado | Ninguno |
| Combo AGC (pestaña Audio) | FAST | Ninguno |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Apagado | Ninguno |
| Botón ADSP (pestaña DSP) | Abre el cuadro de diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene estilo de un conmutador de DSP del lado de la radio, pero no se puede marcar. Al hacer clic, abre y enfoca el cuadro de diálogo no modal AetherDSP Settings. |
| Botón AetherVoice (pestaña DSP) | Alterna la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Combo Mode (pestaña Mode) | USB | Ninguno |
| Botones de preestablecidos de filtro (pestaña Mode) | Aplica un ancho de filtro guardado preestablecido. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. | `FilterPresets` |
| Botones y etiquetas RIT / XIT (pestaña X/RIT) | Apagado | Ninguno |
| Combo DAX channel (pestaña DAX) | Apagado | Ninguno |
| Botón de grosor del marcador | 1 px | `Slice{N}_MarkerWidth` |
| Botón de bordes del filtro | Mostrado | `Slice{N}_FilterEdgesHidden` |

El ajuste `SliceFlagCollapsed_{N}` se almacena por porción, donde `{N}` es el número de la porción. Contraer una porción no afecta a otras porciones.

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP en el panel VFO ahora muestra solo los algoritmos de reducción de ruido y filtrado suministrados directamente por la radio. Los siguientes botones se han eliminado de la cuadrícula de la pestaña DSP:

- **NR2** (reducción de ruido espectral)
- **RN2** (supresión de ruido RNNoise)
- **BNR** (eliminación de ruido neuronal por GPU)
- **NR4** (reducción de ruido por blanqueo espectral)
- **MNR** (reducción de ruido MMSE-Wiener en macOS)
- **DFNR** (reducción de ruido neuronal DeepFilterNet3)

Estos algoritmos de procesamiento del lado del cliente aún están disponibles. Acceda a ellos a través del menú superpuesto del espectro o del applet AetherDSP.

Los botones que permanecen en la cuadrícula de la pestaña DSP ahora están organizados en un diseño de cuatro columnas, estando presentes todos los botones de DSP del lado del cliente:

| Posición | Botón |
|---|---|
| Fila 0, Col 0 | NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR |
| Fila 0, Col 1 | NRL |
| Fila 0, Col 2 | NRS |
| Fila 0, Col 3 | RNN |
| Fila 1, Col 0 | NRF |
| Fila 1, Cols 1-3 | (vacío) |
| Fila 2, Col 0 | ADSP |
| Fila 2, Cols 1-2 | AetherVoice (ocupa 2 columnas) |

Nota: La entrada del botón NR en la cuadrícula ahora representa un grupo de botones de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR). Los botones específicos que se muestran dependen de la serie de radio y la configuración de compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el cuadro de diálogo AetherDSP Settings para ese algoritmo.

### Deslizador de nivel DSP

Una fila de deslizador de nivel compartido aparece debajo de la cuadrícula de botones DSP. El deslizador se dirige al algoritmo DSP con nivel que se habilitó más recientemente. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor numérico se muestra a la derecha.

| Control | Rango | Comportamiento |
|---|---|---|
| Deslizador de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP activo. Cambia de objetivo automáticamente cuando habilita un algoritmo diferente. |

La fila del deslizador permanece en el diseño en todo momento. Cuando no hay un algoritmo compatible activo — o cuando solo están activos RNN, ANFT o APF — la fila del deslizador se atenúa y no responde a la entrada. Al habilitar un algoritmo compatible, la fila se vuelve visible y el deslizador se reorienta hacia ese algoritmo.

Algoritmos a los que el deslizador de nivel puede dirigirse: NR, NB, ANF, NRL, NRS, NRF, ANFL.

El deslizador de nivel ahora refleja correctamente el estado de la radio en la conexión inicial. Cuando un algoritmo DSP con nivel ya está activo en el perfil guardado de la radio, el deslizador aparece inmediatamente en lugar de requerir una activación manual (#startup-slider, v0.9.8).

### Comportamiento del squelch en modo RTTY

A partir de v26.5.1, el botón y el deslizador de squelch están deshabilitados en modo RTTY. El squelch de la radio bloquea las señales FSK débiles, lo que interfiere con los decodificadores externos que esperan un flujo de audio continuo a través de DAX. Si el squelch estaba habilitado al cambiar al modo RTTY, se desactiva automáticamente. El estado guardado del squelch se restaura al volver a un modo de voz.

## Entrada de frecuencia en bandas XVTR

Al introducir una frecuencia en bandas XVTR (rango de 100–999 MHz), el panel VFO aplica una conversión de conveniencia: una entrada de número entero simple como `1446` se interpreta como `144.6 MHz` insertando un decimal después del tercer dígito. Esto solo se aplica cuando:
- La porción está sintonizada en una banda XVTR (frecuencia superior a 54 MHz o usando una antena que comienza con `XVT`)
- La frecuencia actual está en el rango de 100–999 MHz (banda de tres dígitos)
- El valor ingresado es superior a 450 MHz y no contiene un punto decimal

Para frecuencias en bandas de 23 cm y microondas (por encima de 1000 MHz), un número entero simple se interpreta directamente como MHz (por ejemplo, `1296` significa `1296 MHz`, no `129.6 MHz`).

La entrada de frecuencia acepta valores de hasta 50000 MHz en bandas XVTR.

### Reconocimiento explícito de entrada en MHz

A partir de v26.5.3, el analizador de entrada de frecuencia ahora reconoce explícitamente los valores ingresados en formato MHz. Si introduce una frecuencia superior a 54 MHz usando una notación explícita de MHz (por ejemplo, `144.000` o `432.100`), el analizador lo trata como una entrada directa en MHz, en lugar de intentar una conversión a Hz o kHz. Esto le permite ingresar frecuencias VHF/UHF directamente sin requerir una antena XVTR o una frecuencia preexistente superior a 54 MHz.

El analizador normaliza los puntos múltiples (por ejemplo, `14.225.000` se convierte en `14.225000`) usando `FrequencyEntryParser::normalizedMhzText()` antes de intentar analizar. La bandera de entrada explícita en MHz permite que el analizador omita la lógica de conversión a Hz/kHz para valores superiores a 54 MHz que se ingresaron claramente como MHz.

## Comportamiento de desplazamiento en porciones bloqueadas

Cuando una porción está bloqueada por VFO, el desplazamiento de la rueda del ratón sobre el panel VFO no cambia la frecuencia. En su lugar, la pantalla de frecuencia muestra brevemente una superposición **LOCKED** para indicar que la sintonización está bloqueada. Esto se aplica tanto en la vista contraída como en la expandida. La notificación la proporciona `SliceModel::notifyTuneBlockedByLock()`.

## Optimización de la altura de la pila de pestañas

A partir de v26.5.3, el panel VFO utiliza un widget `TabStack` (una subclase de `QStackedWidget`) que informa solo el tamaño preferido de la pestaña actual. Esto evita un espacio vertical excesivo al cambiar entre pestañas de diferentes alturas; por ejemplo, cuando la pestaña DSP es más alta que la pestaña Mode debido al subcontenedor de modo digital que aparece en los modos DIGU/DIGL. No hay cambios en el comportamiento visual; el panel ahora utiliza el espacio de manera más eficiente.

## Mejoras de soporte de temas en v26.6.1

El panel VFO ahora participa completamente en el sistema de temas de AetherSDR. Al panel se le asigna un ámbito de contenedor de tema `spectrum/vfo` para que los clics del inspector en el panel VFO se informen correctamente bajo el ámbito VFO en lugar de ascender al espectro.

Los siguientes tokens de tema se declaran para el panel VFO:
- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

Estos tokens son utilizados por las llamadas sin formato de `QPainter` para el medidor de señal, la insignia de la porción y la representación del fondo. Cuando se usa el inspector de temas, al hacer clic en la bandera VFO, la insignia de indicativo o la tira del medidor de señal, estos tokens aparecen en la lista de resultados.

### Apariencia del deslizador de marca central

El deslizador Pan en la pestaña Audio utiliza un `CenterMarkSlider` que pinta un punto de marca central para indicar la posición neutral (50). A partir de v26.6.1, el relleno del deslizador está anclado desde el centro hacia afuera: el lado izquierdo de la ranura se rellena con el color de fondo, y el lado derecho desde el centro hasta el control se rellena con el color de acento. Esto proporciona una indicación visual del desplazamiento de paneo/balance desde el punto medio. El punto central se pinta en el punto medio de la ranura del deslizador.

### Tematización de botones

Los botones de acción del panel VFO ahora usan hojas de estilo que reconocen el tema en lugar de colores fijos. El estado presionado usa `{{color.accent}}` y el fondo usa `{{color.background.1}}`. Esto garantiza una apariencia coherente en todos los temas.

## Insignias TX y SPLIT

| Indicador | Estados | Significado |
|---|---|---|
| Insignia TX | TX (rojo) u oculta | Se muestra cuando esta porción es la porción transmisora activa. |
| Insignia SPLIT | SPLIT (ámbar) u oculta | Se muestra cuando TX está asignada a una porción diferente a la porción receptora activa. |

## Consejos

- En la vista contraída, desplazar la rueda del ratón sobre la tira sintoniza la frecuencia de la porción según el tamaño de paso actual, igual que al desplazarse sobre la pantalla de frecuencia en el panel completo.
- En la vista contraída, al hacer clic en la insignia TX pintada en la tira, se alterna la asignación de TX para esa porción. Al hacer clic en cualquier otro lugar de la tira, se expande el panel.
- El panel se voltea automáticamente al lado derecho del marcador VFO si expandirlo quedara recortado por el borde de la ventana. Este comportamiento se aplica tanto en los estados expandido como contraído.
- Para acceder a NR2, RN2, BNR, NR4, MNR o DFNR, haga clic derecho en la pantalla del espectro para abrir el menú superpuesto, o abra el applet AetherDSP.

## Relacionados

- [VFO Panel overview](overview.md)
- [Tune the radio by typing a frequency into the VFO panel](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Change the VFO marker line thickness](change-the-vfo-marker-line-thickness.md)
- [Hide or show filter edge lines on the spectrum](hide-or-show-filter-edge-lines-on-the-spectrum.md)
