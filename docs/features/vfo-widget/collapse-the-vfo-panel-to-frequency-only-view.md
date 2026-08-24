# Colapsar el panel VFO a vista solo de frecuencia

Cuando el espacio de pantalla es limitado, puede colapsar el panel VFO a una tira compacta que muestra solo la frecuencia del slice. El estado de colapso se guarda por slice, por lo que persiste entre sesiones.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO del slice debe estar abierto. Si no está visible, haga clic en la bandera del marcador VFO en la pantalla del espectro para ese slice.

## Pasos

1. Localice la insignia del slice en el área del encabezado del panel VFO. La insignia muestra el identificador del slice (por ejemplo, **A** o **B**).
2. Haga clic en la insignia del slice. El panel se colapsa a una tira compacta de solo frecuencia.
3. Para restaurar el panel completo, haga clic en cualquier lugar de la tira colapsada.

## Qué hace cada control

| Control | Predeterminado | Ajuste persistido |
|---|---|---|
| Alternancia de colapso | Expandido | `SliceFlagCollapsed_{N}` |
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de este slice. Usa la `rxAntennaList` del slice cuando esté disponible; de lo contrario, recurre a la lista de antenas de la radio. | Ninguno |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de este slice. Filtra los puertos de antena solo RX. Usa la `txAntennaList` del slice cuando esté disponible. | Ninguno |
| Visualización de frecuencia | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. | Ninguno |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de ajustes preestablecidos de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desfase de 0,1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). | Ninguno |
| Insignia del slice | Muestra la letra del slice. Haga clic para colapsar el panel. Muestra texto con formato HTML (#2606). | Ninguno |
| Deslizador de ganancia AF (pestaña Audio) | 100 | Ninguno: refleja el estado en vivo de la radio. |
| Deslizador Pan (pestaña Audio) | 50 | Ninguno |
| Botón de silencio (pestaña Audio) | Off | Ninguno |
| Botón + deslizador de squelch (pestaña Audio) | Off | Ninguno |
| Combo AGC (pestaña Audio) | FAST | Ninguno |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Off | Ninguno |
| Botón MN (pestaña DSP) | Off. Se muestra solo en radios que informan soporte de notch manual | Ninguno |
| Botón ADSP (pestaña DSP) | Abre el diálogo de Ajustes de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de alternancia DSP del lado de la radio pero no marcable. Al hacer clic, eleva y enfoca el diálogo no modal de Ajustes de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Alterna la tira de canal de audio Aetherial: la suite unificada de DSP TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes de menú/cadena para la tira. |
| Combo Mode (pestaña Mode) | USB | Ninguno |
| Botones de ajustes preestablecidos de filtro (pestaña Mode) | Aplica un ajuste preestablecido de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa posición. | `FilterPresets` |
| Botones + etiquetas RIT / XIT (pestaña X/RIT) | Off | Ninguno |
| Combo de canal DAX (pestaña DAX) | Off | Ninguno |
| Botón de grosor de marcador | 1 px | `Slice{N}_MarkerWidth` |
| Botón de bordes de filtro | Shown | `Slice{N}_FilterEdgesHidden` |

El ajuste `SliceFlagCollapsed_{N}` se guarda por slice, donde `{N}` es el número del slice. Colapsar un slice no afecta a otros slices.

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP del panel VFO ahora muestra solo los algoritmos de reducción de ruido y filtrado suministrados directamente por la radio. Los siguientes botones se han eliminado de la cuadrícula de la pestaña DSP:

- **NR2** (reducción de ruido espectral)
- **RN2** (supresión de ruido RNNoise)
- **BNR** (denoizado neuronal por GPU)
- **NR4** (reducción de ruido por blanqueo espectral)
- **MNR** (reducción de ruido MMSE-Wiener para macOS)
- **DFNR** (reducción de ruido neuronal DeepFilterNet3)

Estos algoritmos de procesamiento del lado del cliente siguen disponibles. Acceda a ellos a través del menú de superposición del espectro o del applet AetherDSP.

Los botones que permanecen en la cuadrícula de la pestaña DSP ahora se organizan en un diseño de cuatro columnas con todos los botones DSP del lado del cliente presentes:

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

Nota: La entrada del botón NR en la cuadrícula ahora representa un grupo de botones de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR). Los botones específicos que se muestran dependen de la serie de radio y la configuración de compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Ajustes de AetherDSP para ese algoritmo.

### Botón de notch manual (MN) en v26.8.4

A partir de v26.8.4, la pestaña DSP incluye un botón **MN** (notch manual). Este botón está oculto por defecto y aparece solo cuando la radio conectada informa soporte de notch manual (`hasManualNotch`). Cuando esté disponible, habilita el filtro de notch manual para el slice y el deslizador de nivel DSP se redirige al nivel MN.

### Deslizador de nivel DSP

Una fila compartida de deslizador de nivel aparece debajo de la cuadrícula de botones DSP. El deslizador apunta al algoritmo DSP con nivel que se haya habilitado más recientemente. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor numérico se muestra a la derecha.

| Control | Rango | Comportamiento |
|---|---|---|
| Deslizador de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP activo. Se redirige automáticamente cuando habilita un algoritmo diferente. |

La fila del deslizador permanece en el diseño en todo momento. Cuando no hay ningún algoritmo compatible activo — o cuando solo RNN, ANFT o APF está encendido — la fila del deslizador se atenúa y no responde a la entrada. Habilitar un algoritmo compatible restaura la fila y redirige el deslizador a ese algoritmo.

Algoritmos a los que el deslizador de nivel puede apuntar: NR, NB, ANF, NRL, NRS, NRF, ANFL, MN.

El deslizador de nivel ahora refleja correctamente el estado de la radio en la conexión inicial. Cuando un algoritmo DSP con nivel ya está activo en el perfil guardado de la radio, el deslizador aparece inmediatamente en lugar de requerir una alternancia manual (#startup-slider, v0.9.8).

### Comportamiento del squelch en modo RTTY

A partir de v26.5.1, el botón y el deslizador de squelch están deshabilitados en modo RTTY. El squelch de la radio bloquea las señales FSK débiles, lo que interfiere con decodificadores externos que esperan un flujo de audio continuo a través de DAX. Si el squelch estaba habilitado al cambiar al modo RTTY, se apaga automáticamente. El estado guardado del squelch se restaura al volver a un modo de voz.

## Entrada de frecuencia en bandas XVTR

Al ingresar una frecuencia en bandas XVTR (rango de 100–999 MHz), el panel VFO aplica una conversión de conveniencia: una entrada entera simple como `1446` se interpreta como `144.6 MHz` insertando un decimal después del tercer dígito. Esto solo se aplica cuando:
- El slice está sintonizado a una banda XVTR (frecuencia superior a 54 MHz o usando una antena que comience con `XVT`)
- La frecuencia actual está en el rango de 100–999 MHz (banda de tres dígitos)
- El valor ingresado es superior a 450 MHz y no contiene punto decimal

Para frecuencias en bandas de 23 cm y microondas (superiores a 1000 MHz), un entero simple se interpreta directamente como MHz (por ejemplo, `1296` significa `1296 MHz`, no `129.6 MHz`).

La entrada de frecuencia acepta valores de hasta 50000 MHz en bandas XVTR.

### Reconocimiento explícito de entrada en MHz

A partir de v26.5.3, el analizador de entrada de frecuencia ahora reconoce explícitamente los valores ingresados en formato MHz. Si ingresa una frecuencia superior a 54 MHz usando notación explícita en MHz (por ejemplo, `144.000` o `432.100`), el analizador la trata como una entrada directa en MHz en lugar de intentar conversión a Hz o kHz. Esto le permite ingresar frecuencias VHF/UHF directamente sin requerir una antena XVTR ni una frecuencia preexistente superior a 54 MHz.

El analizador normaliza múltiples puntos (por ejemplo, `14.225.000` se convierte en `14.225000`) usando `FrequencyEntryParser::normalizedMhzText()` antes de intentar analizar. La marca de entrada explícita en MHz permite que el analizador omita la lógica de conversión Hz/kHz para valores superiores a 54 MHz que se ingresaron claramente como MHz.

## Comportamiento de desplazamiento en slices bloqueados

Cuando un slice está bloqueado por VFO, el desplazamiento de la rueda del mouse sobre el panel VFO no cambia la frecuencia. En su lugar, la visualización de frecuencia muestra brevemente una superposición de **LOCKED** para indicar que la sintonización está bloqueada. Esto se aplica tanto en vista colapsada como expandida. La notificación la proporciona `SliceModel::notifyTuneBlockedByLock()`.

## Optimización de altura de la pila de pestañas

A partir de v26.5.3, el panel VFO usa un widget `TabStack` (una subclase de `QStackedWidget`) que informa solo el tamaño preferido de la pestaña actual. Esto evita espacio vertical excesivo al cambiar entre pestañas de diferentes alturas, por ejemplo, cuando la pestaña DSP es más alta que la pestaña Mode debido al subcontenedor de modo digital que aparece en modos DIGU/DIGL. No hay cambios visuales de comportamiento; el panel ahora usa el espacio de manera más eficiente.

## Mejoras de soporte de temas en v26.6.1

El panel VFO ahora participa completamente en el sistema de temas de AetherSDR. Al panel se le asigna un ámbito de contenedor de tema `spectrum/vfo` para que los clics del inspector en el panel VFO se informen correctamente bajo el ámbito VFO en lugar de propagarse a la pantalla del espectro.

Los siguientes tokens de tema se declaran para el panel VFO:
- `color.background.0`
- `color.background.1`
- `color.background.2`
- `color.text.primary`
- `color.text.label`
- `color.accent`
- `color.accent.bright`

Estos tokens se usan en llamadas directas de `QPainter` para el medidor de señal, la insignia del slice y el renderizado del fondo. Al usar el inspector de temas, al hacer clic en la bandera VFO, la insignia de indicativo o la tira del medidor de señal se muestran estos tokens en la lista de resultados.

### Apariencia del deslizador con marca central

El deslizador Pan en la pestaña Audio usa un `CenterMarkSlider` que dibuja un punto de marca central para indicar la posición neutra (50). A partir de v26.6.1, el relleno del deslizador se ancla desde el centro hacia afuera: el lado izquierdo de la ranura se rellena con el color de fondo, y el lado derecho desde el centro hasta el controlador se rellena con el color de acento. Esto proporciona una indicación visual del desfase de pan/balance desde el punto medio. El punto central se dibuja en el punto medio de la ranura del deslizador.

### Tematización de botones

Los botones de acción del panel VFO ahora usan hojas de estilo conscientes del tema en lugar de colores codificados. El estado presionado usa `{{color.accent}}` y el fondo usa `{{color.background.1}}`. Esto asegura una apariencia consistente en todos los temas.

## Insignias TX y SPLIT

| Indicador | Estados | Significado |
|---|---|---|
| Insignia TX | TX (rojo) u oculta | Se muestra cuando este slice es el slice transmisor activo. |
| Insignia SPLIT | SPLIT (ámbar) u oculta | Se muestra cuando TX está asignado a un slice diferente del slice receptor activo. |

## Mejoras de la barra de pestañas en v26.6.3

La barra de pestañas del panel VFO se ha actualizado para accesibilidad y usabilidad. Los botones de pestaña ahora son instancias de `QPushButton` en lugar de elementos `QLabel`, lo que proporciona soporte nativo de enfoque por teclado.

- Presione **Tab** para navegar por los botones de pestaña. Un indicador de enfoque (borde inferior azul) aparece en la pestaña enfocada.
- **Enter** o **Space** activa la pestaña enfocada.
- La pestaña Audio ahora admite un menú contextual con clic derecho. Haga clic derecho en la pestaña **Speaker** para alternar el silencio del slice actual directamente sin cambiar de pestaña.

## Accesibilidad de la visualización de frecuencia en v26.6.3

La visualización de frecuencia del VFO ahora usa un widget `FreqLineEdit` con soporte de accesibilidad. Cuando la tecnología de asistencia está activa, la frecuencia actualiza el árbol de accesibilidad para anunciar los cambios de frecuencia. Esto asegura que los lectores de pantalla anuncien el valor de frecuencia actual a medida que cambia.

El campo de entrada de frecuencia usa `setHintText()` en lugar de `setPlaceholderText()` para la sugerencia de entrada en MHz.

## Dirección de sintonización con rueda del mouse en v26.6.3

El panel VFO ahora respeta el ajuste de rueda del mouse inversa de `InteractionSettings`. Cuando la rueda del mouse inversa está habilitada, desplazarse con la rueda del mouse sobre el panel VFO sintoniza la frecuencia en la dirección opuesta. Esto se aplica tanto en vista colapsada como expandida.

## Corrección de clic derecho con
