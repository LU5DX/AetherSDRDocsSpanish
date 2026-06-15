# Applet de Audio DAX (v26.6.3)

El applet de Audio DAX proporciona un puente de audio RX por canal y un flujo de audio TX único para operación en modos digitales. Muestra medidores de audio en vivo y controles deslizantes de ganancia para los canales DAX 1–4 y el flujo TX, junto con indicadores de asignación de slices.

## Habilitar Audio DAX

1. Haga clic en el botón `DAX` de la bandeja en la barra lateral derecha para abrir el applet de Audio DAX.
2. Haga clic en `Enable` para iniciar el puente de audio DAX. La configuración persiste como `AutoStartDAX`.
3. Una vez habilitado, todos los flujos DAX RX y TX se activan.

## Ajustar la ganancia DAX RX por canal

Ajuste la ganancia para cada canal de recepción DAX (1–4) para controlar el nivel de audio enviado al software conectado.

### Pasos

1. En el applet de Audio DAX, localice la fila del canal deseado (`DAX 1` a `DAX 4`).
2. Arrastre el control deslizante del medidor/control combinado hacia la izquierda o derecha para disminuir o aumentar la ganancia RX.
3. El valor se guarda inmediatamente y persiste como `DaxRxGain1` a `DaxRxGain4`.

## Ajustar la ganancia DAX TX

Ajuste el control deslizante de ganancia DAX TX para controlar cuánto audio de su slice de transmisión se envía a través del flujo DAX TX al software conectado.

### Pasos

1. En el applet de Audio DAX, localice la fila `TX:` en la parte inferior.
2. Arrastre el control deslizante de `ganancia+medidor TX` hacia la izquierda o derecha para disminuir o aumentar la ganancia TX.
3. El valor se guarda inmediatamente y persiste como `DaxTxGain`.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave persistente |
|---|---|---|---|
| Botón `Enable` | apagado | encendido/apagado | `AutoStartDAX` |
| Control deslizante `DAX 1 ganancia+medidor` | 0.5 | 0.0 – 1.0 | `DaxRxGain1` |
| Control deslizante `DAX 2 ganancia+medidor` | 0.5 | 0.0 – 1.0 | `DaxRxGain2` |
| Control deslizante `DAX 3 ganancia+medidor` | 0.5 | 0.0 – 1.0 | `DaxRxGain3` |
| Control deslizante `DAX 4 ganancia+medidor` | 0.5 | 0.0 – 1.0 | `DaxRxGain4` |
| Control deslizante `TX ganancia+medidor` | 0.5 | 0.0 – 1.0 | `DaxTxGain` |

## Indicadores de asignación de slices

| Indicador | Estados | Significado |
|---|---|---|
| `Asignación DAX 1..4` | — o Slice A–H | El slice actualmente asignado a este canal DAX |
| `Asignación TX` | — o Slice A–H | El slice que actualmente tiene privilegios de TX (controla DAX TX) |

Las letras de slice en los indicadores de asignación ahora se renderizan en formato de texto enriquecido, proporcionando una claridad visual mejorada cuando las etiquetas de slice contienen entidades HTML (problema #2606).

## Accesibilidad

Cada control deslizante de ganancia DAX RX y el control deslizante de ganancia TX ahora tienen un nombre accesible. Los lectores de pantalla anuncian `DAX RX 1 gain` a `DAX RX 4 gain` para los controles deslizantes de canal de recepción, y `DAX TX gain` para el control deslizante de ganancia de transmisión.

## Consejos

- Las barras del medidor reflejan el nivel posterior al fader: muestran el nivel de salida real después de aplicar su configuración de ganancia. Mover un control deslizante proporciona retroalimentación visual inmediata incluso antes de transmitir.
- Una ganancia de 0.5 es el punto de partida predeterminado. Si su software de modo digital reporta audio sobreamplificado o débil, ajuste desde allí en pequeños incrementos.
- En Linux, la latencia de DAX RX se ha reducido de aproximadamente 400 ms a aproximadamente 200 ms utilizando una ruta de origen `pw_stream` nativa de PipeWire, reemplazando el cliente PulseAudio anterior.

## Relacionados

- [Descripción general de Audio DAX](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identificar qué slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
