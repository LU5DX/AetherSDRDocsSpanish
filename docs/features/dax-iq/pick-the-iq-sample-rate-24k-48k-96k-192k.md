# Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)

Esta página explica cómo cambiar la tasa de muestreo IQ para cualquiera de los cuatro canales DAX IQ. Use una tasa más alta cuando su software SDR externo requiera mayor ancho de banda; use una tasa más baja para reducir la carga de CPU y de red.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El applet DAX IQ debe estar visible. Si no lo está, haga clic en el botón IQ del área de notificación en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice la fila del canal que desea modificar: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
2. Haga clic en el cuadro combinado de tasa en esa fila. Actualmente muestra la tasa activa (predeterminada **48k**).
3. Seleccione una de las cuatro tasas: **24k**, **48k**, **96k** o **192k**.

La nueva tasa entra en vigor de inmediato y se envía a la radio. Si el flujo de ese canal está activo, el cuadro combinado se sincronizará con la tasa reportada por la radio para confirmar que el cambio fue aceptado.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Valores válidos | Configuración persistida |
|---|---|---|---|---|
| Cuadro combinado de tasa (IQ 1–4) | Establece la tasa de muestreo IQ para ese canal | 48k | 24k (24000), 48k (48000), 96k (96000), 192k (192000) | `DaxIqRate1` – `DaxIqRate4` |
| Interruptor Off/On (IQ 1–4) | Habilita o deshabilita el flujo IQ para ese canal | Off | Off, On | `DaxIqEnabled1` – `DaxIqEnabled4` |
| Medidor de nivel (IQ 1–4) | Muestra el nivel RMS del flujo activo (escala de 0 a 100) | 0 | 0–100 | — |

## Consejos

- El cuadro combinado de tasa se sincroniza con la tasa reportada por la radio cuando un flujo está activo. Si el valor seleccionado no se mantiene, la radio rechazó el cambio de tasa; intente deshabilitar el flujo primero, cambiar la tasa y luego volver a habilitarlo.
- Los ajustes de tasa son persistidos. Al reconectarse, AetherSDR restaura la última tasa utilizada para cada canal desde `DaxIqRate1` hasta `DaxIqRate4`.
- El estado de habilitación del flujo también es persistido. Si un canal quedó en **On** al desconectarse, AetherSDR lo volverá a habilitar automáticamente aproximadamente 1.5 segundos después de la reconexión, para permitir que la configuración de sesión de la radio se complete primero.

## Solución de problemas

- **El cuadro combinado de tasa revierte al valor anterior después de la selección** — La radio rechazó el cambio de tasa mientras el flujo estaba activo. Haga clic en **On** para cambiar el canal a **Off**, establezca la tasa deseada y luego haga clic en **Off** para volver a **On**.
- **El cuadro combinado muestra una tasa diferente a la seleccionada** — La radio reportó una tasa distinta para el flujo activo y el cuadro combinado se sincronizó para coincidir con ella. El valor reportado por la radio es autoritativo cuando hay un flujo en ejecución.

## Relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Descripción general de DAX IQ](overview.md)
