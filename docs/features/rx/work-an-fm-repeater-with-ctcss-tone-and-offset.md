# Trabajar un repetidor FM con tono CTCSS y desplazamiento +/−

Configure un slice para operación FM dúplex con desplazamiento de repetidor y tono de acceso CTCSS, de modo que pueda escuchar la salida del repetidor y activarlo correctamente en transmisión.

## Antes de comenzar

- AetherSDR está conectado a su FLEX-8600.
- El applet RX Controls es visible en la barra lateral derecha. Si no lo está, haga clic en el botón RX tray de la barra lateral derecha.
- Conoce la frecuencia de salida del repetidor, la dirección del desplazamiento, la magnitud del desplazamiento y la frecuencia del tono CTCSS.

## Pasos

1. En el applet RX Controls, haga clic en el combo Mode y seleccione **FM** (o **NFM** para FM estrecha).
2. Haga clic en la etiqueta Frequency para abrir el campo de edición de frecuencia. Escriba la frecuencia de **salida** (recepción) del repetidor en MHz y presione Enter.
3. En el cuadro numérico **Offset (FM)**, establezca la magnitud del desplazamiento en MHz. Use las flechas del cuadro numérico o escriba un valor directamente. El rango válido es de 0.0 a 100.0 MHz en pasos de 0.1 MHz. El valor predeterminado es 0.0 MHz.
4. Establezca la dirección del desplazamiento haciendo clic en uno de los tres botones de selección:
   - **−** — La frecuencia de TX está por debajo de la frecuencia de RX.
   - **Simplex** — La frecuencia de TX es igual a la frecuencia de RX (predeterminado).
   - **+** — La frecuencia de TX está por encima de la frecuencia de RX.
5. Haga clic en el combo **Tone mode (FM)** (predeterminado: **Off**) y seleccione **CTCSS TX**.
6. Haga clic en el combo **CTCSS tone value** y seleccione la frecuencia de tono requerida por el repetidor. Los tonos disponibles siguen el estándar EIA/TIA-603 de 41 tonos, desde 67.0 Hz hasta 254.1 Hz.
7. Confirme que el squelch esté configurado de manera apropiada para la banda. Consulte [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md) si es necesario.

## Qué hace cada control

| Control | Predeterminado | Rango válido / opciones | Notas |
|---|---|---|---|
| Mode combo | USB | FM, NFM, DFM (entre otros) | Los preajustes de ancho de filtro están ocultos para todos los modos de la familia FM. |
| Tone mode (FM) | Off | Off, CTCSS TX | Visible solo cuando el modo es FM, NFM o DFM. |
| CTCSS tone value | — | 67.0 Hz – 254.1 Hz (41 tonos EIA/TIA-603) | Habilitado solo cuando Tone mode está configurado en CTCSS TX. |
| Offset (FM) | 0.0 MHz | 0.0 – 100.0 MHz, paso 0.1 | Establece la magnitud del desplazamiento del repetidor. |
| − (desplazamiento hacia abajo) | — | selección | La frecuencia de TX se ubica por debajo de la frecuencia de RX. |
| Simplex | activado | selección | Las frecuencias de TX y RX son iguales. |
| + (desplazamiento hacia arriba) | — | selección | La frecuencia de TX se ubica por encima de la frecuencia de RX. |
| REV | — | selección | Invierte el signo del desplazamiento configurado; úselo para escuchar en un par de repetidor invertido. |

## Consejos

- Si necesita escuchar en la frecuencia de entrada del repetidor para verificar si el canal está ocupado antes de transmitir, haga clic en **REV** para invertir temporalmente la dirección del desplazamiento.
- Los modos de la familia FM ocultan los botones de preajuste de ancho de filtro. Esto es esperado; el ancho de filtro para FM está determinado por el propio modo.

## Solución de problemas

- **El repetidor no responde a sus transmisiones** — Confirme que el valor de CTCSS tone value coincida con el que espera el repetidor, y que Tone mode esté configurado en **CTCSS TX** y no en **Off**.
- **La frecuencia de TX parece incorrecta** — Verifique que el botón de dirección del desplazamiento (**−**, **Simplex** o **+**) coincida con la dirección de desplazamiento publicada por el repetidor, y que el valor de Offset (FM) esté configurado con la magnitud correcta (p. ej., 0.6 MHz para un repetidor típico de 2 m).
- **Los controles Tone mode y CTCSS no son visibles** — El modo del slice debe ser **FM**, **NFM** o **DFM**. Estos controles están ocultos en todos los demás modos.

## Relacionados

- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Seleccionar la antena de RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
