# Trabajar con un repetidor de FM usando tono CTCSS y desplazamiento +/- 

Configure una rebanada para operación dúplex en FM con desplazamiento de repetidor y un tono de acceso CTCSS para poder escuchar la salida del repetidor y abrirlo correctamente al transmitir.

## Antes de comenzar

- AetherSDR está conectado a su FLEX-8600.
- El applet Controles de RX está visible en la barra lateral derecha. Si no lo está, haga clic en el botón de la bandeja de RX en la barra lateral derecha.
- Conoce la frecuencia de salida del repetidor, la dirección del desplazamiento, la magnitud del desplazamiento y la frecuencia del tono CTCSS.

## Pasos

1. En el applet Controles de RX, haga clic en el combo Modo y seleccione **FM** (o **NFM** para FM angosta).
2. Haga clic en la etiqueta Frecuencia para abrir el campo de edición de frecuencia. Escriba la frecuencia de **salida** (recepción) del repetidor en MHz y presione Enter.
3. En el control giratorio **Desplazamiento (FM)**, ajuste la magnitud del desplazamiento en MHz. Use las flechas del control giratorio o escriba un valor directamente. El rango válido es 0,0–100,0 MHz en pasos de 0,1 MHz. El valor predeterminado es 0,0 MHz.
4. Establezca la dirección del desplazamiento haciendo clic en uno de los tres botones de alternancia:
   - **−** — La frecuencia de TX está por debajo de la frecuencia de RX.
   - **Símplex** — La frecuencia de TX es igual a la frecuencia de RX (predeterminado).
   - **+** — La frecuencia de TX está por encima de la frecuencia de RX.
5. Haga clic en el combo **Modo de tono (FM)** (predeterminado: **Apagado**) y seleccione **CTCSS TX**.
6. Haga clic en el combo **Valor del tono CTCSS** y seleccione la frecuencia de tono requerida por el repetidor. Los tonos disponibles siguen el estándar EIA/TIA-603 de 41 tonos, desde 67,0 Hz hasta 254,1 Hz.
7. Confirme que el squelch esté configurado adecuadamente para la banda. Consulte [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md) si es necesario.

## Qué hace cada control

| Control                     | Predeterminado | Rango válido / opciones                   |
|-----------------------------|----------------|-------------------------------------------|
| Combo Modo                  | USB            | FM, NFM, DFM (entre otros)                |
| Botón WFM                   | apagado        | alternancia                               |
| Modo de tono (FM)           | Apagado        | Apagado, CTCSS TX                         |
| Valor del tono CTCSS        | —              | 67,0 Hz – 254,1 Hz (41 tonos EIA/TIA-603) |
| Desplazamiento (FM)         | 0,0 MHz        | 0,0 – 100,0 MHz, paso 0,1                |
| − (desplazamiento hacia abajo) | —           | alternancia                               |
| Símplex                     | marcado        | alternancia                               |
| + (desplazamiento hacia arriba) | —          | alternancia                               |
| REV                         | —              | alternancia                               |

## Consejos

- Si necesita escuchar en la frecuencia de entrada del repetidor para verificar si el canal está ocupado antes de transmitir, haga clic en **REV** para intercambiar temporalmente la dirección del desplazamiento.
- Los modos de la familia FM ocultan los botones preestablecidos de ancho de filtro. Esto es esperado; el ancho de filtro para FM está fijado por el modo mismo.
- El botón **WFM** (demodulador FM por software) es independiente del combo de modo FM. Haga clic en él para habilitar una ruta de demodulación FM de banda ancha basada en software que envía audio IQ de DAX a través del Cable Hi-Fi. WFM se apaga automáticamente cuando selecciona cualquier modo de radio real desde el combo Modo.
- Los botones de pestaña de rebanada y la insignia de rebanada tienen código de colores por rebanada usando SliceColorManager (v0.9.3+). Los colores persisten entre sesiones y se reflejan en las pestañas de rebanada, la insignia de rebanada, los widgets VFO y las barras de medidores.
- Cuando la radio informa un número diferente de rebanadas disponibles del que se creó para la fila de pestañas, AetherSDR ahora destruye los botones de pestaña de rebanada existentes y los reconstruye para el nuevo conteo antes de reconectar los manejadores de clic (v0.9.5.1, #2254). Esto evita que aparezcan botones obsoletos después de una reconexión o un cambio en la configuración del hardware.
- Los preajustes de ancho de filtro se almacenan en el formato `lo:hi` (bordes de la banda de paso en Hz) o como un valor de ancho simple, dependiendo de si el preajuste se guardó con posiciones de borde explícitas. Ambos formatos se leen correctamente cuando vuelve a abrir el applet o cambia de modo (#2259).
- El indicador de ancho de filtro se comparte con el panel VFO mediante `RxApplet::formatFilterWidth()`. En v0.9.8+, este método ahora es una función estática pública para que ambos widgets produzcan formato idéntico y consciente del modo para modos SSB, digital y AM (#2197).
- Los accesos directos de ampliar/reducir (ej. Ctrl+Mayús+W, Ctrl+Mayús+N) llaman a `stepFilterWidth(int direction)`, que recorre la lista de preajustes de filtro por modo para encontrar el siguiente ancho válido y lo aplica con la geometría de borde correcta para el modo actual (#2208).
- La insignia de rebanada ahora admite formato de texto enriquecido (HTML) para la visualización de la letra de la rebanada (#2606).
- La selección de antena tanto para RX como para TX ahora prioriza la lista de antenas propia de la rebanada cuando está disponible. El menú muestra etiquetas de antena con información sobre herramientas y sugerencias de estado, con los datos reales de la antena almacenados por separado del texto mostrado. Los menús de antena TX filtran los puertos con el prefijo "RX" e incluyen solo antenas que coinciden con patrones como "ANT", "TX" o "XVTR".
- De forma predeterminada, AetherSDR utiliza un algoritmo de squelch automático que sobrescribe el squelchLevel de la rebanada con valores sugeridos por el algoritmo. El último umbral de squelch manual elegido por el usuario ahora se conserva en el lado del cliente en la configuración `LastManualSquelchLevel` y se restaura entre sesiones y ciclos de modo.
- El botón de silencio utiliza un mecanismo de un solo clic diferido para evitar conflictos con acciones de doble clic. Un solo clic silencia o reactiva el audio de la rebanada actual. Un doble clic silencia o reactiva el audio de todas las rebanadas propias. El ícono se actualiza solo cuando la radio confirma el cambio de estado de silencio, asegurando que el estado mostrado siempre coincida con el estado real de la radio.
- El control deslizante **Umbral AGC** tiene un menú contextual con clic derecho. Haga clic derecho en el control deslizante y seleccione **Calibrar AGC-T contra el piso de ruido…** para abrir el panel de calibración de ruido AGC-T. La información sobre herramientas también anuncia esta función.
- Al ingresar una frecuencia en el campo de edición de frecuencia, AetherSDR usa `FrequencyEntryParser` para normalizar la entrada. Si escribe un valor superior a 54 MHz sin estar en una antena XVTR, el analizador verifica si se ingresó como un valor explícito en MHz. Si es así, la frecuencia máxima permitida se eleva a 50000 MHz, lo que permite ingresar frecuencias VHF/UHF por encima del límite normal de 54 MHz sin cambiar primero a una antena XVTR (ej., escribir 146.520 MHz en una antena no XVTR).
- Los botones de dirección de desplazamiento y el botón REV son parte de un grupo de botones exclusivo; seleccionar uno deselecciona automáticamente los otros.
- El control deslizante de paneo L/R ahora pinta su relleno desde el centro hacia afuera. Esto proporciona una indicación visual de la posición neutral (centro) de un vistazo. La marca central es un pequeño punto pintado en la ranura.
- Los botones de preajuste de filtro y otros botones con estilo ahora usan colores de hoja de estilo tokenizados a través de ThemeManager. Esto significa que la apariencia del botón se actualiza automáticamente cuando cambia de tema, de manera consistente con el resto de la interfaz de usuario (v26.6.1).

## Resolución de problemas

- **El repetidor no responde a sus transmisiones** — Confirme que el valor del tono CTCSS coincida con el que espera el repetidor y que el Modo de tono esté configurado en **CTCSS TX** en lugar de **Apagado**.
- **La frecuencia de TX parece incorrecta** — Verifique que el botón de dirección de desplazamiento (**−**, **Símplex** o **+**) coincida con la dirección de desplazamiento publicada del repetidor y que el valor de Desplazamiento (FM) esté ajustado a la magnitud correcta (ej., 0,6 MHz para un repetidor típico de 2 m).
- **Los controles de Modo de tono y CTCSS no son visibles** — El modo de la rebanada debe ser **FM**, **NFM** o **DFM**. Estos controles están ocultos en todos los demás modos.
- **Los controles de squelch están atenuados** — El squelch se deshabilita automáticamente cuando el modo de la rebanada es **DIGU**, **DIGL**, **NT**, **RTTY**, **CW** o **CWL**. Cambie a un modo FM o SSB para habilitar los controles de squelch.
- **Los botones de pestaña de rebanada parecen incorrectos después de reconectar** — Si la fila de pestañas de rebanada muestra el número incorrecto de botones o un diseño obsoleto después de que la radio se reconecta, desconéctese y reconéctese manualmente. En v0.9.5.1 esto se corrige automáticamente: el applet llama a `clearSliceButtons()` para eliminar los botones antiguos y restaurar la insignia de rebanada estática antes de reconstruir la fila de pestañas para el nuevo conteo de rebanadas (#2254).
- **El botón de preajuste de filtro no cambia la banda de paso** — Si el ancho actual no es un valor preestablecido estándar, el paso de ampliar/reducir puede no cambiar la banda de paso. Este es un comportamiento esperado; haga clic en un botón de preajuste de filtro específico o escriba una frecuencia para cambiar la banda de paso, luego los accesos directos de ampliar/reducir funcionarán desde el nuevo ancho.
- **El ícono de silencio no cambia al hacer clic** — El ícono de silencio se actualiza solo cuando la radio confirma el cambio de estado de silencio. Si el ícono no cambia, es posible que la radio no haya confirmado el nuevo estado. Esto es esperado según la Política de Configuración Autoritativa de la Radio (#2489).
- **El campo de edición de frecuencia no acepta la entrada escrita** — El campo de edición de frecuencia ahora usa `FreqLineEdit` que proporciona una etiqueta de sugerencia "MHz" en lugar de texto de marcador de posición. Haga clic en la etiqueta de frecuencia para entrar en modo de edición, escriba la frecuencia en MHz y presione Enter para aplicarla.

## Notas sobre el modo NT y el modo RTTY

Los modos **NT** y **RTTY** se tratan como modos digitales en el applet Controles de RX (v0.9.3+ para NT, v26.5.1 para RTTY). Esto tiene los siguientes efectos:

- NT y RTTY usan los mismos preajustes de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El indicador de ancho de filtro calcula el ancho de banda de la misma manera que USB (usando el borde superior de la banda de paso).
- El squelch está deshabilitado mientras NT o RTTY están activos. Si el squelch estaba encendido cuando cambió a NT o RTTY, se apaga automáticamente y se restaura cuando sale del modo.
- Para el modo RTTY específicamente, el squelch está deshabilitado porque anularía los caracteres FSK y rompería la decodificación (#2504).

## Relacionados

- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Seleccionar la antena de RX o TX para esta rebanada](select-the-rx-or-tx-antenna-for-this-slice.md)
- Calibrar AGC-T contra el piso de ruido
