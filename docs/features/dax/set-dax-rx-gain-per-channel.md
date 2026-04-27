# Ajustar la ganancia de RX de DAX por canal

Cada canal DAX RX (1–4) tiene un control de ganancia independiente en el applet DAX Audio. Ajustar estos controles permite igualar el nivel de audio enviado a software de modos digitales u otras aplicaciones que reciben audio DAX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El applet DAX Audio debe estar abierto. Si no está visible, haga clic en el botón **DAX** de la barra lateral derecha para mostrarlo.
- DAX debe estar habilitado. Si el botón **Enable** no está iluminado, haga clic en **Enable** en el applet DAX Audio antes de ajustar la ganancia.

## Pasos

1. Haga clic en el botón **DAX** de la barra lateral derecha para abrir el applet DAX Audio.
2. Localice la fila del canal que desea ajustar: **DAX 1:**, **DAX 2:**, **DAX 3:**, o **DAX 4:**.
3. Arrastre el medidor/deslizador combinado de ese canal hacia la izquierda o la derecha para disminuir o aumentar la ganancia de RX.
4. Suelte el arrastre. El nuevo valor se guarda de inmediato.

Repita el procedimiento para cualquier otro canal que requiera ajuste.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Ganancia+medidor DAX 1 | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| Ganancia+medidor DAX 2 | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| Ganancia+medidor DAX 3 | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| Ganancia+medidor DAX 4 | 0.5 | 0.0–1.0 | `DaxRxGain4` |

Cada control es un medidor de nivel y deslizador de ganancia combinados. La barra de fondo muestra en tiempo real el nivel de señal suavizado posterior al fader. La línea vertical del cursor marca la posición actual de la ganancia. Al arrastrar el cursor se aplica la nueva ganancia y se guarda de inmediato.

El indicador de asignación de slice a la izquierda de cada deslizador (que muestra **—** o **Slice A**–**Slice H**) es de solo lectura e indica qué slice está enrutado actualmente hacia ese canal DAX.

## Sugerencias

- El relleno del medidor de nivel refleja el nivel de salida posterior al fader, es decir, el audio entrante multiplicado por la ganancia actual. Al mover el deslizador se obtiene retroalimentación visual inmediata sobre la salida efectiva.
- Los valores de ganancia se almacenan como números de punto flotante con dos decimales (por ejemplo, `0.75`). Se restauran desde `DaxRxGain1`–`DaxRxGain4` cada vez que AetherSDR inicia.
- Si un canal muestra **—** en el indicador de asignación de slice, ningún slice está enrutado hacia él y el medidor no mostrará actividad independientemente del valor de ganancia configurado.

## Resolución de problemas

- **El medidor no muestra actividad aunque la ganancia esté por encima de 0.0** — Verifique el indicador de asignación de slice de esa fila. Si muestra **—**, no hay ningún slice asignado a ese canal DAX. Asigne un slice al canal en la configuración de su radio y confirme que el botón **Enable** esté activo.
- **La ganancia vuelve a 0.5 después de reiniciar** — El ajuste no se guardó. Confirme que el arrastre se completó antes de cerrar AetherSDR. El guardado ocurre al soltar el deslizador.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia de TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando cada canal DAX actualmente](see-which-slice-is-currently-using-each-dax-channel.md)
- [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md)
