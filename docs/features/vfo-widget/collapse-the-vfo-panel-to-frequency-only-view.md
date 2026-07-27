# Colapsar el panel VFO a una vista solo de frecuencia

Cuando el espacio en pantalla es limitado, puede colapsar el panel VFO a una tira compacta que muestra únicamente la frecuencia del slice. El estado colapsado se guarda por cada slice, por lo que persiste entre sesiones.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa con el radio.
- El panel VFO del slice debe estar abierto. Si no es visible, haga clic en la bandera marcadora VFO en la pantalla del espectro de ese slice.

## Pasos

1. Localice la insignia del slice en el área del encabezado del panel VFO. La insignia muestra el identificador del slice (por ejemplo, **A** o **B**).
2. Haga clic en la insignia del slice. El panel se colapsa en una tira compacta que solo muestra la frecuencia.
3. Para restaurar el panel completo, haga clic en cualquier parte de la tira colapsada.

## Qué hace cada control

| Control | Valor predeterminado | Ajuste persistente |
|---|---|---|
| Alternador de colapso | Expandido | `SliceFlagCollapsed_{N}` |
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de este slice. Usa la `rxAntennaList` del slice cuando está disponible; de lo contrario, recurre a la lista de antenas del radio. | Ninguno |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de este slice. Filtra los puertos de antena solo RX. Usa la `txAntennaList` del slice cuando está disponible. | Ninguno |
| Visualización de frecuencia | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. | Ninguno |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). | Ninguno |
| Insignia del slice | Muestra la letra del slice. Haga clic para colapsar el panel. Muestra texto con formato HTML (#2606). | Ninguno |
| Deslizador de ganancia AF (pestaña Audio) | 100 | Ninguno — refleja el estado en vivo del radio. |
| Deslizador Pan (pestaña Audio) | 50 | Ninguno |
| Botón Mute (pestaña Audio) | Apagado | Ninguno |
| Botón + deslizador Squelch (pestaña Audio) | Apagado | Ninguno |
| Combo AGC (pestaña Audio) | FAST | Ninguno |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Apagado | Ninguno |
| Botón ADSP (pestaña DSP) | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene estilo como un alternador DSP del lado del radio pero no es marcable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Alterna el Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX (v0.9.8). | Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena. |
| Combo Mode (pestaña Mode) | USB | Ninguno |
| Botones preestablecidos de filtro (pestaña Mode) | Aplica un ancho de filtro guardado preestablecido. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. | `FilterPresets` |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Apagado | Ninguno |
| Combo de canal DAX (pestaña DAX) | Apagado | Ninguno |
| Botón de grosor de marcador | 1 px | `Slice{N}_MarkerWidth` |
| Botón de bordes de filtro | Mostrado | `Slice{N}_FilterEdgesHidden` |

El ajuste `SliceFlagCollapsed_{N}` se almacena por slice, donde `{N}` es el número de slice. Colapsar un slice no afecta a otros slices.

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP en el panel VFO ahora muestra solo los algoritmos de reducción de ruido y filtrado proporcionados directamente por el radio. Los siguientes botones se han eliminado de la cuadrícula de la pestaña DSP:

- **NR2** (reducción de ruido espectral)
- **RN2** (supresión de ruido RNNoise)
- **BNR** (eliminación de ruido neuronal por GPU)
- **NR4** (reducción de ruido por blanqueo espectral)
- **MNR** (reducción de ruido MMSE-Wiener para macOS)
- **DFNR** (reducción de ruido neuronal DeepFilterNet3)

Estos algoritmos de procesamiento del lado cliente aún están disponibles. Acceda a ellos a través del menú superpuesto del espectro o del applet de AetherDSP.

Los botones que permanecen en la cuadrícula de la pestaña DSP ahora están organizados en un diseño de cuatro columnas con todos los botones DSP del lado cliente presentes:

| Posición | Botón |
|---|---|
| Fila 0, Col 0 | NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR |
| Fila 0, Col 1 | NRL |
| Fila 0, Col 2 | NRS |
| Fila 0, Col 3 | RNN |
| Fila 1, Col 0 | NRF |
| Fila 1, Cols 1-3 | (vacío) |
| Fila 2, Col 0 | ADSP |
| Fila 2, Cols 1-2 | AetherVoice (abarca 2 columnas) |

Nota: La entrada del botón NR en la cuadrícula ahora representa un grupo de botones de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR). Los botones específicos que se muestran dependen de la serie del radio y la configuración de compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo.

### Deslizador de nivel DSP

Una fila de deslizador de nivel compartido aparece debajo de la cuadrícula de botones DSP. El deslizador se dirige al algoritmo DSP nivelado que se haya habilitado más recientemente. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor numérico se muestra a la derecha.

| Control | Rango | Comportamiento |
|---|---|---|
| Deslizador de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP activo. Se redirige automáticamente cuando se habilita un algoritmo diferente. |

La fila del deslizador permanece en el diseño en todo momento. Cuando ningún algoritmo compatible está activo — o cuando solo RNN, ANFT o APF están encendidos — la fila del deslizador se atenúa y no responde a la entrada. Habilitar un algoritmo compatible vuelve a atenuar la fila y redirige el deslizador a ese algoritmo.

Algoritmos a los que el deslizador de nivel puede dirigirse: NR, NB, ANF, NRL, NRS, NRF, ANFL.

El deslizador de nivel ahora refleja correctamente el estado del radio en la conexión inicial. Cuando un algoritmo DSP nivelado ya está activo en el perfil guardado del radio, el deslizador aparece inmediatamente sin necesidad de un alternado manual (#startup-slider, v0.9.8).

### Comportamiento de Squelch en modo RTTY

A partir de v26.5.1, el botón y el deslizador de squelch están deshabilitados en modo RTTY. El squelch del radio bloquea las señales FSK débiles, lo que interfiere con decodificadores externos que esperan un flujo de audio continuo a través de DAX. Si el squelch estaba habilitado al cambiar al modo RTTY, se apaga automáticamente. El estado de squelch guardado se restaura al cambiar de nuevo a un modo de voz.

## Entrada de frecuencia en bandas XVTR

Al ingresar una frecuencia en bandas XVTR (rango de 100–999 MHz), el panel VFO aplica una conversión de conveniencia: una entrada de entero simple como `1446` se interpreta como `144.6 MHz` insertando un decimal después del tercer dígito. Esto solo se aplica cuando:
- El slice está sintonizado en una banda XVTR (frecuencia superior a 54 MHz o usando una antena que comienza con `XVT`)
- La frecuencia actual está en el rango de 100–999 MHz (banda de tres dígitos)
- El valor ingresado está por encima de 450 MHz y no contiene un punto decimal

Para frecuencias en bandas de 23 cm y microondas (por encima de 1000 MHz), un entero simple se interpreta directamente como MHz (por ejemplo, `1296` significa `1296 MHz`, no `129.6 MHz`).

La entrada de frecuencia acepta valores de hasta 50000 MHz en bandas XVTR.

### Reconocimiento explícito de entrada en MHz

A partir de v26.5.3, el analizador de entrada de frecuencia ahora reconoce explícitamente los valores ingresados en formato MHz. Si ingresa una frecuencia superior a 54 MHz usando una notación explícita en MHz (por ejemplo, `144.000` o `432.100`), el analizador lo trata como una entrada directa en MHz en lugar de intentar una conversión a Hz o kHz. Esto le permite ingresar frecuencias VHF/UHF directamente sin requerir una antena XVTR o una frecuencia preexistente superior a 54 MHz.

El analizador normaliza múltiples puntos (por ejemplo, `14.225.000` se convierte en `14.225000`) usando `FrequencyEntryParser::normalizedMhzText()` antes de intentar analizar. La bandera de entrada explícita en MHz permite que el analizador omita la lógica de conversión Hz/kHz para valores superiores a 54 MHz que se ingresaron claramente como MHz.

## Comportamiento de desplazamiento en slices bloqueados

Cuando un slice está bloqueado por VFO, el desplazamiento de la rueda del mouse sobre el panel VFO no cambia la frecuencia. En su lugar, la visualización de frecuencia muestra brevemente una superposición **LOCKED** para indicar que la sintonización está bloqueada. Esto se aplica tanto en vistas colapsadas como expandidas. La notificación la proporciona `SliceModel::notifyTuneBlockedByLock()`.

## Optimización de altura de la pila de pestañas

A partir de v26.5.3, el panel VFO usa un widget `TabStack` (una subclase de `QStackedWidget`) que informa solo el tamaño preferido de la pestaña actual. Esto evita un espacio vertical excesivo al cambiar entre pestañas de diferentes alturas — por ejemplo, cuando la pestaña DSP es más alta que la pestaña Mode debido al subcontenedor de modo digital que aparece en modos DIGU/DIGL. No hay cambios en el comportamiento visual; el panel ahora usa el espacio de manera más eficiente.

## Mejoras de soporte de temas en v26.6.1

El panel VFO ahora participa completamente en el sistema de temas de AetherSDR. Al panel se le asigna un ámbito de contenedor de tema `spectrum/vfo` para que los clics del inspector en el panel VFO se reporten correctamente bajo el ámbito VFO en lugar de propagarse a la pantalla del espectro.

Los siguientes tokens de tema se declaran para el panel VFO:
- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

Estos tokens son utilizados por llamadas `QPainter` sin procesar para el medidor de señal, la insignia del slice y la representación del fondo. Al usar el inspector de temas, al hacer clic en la bandera VFO, la insignida de indicativo o la tira del medidor de señal, estos tokens aparecen en la lista de aciertos.

### Apariencia del deslizador de marca central

El deslizador Pan en la pestaña Audio usa un `CenterMarkSlider` que pinta un punto de marca central para indicar la posición neutral (50). A partir de v26.6.1, el relleno del deslizador se ancla desde el centro hacia afuera — el lado izquierdo de la ranura se llena con el color de fondo, y el lado derecho desde el centro hasta el mango se llena con el color de acento. Esto proporciona una indicación visual del desplazamiento de pan/balance desde el punto medio. El punto central se pinta en el punto medio de la ranura del deslizador.

### Tematización de botones

Los botones de acción del panel VFO ahora usan hojas de estilo conscientes del tema en lugar de colores codificados. El estado presionado usa `{{color.accent}}` y el fondo usa `{{color.background.1}}`. Esto asegura una apariencia consistente en todos los temas.

## Insignias TX y SPLIT

| Indicador | Estados | Significado |
|---|---|---|
| Insignia TX | TX (rojo) u oculto | Se muestra cuando este slice es el slice de transmisión activo. |
| Insignia SPLIT | SPLIT (ámbar) u oculto | Se muestra cuando TX está asignado a un slice diferente al slice de recepción activo. |

## Mejoras en la barra de pestañas en v26.6.3

La barra de pestañas del panel VFO se ha actualizado para accesibilidad y usabilidad. Los botones de pestaña ahora son instancias de `QPushButton` en lugar de elementos `QLabel`, proporcionando soporte nativo de enfoque de teclado.

- Presione **Tab** para navegar a través de los botones de pestaña. Un indicador de enfoque (borde inferior azul) aparece en la pestaña enfocada.
- **Enter** o **Space** activa la pestaña enfocada.
- La pestaña Audio ahora admite un menú contextual con clic derecho. Haga clic derecho en la pestaña **Speaker** para alternar el silencio del slice actual directamente sin cambiar de pestaña.

## Accesibilidad de la visualización de frecuencia en v26.6.3

La pantalla de frecuencia VFO ahora usa un widget `FreqLineEdit` con soporte de accesibilidad. Cuando la tecnología de asistencia está activa, la frecuencia actualiza el árbol de accesibilidad para anunciar los cambios de frecuencia. Esto asegura que los lectores de pantalla anuncien el valor de frecuencia actual a medida que cambia.

El campo de entrada de frecuencia usa `setHintText()` en lugar de `setPlaceholderText()` para la sugerencia de entrada en MHz.

## Dirección de sintonización con rueda del mouse en v26.6.3

El panel VFO ahora respeta la configuración de rueda del mouse inversa de `InteractionSettings`. Cuando la rueda del mouse inversa está habilitada, desplazar la rueda del mouse sobre el panel VFO sintoniza la frecuencia en la dirección opuesta. Esto se aplica tanto en vistas colapsadas como expandidas.

## Consejo

- En la vista colapsada, desplazar la rueda del mouse sobre la tira sintoniza la frecuencia del slice en el tamaño de paso actual — lo mismo que desplazarse sobre la pantalla de frecuencia en el panel completo.
- En la vista colapsada, hacer clic en la insignia TX pintada en la tira alterna la asignación TX para ese slice. Hacer clic en cualquier otro lugar de la tira expande el panel.
- El panel se voltea al lado derecho del marcador VFO automáticamente si expandirlo se recortaría con el borde de la ventana. Este comportamiento se aplica tanto en estados expandidos como colapsados
