# Trabajar con un repetidor de FM usando tono CTCSS y desplazamiento +/- 

Configure un slice para operación en dúplex FM con desplazamiento de repetidor y un tono de acceso CTCSS para poder escuchar la salida del repetidor y activarlo correctamente en transmisión.

## Antes de comenzar

- AetherSDR está conectado a su FLEX-8600.
- El applet RX Controls está visible en la barra lateral derecha. Si no lo está, haga clic en el botón de la bandeja RX en la barra lateral derecha.
- Usted conoce la frecuencia de salida del repetidor, la dirección del desplazamiento, la magnitud del desplazamiento y la frecuencia del tono CTCSS.

## Pasos

1. En el applet RX Controls, haga clic en el combo Mode y seleccione **FM** (o **NFM** para FM estrecha).
2. Haga clic en la etiqueta Frequency para abrir el campo de edición de frecuencia. Escriba la frecuencia de **salida** (recepción) del repetidor en MHz y presione Enter.
3. En el control de giro **Offset (FM)**, ajuste la magnitud del desplazamiento en MHz. Use las flechas del control de giro o escriba un valor directamente. El rango válido es 0.0–100.0 MHz en pasos de 0.1 MHz. El valor predeterminado es 0.0 MHz.
4. Establezca la dirección del desplazamiento haciendo clic en uno de los tres botones de alternancia:
   - **−** — La frecuencia TX está por debajo de la frecuencia RX.
   - **Simplex** — La frecuencia TX es igual a la frecuencia RX (predeterminado).
   - **+** — La frecuencia TX está por encima de la frecuencia RX.
5. Haga clic en el combo **Tone mode (FM)** (predeterminado: **Off**) y seleccione **CTCSS TX**.
6. Haga clic en el combo **CTCSS tone value** y seleccione la frecuencia de tono requerida por el repetidor. Los tonos disponibles siguen el estándar de 41 tonos EIA/TIA-603, desde 67.0 Hz hasta 254.1 Hz.
7. Confirme que el squelch esté ajustado adecuadamente para la banda. Consulte [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md) si es necesario.

## Qué hace cada control

| Control               | Predeterminado | Rango/opciones válidos                     |
|-----------------------|----------------|--------------------------------------------|
| Combo Mode            | USB            | FM, NFM, DFM (entre otros)                 |
| Tone mode (FM)        | Off            | Off, CTCSS TX                              |
| Valor de tono CTCSS   | —              | 67.0 Hz – 254.1 Hz (41 tonos EIA/TIA-603)  |
| Offset (FM)           | 0.0 MHz        | 0.0 – 100.0 MHz, paso 0.1                  |
| − (desplazamiento hacia abajo) | —    | alternancia                                |
| Simplex               | marcado        | alternancia                                |
| + (desplazamiento hacia arriba)  | —    | alternancia                                |
| REV                   | —              | alternancia                                |

## Consejos

- Si necesita escuchar en la frecuencia de entrada del repetidor para verificar si el canal está ocupado antes de transmitir, haga clic en **REV** para intercambiar temporalmente la dirección del desplazamiento.
- Los modos de la familia FM ocultan los botones predefinidos de ancho de filtro. Esto es esperado; el ancho de filtro para FM es fijado por el modo mismo.
- Los botones de la pestaña del slice y la placa del slice tienen códigos de color por slice usando SliceColorManager (v0.9.3+). Los colores persisten entre sesiones y se reflejan en las pestañas del slice, la placa del slice, los widgets VFO y las barras de medidores.
- Cuando la radio informa un número diferente de slices disponibles del que fue construida la fila de pestañas, AetherSDR ahora elimina los botones existentes de las pestañas del slice y los reconstruye para el nuevo recuento antes de reconectar los controladores de clic (v0.9.5.1, #2254). Esto evita que aparezcan botones obsoletos después de una reconexión o un cambio en la configuración del hardware.
- Los predefinidos de ancho de filtro se almacenan en el formato `lo:hi` (bordes de la banda de paso en Hz) o como un valor de ancho simple, dependiendo de si el predefinido fue guardado con posiciones de borde explícitas. Ambos formatos se leen correctamente cuando se vuelve a abrir el applet o se cambia de modo (#2259).
- El indicador de ancho de filtro se comparte con el panel VFO a través de `RxApplet::formatFilterWidth()`. En v0.9.8+, este método ahora es una función estática pública para que ambos widgets produzcan un formato idéntico y consciente del modo para modos SSB, digital y AM (#2197).
- Los atajos de ensanchar/estrechar (p. ej., Ctrl+Shift+W, Ctrl+Shift+N) llaman a `stepFilterWidth(int direction)`, que recorre la lista de predefinidos de filtro por modo para encontrar el siguiente ancho válido y lo aplica con la geometría de borde correcta para el modo actual (#2208).

## Solución de problemas

- **El repetidor no responde a sus transmisiones** — Confirme que el valor del tono CTCSS coincida con lo que espera el repetidor y que Tone mode esté configurado en **CTCSS TX** en lugar de **Off**.
- **La frecuencia TX parece incorrecta** — Verifique que el botón de dirección de desplazamiento (**−**, **Simplex** o **+**) coincida con la dirección de desplazamiento publicada del repetidor y que el valor de Offset (FM) esté configurado con la magnitud correcta (p. ej., 0.6 MHz para un repetidor típico de 2 m).
- **Los controles de Tone mode y CTCSS no son visibles** — El modo del slice debe ser **FM**, **NFM** o **DFM**. Estos controles están ocultos en todos los demás modos.
- **Los controles de squelch están atenuados** — El squelch se desactiva automáticamente cuando el modo del slice es **DIGU**, **DIGL**, **NT**, **CW** o **CWL**. Cambie a un modo FM o SSB para habilitar los controles de squelch.
- **Los botones de la pestaña del slice aparecen incorrectos después de reconectar** — Si la fila de pestañas del slice muestra el número incorrecto de botones o un diseño obsoleto después de que la radio se reconecte, desconéctese y reconéctese manualmente. En v0.9.5.1 esto se corrige automáticamente: el applet llama a `clearSliceButtons()` para eliminar los botones antiguos y restaurar la placa estática del slice antes de reconstruir la fila de pestañas para el nuevo recuento de slices (#2254).
- **El botón predefinido de filtro no cambia la banda de paso** — Si el ancho actual no es un valor predefinido estándar, el paso de ensanchar/estrechar puede no cambiar la banda de paso. Este comportamiento es esperado; haga clic en un botón predefinido de filtro específico o escriba una frecuencia para cambiar la banda de paso, luego los atajos de ensanchar/estrechar funcionarán desde el nuevo ancho.

## Notas sobre el modo NT

El modo **NT** se trata como un modo digital en el applet RX Controls (v0.9.3+). Esto tiene los siguientes efectos:

- NT utiliza los mismos predefinidos de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El indicador de ancho de filtro calcula el ancho de banda de la misma manera que USB (usando el borde superior de la banda de paso).
- El squelch se desactiva mientras NT está activo. Si el squelch estaba activado cuando cambió a NT, se apaga automáticamente y se restaura cuando sale del modo.

## Relacionados

- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Seleccionar la antena RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
