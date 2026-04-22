# Ajustar la ganancia TX de DAX

Ajuste el control deslizante de ganancia TX en el applet DAX Audio para controlar el nivel del flujo de audio de transmisión enviado desde su computadora a la radio. Configurarlo correctamente evita que la ruta DAX TX reciba una señal excesiva o insuficiente al usar software de modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet DAX Audio requiere una conexión activa con la radio.
- DAX debe estar habilitado. Haga clic en Enable en el applet DAX Audio si aún no está activo.

## Pasos

1. Haga clic en el botón DAX de la barra lateral derecha para abrir el applet DAX Audio.
2. Localice la fila **TX:** en la parte inferior del applet. El medidor combinado con el control deslizante muestra la posición actual de la ganancia TX y el nivel de audio TX en tiempo real.
3. Arrastre el control deslizante hacia la izquierda para disminuir la ganancia TX o hacia la derecha para aumentarla. El rango válido es de 0.0 a 1.0. El valor predeterminado es 0.5.
4. Suelte el control deslizante. El valor se guarda inmediatamente en `DaxTxGain` y surte efecto sin necesidad de reiniciar.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Ganancia TX + medidor | 0.5 | 0.0–1.0 | `DaxTxGain` | Arrastre para ajustar la ganancia del flujo TX. El medidor detrás del cursor muestra el nivel de transmisión en tiempo real, posterior al fader. |
| Indicador de asignación TX | — | — o Slice A–H | — | Muestra qué slice tiene actualmente los privilegios de TX y controla el flujo DAX TX. Solo lectura. |
| Enable | off | on/off | `AutoStartDAX` | Interruptor principal para todos los flujos DAX, incluido TX. La ganancia TX no tiene efecto mientras DAX está deshabilitado. |

## Consejos

- El relleno del medidor detrás del control deslizante refleja el nivel posterior al fader — el nivel de entrada sin procesar multiplicado por la ganancia actual — por lo que puede ver el nivel de salida TX efectivo mientras arrastra.
- Si el indicador de asignación TX muestra —, ningún slice tiene actualmente los privilegios de TX. Asegúrese de que su slice de transmisión esté seleccionado en la radio antes de ajustar la ganancia TX.

## Resolución de problemas

- **El medidor TX no muestra actividad** — El audio DAX TX solo fluye mientras la radio está transmitiendo o una aplicación de modo digital está enviando audio al dispositivo DAX TX. Verifique que su software (WSJT-X, fldigi, etc.) esté enrutado al dispositivo de audio DAX TX correcto.
- **La ganancia TX se restablece después de reiniciar** — Verifique que `AutoStartDAX` esté habilitado para que el puente DAX se inicie al arrancar y restaure el valor guardado de `DaxTxGain`. Consulte [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md).

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia DAX RX por canal](set-dax-rx-gain-per-channel.md)
- [Identificar cuál slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md)
