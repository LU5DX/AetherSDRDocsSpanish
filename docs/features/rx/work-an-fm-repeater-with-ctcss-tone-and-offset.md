# Trabajar en un repetidor FM con tono CTCSS y desplazamiento +/-

Configure una slice para operación FM dúplex con un desplazamiento de repetidor y un tono de acceso CTCSS para que pueda escuchar tanto la salida del repetidor como activarlo correctamente en transmisión.

## Antes de comenzar

- AetherSDR está conectado a su FLEX-8600.
- El applet RX Controls es visible en la barra lateral derecha. Si no aparece, haga clic en el botón RX tray en la barra lateral derecha.
- Conoce la frecuencia de salida del repetidor, la dirección del desplazamiento, la magnitud del desplazamiento y la frecuencia del tono CTCSS.

## Pasos

1. En el applet RX Controls, haga clic en el combo Mode y seleccione **FM** (o **NFM** para FM angosto).
2. Haga clic en la etiqueta Frequency para abrir el campo de edición de frecuencia. Escriba la frecuencia de **salida** (recepción) del repetidor en MHz y presione Intro.
3. En el spinbox **Offset (FM)**, establezca la magnitud del desplazamiento en MHz. Use las flechas del spinbox o escriba un valor directamente. El rango válido es 0,0–100,0 MHz en pasos de 0,1 MHz. El valor predeterminado es 0,0 MHz.
4. Establezca la dirección del desplazamiento haciendo clic en uno de los tres botones de alternancia:
   - **−** — La frecuencia TX está por debajo de la frecuencia RX.
   - **Simplex** — La frecuencia TX es igual a la frecuencia RX (predeterminado).
   - **+** — La frecuencia TX está por encima de la frecuencia RX.
5. Haga clic en el combo **Tone mode (FM)** (predeterminado: **Off**) y seleccione **CTCSS TX**.
6. Haga clic en el combo **CTCSS tone value** y seleccione la frecuencia de tono requerida por el repetidor. Los tonos disponibles siguen el estándar 41-tone EIA/TIA-603, desde 67,0 Hz hasta 254,1 Hz.
7. Confirme que el squelch está configurado apropiadamente para la banda. Consulte [Turn on the squelch and set its threshold](turn-on-the-squelch-and-set-its-threshold.md) si es necesario.

## Qué hace cada control

| Control          | Predeterminado | Rango válido / opciones                   |
|------------------|----------------|-------------------------------------------|
| Mode combo       | USB            | FM, NFM, DFM (entre otros)                |
| Tone mode (FM)   | Off            | Off, CTCSS TX                             |
| CTCSS tone value | —              | 67,0 Hz – 254,1 Hz (41 tonos EIA/TIA-603)|
| Offset (FM)      | 0,0 MHz        | 0,0 – 100,0 MHz, paso 0,1                 |
| − (offset down)  | —              | alternancia                               |
| Simplex          | marcado        | alternancia                               |
| + (offset up)    | —              | alternancia                               |
| REV              | —              | alternancia                               |

## Consejos

- Si necesita escuchar en la frecuencia de entrada del repetidor para verificar si el canal está ocupado antes de transmitir, haga clic en **REV** para invertir temporalmente la dirección del desplazamiento.
- Los modos de la familia FM ocultan los botones de preajuste de ancho de filtro. Esto es normal; el ancho de filtro para FM es fijo según el modo.
- Los botones de pestaña de slice y el badge de slice están codificados por color según la slice mediante SliceColorManager (v0.9.3+). Los colores persisten entre sesiones y se reflejan en las pestañas de slice, el badge de slice, los widgets VFO y las tiras de medidor.

## Solución de problemas

- **El repetidor no responde a sus transmisiones** — Confirme que el valor del tono CTCSS coincida con lo que espera el repetidor y que Tone mode esté configurado en **CTCSS TX** en lugar de **Off**.
- **La frecuencia TX aparece incorrecta** — Compruebe que el botón de dirección del desplazamiento (**−**, **Simplex** o **+**) coincida con la dirección del desplazamiento publicada del repetidor y que el valor Offset (FM) esté establecido en la magnitud correcta (por ejemplo, 0,6 MHz para un repetidor típico de 2 m).
- **Los controles Tone mode y CTCSS no son visibles** — El modo de slice debe ser **FM**, **NFM** o **DFM**. Estos controles están ocultos en todos los demás modos.
- **Los controles de squelch están deshabilitados** — El squelch se deshabilita automáticamente cuando el modo de slice es **DIGU**, **DIGL**, **NT**, **CW** o **CWL**. Cambie a un modo FM o SSB para habilitar los controles de squelch.

## Notas del modo NT

El modo **NT** se trata como un modo digital en el applet RX Controls (v0.9.3+). Esto tiene los siguientes efectos:

- NT utiliza los mismos preajustes de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El indicador de ancho de filtro calcula el ancho de banda de la misma manera que USB (usando el borde de banda pasante superior).
- El squelch se deshabilita mientras NT está activo. Si el squelch estaba activado cuando cambió a NT, se desactiva automáticamente y se restaura cuando abandone el modo.

## Relacionado

- [Change mode (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Tune the radio to a frequency (type MHz in the readout)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Turn on the squelch and set its threshold](turn-on-the-squelch-and-set-its-threshold.md)
- [Select the RX or TX antenna for this slice](select-the-rx-or-tx-antenna-for-this-slice.md)
