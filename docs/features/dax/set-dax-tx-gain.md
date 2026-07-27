# Applet de Audio DAX (v26.7.4)

El applet de Audio DAX proporciona un puente de audio RX por canal y un flujo de audio TX único para la operación en modos digitales. Muestra medidores de audio en vivo y controles deslizantes de ganancia para los canales DAX 1–4 y el flujo TX, junto con indicadores de asignación de slice.

> **Nota para Windows:** AetherSDR no incluye un controlador de audio DAX integrado en Windows. En Windows, el applet muestra solo una nota informativa; todos los controles están desactivados. Use los controladores DAX de TCI o SmartSDR de FlexRadio. Consulte Ayuda → Configuración de modos de datos para instrucciones de configuración.

## Habilitar el Audio DAX

1. Haga clic en el botón `DAX` en la barra lateral derecha para abrir el applet de Audio DAX.
2. Haga clic en `Enable` para iniciar el puente de audio DAX. La configuración se guarda como `AutoStartDAX`.
3. Una vez habilitado, todos los flujos DAX RX y TX se activan.
4. La etiqueta del botón cambia a `Enabled` cuando el puente está activo y `Disabled` cuando está inactivo.

## Ajustar la ganancia RX de DAX por canal

Ajuste la ganancia de cada canal de recepción DAX (1–4) para controlar el nivel de audio enviado al software conectado.

### Pasos

1. En el applet de Audio DAX, localice la fila del canal deseado (`DAX 1` a `DAX 4`).
2. Arrastre el control deslizante del medidor combinado hacia la izquierda o derecha para disminuir o aumentar la ganancia RX.
3. El valor se guarda inmediatamente y persiste como `DaxRxGain1` a `DaxRxGain4`.

## Ajustar la ganancia TX de DAX

Ajuste el control deslizante de ganancia TX de DAX para controlar cuánto audio de su slice de transmisión se envía a través del flujo TX de DAX al software conectado.

### Pasos

1. En el applet de Audio DAX, localice la fila `TX:` en la parte inferior.
2. Arrastre el control deslizante combinado de `Ganancia TX+medidor` hacia la izquierda o derecha para disminuir o aumentar la ganancia TX.
3. El valor se guarda inmediatamente y persiste como `DaxTxGain`.

## Qué hace cada control

| Control | Valor por defecto | Rango | Clave persistida |
|---|---|---|---|
| Botón `Enable` | off | on/off | `AutoStartDAX` |
| Control deslizante `Ganancia+medidor DAX 1` | 0.5 | 0.0 – 1.0 | `DaxRxGain1` |
| Control deslizante `Ganancia+medidor DAX 2` | 0.5 | 0.0 – 1.0 | `DaxRxGain2` |
| Control deslizante `Ganancia+medidor DAX 3` | 0.5 | 0.0 – 1.0 | `DaxRxGain3` |
| Control deslizante `Ganancia+medidor DAX 4` | 0.5 | 0.0 – 1.0 | `DaxRxGain4` |
| Control deslizante `Ganancia+medidor TX` | 0.5 | 0.0 – 1.0 | `DaxTxGain` |

## Indicadores de asignación de slice

| Indicador | Estados | Significado |
|---|---|---|
| `Asignación DAX 1..4` | — o Slice A–H | El slice actualmente asignado a este canal DAX |
| `Asignación TX` | — o Slice A–H | El slice que actualmente tiene privilegios TX (conduce el DAX TX) |

Las letras de slice en los indicadores de asignación se muestran en formato de texto enriquecido, lo que proporciona una claridad visual mejorada cuando las etiquetas de slice contienen entidades HTML (problema #2606).

## Accesibilidad

Cada control deslizante de ganancia RX de DAX y el control deslizante de ganancia TX tienen un nombre accesible. Los lectores de pantalla anuncian `Ganancia DAX RX 1` a `Ganancia DAX RX 4` para los controles deslizantes de los canales de recepción, y `Ganancia DAX TX` para el control deslizante de ganancia de transmisión. El botón Habilitar DAX tiene un nombre accesible de `Habilitar DAX` y una descripción accesible de `Habilitar o deshabilitar el enrutamiento de audio digital DAX`.

## Consejos

- Las barras del medidor reflejan el nivel posterior al fader: muestran el nivel de salida real después de aplicar su configuración de ganancia. Mover un control deslizante proporciona retroalimentación visual inmediata incluso antes de transmitir.
- Una ganancia de 0.5 es el punto de partida predeterminado. Si su software de modo digital reporta audio saturado o débil, ajuste desde allí en pequeños incrementos.
- En Linux, la latencia RX de DAX se ha reducido de aproximadamente 400 ms a aproximadamente 200 ms utilizando una ruta de origen nativa `pw_stream` de PipeWire, reemplazando el cliente PulseAudio anterior.

## Relacionados

- [Descripción general de Audio DAX](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identificar qué slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
