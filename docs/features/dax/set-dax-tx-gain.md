# Configurar la ganancia de TX de DAX

Ajuste el control deslizante de ganancia de TX de DAX para controlar cuánto audio de su slice de transmisión se envía a través del flujo de TX de DAX al software conectado.

## Antes de comenzar

- La radio debe estar conectada. El applet DAX Audio requiere una conexión de radio activa.
- DAX debe estar habilitado. Haga clic en `Enable` en el applet DAX Audio si aún no está activo.

## Pasos

1. Haga clic en el botón de la bandeja `DAX` en la barra lateral derecha para abrir el applet DAX Audio.
2. Localice la fila `TX:` en la parte inferior del applet. El control deslizante a la derecha del indicador de estado de TX es el control de ganancia de TX.
3. Arrastre el control del deslizante `TX gain+meter` hacia la izquierda o derecha para disminuir o aumentar la ganancia de TX. El valor se guarda inmediatamente y persiste como `DaxTxGain`.

## Función de cada control

| Control | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|
| Deslizante `TX gain+meter` | 0.5 | 0.0 – 1.0 | `DaxTxGain` |
| Indicador de estado TX | — | — o Slice A–H | *(ninguna)* |

El indicador de estado TX muestra qué slice posee actualmente los privilegios de TX. Se actualiza automáticamente a medida que cambia el slice de TX. La barra de medidor detrás del deslizante muestra el nivel de audio de TX en vivo escalado por la configuración de ganancia actual.

## Consejos

- La barra del medidor refleja el nivel posterior al fader: muestra el nivel de salida real después de aplicar su configuración de ganancia. Mover el deslizante proporciona retroalimentación visual inmediata incluso antes de transmitir.
- Una ganancia de 0.5 es el punto de partida predeterminado. Si su software de modo digital reporta audio sobremodulado o débil, ajuste desde allí en pequeños incrementos.

## Relacionados

- [DAX Audio overview](overview.md)
- [Enable DAX to route slice audio to WSJT-X / FLDigi / other digital software](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Set DAX RX gain per channel](set-dax-rx-gain-per-channel.md)
- [Identify which slice is the TX slice](identify-which-slice-is-the-tx-slice.md)
- [Setting up digital modes (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
