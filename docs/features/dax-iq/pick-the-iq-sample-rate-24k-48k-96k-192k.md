# Elegir la frecuencia de muestreo de IQ (24k/48k/96k/192k)

Seleccione la frecuencia de muestreo para cada canal IQ de DAX de acuerdo con los requisitos de su software SDR externo. Frecuencias más altas proporcionan más ancho de banda; frecuencias más bajas reducen la carga de CPU y de red.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El applet DAX IQ debe estar visible. Si no lo está, haga clic en el botón **IQ** de la bandeja en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice la fila correspondiente al canal que desea configurar: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
2. Haga clic en el cuadro combinado de frecuencia en esa fila. Muestra la frecuencia actual (por defecto **48k**).
3. Seleccione una de las cuatro opciones: **24k**, **48k**, **96k** o **192k**.

AetherSDR envía inmediatamente la nueva frecuencia al radio y guarda su selección. La configuración persiste tras los reinicios como `DaxIqRate1` hasta `DaxIqRate4`.

Si el flujo ya está activo, el cuadro combinado se sincronizará nuevamente con la frecuencia informada por el radio cuando este confirme el estado del flujo.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave de configuración persistida |
|---|---|---|---|
| Cuadro combinado de frecuencia (por canal) | 48k | 24k (24000 Hz), 48k (48000 Hz), 96k (96000 Hz), 192k (192000 Hz) | `DaxIqRate1` … `DaxIqRate4` |
| Activación/desactivación (por canal) | Off | Off, On | `DaxIqEnabled1` … `DaxIqEnabled4` |
| Medidor de nivel (por canal) | 0 | 0–100 (escalado desde RMS × 200) | — |

## Consejos

- Puede cambiar la frecuencia tanto si el flujo está desactivado como activado. Si el flujo ya está habilitado, el radio aplica la nueva frecuencia al flujo activo.
- Al reconectarse, el cuadro combinado se restablece brevemente antes de que el radio informe el estado confirmado del flujo. La frecuencia mostrada se sincronizará automáticamente una vez que el flujo se restablezca.
- Los eventos de la rueda del ratón en el cuadro combinado se suprimen cuando el bloqueo de desplazamiento del panel del applet está activo. Si el cuadro combinado no responde a la rueda del ratón, desplace el panel a la posición deseada y luego haga clic directamente en el cuadro.

## Solución de problemas

- **El cuadro combinado de frecuencia muestra un valor diferente al seleccionado** — El radio ha informado una frecuencia diferente para el flujo activo y el cuadro se ha sincronizado para coincidir. Esto es normal. Desactive el flujo, cambie la frecuencia y luego reactívelo.
- **El cuadro combinado de frecuencia no responde a la rueda del ratón** — El bloqueo de desplazamiento del panel del applet está activo. Haga clic en el cuadro combinado para abrir la lista desplegable.

## Relacionado

- [Información general sobre DAX IQ](overview.md)
- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
