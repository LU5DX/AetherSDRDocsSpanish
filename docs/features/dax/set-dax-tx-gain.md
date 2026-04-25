# Ajustar la ganancia TX de DAX

Mueva el control deslizante de ganancia TX en el applet DAX Audio para controlar el nivel de salida del flujo de transmisión DAX enviado desde el audio de su computadora hacia la radio. Esto es útil cuando el nivel de salida de audio de su software de modos digitales es demasiado alto o demasiado bajo en relación con el nivel de entrada esperado por la radio.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet DAX requiere una conexión de radio activa.
- Abra el applet DAX haciendo clic en el botón DAX de la bandeja en la barra lateral derecha. El applet está oculto de manera predeterminada.
- DAX debe estar habilitado. Si el botón Enable no está iluminado, haga clic en Enable para iniciar el puente de audio DAX.

## Pasos

1. Haga clic en el botón DAX de la bandeja en la barra lateral derecha para abrir el applet DAX Audio.
2. Ubique la fila TX en la parte inferior del applet. Muestra la etiqueta "TX:", un indicador de asignación de slice y un medidor/deslizador combinado.
3. Arrastre el control del deslizador TX de ganancia+medidor hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El rango válido es de 0.0 a 1.0.
4. Suelte el botón del mouse. El nuevo valor se guarda inmediatamente en `DaxTxGain`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Deslizador TX de ganancia+medidor | 0.5 | 0.0–1.0 | `DaxTxGain` | Establece la ganancia para el flujo TX de DAX. La barra del medidor detrás del deslizador muestra el nivel de salida actual después del fader. |
| Indicador de asignación TX | — | — o Slice A–H | *(none)* | Muestra qué slice tiene actualmente los privilegios de TX y maneja el flujo TX de DAX. |

## Consejos

- La barra del medidor detrás del deslizador muestra el nivel posterior al fader, es decir, el nivel de audio entrante multiplicado por la configuración de ganancia actual. Una barra que permanece cerca del borde derecho con la ganancia actual sugiere que la ganancia es demasiado alta; redúzcala para evitar recorte de señal (clipping).
- El valor de ganancia persiste entre sesiones. No es necesario volver a ingresarlo después de reiniciar AetherSDR.

## Solución de problemas

- **El medidor TX no muestra actividad** — Es posible que el slice TX aún no esté asignado. Verifique el indicador de asignación TX. Si muestra "—", ningún slice tiene actualmente los privilegios de TX. Consulte [Identificar cuál slice es el slice TX](identify-which-slice-is-the-tx-slice.md).
- **La posición del deslizador se restablece al volver a abrir** — Si DAX no estaba habilitado cuando configuró la ganancia, el ajuste igualmente se guarda; sin embargo, confirme que Enable esté activo para que el puente esté en funcionamiento y el valor surta efecto.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Identificar cuál slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Inicio automático de DAX al lanzar la aplicación](autostart-dax-on-launch.md)
