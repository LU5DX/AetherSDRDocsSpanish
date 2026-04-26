# Ajustar la ganancia TX de DAX

Mueva el control deslizante de ganancia TX de DAX para controlar el nivel de audio enviado desde su computadora a la cadena de transmisión del radio a través del puente de audio DAX.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet de DAX requiere una conexión de radio activa.
- DAX debe estar habilitado. Haga clic en Enable en el applet DAX Audio para iniciar el puente DAX antes de ajustar la ganancia TX.

## Pasos

1. Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para abrir el applet DAX Audio.
2. Si el botón Enable no está encendido, haga clic en **Enable** para iniciar el puente DAX.
3. Localice la fila **TX:** en la parte inferior del applet. El medidor y control deslizante combinados muestran la ganancia TX actual y el nivel de audio TX en tiempo real.
4. Arrastre el control deslizante hacia la izquierda para reducir la ganancia TX o hacia la derecha para aumentarla. El valor se guarda inmediatamente como `DaxTxGain`.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Enable | Inicia el puente de audio DAX. Debe estar activo para que fluya el audio TX. | Off | On / Off | `AutoStartDAX` |
| TX gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el flujo DAX TX. Arrastre el control para ajustar la ganancia. La barra del medidor refleja el nivel de salida posterior al fader. | 0.5 | 0.0 – 1.0 | `DaxTxGain` |
| Indicador de asignación TX | Muestra qué slice (canal receptor) tiene actualmente los privilegios TX y controla el flujo DAX TX. Muestra `—` cuando no hay ningún slice TX asignado, o `Slice A` a `Slice H`. | — | — / Slice A–H | — |

## Sugerencias

- La barra del medidor en la fila TX refleja el nivel posterior al fader: escala con la posición del control deslizante, por lo que obtiene retroalimentación visual inmediata al arrastrar.
- El valor de ganancia se guarda en cuanto suelta el control deslizante. Al reiniciar AetherSDR se restaura el valor guardado.
- Verifique el indicador de asignación TX en la fila TX para confirmar que el slice esperado está controlando DAX TX antes de transmitir.

## Solución de problemas

- **El medidor TX no muestra actividad durante la transmisión** — Verifique que Enable esté activo (botón encendido en verde). Confirme que su software de modo digital está enviando audio al dispositivo DAX TX correcto. Revise el indicador de asignación TX para asegurarse de que haya un slice asignado.
- **La ganancia se restablece a 0.5 después de reiniciar** — Si `DaxTxGain` no está presente en la configuración guardada, AetherSDR utiliza el valor predeterminado de 0.5. Realice un pequeño ajuste y suelte el control deslizante para forzar el guardado.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Identificar cuál slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Inicio automático de DAX al lanzar la aplicación](autostart-dax-on-launch.md)
