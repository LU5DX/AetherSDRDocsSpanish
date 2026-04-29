# Seleccionar la frecuencia de muestreo IQ (24k/48k/96k/192k)

Seleccione la frecuencia de muestreo para cada canal DAX IQ según los requisitos de su software SDR externo. Las frecuencias más altas ofrecen mayor ancho de banda; las más bajas reducen la carga de CPU y de red.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El applet DAX IQ debe estar visible. Si no lo está, haga clic en el botón **IQ** de la bandeja en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice la fila del canal que desea configurar: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
2. Haga clic en el cuadro combinado de frecuencia de muestreo en esa fila. Muestra la frecuencia actual (predeterminada: **48k**).
3. Seleccione una de las cuatro opciones: **24k**, **48k**, **96k** o **192k**.

AetherSDR envía inmediatamente la nueva frecuencia de muestreo a la radio y guarda su elección. La configuración persiste entre reinicios como `DaxIqRate1` hasta `DaxIqRate4`.

Si el flujo ya está activo, el cuadro combinado se sincronizará con la frecuencia reportada por la radio cada vez que esta confirme el estado del flujo.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave de configuración persistida |
|---|---|---|---|
| Cuadro combinado de frecuencia de muestreo (por canal) | 48k | 24k (24000 Hz), 48k (48000 Hz), 96k (96000 Hz), 192k (192000 Hz) | `DaxIqRate1` … `DaxIqRate4` |
| Interruptor On/Off (por canal) | Off | Off, On | `DaxIqEnabled1` … `DaxIqEnabled4` |
| Medidor de nivel (por canal) | 0 | 0–100 (escalado desde RMS × 200) | — |

## Consejos

- Puede cambiar la frecuencia de muestreo tanto si el flujo está desactivado como activado. Si el flujo ya está habilitado, la radio aplica la nueva frecuencia al flujo activo.
- Al reconectarse, el cuadro combinado se restablece brevemente antes de que la radio reporte el estado confirmado del flujo. La frecuencia mostrada se sincronizará automáticamente una vez que el flujo se restablezca.
- Los eventos de rueda de desplazamiento en el cuadro combinado se suprimen cuando el bloqueo de desplazamiento del panel del applet está activo. Si el cuadro combinado no responde a la rueda de desplazamiento, desplace el panel hasta la posición deseada y luego haga clic directamente en el cuadro combinado.

## Solución de problemas

- **El cuadro combinado muestra un valor diferente al seleccionado** — La radio ha reportado una frecuencia de muestreo diferente para el flujo activo y el cuadro combinado se ha sincronizado para coincidir. Esto es normal. Deshabilite el flujo, cambie la frecuencia de muestreo y vuelva a habilitarlo.
- **El cuadro combinado no responde a la rueda de desplazamiento** — El bloqueo de desplazamiento del panel del applet está activo. Haga clic en el cuadro combinado para abrir la lista desplegable.

## Relacionados

- [Descripción general de DAX IQ](overview.md)
- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
