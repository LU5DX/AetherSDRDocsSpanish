# Trabajar con un repetidor FM con tono CTCSS y desplazamiento +/−

Configure un slice para operación en repetidor FM: seleccione el modo FM, introduzca el desplazamiento de entrada del repetidor y agregue un tono de acceso CTCSS para abrir el repetidor.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. Si no lo está, use `Settings > Connect to Radio...` para conectarse.
- Necesita conocer la frecuencia de salida del repetidor, la dirección del desplazamiento (+ o −), el valor del desplazamiento en MHz y la frecuencia del tono CTCSS (si es requerida).

## Pasos

1. Abra el applet RX Controls. Siempre está visible en el panel de applets (barra lateral derecha). Si el panel está oculto, haga clic en el botón RX de la barra lateral derecha.
2. Si tiene más de un slice activo, haga clic en la pestaña del slice correcto (A hasta H) en la parte superior del applet.
3. Haga clic en el combo Mode y seleccione **FM**, **NFM** o **DFM** según el tipo de emisión del repetidor.
4. Haga clic en la etiqueta Frequency para activar el modo de edición. Escriba la frecuencia de **salida** (recepción) del repetidor en MHz y presione Enter.
5. Establezca el valor del desplazamiento: haga clic en el spinbox Offset (FM) y ajústelo al valor de desplazamiento del repetidor en MHz. El rango válido es de 0.0 a 100.0 MHz en pasos de 0.1 MHz. Por ejemplo, escriba `0.6` para un desplazamiento estándar de 2 m.
6. Establezca la dirección del desplazamiento:
   - Haga clic en `+` (desplazamiento hacia arriba) si la entrada del repetidor está por encima de su salida.
   - Haga clic en `−` (desplazamiento hacia abajo) si la entrada del repetidor está por debajo de su salida.
   - Haga clic en Simplex si trabaja en simplex (TX = RX). Simplex es la opción predeterminada.
7. Si el repetidor requiere un tono de acceso CTCSS:
   1. Haga clic en el combo Tone mode (FM) y seleccione **CTCSS TX**.
   2. Haga clic en el combo de valor de tono CTCSS y seleccione la frecuencia de tono requerida. La lista contiene los 41 tonos estándar EIA/TIA-603, desde 67.0 Hz hasta 254.1 Hz.
8. Si necesita escuchar en la frecuencia de entrada del repetidor para verificar si está en uso, haga clic en REV. Haga clic en REV nuevamente para volver a la operación normal.

## Qué hace cada control

| Control | Predeterminado | Rango / opciones válidas | Comportamiento |
|---|---|---|---|
| Combo Mode | USB | FM, NFM, DFM (entre otros) | Establece el slice en un modo de la familia FM; oculta los preajustes de ancho de filtro. |
| Offset (FM) | 0.0 MHz | 0.0–100.0 MHz, paso 0.1 | Establece el valor del desplazamiento TX del repetidor. |
| − (desplazamiento hacia abajo) | — | alternado | Fija la frecuencia TX por debajo de la frecuencia RX según el valor de desplazamiento. |
| Simplex | activado | alternado | Fija la frecuencia TX igual a la frecuencia RX (sin desplazamiento). |
| + (desplazamiento hacia arriba) | — | alternado | Fija la frecuencia TX por encima de la frecuencia RX según el valor de desplazamiento. |
| REV | — | alternado | Invierte la dirección del desplazamiento para monitorear la entrada del repetidor. |
| Tone mode (FM) | Off | Off, CTCSS TX | Selecciona si se envía un tono CTCSS durante la transmisión. |
| Valor de tono CTCSS | — | 67.0–254.1 Hz (41 tonos EIA/TIA-603) | Selecciona la frecuencia del tono CTCSS. Activo solo cuando Tone mode es CTCSS TX. |

## Consejos

- Los botones de preajuste de ancho de filtro no se muestran en los modos FM, NFM ni DFM. El ajuste `FilterPresets` no aplica en estos modos.
- Haga doble clic en el deslizador de paneo L / R para restablecerlo al centro (50) si se ha modificado el balance de audio.
- Para activar el squelch de modo que el audio se abra solo cuando el repetidor esté activo, consulte [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md).

## Solución de problemas

- **El repetidor no responde a su transmisión** — Confirme que el valor del tono CTCSS coincide con el tono de acceso publicado por el repetidor y que Tone mode está configurado en CTCSS TX, no en Off.
- **La frecuencia TX parece estar en el lado incorrecto respecto a la salida del repetidor** — Verifique que ha seleccionado la dirección de desplazamiento correcta (`+` o `−`). Use REV temporalmente para confirmar en qué lado está la entrada.
- **El spinbox Offset (FM) no está visible** — Los controles de desplazamiento aparecen únicamente cuando el modo del slice es FM, NFM o DFM. Verifique que el combo Mode muestre una de esas opciones.

## Relacionados

- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Seleccionar la antena RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
