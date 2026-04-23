# Trabajar un repetidor FM con tono CTCSS y desplazamiento +/−

Configure un slice para operación en repetidor FM estableciendo el modo, la frecuencia de desplazamiento del repetidor, su dirección y un tono CTCSS opcional para abrir el squelch del repetidor.

## Antes de comenzar

- AetherSDR debe estar conectado al radio Flex.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX del panel lateral derecho para mostrarlo.
- Conozca la frecuencia de salida del repetidor, la dirección del desplazamiento, la magnitud del desplazamiento y el tono CTCSS (si es requerido).

## Pasos

1. En el applet RX Controls, seleccione el slice que desea usar haciendo clic en la pestaña correspondiente (A hasta H), si hay más de un slice disponible.
2. Haga clic en el combo Mode y seleccione **FM**, **NFM** o **DFM** según corresponda para el repetidor.
3. Haga clic en la etiqueta Frequency para entrar al modo de edición. Escriba la frecuencia de **salida** (recepción) del repetidor en MHz y presione Enter.
4. En el spinbox Offset (FM), establezca la magnitud del desplazamiento del repetidor. El rango válido es de 0.0 a 100.0 MHz en pasos de 0.1 MHz. Por ejemplo, introduzca `0.6` para un desplazamiento estándar de 2 m.
5. Haga clic en el botón de dirección del desplazamiento que corresponda al repetidor:
   - Haga clic en **+** si la entrada del repetidor (su frecuencia de transmisión) está por encima de la salida.
   - Haga clic en **−** si la entrada del repetidor está por debajo de la salida.
   - Haga clic en **Simplex** para cancelar cualquier desplazamiento (TX = RX). Simplex es el valor predeterminado.
6. Si el repetidor requiere un tono CTCSS, haga clic en el combo Tone mode (FM) y seleccione **CTCSS TX**.
7. Haga clic en el combo de valor de tono CTCSS y seleccione la frecuencia de tono requerida por el repetidor. Están disponibles los 41 tonos estándar EIA/TIA-603, de 67.0 Hz a 254.1 Hz.
8. Para verificar que el radio transmite en la frecuencia correcta antes de un QSO, puede hacer clic en **REV** para invertir temporalmente la dirección del desplazamiento y escuchar en la entrada del repetidor. Haga clic en REV nuevamente para volver a la operación normal.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Combo Mode | USB | FM, NFM, DFM (entre otros) | Establece el slice en un modo de la familia FM. Los preajustes de ancho de filtro se ocultan en los modos FM. |
| Offset (FM) | 0.0 MHz | 0.0–100.0 MHz, paso 0.1 | Establece la magnitud del desplazamiento del repetidor en MHz. |
| − (desplazamiento hacia abajo) | — | — | Establece la frecuencia TX por debajo de la frecuencia RX según la cantidad de desplazamiento. |
| Simplex | activado | — | Establece la frecuencia TX igual a la frecuencia RX (sin desplazamiento). |
| + (desplazamiento hacia arriba) | — | — | Establece la frecuencia TX por encima de la frecuencia RX según la cantidad de desplazamiento. |
| REV | — | — | Invierte la dirección del desplazamiento actual. Útil para escuchar en la entrada del repetidor. |
| Tone mode (FM) | Off | Off, CTCSS TX | Selecciona si se transmite un tono CTCSS. Visible solo en modos de la familia FM. |
| Valor de tono CTCSS | — | 67.0 Hz–254.1 Hz (41 tonos) | Selecciona la frecuencia del tono CTCSS. Activo solo cuando Tone mode está configurado en CTCSS TX. |

## Consejos

- La fila de preajustes de ancho de filtro se oculta automáticamente cuando el modo es FM, NFM o DFM. Esto es normal.
- Si desea evitar un resintonizado accidental mientras monitorea un repetidor concurrido, haga clic en el botón 🔓 en la fila de encabezado para bloquear el slice. El ícono cambia a 🔒 cuando está bloqueado.
- Para silenciar el audio mientras configura el slice, haga clic en el botón 🔊 / 🔇. Haga clic nuevamente para restaurar el audio.
- Ajuste el squelch para reducir el ruido entre transmisiones: haga clic en SQL para activarlo y luego ajuste el control deslizante Squelch level. Un valor inicial de 20 (el predeterminado) es una referencia razonable para FM.

## Solución de problemas

- **Los controles Tone mode (FM) y valor de tono CTCSS no son visibles** — El modo del slice no está configurado en FM, NFM o DFM. Estos controles aparecen solo en modos de la familia FM. Cambie el combo Mode a FM, NFM o DFM.
- **La frecuencia TX es incorrecta después de establecer el desplazamiento** — Confirme que el botón de dirección del desplazamiento (+, − o Simplex) corresponda a la especificación del repetidor. Use REV para escuchar en la entrada del repetidor y verificar qué dirección es la correcta.
- **El repetidor no responde a las transmisiones** — Confirme que el valor del tono CTCSS coincida exactamente con el tono requerido por el repetidor y que Tone mode (FM) esté configurado en CTCSS TX en lugar de Off.

## Relacionados

- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Bloquear el slice para evitar un resintonizado accidental](lock-the-slice-to-prevent-accidental-retuning.md)
