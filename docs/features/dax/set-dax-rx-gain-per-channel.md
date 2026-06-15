# Ajustar la ganancia de RX de DAX por canal

Cada canal de RX de DAX (1–4) tiene un control de ganancia independiente en el applet de Audio DAX. Ajustarlos le permite igualar el nivel de audio entregado al software de modo digital u otras aplicaciones que reciben audio de DAX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El applet de Audio DAX debe estar abierto. Si no está visible, haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para mostrarlo.
- DAX debe estar habilitado. Si el botón **Enable** no está iluminado, haga clic en **Enable** en el applet de Audio DAX antes de ajustar la ganancia.

## Pasos

1. Haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para abrir el applet de Audio DAX.
2. Localice la fila del canal que desea ajustar: **DAX 1:**, **DAX 2:**, **DAX 3:** o **DAX 4:**.
3. Arrastre el medidor/deslizador combinado de ese canal hacia la izquierda o la derecha para disminuir o aumentar la ganancia de RX.
4. Suelte el arrastre. El nuevo valor se guarda de inmediato.

Repita el proceso para cualquier otro canal que necesite ajuste.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de persistencia |
|---|---|---|---|
| Ganancia+medidor DAX 1 | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| Ganancia+medidor DAX 2 | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| Ganancia+medidor DAX 3 | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| Ganancia+medidor DAX 4 | 0.5 | 0.0–1.0 | `DaxRxGain4` |

Cada control es un medidor de nivel combinado con un deslizador de ganancia. La barra de fondo muestra el nivel de señal post-fader suavizado en tiempo real. La línea vertical del pulgar marca la posición de ganancia actual. Arrastrar el pulgar emite la nueva ganancia y la persiste de inmediato.

Cada deslizador tiene un nombre de accesibilidad establecido como "DAX RX 1 gain", "DAX RX 2 gain", "DAX RX 3 gain" o "DAX RX 4 gain" respectivamente para compatibilidad con lectores de pantalla.

El indicador de asignación de slice a la izquierda de cada deslizador (que muestra **—** o **Slice A**–**Slice H**) es de solo lectura y refleja qué slice está enrutado actualmente a ese canal de DAX.

## Consejos

- El relleno del medidor de nivel refleja el nivel de salida post-fader — es decir, el audio entrante multiplicado por la ganancia actual. Mover el deslizador proporciona retroalimentación visual inmediata sobre la salida efectiva.
- Los valores de ganancia se almacenan como flotantes con dos decimales (por ejemplo, `0.75`). Se restauran desde `DaxRxGain1`–`DaxRxGain4` cada vez que se inicia AetherSDR.
- Si un canal muestra **—** en el indicador de asignación de slice, ningún slice está enrutado a él y el medidor no mostrará actividad independientemente del ajuste de ganancia.
- En Linux, el puente de audio de DAX utiliza una ruta de fuente de flujo PipeWire nativa, lo que reduce la latencia de RX de aproximadamente 400 ms a aproximadamente 200 ms en comparación con el cliente PulseAudio anterior.

## Solución de problemas

- **El medidor no muestra actividad aunque la ganancia esté ajustada por encima de 0.0** — Verifique el indicador de asignación de slice para esa fila. Si muestra **—**, no se ha asignado ningún slice a ese canal de DAX. Asigne un slice al canal en la configuración de su radio, luego verifique que el botón **Enable** esté activo.
- **La ganancia se restablece a 0.5 después de reiniciar** — La configuración no se guardó. Confirme que el arrastre se completó antes de cerrar AetherSDR. El guardado ocurre al soltar el deslizador.

## Temas relacionados

- [Resumen de Audio DAX](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia de TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal de DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Iniciar DAX automáticamente al lanzar](autostart-dax-on-launch.md)
