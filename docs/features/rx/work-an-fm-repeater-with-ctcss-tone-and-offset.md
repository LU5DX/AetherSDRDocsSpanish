# Trabajar con un repetidor de FM usando tono CTCSS y desplazamiento +/- 

Configure un slice para operación dúplex en FM con un desplazamiento de repetidor y un tono de acceso CTCSS para poder escuchar la salida del repetidor y activarlo correctamente en transmisión.

## Antes de comenzar

- AetherSDR está conectado a su FLEX-8600.
- El applet RX Controls está visible en la barra lateral derecha. Si no lo está, haga clic en el botón de la bandeja RX en la barra lateral derecha.
- Conoce la frecuencia de salida del repetidor, la dirección del desplazamiento, la magnitud del desplazamiento y la frecuencia del tono CTCSS.

## Pasos

1. En el applet RX Controls, haga clic en el combo Mode y seleccione **FM** (o **NFM** para FM estrecha).
2. Haga clic en la etiqueta Frequency para abrir el campo de edición de frecuencia. Escriba la frecuencia **de salida** (recepción) del repetidor en MHz y presione Enter.
3. En el control giratorio **Offset (FM)**, ajuste la magnitud del desplazamiento en MHz. Use las flechas del control giratorio o escriba un valor directamente. El rango válido es de 0,0 a 100,0 MHz en pasos de 0,1 MHz. El valor predeterminado es 0,0 MHz.
4. Ajuste la dirección del desplazamiento haciendo clic en uno de los tres botones de alternancia:
   - **−** — La frecuencia de TX está por debajo de la frecuencia de RX.
   - **Simplex** — La frecuencia de TX es igual a la frecuencia de RX (predeterminado).
   - **+** — La frecuencia de TX está por encima de la frecuencia de RX.
5. Haga clic en el combo **Tone mode (FM)** (predeterminado: **Off**) y seleccione **CTCSS TX**.
6. Haga clic en el combo **CTCSS tone value** y seleccione la frecuencia de tono requerida por el repetidor. Los tonos disponibles siguen el estándar de 41 tonos EIA/TIA-603, desde 67,0 Hz hasta 254,1 Hz.
7. Confirme que el squelch esté ajustado apropiadamente para la banda. Consulte [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md) si es necesario.

## Qué hace cada control

| Control                  | Predeterminado | Rango válido / opciones                      |
|--------------------------|----------------|----------------------------------------------|
| Mode combo               | USB            | FM, NFM, DFM (entre otros)                   |
| Tone mode (FM)           | Off            | Off, CTCSS TX                                |
| CTCSS tone value         | —              | 67,0 Hz – 254,1 Hz (41 tonos EIA/TIA-603)    |
| Offset (FM)              | 0,0 MHz        | 0,0 – 100,0 MHz, paso 0,1                    |
| − (desplazamiento abajo) | —              | alternancia                                  |
| Simplex                  | marcado        | alternancia                                  |
| + (desplazamiento arriba)| —              | alternancia                                  |
| REV                      | —              | alternancia                                  |

## Consejos

- Si necesita escuchar en la frecuencia de entrada del repetidor para verificar si el canal está ocupado antes de transmitir, haga clic en **REV** para intercambiar temporalmente la dirección del desplazamiento.
- Los modos de la familia FM ocultan los botones predefinidos de ancho de filtro. Esto es normal; el ancho de filtro para FM es fijo según el modo mismo.
- Los botones de la pestaña de slice y la insignia del slice están codificados por color por slice usando SliceColorManager (v0.9.3+). Los colores se mantienen entre sesiones y se reflejan en las pestañas de slice, la insignia del slice, los widgets VFO y las barras de medidores.
- Cuando la radio informa un número diferente de slices disponibles del que se creó para la fila de pestañas, AetherSDR ahora elimina los botones de pestaña de slice existentes y los reconstruye para el nuevo conteo antes de reconectar los controladores de clic (v0.9.5.1, #2254). Esto evita que aparezcan botones obsoletos después de una reconexión o un cambio en la configuración del hardware.
- Los predefinidos de ancho de filtro se almacenan en el formato `lo:hi` (bordes de la banda pasante en Hz) o como un valor de ancho simple, dependiendo de si el predefinido se guardó con posiciones de borde explícitas. Ambos formatos se leen correctamente cuando vuelve a abrir el applet o cambia de modo (#2259).
- La lectura del ancho de filtro se comparte con el panel VFO a través de `RxApplet::formatFilterWidth()`. En v0.9.8+, este método es ahora una función estática pública para que ambos widgets produzcan un formato idéntico y consciente del modo para modos SSB, digital y AM (#2197).
- Los atajos de ampliar/reducir (por ejemplo, Ctrl+Shift+W, Ctrl+Shift+N) llaman a `stepFilterWidth(int direction)`, que recorre la lista de predefinidos de filtro por modo para encontrar el siguiente ancho válido y lo aplica con la geometría de borde correcta para el modo actual (#2208).

## Solución de problemas

- **El repetidor no responde a sus transmisiones** — Confirme que el valor del tono CTCSS coincida con lo que espera el repetidor y que Tone mode esté configurado en **CTCSS TX** en lugar de **Off**.
- **La frecuencia de TX parece incorrecta** — Verifique que el botón de dirección de desplazamiento (**−**, **Simplex** o **+**) coincida con la dirección de desplazamiento publicada del repetidor y que el valor Offset (FM) esté ajustado a la magnitud correcta (por ejemplo, 0,6 MHz para un repetidor típico de 2 m).
- **Los controles Tone mode y CTCSS no están visibles** — El modo del slice debe ser **FM**, **NFM** o **DFM**. Estos controles están ocultos en todos los demás modos.
- **Los controles de squelch están atenuados** — El squelch se deshabilita automáticamente cuando el modo del slice es **DIGU**, **DIGL**, **NT**, **RTTY**, **CW** o **CWL**. Cambie a un modo FM o SSB para habilitar los controles de squelch.
- **Los botones de la pestaña de slice aparecen incorrectos después de reconectar** — Si la fila de pestañas de slice muestra el número incorrecto de botones o un diseño obsoleto después de que la radio se reconecta, desconecte y reconecte manualmente. En v0.9.5.1 esto se corrige automáticamente: el applet llama a `clearSliceButtons()` para eliminar los botones antiguos y restaurar la insignia de slice estática antes de reconstruir la fila de pestañas para el nuevo conteo de slices (#2254).
- **El botón predefinido de filtro no cambia la banda pasante** — Si el ancho actual no es un valor predefinido estándar, el paso de ampliar/reducir puede no cambiar la banda pasante. Este comportamiento es normal; haga clic en un botón predefinido de filtro específico o escriba una frecuencia para cambiar la banda pasante, luego los atajos de ampliar/reducir funcionarán desde el nuevo ancho.

## Notas sobre el modo NT y el modo RTTY

Los modos **NT** y **RTTY** se tratan como modos digitales en el applet RX Controls (v0.9.3+ para NT, v26.5.1 para RTTY). Esto tiene los siguientes efectos:

- NT y RTTY usan los mismos predefinidos de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El indicador de ancho de filtro calcula el ancho de banda de la misma manera que USB (usando el borde superior de la banda pasante).
- El squelch se deshabilita mientras NT o RTTY esté activo. Si el squelch estaba encendido cuando cambió a NT o RTTY, se apaga automáticamente y se restaura cuando sale del modo.
- Para el modo RTTY específicamente, el squelch se deshabilita porque eliminaría los caracteres FSK y rompería la decodificación (#2504).

## Relacionados

- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Seleccionar la antena RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
