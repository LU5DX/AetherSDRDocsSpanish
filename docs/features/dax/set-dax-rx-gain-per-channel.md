# Ajustar la ganancia RX de DAX por canal

Ajuste el nivel de audio de recepción para cada uno de los cuatro canales DAX (DAX 1–4), de modo que el software de modos digitales u otras aplicaciones que consumen audio reciban la señal al nivel correcto.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- El applet de DAX debe estar abierto. Si no está visible, haga clic en el botón DAX del panel lateral derecho para mostrarlo.
- DAX debe estar habilitado. Si el botón Enable no está encendido, haga clic en Enable para iniciar el puente de audio DAX.

## Pasos

1. Haga clic en el botón DAX del panel lateral derecho para abrir el applet DAX Audio.
2. Localice la fila del canal que desea ajustar: DAX 1, DAX 2, DAX 3 o DAX 4.
3. Arrastre el medidor/deslizador de esa fila hacia la izquierda o la derecha para disminuir o aumentar la ganancia RX.
4. Suelte el botón del mouse. La nueva ganancia se guarda de inmediato.

Repita el procedimiento para cualquier otro canal que requiera ajuste.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistido |
|---|---|---|---|
| Ganancia+medidor DAX 1 | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| Ganancia+medidor DAX 2 | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| Ganancia+medidor DAX 3 | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| Ganancia+medidor DAX 4 | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| Estado de asignación de slice | — | — o Slice A–H | _(no persistido)_ |

Cada medidor/deslizador es un control combinado. La barra de fondo muestra el nivel de audio RMS suavizado posterior al fader; el cursor arrastrables establece la ganancia. Al mover el cursor, el nivel mostrado se actualiza de inmediato. Los valores de ganancia se almacenan con dos decimales (por ejemplo, `0.50`).

El indicador de asignación de slice a la izquierda de cada medidor muestra qué slice está enrutado actualmente a ese canal (por ejemplo, Slice A). Un guion (—) indica que no hay ningún slice asignado.

## Consejos

- La ganancia se aplica después del fader: la barra del medidor refleja el nivel de salida real tras el ajuste de ganancia, no el nivel de entrada sin procesar. Úsela para confirmar que la señal que llega a su software de modos digitales no está recortada ni es demasiado baja.
- Los ajustes de ganancia persisten entre reinicios. No es necesario reajustarlos en cada sesión.
- Si un canal muestra — en el indicador de asignación de slice, no pasará audio sin importar el valor de ganancia. Primero asigne un slice a ese canal DAX.

## Solución de problemas

- **Arrastrar el deslizador no tiene efecto** — Verifique que Enable esté activo (encendido en verde). Los cambios de ganancia se aceptan en cualquier momento, pero no fluye audio a menos que el puente DAX esté en ejecución.
- **La barra del medidor no muestra movimiento tras ajustar la ganancia** — Compruebe que haya un slice asignado al canal (el indicador debe mostrar Slice A–H, no —). Si el indicador muestra —, asigne un slice al canal DAX desde los controles de slice de la radio.
- **La ganancia vuelve a 0.5 después de reiniciar** — Esto puede ocurrir si AetherSDR no puede escribir su archivo de configuración. Verifique los permisos del sistema de archivos en el directorio de configuración de AetherSDR.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software de modos digitales](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Iniciar DAX automáticamente al arrancar](autostart-dax-on-launch.md)
