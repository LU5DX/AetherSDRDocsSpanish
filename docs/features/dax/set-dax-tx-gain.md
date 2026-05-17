# Applet de Audio DAX (v26.5.2.1)

El applet de Audio DAX proporciona un puente de audio RX por canal y un flujo de audio TX único para operación en modos digitales. Muestra medidores de audio en vivo y controles deslizantes de ganancia para los canales DAX 1–4 y el flujo TX, junto con indicadores de asignación de slice.

## Habilitación del Audio DAX

1. Haga clic en el botón de bandeja `DAX` en la barra lateral derecha para abrir el applet de Audio DAX.
2. Haga clic en `Enable` para iniciar el puente de audio DAX. La configuración persiste como `AutoStartDAX`.
3. Una vez habilitado, todos los flujos DAX RX y TX se activan.

## Ajuste de ganancia RX DAX por canal

Ajuste la ganancia para cada canal de recepción DAX (1–4) para controlar el nivel de audio enviado al software conectado.

### Pasos

1. En el applet de Audio DAX, localice la fila del canal deseado (`DAX 1` hasta `DAX 4`).
2. Arrastre el control deslizante combinado de medidor/ganancia hacia la izquierda o derecha para disminuir o aumentar la ganancia RX.
3. El valor se guarda inmediatamente y persiste como `DaxRxGain1` hasta `DaxRxGain4`.

## Ajuste de ganancia TX DAX

Ajuste el control deslizante de ganancia TX DAX para controlar cuánto audio de su slice de transmisión se envía a través del flujo DAX TX al software conectado.

### Pasos

1. En el applet de Audio DAX, localice la fila `TX:` en la parte inferior.
2. Arrastre el control deslizante `TX gain+meter` hacia la izquierda o derecha para disminuir o aumentar la ganancia TX.
3. El valor se guarda inmediatamente y persiste como `DaxTxGain`.

## Función de cada control

| Control | Predeterminado | Rango | Clave persistida |
|---|---|---|---|
| Botón `Enable` | desactivado | activado/desactivado | `AutoStartDAX` |
| Control deslizante `DAX 1 gain+meter` | 0.5 | 0.0 – 1.0 | `DaxRxGain1` |
| Control deslizante `DAX 2 gain+meter` | 0.5 | 0.0 – 1.0 | `DaxRxGain2` |
| Control deslizante `DAX 3 gain+meter` | 0.5 | 0.0 – 1.0 | `DaxRxGain3` |
| Control deslizante `DAX 4 gain+meter` | 0.5 | 0.0 – 1.0 | `DaxRxGain4` |
| Control deslizante `TX gain+meter` | 0.5 | 0.0 – 1.0 | `DaxTxGain` |

## Indicadores de asignación de slice

| Indicador | Estados | Significado |
|---|---|---|
| `DAX 1..4 assignment` | — o Slice A–H | El slice actualmente asignado a este canal DAX |
| `TX assignment` | — o Slice A–H | El slice que actualmente tiene privilegios TX (impulsa DAX TX) |

Las letras de slice en los indicadores de asignación ahora se muestran en formato de texto enriquecido, lo que proporciona una claridad visual mejorada cuando las etiquetas de slice contienen entidades HTML (problema #2606).

## Consejos

- Las barras del medidor reflejan el nivel posterior al fader: muestran el nivel de salida real después de aplicar su ajuste de ganancia. Mover un control deslizante proporciona retroalimentación visual inmediata incluso antes de transmitir.
- Una ganancia de 0.5 es el punto de partida predeterminado. Si su software de modo digital reporta audio sobremodulado o débil, ajuste desde allí en incrementos pequeños.
- En Linux, la latencia RX de DAX se ha reducido de aproximadamente 400 ms a aproximadamente 200 ms utilizando una ruta de fuente `pw_stream` nativa de PipeWire, reemplazando el cliente PulseAudio anterior.

## Relacionado

- [Descripción general de Audio DAX](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identificar qué slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
