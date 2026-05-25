# Trabajar con un repetidor de FM con tono CTCSS y desplazamiento +/- 

Configure un slice para operación dúplex en FM con desplazamiento de repetidor y tono de acceso CTCSS para poder escuchar la salida del repetidor y activarlo correctamente en transmisión.

## Antes de comenzar

- AetherSDR está conectado a su FLEX-8600.
- El applet Controles de RX está visible en la barra lateral derecha. Si no lo está, haga clic en el botón de la bandeja RX en la barra lateral derecha.
- Usted conoce la frecuencia de salida del repetidor, la dirección del desplazamiento, la magnitud del desplazamiento y la frecuencia del tono CTCSS.

## Pasos

1. En el applet Controles de RX, haga clic en el combo Modo y seleccione **FM** (o **NFM** para FM estrecha).
2. Haga clic en la etiqueta Frecuencia para abrir el campo de edición de frecuencia. Escriba la frecuencia de **salida** (recepción) del repetidor en MHz y presione Enter.
3. En el cuadro giratorio **Desplazamiento (FM)**, establezca la magnitud del desplazamiento en MHz. Use las flechas del cuadro giratorio o escriba un valor directamente. El rango válido es 0.0–100.0 MHz en pasos de 0.1 MHz. El valor predeterminado es 0.0 MHz.
4. Establezca la dirección del desplazamiento haciendo clic en uno de los tres botones de alternancia:
   - **−** — La frecuencia TX está por debajo de la frecuencia RX.
   - **Símplex** — La frecuencia TX es igual a la frecuencia RX (predeterminado).
   - **+** — La frecuencia TX está por encima de la frecuencia RX.
5. Haga clic en el combo **Modo de tono (FM)** (predeterminado: **Off**) y seleccione **CTCSS TX**.
6. Haga clic en el combo **Valor de tono CTCSS** y seleccione la frecuencia de tono requerida por el repetidor. Los tonos disponibles siguen el estándar de 41 tonos EIA/TIA-603, desde 67.0 Hz hasta 254.1 Hz.
7. Confirme que el squelch esté configurado apropiadamente para la banda. Consulte [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md) si es necesario.

## Qué hace cada control

| Control                   | Predeterminado | Rango válido / opciones                    |
|---------------------------|----------------|--------------------------------------------|
| Combo Modo                | USB            | FM, NFM, DFM (entre otros)                 |
| Modo de tono (FM)         | Off            | Off, CTCSS TX                              |
| Valor de tono CTCSS       | —              | 67.0 Hz – 254.1 Hz (41 tonos EIA/TIA-603) |
| Desplazamiento (FM)       | 0.0 MHz        | 0.0 – 100.0 MHz, paso 0.1                 |
| − (desplazamiento abajo)  | —              | alternancia                                |
| Símplex                   | marcado        | alternancia                                |
| + (desplazamiento arriba) | —              | alternancia                                |
| REV                       | —              | alternancia                                |

## Consejos

- Si necesita escuchar en la frecuencia de entrada del repetidor para verificar si el canal está ocupado antes de transmitir, haga clic en **REV** para intercambiar temporalmente la dirección del desplazamiento.
- Los modos de la familia FM ocultan los botones preestablecidos de ancho de filtro. Esto es normal; el ancho de filtro para FM es fijado por el modo mismo.
- Los botones de pestaña de slice y la etiqueta de slice se codifican por colores por slice usando SliceColorManager (v0.9.3+). Los colores persisten entre sesiones y se reflejan en las pestañas de slice, la etiqueta de slice, los widgets VFO y las barras de medidor.
- Cuando la radio reporta un número diferente de slices disponibles del que la fila de pestañas fue construida, AetherSDR ahora elimina los botones de pestaña de slice existentes y los reconstruye para el nuevo recuento antes de reconectar los manejadores de clic (v0.9.5.1, #2254). Esto evita botones obsoletos después de una reconexión o un cambio en la configuración del hardware.
- Los preestablecimientos de ancho de filtro se almacenan en el formato `lo:hi` (bordes de la banda pasante en Hz) o como un valor de ancho simple, dependiendo de si el preestablecimiento se guardó con posiciones de borde explícitas. Ambos formatos se leen correctamente cuando vuelve a abrir el applet o cambia de modo (#2259).
- La lectura del ancho de filtro se comparte con el panel VFO a través de `RxApplet::formatFilterWidth()`. En v0.9.8+, este método es ahora una función estática pública para que ambos widgets produzcan un formato idéntico y consciente del modo para modos SSB, digital y AM (#2197).
- Los atajos de ampliar/reducir (ej. Ctrl+Mayús+W, Ctrl+Mayús+N) llaman a `stepFilterWidth(int direction)`, que recorre la lista de preestablecimientos de filtro por modo para encontrar el siguiente ancho válido y lo aplica con la geometría de borde correcta para el modo actual (#2208).
- La etiqueta de slice ahora admite formato de texto enriquecido (HTML) para la visualización de la letra del slice (#2606).
- La selección de antena tanto para RX como para TX ahora prioriza la lista de antenas del propio slice cuando está disponible. El menú muestra etiquetas de antena con información sobre herramientas y consejos de estado, con los datos reales de la antena almacenados por separado del texto mostrado. Los menús de antena TX filtran los puertos con el prefijo "RX" e incluyen solo antenas que coinciden con patrones como "ANT", "TX" o "XVTR".
- Por defecto, AetherSDR usa un algoritmo de squelch Automático que sobrescribe el squelchLevel del slice con valores sugeridos por el algoritmo. El último umbral de squelch Manual elegido por el usuario ahora se persiste en el lado del cliente en la configuración `LastManualSquelchLevel` y se restaura entre sesiones y ciclos de modo.
- El botón de silencio utiliza un mecanismo de un solo clic diferido para evitar conflictos con acciones de doble clic. Un solo clic silencia o reactiva el sonido del slice actual. Un doble clic silencia o reactiva el sonido de todos los slices propios. El ícono se actualiza solo cuando la radio reconoce el cambio de estado de silencio, asegurando que el estado mostrado siempre coincida con el estado real de la radio.
- Al ingresar una frecuencia en el campo de edición de frecuencia, AetherSDR usa `FrequencyEntryParser` para normalizar la entrada. Si escribe un valor superior a 54 MHz sin estar en una antena XVTR, el analizador verifica si se ingresó como un valor explícito en MHz. Si es así, la frecuencia máxima permitida se eleva a 50000 MHz, permitiendo la entrada de frecuencias VHF/UHF por encima del límite normal de 54 MHz sin cambiar a una antena XVTR primero (ej., escribir 146.520 MHz en una antena no-XVTR).
- Los botones de dirección de desplazamiento y el botón REV son parte de un grupo de botones exclusivo; seleccionar uno deselecciona automáticamente los otros.

## Solución de problemas

- **El repetidor no responde a sus transmisiones** — Confirme que el valor del tono CTCSS coincide con lo que espera el repetidor y que el Modo de tono está configurado en **CTCSS TX** en lugar de **Off**.
- **La frecuencia TX parece incorrecta** — Verifique que el botón de dirección de desplazamiento (**−**, **Símplex** o **+**) coincida con la dirección de desplazamiento publicada por el repetidor y que el valor de Desplazamiento (FM) esté establecido en la magnitud correcta (ej., 0.6 MHz para un repetidor típico de 2 m).
- **Los controles de Modo de tono y CTCSS no están visibles** — El modo del slice debe ser **FM**, **NFM** o **DFM**. Estos controles están ocultos en todos los demás modos.
- **Los controles de squelch están atenuados** — El squelch se desactiva automáticamente cuando el modo del slice es **DIGU**, **DIGL**, **NT**, **RTTY**, **CW** o **CWL**. Cambie a un modo FM o SSB para habilitar los controles de squelch.
- **Los botones de pestaña de slice aparecen incorrectos después de reconectar** — Si la fila de pestañas de slice muestra un número incorrecto de botones o un diseño obsoleto después de que la radio se reconecta, desconéctese y reconéctese manualmente. En v0.9.5.1 esto se corrige automáticamente: el applet llama a `clearSliceButtons()` para eliminar los botones antiguos y restaurar la etiqueta de slice estática antes de reconstruir la fila de pestañas para el nuevo recuento de slices (#2254).
- **El botón preestablecido de filtro no cambia la banda pasante** — Si el ancho actual no es un valor preestablecido estándar, el paso de ampliar/reducir puede no cambiar la banda pasante. Este es un comportamiento esperado; haga clic en un botón preestablecido de filtro específico o escriba una frecuencia para cambiar la banda pasante, luego los atajos de ampliar/reducir funcionarán desde el nuevo ancho.
- **El ícono de silencio no cambia al hacer clic** — El ícono de silencio se actualiza solo cuando la radio reconoce el cambio de estado de silencio. Si el ícono no cambia, es posible que la radio no haya confirmado el nuevo estado. Esto es esperado según la Política de Configuración Autoritativa de la Radio (#2489).

## Notas sobre el modo NT y el modo RTTY

Los modos **NT** y **RTTY** se tratan como modos digitales en el applet Controles de RX (v0.9.3+ para NT, v26.5.1 para RTTY). Esto tiene los siguientes efectos:

- NT y RTTY usan los mismos preestablecimientos de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El indicador de ancho de filtro calcula el ancho de banda de la misma manera que USB (usando el borde superior de la banda pasante).
- El squelch se desactiva mientras NT o RTTY está activo. Si el squelch estaba encendido cuando cambió a NT o RTTY, se apaga automáticamente y se restaura cuando sale del modo.
- Para el modo RTTY específicamente, el squelch se desactiva porque eliminaría los caracteres FSK e interrumpiría la decodificación (#2504).

## Relacionado

- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Seleccionar la antena RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
