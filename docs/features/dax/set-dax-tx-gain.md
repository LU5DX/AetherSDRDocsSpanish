# Applet de Audio DAX (v26.8.4)

El applet de Audio DAX proporciona un puente de audio RX por canal y un único flujo de audio TX para la operación en modos digitales. Muestra medidores de audio en vivo y controles deslizantes de ganancia para los canales DAX 1–8 y el flujo TX, junto con indicadores de asignación de slices.

> **Nota para Windows:** AetherSDR no incluye un controlador de audio DAX integrado en Windows. En Windows, el applet muestra solo una nota informativa; todos los controles están inactivos. Use los controladores TCI o los controladores SmartSDR DAX de FlexRadio en su lugar. Consulte Help → Configuring Data Modes para las instrucciones de configuración.

## Habilitar Audio DAX

1. Haga clic en el botón de bandeja `DAX` en la barra lateral derecha para abrir el applet de Audio DAX.
2. Haga clic en `Enable` para iniciar el puente de audio DAX. La configuración se guarda como `AutoStartDAX`.
3. Una vez habilitado, todos los flujos RX y TX de DAX se activan.
4. La etiqueta del botón cambia a `Enabled` cuando el puente está activo y a `Disabled` cuando está inactivo.

## Ajustar la ganancia RX de DAX por canal

Ajuste la ganancia de cada canal de recepción DAX (1–8) para controlar el nivel de audio enviado al software conectado. Las filas de los canales que superan la capacidad de slices de su radio se ocultan automáticamente.

### Pasos

1. En el applet de Audio DAX, localice la fila del canal deseado (`DAX 1` a `DAX 8`).
2. Arrastre el control del medidor/deslizador combinado hacia la izquierda o la derecha para disminuir o aumentar la ganancia RX.
3. El valor se guarda inmediatamente y persiste como `DaxRxGain1` a `DaxRxGain8`.

## Ajustar la ganancia TX de DAX

Ajuste el control deslizante de ganancia TX de DAX para controlar cuánto audio de su slice de transmisión se envía a través del flujo TX de DAX al software conectado.

### Pasos

1. En el applet de Audio DAX, localice la fila `TX:` en la parte inferior.
2. Arrastre el control del deslizador `TX gain+meter` hacia la izquierda o la derecha para disminuir o aumentar la ganancia TX.
3. El valor se guarda inmediatamente y persiste como `DaxTxGain`.

## Función de cada control

| Control                   | Valor predeterminado | Rango |
|---------------------------|---------|-------|
| Botón `Enable`            | off     | on/off |
| Deslizador `DAX 1 gain+meter` | 0.5 | 0.0 – 1.0 |
| Deslizador `DAX 2 gain+meter` | 0.5 | 0.0 – 1.0 |
| Deslizador `DAX 3 gain+meter` | 0.5 | 0.0 – 1.0 |
| Deslizador `DAX 4 gain+meter` | 0.5 | 0.0 – 1.0 |
| Deslizador `DAX 5 gain+meter` | 0.5 | 0.0 – 1.0 |
| Deslizador `DAX 6 gain+meter` | 0.5 | 0.0 – 1.0 |
| Deslizador `DAX 7 gain+meter` | 0.5 | 0.0 – 1.0 |
| Deslizador `DAX 8 gain+meter` | 0.5 | 0.0 – 1.0 |
| Deslizador `TX gain+meter` | 0.5 | 0.0 – 1.0 |
| `DAX 5 gain+meter`        | Medidor/deslizador combinado; arrástrelo para ajustar la ganancia RX en el canal DAX 5. | Visible solo cuando la radio conectada admite al menos 5 slices. |
| `DAX 6 gain+meter`        | Medidor/deslizador combinado; arrástrelo para ajustar la ganancia RX en el canal DAX 6. | Visible solo cuando la radio conectada admite al menos 6 slices. |
| `DAX 7 gain+meter`        | Medidor/deslizador combinado; arrástrelo para ajustar la ganancia RX en el canal DAX 7. | Visible solo cuando la radio conectada admite al menos 7 slices. |
| `DAX 8 gain+meter`        | Medidor/deslizador combinado; arrástrelo para ajustar la ganancia RX en el canal DAX 8. | Visible solo en una radio con capacidad de 8 slices. |
| Nota de Windows           | En las compilaciones para Windows, el applet muestra solo la nota `No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX.` (#4112). | Windows no tiene puente DAX integrado (sin controlador de audio en modo kernel); todos los demás controles se omiten y sus ajustadores están protegidos contra valores nulos. |

Las filas de los canales DAX que superan la capacidad de slices de la radio conectada se ocultan automáticamente, por lo que una radio pequeña no muestra controles de ganancia inactivos. Por ejemplo, una radio de 2 slices (como la FLEX-6300) muestra solo DAX 1–2, mientras que una radio de 8 slices (FLEX-6700) muestra los ocho canales.

## Indicadores de asignación de slices

| Indicador | Estados | Significado |
|---|---|---|
| `DAX 1..8 assignment` | — o Slice A–H | El slice actualmente asignado a este canal DAX |
| `TX assignment` | — o Slice A–H | El slice que actualmente tiene privilegios de TX (impulsa DAX TX) |

Las letras de slice en los indicadores de asignación se muestran en formato de texto enriquecido, lo que proporciona una mayor claridad visual cuando las etiquetas de slice contienen entidades HTML (problema #2606).

## Accesibilidad

Cada control deslizante de ganancia RX de DAX y el control deslizante de ganancia TX tienen un nombre accesible. Los lectores de pantalla anuncian `DAX RX 1 gain` hasta `DAX RX 8 gain` para los controles de los canales de recepción, y `DAX TX gain` para el control de ganancia de transmisión. El botón de habilitar DAX tiene un nombre accesible de `DAX enable` y una descripción accesible de `Enable or disable DAX digital audio routing`.

## Consejos

- Las barras del medidor reflejan el nivel posterior al fader: muestran el nivel de salida real después de aplicar su configuración de ganancia. Mover un control deslizante proporciona retroalimentación visual inmediata incluso antes de transmitir.
- Los niveles del medidor RX se suavizan exponencialmente (ataque rápido, caída lenta) para proporcionar lecturas receptivas pero estables.
- Una ganancia de 0.5 es el punto de partida predeterminado. Si su software de modos digitales informa audio distorsionado o débil, ajuste desde allí en incrementos pequeños.
- En Linux, la latencia de RX de DAX se ha reducido de aproximadamente 400 ms a aproximadamente 200 ms utilizando una ruta nativa de origen `pw_stream` de PipeWire, reemplazando el cliente PulseAudio anterior.

## Relacionado

- [Descripción general de Audio DAX](overview.md)
- [Habilitar DAX para enrutar el audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identificar qué slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
