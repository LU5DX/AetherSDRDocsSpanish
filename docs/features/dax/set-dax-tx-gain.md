# Configurar la ganancia TX de DAX

Ajuste el control deslizante de ganancia TX de DAX para controlar cuánto audio de su slice de transmisión se envía a través del flujo DAX TX al software conectado.

## Antes de comenzar

- El radio debe estar conectado. El applet DAX Audio requiere una conexión activa con el radio.
- DAX debe estar habilitado. Haga clic en `Enable` en el applet DAX Audio si no está activo todavía.

## Pasos

1. Haga clic en el botón de bandeja `DAX` en la barra lateral derecha para abrir el applet DAX Audio.
2. Localice la fila `TX:` en la parte inferior del applet. El control deslizante a la derecha del indicador de estado TX es el control de ganancia TX.
3. Arrastre el control del slider `TX gain+meter` hacia la izquierda o la derecha para disminuir o aumentar la ganancia TX. El valor se guarda inmediatamente y persiste como `DaxTxGain`.

## Qué hace cada control

| Control | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|
| Slider `TX gain+meter` | 0.5 | 0.0 – 1.0 | `DaxTxGain` |
| Indicador de estado TX | — | — o Slice A–H | *(ninguna)* |

El indicador de estado TX muestra qué slice tiene actualmente los privilegios de TX. Se actualiza automáticamente conforme cambia el slice de TX. La barra de nivel detrás del slider muestra el nivel de audio TX en vivo, escalado según la configuración de ganancia actual.

## Consejos

- La barra de nivel refleja el nivel post-fader: muestra el nivel de salida real después de aplicar su configuración de ganancia. Mover el slider proporciona retroalimentación visual inmediata incluso antes de transmitir.
- Una ganancia de 0.5 es el punto de partida predeterminado. Si su software de modos digitales reporta audio sobremodulado o demasiado débil, ajuste desde ese valor en incrementos pequeños.

## Relacionado

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Configurar la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Identificar cuál slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
