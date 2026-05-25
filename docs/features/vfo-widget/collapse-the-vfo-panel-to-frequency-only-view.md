# Contraer el panel VFO a una vista solo de frecuencia

Cuando el espacio en pantalla es limitado, puede contraer el panel VFO a una tira compacta que muestra únicamente la frecuencia del segmento. El estado contraído se guarda por segmento, por lo que persiste entre sesiones.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El panel VFO requiere una conexión activa con el radio.
- El panel VFO del segmento debe estar abierto. Si no está visible, haga clic en la bandera del marcador VFO en la pantalla del espectro correspondiente a ese segmento.

## Pasos

1. Localice la insignia del segmento en el área del encabezado del panel VFO. La insignia muestra el identificador del segmento (por ejemplo, **A** o **B**).
2. Haga clic en la insignia del segmento. El panel se contrae a una tira compacta que solo muestra la frecuencia.
3. Para restaurar el panel completo, haga clic en cualquier lugar de la tira contraída.

## Qué hace cada control

| Control | Valor predeterminado | Ajuste persistente |
|---|---|---|
| Alternar contracción | Expandido | `SliceFlagCollapsed_{N}` |
| Botón de antena RX | Abre el menú de selección de antena para la antena receptora de este segmento. Utiliza `rxAntennaList` del segmento cuando está disponible; de lo contrario, recurre a la lista de antenas del equipo. | Ninguno |
| Botón de antena TX | Abre el menú de selección de antena para la antena transmisora de este segmento. Filtra los puertos de antena solo de recepción. Utiliza `txAntennaList` del segmento cuando está disponible. | Ninguno |
| Visualización de frecuencia | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba en MHz y presione Enter o Tab. | Ninguno |
| Etiqueta de ancho de filtro | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de ajustes predefinidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de información, corrigiendo un desfase de 0,1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). | Ninguno |
| Insignia del segmento | Muestra la letra del segmento. Haga clic para contraer el panel. Muestra texto con formato HTML (#2606). | Ninguno |
| Deslizador de ganancia AF (pestaña Audio) | 100 | Ninguno — refleja el estado en vivo del radio. |
| Deslizador Pan (pestaña Audio) | 50 | Ninguno |
| Botón de silencio (pestaña Audio) | Desactivado | Ninguno |
| Botón y deslizador de squelch (pestaña Audio) | Desactivado | Ninguno |
| Combo AGC (pestaña Audio) | FAST | Ninguno |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Desactivado | Ninguno |
| Botón ADSP (pestaña DSP) | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene estilo de alternancia de DSP del lado del radio, pero no es seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Alterna el Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para el strip. |
| Combo Mode (pestaña Mode) | USB | Ninguno |
| Botones de ajustes predefinidos de filtro (pestaña Mode) | Aplica un ajuste predefinido de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. | `FilterPresets` |
| Botones y etiquetas RIT / XIT (pestaña X/RIT) | Desactivado | Ninguno |
| Combo de canal DAX (pestaña DAX) | Desactivado | Ninguno |
| Botón de grosor del marcador | 1 px | `Slice{N}_MarkerWidth` |
| Botón de bordes de filtro | Mostrado | `Slice{N}_FilterEdgesHidden` |

El ajuste `SliceFlagCollapsed_{N}` se almacena por segmento, donde `{N}` es el número de segmento. Contraer un segmento no afecta a los demás.

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP en el panel VFO ahora muestra solo los algoritmos de reducción de ruido y filtrado proporcionados directamente por el equipo. Los siguientes botones se han eliminado de la cuadrícula de la pestaña DSP:

- **NR2** (reducción de ruido espectral)
- **RN2** (supresión de ruido RNNoise)
- **BNR** (denoising neuronal por GPU)
- **NR4** (reducción de ruido por blanqueo espectral)
- **MNR** (reducción de ruido MMSE-Wiener en macOS)
- **DFNR** (reducción de ruido neuronal DeepFilterNet3)

Estos algoritmos de procesamiento del lado del cliente siguen estando disponibles. Acceda a ellos a través del menú superpuesto del espectro o del applet AetherDSP.

Los botones que permanecen en la cuadrícula de la pestaña DSP ahora están dispuestos en un diseño de cuatro columnas con todos los botones de DSP del lado del cliente presentes:

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

Nota: La entrada del botón NR en la cuadrícula ahora representa un grupo de botones de reducción de ruido (NR, NR2, RN2, NR4, MNR, DFNR, BNR). Los botones específicos que se muestran dependen de la serie del equipo y la configuración de compilación. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo.

### Deslizador de nivel DSP

Una fila compartida de deslizador de nivel aparece debajo de la cuadrícula de botones DSP. El deslizador apunta al algoritmo DSP con nivel que se haya habilitado más recientemente. La etiqueta a la izquierda del deslizador muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor numérico se muestra a la derecha.

| Control | Rango | Comportamiento |
|---|---|---|
| Deslizador de nivel DSP | 0–100 | Establece el nivel para el algoritmo DSP activo. Se reasigna automáticamente cuando habilita un algoritmo diferente. |

La fila del deslizador permanece en el diseño en todo momento. Cuando no hay ningún algoritmo compatible activo — o solo RNN, ANFT o APF está encendido — la fila del deslizador se atenúa y no responde a la entrada. Al habilitar un algoritmo compatible, la fila se vuelve a iluminar y el deslizador se reasigna a ese algoritmo.

Algoritmos a los que el deslizador de nivel puede apuntar: NR, NB, ANF, NRL, NRS, NRF, ANFL.

El deslizador de nivel ahora refleja correctamente el estado del equipo en la conexión inicial. Cuando un algoritmo DSP con nivel ya está activo en el perfil guardado del equipo, el deslizador aparece de inmediato sin necesidad de una alternancia manual (#startup-slider, v0.9.8).

### Comportamiento del squelch en modo RTTY

A partir de v26.5.1, el botón y el deslizador de squelch están deshabilitados en modo RTTY. El squelch del equipo bloquea las señales FSK débiles, lo que interfiere con decodificadores externos que esperan un flujo de audio continuo a través de DAX. Si el squelch estaba habilitado al cambiar al modo RTTY, se desactiva automáticamente. El estado guardado del squelch se restaura al cambiar de nuevo a un modo de voz.

## Entrada de frecuencia en bandas XVTR

Al ingresar una frecuencia en bandas XVTR (rango de 100–999 MHz), el panel VFO aplica una conversión de conveniencia: una entrada de número entero como `1446` se interpreta como `144,6 MHz` insertando un punto decimal después del tercer dígito. Esto solo se aplica cuando:
- El segmento está sintonizado en una banda XVTR (frecuencia superior a 54 MHz o usando una antena que comienza con `XVT`)
- La frecuencia actual está en el rango de 100–999 MHz (banda de tres dígitos)
- El valor ingresado es superior a 450 MHz y no contiene un punto decimal

Para frecuencias en bandas de 23 cm y microondas (por encima de 1000 MHz), un número entero se interpreta directamente como MHz (por ejemplo, `1296` significa `1296 MHz`, no `129,6 MHz`).

La entrada de frecuencia acepta valores de hasta 50000 MHz en bandas XVTR.

### Reconocimiento explícito de entrada en MHz

A partir de v26.5.3, el analizador de entrada de frecuencia ahora reconoce explícitamente los valores ingresados en formato MHz. Si introduce una frecuencia superior a 54 MHz usando una notación explícita en MHz (por ejemplo, `144.000` o `432.100`), el analizador la trata como una entrada directa en MHz en lugar de intentar una conversión a Hz o kHz. Esto permite ingresar frecuencias de VHF/UHF directamente sin necesidad de una antena XVTR o una frecuencia preexistente superior a 54 MHz.

El analizador normaliza los puntos múltiples (por ejemplo, `14.225.000` se convierte en `14.225000`) usando `FrequencyEntryParser::normalizedMhzText()` antes de intentar analizar. La bandera de entrada explícita en MHz permite que el analizador omita la lógica de conversión a Hz/kHz para valores superiores a 54 MHz que se ingresaron claramente como MHz.

## Comportamiento de desplazamiento en segmentos bloqueados

Cuando un segmento está bloqueado por VFO, el desplazamiento de la rueda del ratón sobre el panel VFO no cambia la frecuencia. En su lugar, la pantalla de frecuencia muestra brevemente una superposición **LOCKED** para indicar que la sintonización está bloqueada. Esto se aplica tanto en la vista contraída como en la expandida. La notificación la proporciona `SliceModel::notifyTuneBlockedByLock()`.

## Optimización de altura de la pila de pestañas

A partir de v26.5.3, el panel VFO utiliza un widget `TabStack` (una subclase de `QStackedWidget`) que informa solo del tamaño preferido de la pestaña actual. Esto evita el espacio vertical excesivo al cambiar entre pestañas de diferentes alturas, por ejemplo, cuando la pestaña DSP es más alta que la pestaña Mode debido al subcontenedor de modo digital que aparece en los modos DIGU/DIGL. Sin cambios en el comportamiento visual; el panel ahora utiliza el espacio de manera más eficiente.

## Consejos

- En la vista contraída, desplazar la rueda del ratón sobre la tira sintoniza la frecuencia del segmento en el tamaño de paso actual, igual que al desplazarse sobre la pantalla de frecuencia en el panel completo.
- En la vista contraída, hacer clic en la insignia TX pintada en la tira alterna la asignación de TX para ese segmento. Hacer clic en cualquier otro lugar de la tira expande el panel.
- El panel se voltea automáticamente al lado derecho del marcador VFO si al expandirlo quedara recortado por el borde de la ventana. Este comportamiento se aplica tanto en estado expandido como contraído.
- Para acceder a NR2, RN2, BNR, NR4, MNR o DFNR, haga clic derecho en la pantalla del espectro para abrir el menú superpuesto, o abra el applet AetherDSP.

## Relacionados

- [VFO Panel overview](overview.md)
- [Tune the radio by typing a frequency into the VFO panel](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Change the VFO marker line thickness](change-the-vfo-marker-line-thickness.md)
- [Hide or show filter edge lines on the spectrum](hide-or-show-filter-edge-lines-on-the-spectrum.md)
