# Trabajar con un repetidor FM usando tono CTCSS y desplazamiento +/- 

Configure un slice para operación dúplex en FM con un desplazamiento de repetidor y un tono de acceso CTCSS para poder escuchar la salida del repetidor y activarlo correctamente en transmisión.

## Antes de comenzar

- AetherSDR está conectado a su FLEX-8600.
- El applet RX Controls está visible en la barra lateral derecha. Si no lo está, haga clic en el botón de la bandeja RX en la barra lateral derecha.
- Conoce la frecuencia de salida del repetidor, la dirección del desplazamiento, la magnitud del desplazamiento y la frecuencia del tono CTCSS.

## Pasos

1. En el applet RX Controls, haga clic en el combo Mode y seleccione **FM** (o **NFM** para FM estrecha).
2. Haga clic en la etiqueta Frequency para abrir el campo de edición de frecuencia. Escriba la frecuencia de **salida** (recepción) del repetidor en MHz y presione Enter.
3. En el campo giratorio **Offset (FM)**, ajuste la magnitud del desplazamiento en MHz. Use las flechas del campo giratorio o escriba un valor directamente. El rango válido es de 0,0 a 100,0 MHz en pasos de 0,1 MHz. El valor predeterminado es 0,0 MHz.
4. Establezca la dirección del desplazamiento haciendo clic en uno de los tres botones de alternancia:
   - **—** — La frecuencia de TX está por debajo de la frecuencia de RX.
   - **Simplex** — La frecuencia de TX es igual a la frecuencia de RX (predeterminado).
   - **+** — La frecuencia de TX está por encima de la frecuencia de RX.
5. Haga clic en el combo **Tone mode (FM)** (predeterminado: **Off**) y seleccione **CTCSS TX**.
6. Haga clic en el combo **CTCSS tone value** y seleccione la frecuencia de tono requerida por el repetidor. Los tonos disponibles siguen el estándar EIA/TIA-603 de 41 tonos, desde 67,0 Hz hasta 254,1 Hz.
7. Confirme que el squelch esté configurado adecuadamente para la banda. Consulte [Turn on the squelch and set its threshold](turn-on-the-squelch-and-set-its-threshold.md) si es necesario.

## Qué hace cada control

| Control               | Predeterminado | Rango/opciones válidos                     |
|-----------------------|----------------|--------------------------------------------|
| Combo Mode            | USB            | FM, NFM, DFM (entre otros)                 |
| Tone mode (FM)        | Off            | Off, CTCSS TX                              |
| CTCSS tone value      | —              | 67,0 Hz – 254,1 Hz (41 tonos EIA/TIA-603) |
| Offset (FM)           | 0,0 MHz        | 0,0 – 100,0 MHz, paso 0,1                 |
| − (desplazamiento abajo) | —           | alternancia                                |
| Simplex               | marcado        | alternancia                                |
| + (desplazamiento arriba) | —          | alternancia                                |
| REV                   | —              | alternancia                                |

## Consejos

- Si necesita escuchar en la frecuencia de entrada del repetidor para comprobar si el canal está ocupado antes de transmitir, haga clic en **REV** para intercambiar temporalmente la dirección del desplazamiento.
- Los modos de la familia FM ocultan los botones preestablecidos de ancho de filtro. Esto es normal; el ancho de filtro para FM está fijado por el modo mismo.
- Los botones de la pestaña del slice y la insignia del slice están codificados por color por slice usando SliceColorManager (v0.9.3+). Los colores persisten entre sesiones y se reflejan en las pestañas del slice, la insignia del slice, los widgets VFO y las tiras de medidores.
- Cuando la radio informa un número diferente de slices disponibles del que se construyó la fila de pestañas, AetherSDR ahora elimina los botones de pestaña de slice existentes y los reconstruye para la nueva cantidad antes de reconectar los manejadores de clic (v0.9.5.1, #2254). Esto evita que aparezcan botones obsoletos después de una reconexión o un cambio en la configuración del hardware.
- Los preestablecidos de ancho de filtro se almacenan en el formato `lo:hi` (bordes de la banda pasante en Hz) o como un valor de ancho simple, dependiendo de si el preestablecido se guardó con posiciones de borde explícitas. Ambos formatos se leen correctamente cuando vuelve a abrir el applet o cambia de modo (#2259).
- El indicador de ancho de filtro se comparte con el panel VFO a través de `RxApplet::formatFilterWidth()`. En v0.9.8+, este método ahora es una función estática pública para que ambos widgets produzcan un formato idéntico y consciente del modo para modos SSB, digital y AM (#2197).
- Los atajos de ensanchar/estrechar (por ejemplo, Ctrl+Shift+W, Ctrl+Shift+N) llaman a `stepFilterWidth(int direction)`, que recorre la lista de preestablecidos de filtro por modo para encontrar el siguiente ancho válido y lo aplica con la geometría de borde correcta para el modo actual (#2208).
- La insignia del slice ahora admite formato de texto enriquecido (HTML) para la visualización de la letra del slice (#2606).
- La selección de antena tanto para RX como para TX ahora prioriza la lista de antenas del propio slice cuando está disponible. El menú muestra etiquetas de antena con información sobre herramientas y sugerencias de estado, con los datos reales de la antena almacenados por separado del texto mostrado. Los menús de antena TX filtran los puertos con el prefijo "RX" e incluyen solo antenas que coinciden con patrones como "ANT", "TX" o "XVTR".
- De forma predeterminada, AetherSDR utiliza un algoritmo de squelch Auto que sobrescribe el squelchLevel del slice con valores sugeridos por el algoritmo. El último umbral de squelch Manual elegido por el usuario ahora se conserva en el lado del cliente en la configuración `LastManualSquelchLevel` y se restaura entre sesiones y ciclos de modo.
- El botón de silencio utiliza un mecanismo de un solo clic diferido para evitar conflictos con acciones de doble clic. Un solo clic silencia o reactiva el slice actual. Un doble clic silencia o reactiva todos los slices propios. El ícono se actualiza solo cuando la radio confirma el cambio de estado de silencio, lo que garantiza que el estado mostrado siempre coincida con el estado real de la radio.
- Al ingresar una frecuencia en el campo de edición de frecuencia, AetherSDR usa `FrequencyEntryParser` para normalizar la entrada. Si escribe un valor superior a 54 MHz sin estar en una antena XVTR, el analizador verifica si se ingresó como un valor explícito en MHz. Si es así, la frecuencia máxima permitida se eleva a 50000 MHz, lo que permite ingresar frecuencias de VHF/UHF por encima del límite normal de 54 MHz sin cambiar primero a una antena XVTR (por ejemplo, escribiendo 146,520 MHz en una antena no XVTR).
- Los botones de dirección de desplazamiento y el botón REV son parte de un grupo de botones exclusivo; seleccionar uno deselecciona automáticamente los demás.
- El control deslizante de paneo L/R ahora pinta su relleno desde el centro hacia afuera. Esto proporciona una indicación visual de la posición neutral (centro) de un vistazo. La marca central es un pequeño punto pintado en la ranura.
- Los botones preestablecidos de filtro y otros botones con estilo ahora usan colores de hoja de estilo tokenizados a través de ThemeManager. Esto significa que la apariencia del botón se actualiza automáticamente cuando cambia de tema, de manera consistente con el resto de la interfaz de usuario (v26.6.1).

## Solución de problemas

- **El repetidor no responde a sus transmisiones** — Confirme que el valor del tono CTCSS coincida con lo que espera el repetidor y que Tone mode esté configurado en **CTCSS TX** en lugar de **Off**.
- **La frecuencia de TX parece incorrecta** — Verifique que el botón de dirección de desplazamiento (**−**, **Simplex** o **+**) coincida con la dirección de desplazamiento publicada del repetidor y que el valor Offset (FM) esté configurado con la magnitud correcta (por ejemplo, 0,6 MHz para un repetidor típico de 2 m).
- **Los controles Tone mode y CTCSS no son visibles** — El modo del slice debe ser **FM**, **NFM** o **DFM**. Estos controles están ocultos en todos los demás modos.
- **Los controles de squelch están atenuados** — El squelch se deshabilita automáticamente cuando el modo del slice es **DIGU**, **DIGL**, **NT**, **RTTY**, **CW** o **CWL**. Cambie a un modo FM o SSB para habilitar los controles de squelch.
- **Los botones de la pestaña del slice aparecen incorrectos después de reconectar** — Si la fila de pestañas del slice muestra el número incorrecto de botones o un diseño desactualizado después de que la radio se reconecta, desconéctese y reconéctese manualmente. En v0.9.5.1 esto se corrige automáticamente: el applet llama a `clearSliceButtons()` para eliminar los botones antiguos y restaurar la insignia estática del slice antes de reconstruir la fila de pestañas para la nueva cantidad de slices (#2254).
- **El botón preestablecido de filtro no cambia la banda pasante** — Si el ancho actual no es un valor preestablecido estándar, el paso de ensanchar/estrechar puede no cambiar la banda pasante. Esto es un comportamiento esperado; haga clic en un botón preestablecido de filtro específico o escriba una frecuencia para cambiar la banda pasante, luego los atajos de ensanchar/estrechar funcionarán desde el nuevo ancho.
- **El ícono de silencio no cambia al hacer clic** — El ícono de silencio se actualiza solo cuando la radio confirma el cambio de estado de silencio. Si el ícono no cambia, es posible que la radio no haya confirmado el nuevo estado. Esto es esperado según la Política de Configuraciones Autoritativas de la Radio (#2489).

## Notas sobre el modo NT y el modo RTTY

Los modos **NT** y **RTTY** se tratan como modos digitales en el applet RX Controls (v0.9.3+ para NT, v26.5.1 para RTTY). Esto tiene los siguientes efectos:

- NT y RTTY usan los mismos preestablecidos de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El indicador de ancho de filtro calcula el ancho de banda de la misma manera que USB (usando el borde superior de la banda pasante).
- El squelch está deshabilitado mientras NT o RTTY está activo. Si el squelch estaba encendido cuando cambió a NT o RTTY, se apaga automáticamente y se restaura cuando sale del modo.
- Para el modo RTTY específicamente, el squelch está deshabilitado porque silenciaría los caracteres FSK y rompería la decodificación (#2504).

## Relacionados

- [Change mode (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Tune the radio to a frequency (type MHz in the readout)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Turn on the squelch and set its threshold](turn-on-the-squelch-and-set-its-threshold.md)
- [Select the RX or TX antenna for this slice](select-the-rx-or-tx-antenna-for-this-slice.md)
