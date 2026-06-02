# Seleccione la tasa de muestreo IQ (24k/48k/96k/192k)

Seleccione la tasa de muestreo para cada canal IQ de DAX según los requisitos de su software SDR externo. Las tasas más altas proporcionan más ancho de banda; las tasas más bajas reducen la carga de la CPU y la red.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El applet DAX IQ debe estar visible. Si no lo está, haga clic en el botón **IQ** de la barra lateral derecha para mostrarlo.

## Pasos

1. Localice la fila correspondiente al canal que desea configurar: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
2. Haga clic en el cuadro combinado de tasa en esa fila. Muestra la tasa actual (por defecto **48k**).
3. Seleccione una de las cuatro opciones: **24k**, **48k**, **96k** o **192k**.

AetherSDR envía inmediatamente la nueva tasa a la radio y guarda su selección. El ajuste persiste tras los reinicios como `DaxIqRate1` hasta `DaxIqRate4`.

Si el flujo ya está activo, el cuadro combinado se sincronizará con la tasa informada por la radio cada vez que la radio confirme el estado del flujo.

## Qué hace cada control

| Control | Valor por defecto | Valores válidos | Clave de ajuste persistente |
|---|---|---|---|
| Cuadro combinado de tasa (por canal) | 48k | 24k (24000 Hz), 48k (48000 Hz), 96k (96000 Hz), 192k (192000 Hz) | `DaxIqRate1` … `DaxIqRate4` |
| Interruptor de encendido/apagado (por canal) | Off | Off, On | `DaxIqEnabled1` … `DaxIqEnabled4` |
| Medidor de nivel (por canal) | 0 | 0–100 (escalado desde RMS × 200) | — |

## Consejos

- Puede cambiar la tasa tanto si el flujo está apagado como encendido. Si el flujo ya está habilitado, la radio aplica la nueva tasa al flujo activo.
- Al reconectar, el cuadro combinado se restablece brevemente antes de que la radio informe del estado confirmado del flujo. La tasa mostrada se sincronizará automáticamente una vez que se restablezca el flujo.
- Los eventos de la rueda del ratón en el cuadro combinado se suprimen cuando el bloqueo de desplazamiento del panel del applet está activo. Si el cuadro combinado no responde a la rueda del ratón, desplace el panel a la posición deseada y luego haga clic directamente en el cuadro.
- El medidor de nivel ahora utiliza el color de acento y la paleta de fondo del tema actual en lugar de colores fijos.

## Solución de problemas

- **El cuadro combinado de tasa muestra un valor diferente al que seleccionó**: la radio ha informado una tasa diferente para el flujo activo, y el cuadro se ha sincronizado para coincidir. Esto es normal. Deshabilite el flujo, cambie la tasa y luego vuelva a habilitarlo.
- **El cuadro combinado de tasa no responde a la rueda del ratón**: el bloqueo de desplazamiento del panel del applet está activo. Haga clic en el cuadro combinado para abrir la lista desplegable en su lugar.
- **Los colores del medidor de nivel se ven diferentes a lo esperado**: el medidor sigue el tema activo. Cambie el tema en **Settings > Appearance > Theme** para ajustar los colores del medidor.

## Relacionados

- [DAX IQ overview](overview.md)
- [Enable an IQ stream for external SDR software](enable-an-iq-stream-for-external-sdr-software.md)
- [Disable an IQ stream to free bandwidth](disable-an-iq-stream-to-free-bandwidth.md)
- [Monitor the RMS level of each IQ stream](monitor-the-rms-level-of-each-iq-stream.md)
