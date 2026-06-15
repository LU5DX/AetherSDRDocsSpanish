# Contraer el panel VFO a la vista solo de frecuencia

Cuando el espacio en pantalla es limitado, puede contraer el panel VFO a una franja compacta que muestra solo la frecuencia del slice. El estado contraído se guarda por slice, por lo que persiste entre sesiones.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa con el radio.
- El panel VFO del slice debe estar abierto. Si no está visible, haga clic en la bandera marcadora VFO en la visualización del espectro de ese slice.

## Pasos

1. Localice la insignia del slice en el área del encabezado del panel VFO. La insignia muestra el identificador del slice (por ejemplo, **A** o **B**).
2. Haga clic en la insignia del slice. El panel se contrae a una franja compacta solo de frecuencia.
3. Para restaurar el panel completo, haga clic en cualquier lugar de la franja contraída.

## Qué hace cada control

| Control | Valor predeterminado | Ajuste persistente |
|---|---|---|
| Alternar colapso | Expandido | `SliceFlagCollapsed_{N}` |
| Botón de antena RX | Abre el menú de selección de antena para la antena de recepción de este slice. Utiliza la `rxAntennaList` del slice cuando está disponible; de lo contrario, recurre a la lista de antenas del radio. | Ninguno |
| Botón de antena TX | Abre el menú de selección de antena para la antena de transmisión de este slice. Filtra los puertos de antena solo RX. Utiliza la `txAntennaList` del slice cuando está disponible. | Ninguno |
| Visualización de frecuencia | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. | Ninguno |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). | Ninguno |
| Insignia del slice | Muestra la letra del slice. Haga clic para contraer el panel. Muestra texto con formato HTML (#2606). | Ninguno |
| Deslizador de ganancia AF (pestaña Audio) | 100 | Ninguno — refleja el estado en vivo del radio. |
| Deslizador Pan (pestaña Audio) | 50 | Ninguno |
| Botón de silencio (pestaña Audio) | Apagado | Ninguno |
| Botón + deslizador de squelch (pestaña Audio) | Apagado | Ninguno |
| Combo AGC (pestaña Audio) | FAST | Ninguno |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Apagado | Ninguno |
| Botón ADSP (pestaña DSP) | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Estilizado como un conmutador de DSP del lado del radio pero no marcable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Alterna la tira de canal de audio Aetherial — el conjunto unificado de DSP TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Combo Mode (pestaña Mode) | USB | Ninguno |
| Botones de preselección de filtro (pestaña Mode) | Aplica un ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. | `FilterPresets` |
| Botones RIT / XIT + etiquetas (pestaña X/RIT) | Apagado | Ninguno |
| Combo de canal DAX (pestaña DAX) | Apagado | Ninguno |
| Botón de grosor de marcador | 1 px | `Slice{N}_MarkerWidth` |
| Botón de bordes de filtro | Mostrado | `Slice{N}_FilterEdgesHidden` |

El ajuste `SliceFlagCollapsed_{N}` se almacena por slice, donde `{N}` es el número de slice. Contraer un slice no afecta a otros slices.

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP en el panel VFO ahora muestra solo los algoritmos de reducción de ruido y filtrado suministrados directamente por el radio. Los siguientes botones se han eliminado de la cuadrícula de la pestaña DSP:

- **NR2** (reducción de ruido espectral)
- **RN2** (supresión de ruido RNNoise)
- **BNR** (denoización neuronal por GPU)
- **NR4** (reducción de ruido por blanqueo espectral)
- **MNR** (reducción de ruido MMSE-Wiener en macOS)
- **DFNR** (reducción de ruido neuronal DeepFilterNet3)

Estos algoritmos de procesamiento del lado del cliente siguen estando disponibles. Acceda a ellos a través del menú de superposición del espectro o del applet AetherDSP.

Los botones que permanecen en la cuadrícula de la pestaña DSP ahora están dispuestos en un diseño de cuatro columnas con todos los botones DSP del lado del cliente presentes:

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

Nota: La entrada del botón NR en la cuadrícula ahora representa un grupo de botones de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR). Los botones específicos mostrados dependen de la serie del radio y la configuración de compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo.

### Deslizador de nivel DSP

Una fila compartida de deslizador de nivel aparece debajo de la cuadrícula de botones DSP. El deslizador apunta al algoritmo DSP nivelado habilitado más recientemente. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor numérico se muestra a la derecha.

| Control | Rango | Comportamiento |
|---|---|---|
| Deslizador de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP activo. Se reorienta automáticamente cuando habilita un algoritmo diferente. |

La fila del deslizador permanece en el diseño en todo momento. Cuando ningún algoritmo compatible está activo — o cuando solo RNN, ANFT o APF están encendidos — la fila del deslizador se atenúa y no responde a la entrada. Habilitar un algoritmo compatible hace que la fila vuelva a aparecer y reorienta el deslizador hacia ese algoritmo.

Algoritmos a los que el deslizador de nivel puede apuntar: NR, NB, ANF, NRL, NRS, NRF, ANFL.

El deslizador de nivel ahora refleja correctamente el estado del radio en la conexión inicial. Cuando un algoritmo DSP nivelado ya está activo en el perfil guardado del radio, el deslizador aparece inmediatamente en lugar de requerir una activación manual (#startup-slider, v0.9.8).

### Comportamiento del squelch en modo RTTY

A partir de v26.5.1, el botón y el deslizador de squelch están deshabilitados en modo RTTY. El squelch del radio bloquea las señales FSK débiles, lo que interfiere con los decodificadores externos que esperan un flujo de audio continuo a través de DAX. Si el squelch estaba habilitado al cambiar al modo RTTY, se desactiva automáticamente. El estado del squelch guardado se restaura al volver a un modo de voz.

## Entrada de frecuencia en bandas XVTR

Al ingresar una frecuencia en bandas XVTR (rango de 100–999 MHz), el panel VFO aplica una conversión de conveniencia: una entrada de entero simple como `1446` se interpreta como `144.6 MHz` insertando un decimal después del tercer dígito. Esto solo se aplica cuando:
- El slice está sintonizado en una banda XVTR (frecuencia superior a 54 MHz o usando una antena que comienza con `XVT`)
- La frecuencia actual está en el rango de 100–999 MHz (banda de tres dígitos)
- El valor ingresado es superior a 450 MHz y no contiene un punto decimal

Para frecuencias en bandas de 23 cm y microondas (por encima de 1000 MHz), un entero simple se interpreta directamente como MHz (ej., `1296` significa `1296 MHz`, no `129.6 MHz`).

La entrada de frecuencia acepta valores de hasta 50000 MHz en bandas XVTR.

### Reconocimiento explícito de entrada en MHz

A partir de v26.5.3, el analizador de entrada de frecuencia reconoce explícitamente los valores ingresados en formato MHz. Si ingresa una frecuencia superior a 54 MHz usando una notación explícita en MHz (por ejemplo, `144.000` o `432.100`), el analizador la trata como una entrada directa en MHz en lugar de intentar una conversión a Hz o kHz. Esto le permite ingresar frecuencias VHF/UHF directamente sin necesidad de una antena XVTR o una frecuencia preexistente superior a 54 MHz.

El analizador normaliza múltiples puntos (por ejemplo, `14.225.000` se convierte en `14.225000`) usando `FrequencyEntryParser::normalizedMhzText()` antes de intentar analizar. La bandera de entrada explícita en MHz permite que el analizador omita la lógica de conversión Hz/kHz para valores superiores a 54 MHz que se ingresaron claramente como MHz.

## Comportamiento de desplazamiento en slices bloqueados

Cuando un slice está bloqueado por VFO, el desplazamiento de la rueda del ratón sobre el panel VFO no cambia la frecuencia. En su lugar, la visualización de frecuencia muestra brevemente una superposición **LOCKED** para indicar que la sintonización está bloqueada. Esto se aplica tanto en vistas contraídas como expandidas. La notificación la proporciona `SliceModel::notifyTuneBlockedByLock()`.

## Optimización de altura de la pila de pestañas

A partir de v26.5.3, el panel VFO utiliza un widget `TabStack` (una subclase de `QStackedWidget`) que informa solo el tamaño preferido de la pestaña actual. Esto evita un espacio vertical excesivo al cambiar entre pestañas de diferentes alturas — por ejemplo, cuando la pestaña DSP es más alta que la pestaña Mode debido al subcontenedor de modo digital que aparece en modos DIGU/DIGL. No hay cambios en el comportamiento visual; el panel ahora utiliza el espacio de manera más eficiente.

## Mejoras de soporte de temas en v26.6.1

El panel VFO ahora participa completamente en el sistema de temas de AetherSDR. Al panel se le asigna un ámbito de contenedor de tema `spectrum/vfo` para que los clics del inspector en el panel VFO se informen correctamente bajo el ámbito VFO en lugar de propagarse a la visualización del espectro.

Los siguientes tokens de tema se declaran para el panel VFO:
- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

Estos tokens son utilizados por las llamadas sin formato de `QPainter` para el medidor de señal, la insignia del slice y la representación del fondo. Al usar el inspector de temas, al hacer clic en la bandera VFO, la insignida de indicativo o la tira del medidor de señal, estos tokens aparecen en la lista de aciertos.

### Apariencia del deslizador de marca central

El deslizador Pan en la pestaña Audio utiliza un `CenterMarkSlider` que pinta un punto de marca central para indicar la posición neutra (50). A partir de v26.6.1, el relleno del deslizador está anclado desde el centro hacia afuera — el lado izquierdo de la ranura se rellena con el color de fondo, y el lado derecho desde el centro hasta el control se rellena con el color de acento. Esto proporciona una indicación visual del desplazamiento de paneo/balance desde el punto medio. El punto central se pinta en el punto medio de la ranura del deslizador.

### Tematización de botones

Los botones de acción del panel VFO ahora utilizan hojas de estilo conscientes del tema en lugar de colores codificados. El estado presionado usa `{{color.accent}}` y el fondo usa `{{color.background.1}}`. Esto garantiza una apariencia consistente en todos los temas.

## Insignias TX y SPLIT

| Indicador | Estados | Significado |
|---|---|---|
| Insignia TX | TX (rojo) u oculta | Se muestra cuando este slice es el slice de transmisión activo. |
| Insignia SPLIT | SPLIT (ámbar) u oculta | Se muestra cuando TX está asignado a un slice diferente al slice de recepción activo. |

## Mejoras en la barra de pestañas en v26.6.3

La barra de pestañas del panel VFO se ha actualizado para mejorar la accesibilidad y usabilidad. Los botones de pestaña ahora son instancias de `QPushButton` en lugar de elementos `QLabel`, lo que proporciona soporte nativo de enfoque de teclado.

- Presione **Tab** para navegar a través de los botones de pestaña. Un indicador de enfoque (borde inferior azul) aparece en la pestaña enfocada.
- **Enter** o **Space** activa la pestaña enfocada.
- La pestaña Audio ahora admite un menú contextual de clic derecho. Haga clic derecho en la pestaña **Speaker** para alternar el silencio del slice actual directamente sin cambiar de pestaña.

## Accesibilidad de la visualización de frecuencia en v26.6.3

La visualización de frecuencia VFO ahora utiliza un widget `FreqLineEdit` con soporte de accesibilidad. Cuando la tecnología de asistencia está activa, la frecuencia actualiza el árbol de accesibilidad para anunciar los cambios de frecuencia. Esto garantiza que los lectores de pantalla anuncien el valor de frecuencia actual a medida que cambia.

El campo de entrada de frecuencia utiliza `setHintText()` en lugar de `setPlaceholderText()` para la sugerencia de entrada en MHz.

## Dirección de sintonización con la rueda del ratón en v26.6.3

El panel VFO ahora respeta la configuración de rueda del ratón inversa de `InteractionSettings`. Cuando la rueda del ratón inversa está habilitada, desplazar la rueda del ratón sobre el panel VFO sintoniza la frecuencia en la dirección opuesta. Esto se aplica tanto a las vistas contraídas como expandidas.

## Consejos

- En la vista contraída, desplazar la rueda del ratón sobre la franja sintoniza la frecuencia del slice según el tamaño de paso actual — igual que desplazarse sobre la visualización de frecuencia en el panel completo.
- En la vista contraída, hacer clic en la insignia TX pintada en la franja alterna la asignación TX para ese slice. Hacer clic en cualquier otro lugar de la franja expande el panel.
- El panel se voltea automáticamente al lado derecho del marcador VFO si expandirlo quedara recortado por el borde de la ventana. Este comportamiento se aplica tanto en
