# Configurar la ganancia de RX de DAX por canal

Cada canal de RX de DAX (1–4) tiene un control de ganancia independiente en el applet de Audio DAX. Ajustarlos le permite igualar el nivel de audio enviado al software de modos digitales u otras aplicaciones que reciben audio de DAX.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El applet de Audio DAX debe estar abierto. Si no está visible, haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para mostrarlo.
- DAX debe estar habilitado. Si el botón **Enable** no está iluminado, haga clic en **Enable** en el applet de Audio DAX antes de ajustar la ganancia.

## Pasos

1. Haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para abrir el applet de Audio DAX.
2. Localice la fila del canal que desea ajustar: **DAX 1:**, **DAX 2:**, **DAX 3:** o **DAX 4:**.
3. Arrastre el medidor/deslizador combinado de ese canal hacia la izquierda o derecha para disminuir o aumentar la ganancia de RX.
4. Suelte el arrastre. El nuevo valor se guarda inmediatamente.

Repita el proceso para cualquier otro canal que necesite ajuste.

## Función de cada control

| Control | Predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Ganancia+medidor DAX 1 | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| Ganancia+medidor DAX 2 | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| Ganancia+medidor DAX 3 | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| Ganancia+medidor DAX 4 | 0.5 | 0.0–1.0 | `DaxRxGain4` |

Cada control es un medidor de nivel y deslizador de ganancia combinados. La barra de fondo muestra el nivel de señal posterior al fader suavizado en tiempo real. La línea vertical del pulgar marca la posición de ganancia actual. Arrastrar el pulgar emite la nueva ganancia y la persiste inmediatamente.

El indicador de asignación de slice a la izquierda de cada deslizador (que muestra **—** o **Slice A**–**Slice H**) es de solo lectura y refleja qué slice está enrutado actualmente a ese canal de DAX.

## Consejos

- El relleno del medidor de nivel refleja el nivel de salida posterior al fader, es decir, el audio entrante multiplicado por la ganancia actual. Mover el deslizador proporciona retroalimentación visual inmediata sobre la salida efectiva.
- Los valores de ganancia se almacenan como flotantes con dos decimales (por ejemplo, `0.75`). Se restauran desde `DaxRxGain1`–`DaxRxGain4` cada vez que AetherSDR se inicia.
- Si un canal muestra **—** en el indicador de asignación de slice, no hay ningún slice enrutado a él y el medidor no mostrará actividad independientemente del ajuste de ganancia.

## Solución de problemas

- **El medidor no muestra actividad aunque la ganancia esté ajustada por encima de 0.0** — Verifique el indicador de asignación de slice para esa fila. Si muestra **—**, no hay ningún slice asignado a ese canal de DAX. Asigne un slice al canal en la configuración de su radio, luego verifique que el botón **Enable** esté activo.
- **La ganancia se restablece a 0.5 después de reiniciar** — El ajuste no se guardó. Confirme que el arrastre se completó antes de cerrar AetherSDR. El guardado ocurre al soltar el deslizador.

## Relacionados

- [DAX Audio overview](overview.md)
- [Enable DAX to route slice audio to WSJT-X / FLDigi / other digital software](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Set DAX TX gain](set-dax-tx-gain.md)
- [See which slice is currently using each DAX channel](see-which-slice-is-currently-using-each-dax-channel.md)
- [Autostart DAX on launch](autostart-dax-on-launch.md)
