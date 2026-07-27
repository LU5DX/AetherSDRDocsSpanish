# Trabajar con un repetidor de FM usando tono CTCSS y desplazamiento +/- 

Configure un slice para operación dúplex en FM con desplazamiento de repetidor y un tono de acceso CTCSS para poder escuchar la salida del repetidor y activarlo correctamente al transmitir.

## Antes de comenzar

- AetherSDR está conectado a su FLEX-8600.
- El applet RX Controls está visible en la barra lateral derecha. Si no lo está, haga clic en el botón de la bandeja RX en la barra lateral derecha.
- Usted conoce la frecuencia de salida del repetidor, la dirección del desplazamiento, la magnitud del desplazamiento y la frecuencia del tono CTCSS.

## Pasos

1. En el applet RX Controls, haga clic en el combo Mode y seleccione **FM** (o **NFM** para FM estrecha).
2. Haga clic en la etiqueta Frequency para abrir el campo de edición de frecuencia. Escriba la frecuencia de **salida** (recepción) del repetidor en MHz y presione Enter.
3. En el control giratorio **Offset (FM)**, establezca la magnitud del desplazamiento en MHz. Use las flechas del control giratorio o escriba un valor directamente. El rango válido es de 0.0 a 100.0 MHz en pasos de 0.1 MHz. El valor predeterminado es 0.0 MHz.
4. Establezca la dirección del desplazamiento haciendo clic en uno de los tres botones de alternancia:
   - **−** — La frecuencia de TX está por debajo de la frecuencia de RX.
   - **Simplex** — La frecuencia de TX es igual a la frecuencia de RX (predeterminado).
   - **+** — La frecuencia de TX está por encima de la frecuencia de RX.
5. Haga clic en el combo **Tone mode (FM)** (predeterminado: **Off**) y seleccione **CTCSS TX**.
6. Haga clic en el combo **CTCSS tone value** y seleccione la frecuencia de tono requerida por el repetidor. Los tonos disponibles siguen el estándar de 41 tonos EIA/TIA-603, desde 67.0 Hz hasta 254.1 Hz.
7. Confirme que el squelch esté configurado adecuadamente para la banda. Si es necesario, consulte [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md).

## Qué hace cada control

| Control            | Predeterminado | Rango válido / opciones                      |
|--------------------|----------------|----------------------------------------------|
| Combo Mode         | USB            | FM, NFM, DFM (entre otros)                   |
| Tone mode (FM)     | Off            | Off, CTCSS TX                                |
| CTCSS tone value   | —              | 67.0 Hz – 254.1 Hz (41 tonos EIA/TIA-603)    |
| Offset (FM)        | 0.0 MHz        | 0.0 – 100.0 MHz, paso 0.1                    |
| − (desplazamiento hacia abajo) | —    | alternancia                                  |
| Simplex            | marcado        | alternancia                                  |
| + (desplazamiento hacia arriba) | —   | alternancia                                  |
| REV                | —              | alternancia                                  |

## Consejos

- Si necesita escuchar en la frecuencia de entrada del repetidor para verificar si el canal está ocupado antes de transmitir, haga clic en **REV** para intercambiar la dirección del desplazamiento temporalmente.
- Los modos de la familia FM ocultan los botones de preselección de ancho de filtro. Esto es normal; el ancho de filtro para FM es fijado por el modo mismo.
- Los botones de pestaña de slice y la insignia de slice tienen códigos de color por slice usando SliceColorManager (v0.9.3+). Los colores persisten entre sesiones y se reflejan en las pestañas de slice, la insignia de slice, los widgets de VFO y las barras de medidor.
- Cuando la radio informa una cantidad diferente de slices disponibles de la que la fila de pestañas fue construida, AetherSDR ahora elimina los botones de pestaña de slice existentes y los reconstruye para la nueva cantidad antes de reconectar los controladores de clic (v0.9.5.1, #2254). Esto evita que aparezcan botones obsoletos después de una reconexión o un cambio en la configuración del hardware.
- Los preselecciones de ancho de filtro se almacenan en el formato `lo:hi` (bordes de la banda pasante en Hz) o como un valor de ancho simple, dependiendo de si la preselección se guardó con posiciones de borde explícitas. Ambos formatos se leen correctamente cuando vuelve a abrir el applet o cambia de modo (#2259).
- El indicador de ancho de filtro se comparte con el panel VFO a través de `RxApplet::formatFilterWidth()`. En v0.9.8+, este método es ahora una función estática pública para que ambos widgets produzcan un formato idéntico y consciente del modo para modos SSB, digitales y AM (#2197).
- Los atajos de ensanchar/estrechar (ej. Ctrl+Shift+W, Ctrl+Shift+N) llaman a `stepFilterWidth(int direction)`, que recorre la lista de preselecciones de filtro por modo para encontrar el siguiente ancho válido y lo aplica con la geometría de borde correcta para el modo actual (#2208).
- La insignia de slice ahora admite formato de texto enriquecido (HTML) para la visualización de la letra del slice (#2606).
- La selección de antena tanto para RX como para TX ahora prioriza la lista de antenas del propio slice cuando está disponible. El menú muestra las etiquetas de antena con información sobre herramientas y consejos de estado, con los datos reales de la antena almacenados por separado del texto mostrado. Los menús de antena de TX filtran los puertos con el prefijo "RX" e incluyen solo antenas que coinciden con patrones como "ANT", "TX" o "XVTR".
- De forma predeterminada, AetherSDR utiliza un algoritmo de squelch Auto que sobrescribe el squelchLevel del slice con valores sugeridos por el algoritmo. El último umbral de squelch Manual elegido por el usuario ahora se conserva del lado del cliente en la configuración `LastManualSquelchLevel` y se restaura entre sesiones y ciclos de modo.
- El botón de silencio utiliza un mecanismo de un solo clic diferido para evitar conflictos con acciones de doble clic. Un solo clic silencia o reactiva el slice actual. Un doble clic silencia o reactiva todos los slices propios. El icono se actualiza solo cuando la radio confirma el cambio de estado de silencio, asegurando que el estado mostrado siempre coincida con el estado real de la radio.
- El control deslizante **AGC Threshold** tiene un menú contextual de clic derecho. Haga clic derecho en el control deslizante y seleccione **Calibrate AGC-T against noise floor…** para abrir el panel de calibración de ruido AGC-T. La información sobre herramientas también anuncia esta función.
- Al ingresar una frecuencia en el campo de edición Frequency, AetherSDR usa `FrequencyEntryParser` para normalizar la entrada. Si escribe un valor superior a 54 MHz sin estar en una antena XVTR, el analizador verifica si se ingresó como un valor explícito en MHz. Si es así, la frecuencia máxima permitida se eleva a 50000 MHz, lo que permite ingresar frecuencias de VHF/UHF por encima del límite normal de 54 MHz sin cambiar primero a una antena XVTR (ej., escribir 146.520 MHz en una antena no XVTR).
- Los botones de dirección de desplazamiento y el botón REV son parte de un grupo de botones exclusivo; seleccionar uno deselecciona automáticamente los demás.
- El control deslizante de paneo L/R ahora pinta su relleno desde el centro hacia afuera. Esto proporciona una indicación visual de la posición neutral (centro) de un vistazo. La marca central es un pequeño punto pintado en la ranura.
- Los botones de preselección de filtro y otros botones con estilo ahora usan colores de hoja de estilo tokenizados a través de ThemeManager. Esto significa que la apariencia del botón se actualiza automáticamente cuando cambia de tema, de manera consistente con el resto de la interfaz de usuario (v26.6.1).
- El menú de antena RX ahora incluye tokens de antena virtual del KiwiSDR cuando un administrador de KiwiSDR está activo. Los tokens se agregan a la lista de opciones y no son duplicados de antenas físicas existentes. Seleccionar una antena virtual activa una señal `kiwiRxAntennaSelected` en lugar de llamar a `setRxAntenna` directamente (#2781).
- El menú de antena RX se reconstruye como un menú emergente (popup menu) en lugar de un menú en línea. El menú se elimina automáticamente cuando se oculta (#2781).

## Solución de problemas

- **El repetidor no responde a sus transmisiones** — Confirme que el valor del tono CTCSS coincida con el que espera el repetidor y que el modo Tone mode esté configurado en **CTCSS TX** y no en **Off**.
- **La frecuencia de TX parece incorrecta** — Verifique que el botón de dirección de desplazamiento (**−**, **Simplex** o **+**) coincida con la dirección de desplazamiento publicada del repetidor y que el valor Offset (FM) esté configurado con la magnitud correcta (ej. 0.6 MHz para un repetidor típico de 2 m).
- **Los controles Tone mode y CTCSS no son visibles** — El modo del slice debe ser **FM**, **NFM** o **DFM**. Estos controles están ocultos en todos los demás modos.
- **Los controles de squelch están atenuados** — El squelch se desactiva automáticamente cuando el modo del slice es **DIGU**, **DIGL**, **NT**, **RTTY**, **CW** o **CWL**. Cambie a un modo FM o SSB para habilitar los controles de squelch.
- **Los botones de pestaña de slice aparecen incorrectos después de reconectar** — Si la fila de pestañas de slice muestra la cantidad incorrecta de botones o un diseño desactualizado después de que la radio se reconecta, desconecte y reconecte manualmente. En v0.9.5.1 esto se corrige automáticamente: el applet llama a `clearSliceButtons()` para eliminar los botones antiguos y restaurar la insignia de slice estática antes de reconstruir la fila de pestañas para la nueva cantidad de slices (#2254).
- **El botón de preselección de filtro no cambia la banda pasante** — Si el ancho actual no es un valor de preselección estándar, el paso de ensanchar/estrechar puede no cambiar la banda pasante. Esto es un comportamiento esperado; haga clic en un botón de preselección de filtro específico o escriba una frecuencia para cambiar la banda pasante, luego los atajos de ensanchar/estrechar funcionarán desde el nuevo ancho.
- **El icono de silencio no cambia al hacer clic** — El icono de silencio se actualiza solo cuando la radio confirma el cambio de estado de silencio. Si el icono no cambia, es posible que la radio no haya confirmado el nuevo estado. Esto es esperado según la Política de Configuración con Autoridad de la Radio (#2489).
- **El campo de edición de frecuencia no acepta la entrada escrita** — El campo de edición de frecuencia ahora usa `FreqLineEdit` que proporciona una etiqueta de sugerencia "MHz" en lugar de texto de marcador de posición. Haga clic en la etiqueta de frecuencia para ingresar al modo de edición, escriba la frecuencia en MHz y presione Enter para aplicar.

## Notas sobre el modo NT y el modo RTTY

Los modos **NT** y **RTTY** se tratan como modos digitales en el applet RX Controls (v0.9.3+ para NT, v26.5.1 para RTTY). Esto tiene los siguientes efectos:

- NT y RTTY usan las mismas preselecciones de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El indicador de ancho de filtro calcula el ancho de banda de la misma manera que USB (usando el borde superior de la banda pasante).
- El squelch se desactiva mientras NT o RTTY está activo. Si el squelch estaba encendido cuando cambió a NT o RTTY, se apaga automáticamente y se restaura cuando sale del modo.
- Para el modo RTTY específicamente, el squelch está desactivado porque recortaría los caracteres FSK y rompería la decodificación (#2504).

## Relacionados

- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Seleccionar la antena RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
- Calibrar AGC-T contra el piso de ruido
