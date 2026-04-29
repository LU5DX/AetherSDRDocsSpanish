# Configurar la ganancia de TX en DAX

Ajuste el control deslizante de ganancia de TX en DAX para controlar cuánto audio de su slice de transmisión se envía a través del flujo DAX TX al software conectado.

## Antes de comenzar

- El radio debe estar conectado. El applet DAX Audio requiere una conexión activa con el radio.
- DAX debe estar habilitado. Haga clic en `Enable` en el applet DAX Audio si aún no está activo.

## Pasos

1. Haga clic en el botón `DAX` del panel lateral derecho para abrir el applet DAX Audio.
2. Localice la fila `TX:` en la parte inferior del applet. El control deslizante a la derecha del indicador de estado TX es el control de ganancia de TX.
3. Arrastre el cursor del control deslizante `TX gain+meter` hacia la izquierda o la derecha para disminuir o aumentar la ganancia de TX. El valor se guarda de inmediato y se conserva como `DaxTxGain`.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave guardada |
|---|---|---|---|
| Control deslizante `TX gain+meter` | 0.5 | 0.0 – 1.0 | `DaxTxGain` |
| Indicador de estado TX | — | — o Slice A–H | *(ninguna)* |

El indicador de estado TX muestra qué slice tiene actualmente los privilegios de TX. Se actualiza automáticamente cuando cambia el slice de TX. La barra del medidor detrás del control deslizante muestra el nivel de audio TX en tiempo real, escalado según la configuración de ganancia actual.

## Consejos

- La barra del medidor refleja el nivel posterior al fader: muestra el nivel de salida real después de aplicar su configuración de ganancia. Mover el control deslizante proporciona retroalimentación visual inmediata incluso antes de transmitir.
- Una ganancia de 0.5 es el punto de partida predeterminado. Si el software de modos digitales reporta audio saturado o débil, ajuste desde ese valor en incrementos pequeños.

## Relacionado

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Configurar la ganancia de RX en DAX por canal](set-dax-rx-gain-per-channel.md)
- [Identificar cuál slice es el slice de TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
