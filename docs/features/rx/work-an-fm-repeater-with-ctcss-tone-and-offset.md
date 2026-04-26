# Trabajar un repetidor FM con tono CTCSS y desplazamiento +/−

Configure AetherSDR para acceder a un repetidor FM: seleccione el modo FM, introduzca la frecuencia de salida del repetidor, configure la dirección y magnitud del desplazamiento de TX, y agregue un tono CTCSS para que el repetidor abra su silenciador (squelch).

## Antes de comenzar

- AetherSDR está conectado a la radio. El applet RX Controls es visible en el Panel de Applets. Si no lo está, haga clic en el botón RX del área de notificación en la barra lateral derecha.
- Conoce la frecuencia de salida (escucha) del repetidor, la dirección del desplazamiento (+/−), el tamaño del desplazamiento en MHz y la frecuencia del tono CTCSS en Hz.

## Pasos

1. En el applet RX Controls, seleccione el slice que desea usar haciendo clic en la pestaña correspondiente (A hasta H) en la fila de pestañas de slice.
2. Haga clic en el combo Mode y seleccione **FM** (o **NFM** para FM angosta).
3. Haga clic en la etiqueta Frequency para abrir el campo de edición de frecuencia. Escriba la frecuencia de salida del repetidor en MHz y presione Enter. La radio se sintoniza a esa frecuencia.
4. Configure la dirección del desplazamiento del repetidor:
   - Haga clic en **−** si el repetidor transmite por debajo de su frecuencia de salida (TX por debajo de RX).
   - Haga clic en **+** si el repetidor transmite por encima de su frecuencia de salida (TX por encima de RX).
   - Haga clic en **Simplex** si no se necesita desplazamiento (TX = RX).
5. Ajuste el spinbox Offset a la magnitud del desplazamiento. Haga clic en las flechas **<** o **>**, o use la rueda del ratón, para alcanzar el valor correcto en MHz (rango 0.0–100.0 MHz, paso 0.1). Por ejemplo, el desplazamiento estándar de 2 m es 0.6 MHz; el de 70 cm es 5.0 MHz.
6. Ajuste el combo de modo Tone a **CTCSS TX**.
7. Ajuste el combo de valor CTCSS tone a la frecuencia de tono requerida por el repetidor (67.0 Hz a 254.1 Hz, 41 tonos estándar EIA/TIA-603).
8. Para confirmar que el desplazamiento es correcto antes de transmitir, haga clic en **REV** para escuchar en la frecuencia de entrada del repetidor y verificar que el canal esté libre; luego haga clic en **REV** nuevamente para volver a la operación normal.

## Qué hace cada control

| Control | Valor predeterminado | Rango / valores válidos | Comportamiento |
|---|---|---|---|
| Combo Mode | USB | USB, LSB, CW, AM, SAM, **FM**, **NFM**, **DFM**, DIGU, DIGL, RTTY | Establece el modo de demodulación del slice. Seleccione FM o NFM para operar con repetidores. |
| Modo Tone (FM) | Off | Off, CTCSS TX | Habilita la generación del tono CTCSS en transmisión. Solo visible en modos de la familia FM. |
| Valor CTCSS tone | — | 67.0 Hz – 254.1 Hz (41 tonos EIA/TIA-603) | Selecciona el tono subaudible enviado durante TX. Activo solo cuando el modo Tone es CTCSS TX. |
| Offset (FM) | 0.0 MHz | 0.0–100.0 MHz, paso 0.1 | Establece la magnitud del desplazamiento de TX del repetidor. |
| − (desplazamiento hacia abajo) | — | conmutador | Establece la frecuencia de TX por debajo de la frecuencia de RX según el valor de Offset. |
| Simplex | activado | conmutador | Establece la frecuencia de TX igual a la de RX (sin desplazamiento). |
| + (desplazamiento hacia arriba) | — | conmutador | Establece la frecuencia de TX por encima de la frecuencia de RX según el valor de Offset. |
| REV | — | conmutador | Invierte el signo del desplazamiento. Úselo para escuchar en la entrada del repetidor antes de transmitir. |

## Consejos

- Los botones de preajuste de ancho de filtro están ocultos en los modos FM, NFM y DFM. El ancho de filtro está fijado por el modo; no espere que aparezcan botones de preajuste.
- Si no puede escuchar el tono de cortesía del repetidor ni otro tráfico, verifique que el combo Mode muestre FM o NFM, y no USB u otro modo SSB.
- Hacer doble clic en el control deslizante de paneo L / R restablece el paneo de audio al centro (50).

## Solución de problemas

- **El repetidor no responde a su transmisión** — Confirme que el modo Tone está configurado como **CTCSS TX** y que el valor de CTCSS tone coincide con el requisito del repetidor. Confirme que el valor del spinbox Offset y la dirección (+ o −) son correctos para el repetidor.
- **REV parece no hacer nada** — REV solo tiene efecto visible cuando el spinbox Offset es distinto de cero y se ha seleccionado una dirección (+ o −). Verifique que Offset no sea 0.0 MHz y que Simplex no esté activo.
- **TX va a la frecuencia incorrecta** — Verifique qué botón de dirección está activo. Solo uno de −, Simplex o + debe estar seleccionado a la vez. Haga clic en el correcto para deseleccionar los demás.

## Relacionados

- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Activar el silenciador y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Seleccionar la antena de RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
