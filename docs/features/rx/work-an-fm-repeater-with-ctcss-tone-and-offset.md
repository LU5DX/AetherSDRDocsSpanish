# Trabajar con un repetidor FM con tono CTCSS y desplazamiento +/−

Configure un slice para operación FM dúplex con un desplazamiento de repetidor y un tono de acceso CTCSS, de modo que pueda escuchar la salida del repetidor y activarlo correctamente en transmisión.

## Antes de comenzar

- AetherSDR está conectado a su FLEX-8600.
- El applet RX Controls es visible en la barra lateral derecha. Si no lo es, haga clic en el botón RX tray en la barra lateral derecha.
- Conoce la frecuencia de salida del repetidor, la dirección del desplazamiento, la magnitud del desplazamiento y la frecuencia del tono CTCSS.

## Pasos

1. En el applet RX Controls, haga clic en el combo Mode y seleccione **FM** (o **NFM** para FM estrecha).
2. Haga clic en la etiqueta Frequency para abrir el campo de edición de frecuencia. Escriba la frecuencia de **salida** (recepción) del repetidor en MHz y presione Enter.
3. En el spinbox **Offset (FM)**, establezca la magnitud del desplazamiento en MHz. Use las flechas del spinbox o escriba un valor directamente. El rango válido es de 0.0 a 100.0 MHz en pasos de 0.1 MHz. El valor predeterminado es 0.0 MHz.
4. Establezca la dirección del desplazamiento haciendo clic en uno de los tres botones de selección:
   - **−** — la frecuencia de TX está por debajo de la frecuencia de RX.
   - **Simplex** — la frecuencia de TX es igual a la frecuencia de RX (predeterminado).
   - **+** — la frecuencia de TX está por encima de la frecuencia de RX.
5. Haga clic en el combo **Tone mode (FM)** (predeterminado: **Off**) y seleccione **CTCSS TX**.
6. Haga clic en el combo **CTCSS tone value** y seleccione la frecuencia de tono requerida por el repetidor. Los tonos disponibles siguen el estándar EIA/TIA-603 de 41 tonos, de 67.0 Hz a 254.1 Hz.
7. Confirme que el squelch esté configurado de manera adecuada para la banda. Consulte [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md) si es necesario.

## Qué hace cada control

| Control          | Predeterminado | Rango válido / opciones                     |
|------------------|----------------|---------------------------------------------|
| Mode combo       | USB            | FM, NFM, DFM (entre otros)                  |
| Tone mode (FM)   | Off            | Off, CTCSS TX                               |
| CTCSS tone value | —              | 67.0 Hz – 254.1 Hz (41 tonos EIA/TIA-603)  |
| Offset (FM)      | 0.0 MHz        | 0.0 – 100.0 MHz, paso 0.1                  |
| − (offset down)  | —              | alternancia                                 |
| Simplex          | activado       | alternancia                                 |
| + (offset up)    | —              | alternancia                                 |
| REV              | —              | alternancia                                 |

## Consejos

- Si necesita escuchar en la frecuencia de entrada del repetidor para verificar si el canal está ocupado antes de transmitir, haga clic en **REV** para invertir temporalmente la dirección del desplazamiento.
- Los modos de la familia FM ocultan los botones de preajuste de ancho de filtro. Esto es normal; el ancho de filtro para FM está fijado por el propio modo.
- Los botones de pestaña de slice y la insignia de slice tienen código de color por slice mediante SliceColorManager (v0.9.3+). Los colores persisten entre sesiones y se reflejan en las pestañas de slice, la insignia de slice, los widgets VFO y las tiras de medidor.
- Cuando la radio informa un número diferente de slices disponibles al que tenía la fila de pestañas, AetherSDR elimina los botones de pestaña de slice existentes y los reconstruye para el nuevo número antes de reconectar los manejadores de clic (v0.9.5.1, #2254). Esto evita que aparezcan botones obsoletos después de una reconexión o un cambio en la configuración del hardware.
- Los preajustes de ancho de filtro se almacenan en el formato `lo:hi` (bordes de la banda de paso en Hz) o como un valor de ancho simple, según si el preajuste fue guardado con posiciones de borde explícitas. Ambos formatos se leen correctamente al reabrir el applet o cambiar de modo (#2259).

## Solución de problemas

- **El repetidor no responde a sus transmisiones** — Confirme que el valor del tono CTCSS coincide con el que espera el repetidor, y que el modo de tono esté configurado en **CTCSS TX** y no en **Off**.
- **La frecuencia de TX parece incorrecta** — Verifique que el botón de dirección de desplazamiento (**−**, **Simplex** o **+**) coincida con la dirección de desplazamiento publicada por el repetidor, y que el valor de Offset (FM) esté configurado con la magnitud correcta (por ejemplo, 0.6 MHz para un repetidor típico de 2 m).
- **Los controles de Tone mode y CTCSS no son visibles** — El modo del slice debe ser **FM**, **NFM** o **DFM**. Estos controles están ocultos en todos los demás modos.
- **Los controles de squelch están atenuados** — El squelch se deshabilita automáticamente cuando el modo del slice es **DIGU**, **DIGL**, **NT**, **CW** o **CWL**. Cambie a un modo FM o SSB para habilitar los controles de squelch.
- **Los botones de pestaña de slice aparecen incorrectos después de reconectar** — Si la fila de pestañas de slice muestra un número incorrecto de botones o un diseño obsoleto después de que la radio se reconecta, desconéctese y vuelva a conectarse manualmente. En v0.9.5.1 esto se corrige automáticamente: el applet llama a `clearSliceButtons()` para eliminar los botones antiguos y restaurar la insignia de slice estática antes de reconstruir la fila de pestañas para el nuevo número de slices (#2254).

## Notas sobre el modo NT

El modo **NT** se trata como un modo digital en el applet RX Controls (v0.9.3+). Esto tiene los siguientes efectos:

- NT utiliza los mismos preajustes de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El indicador de ancho de filtro calcula el ancho de banda de la misma manera que USB (usando el borde superior de la banda de paso).
- El squelch se deshabilita mientras NT está activo. Si el squelch estaba activado al cambiar a NT, se desactiva automáticamente y se restaura al salir del modo.

## Relacionados

- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en el display)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Seleccionar la antena de RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
