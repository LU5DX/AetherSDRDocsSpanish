# Ajustar la ganancia RX de DAX por canal

Use el applet DAX Audio para ajustar la ganancia de recepción de cada uno de los cuatro canales DAX de forma independiente. La ganancia de cada canal se guarda y se restaura entre sesiones.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles DAX no están disponibles sin una conexión activa al radio.
- El puente de audio DAX debe estar en ejecución. Haga clic en Enable en el applet DAX Audio para iniciarlo si aún no lo ha hecho.

## Pasos

1. Haga clic en el botón DAX de la barra lateral derecha para abrir el applet DAX Audio. Si el panel del applet no está visible, actívelo primero con `View > Applet Panel`.
2. Localice la fila del canal que desea ajustar: **DAX 1**, **DAX 2**, **DAX 3** o **DAX 4**.
3. Arrastre el medidor/deslizador combinado de ese canal hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El rango de ganancia es de 0.0 a 1.0; el valor predeterminado es 0.5.
4. Suelte el arrastre. El nuevo valor se guarda inmediatamente en la clave de configuración correspondiente (`DaxRxGain1`, `DaxRxGain2`, `DaxRxGain3` o `DaxRxGain4`) y entra en vigor de inmediato.

Repita el procedimiento para cualquier otro canal que desee ajustar.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Ganancia+medidor DAX 1 | 0.5 | 0.0–1.0 | `DaxRxGain1` | Establece la ganancia RX para el canal DAX 1. La barra del medidor muestra el nivel de salida post-fader. |
| Ganancia+medidor DAX 2 | 0.5 | 0.0–1.0 | `DaxRxGain2` | Establece la ganancia RX para el canal DAX 2. |
| Ganancia+medidor DAX 3 | 0.5 | 0.0–1.0 | `DaxRxGain3` | Establece la ganancia RX para el canal DAX 3. |
| Ganancia+medidor DAX 4 | 0.5 | 0.0–1.0 | `DaxRxGain4` | Establece la ganancia RX para el canal DAX 4. |
| Estado de asignación de slice | — | — o Slice A–H | — (no persistente) | Muestra qué slice está enrutado a cada canal DAX. Solo lectura. |
| Enable | desactivado | activado/desactivado | `AutoStartDAX` | Interruptor principal del puente de audio DAX. Todos los deslizadores de ganancia están inactivos cuando está desactivado. |

## Consejos

- El fondo del medidor muestra el nivel RMS suavizado multiplicado por la ganancia actual, por lo que la barra refleja el nivel de salida real. Mover el deslizador proporciona retroalimentación visual inmediata incluso antes de que llegue el audio.
- Los valores de ganancia se almacenan con dos decimales (por ejemplo, `0.50`). Se restauran desde el disco cuando AetherSDR se inicia nuevamente, por lo que no es necesario volver a configurarlos después de reiniciar.
- El indicador de estado junto a la etiqueta de cada canal muestra qué slice está asignado a ese canal DAX. Si el indicador muestra —, no hay ningún slice enrutado actualmente. Consulte [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md).

## Solución de problemas

- **Arrastrar el deslizador no tiene efecto en el nivel de audio** — Verifique que Enable esté activo (iluminado en verde). El cambio de ganancia es aplicado por el puente DAX; si el puente no está en ejecución, la configuración se guarda pero no se aplica al flujo de audio.
- **La barra del medidor no muestra actividad** — El indicador de estado junto al canal puede mostrar —, lo que significa que no hay ningún slice asignado a ese canal DAX. Asigne un slice al canal en la configuración de slices de su radio.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Inicio automático de DAX al lanzar](autostart-dax-on-launch.md)
