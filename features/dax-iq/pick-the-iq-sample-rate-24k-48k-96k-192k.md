# Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)

Cambie la tasa de muestreo de un canal DAX IQ para que coincida con los requisitos de entrada de su software SDR externo. Una tasa más alta captura mayor ancho de banda; una tasa más baja reduce la carga de CPU y red.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet DAX IQ requiere una conexión activa al radio.
- El applet DAX IQ debe estar visible. Si está oculto, haga clic en el botón de bandeja **IQ** en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice la fila del canal que desea cambiar: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
2. Haga clic en el cuadro combinado de tasa en esa fila. Muestra la tasa actual (predeterminada: **48k**).
3. Seleccione una de las tasas disponibles: **24k**, **48k**, **96k** o **192k**.

La nueva tasa entra en vigencia de inmediato y se envía al radio. Si la transmisión está activa, el cuadro combinado reflejará la tasa informada por el radio.

## Qué hace cada control

| Control | Predeterminado | Valores válidos | Notas |
|---|---|---|---|
| Cuadro combinado de tasa (IQ 1–4) | 48k | 24k (24000 Hz), 48k (48000 Hz), 96k (96000 Hz), 192k (192000 Hz) | Se sincroniza con la tasa informada por el radio cuando la transmisión está activa. Sin clave de configuración persistente. |
| Interruptor Off/On (IQ 1–4) | Off | Off, On | Debe estar en **On** para que el cambio de tasa afecte una transmisión en vivo. |
| Medidor de nivel (IQ 1–4) | 0 | 0–100 | Muestra el nivel RMS de la transmisión. Se restablece a 0 cuando la transmisión se deshabilita o el radio se desconecta. |

## Consejos

- Puede cambiar la tasa tanto si la transmisión está **On** como **Off**. Si la transmisión está apagada, la tasa seleccionada se usará cuando la habilite.
- Desplazar la rueda del ratón sobre un cuadro combinado de tasa cerrado no tiene efecto — el menú desplegable debe estar abierto para que el desplazamiento funcione. Haga clic primero en el cuadro combinado para abrirlo y luego desplace.
- La configuración de las transmisiones IQ es por sesión y no es persistida por el radio. Después de reconectarse, las transmisiones vuelven a **Off** y el cuadro combinado de tasa regresa a **48k**.

## Solución de problemas

- **El cuadro combinado de tasa vuelve a un valor diferente después de cambiarlo.** — El radio informó una tasa distinta para la transmisión activa. Esto es normal; el cuadro combinado se sincroniza con la tasa confirmada por el radio. Si la transmisión está **On**, deshabilítela con el interruptor **Off/On**, cambie la tasa y luego vuelva a habilitarla.
- **El cuadro combinado de tasa no responde a los clics.** — Es posible que el panel del applet esté en modo de desplazamiento con los controles bloqueados. Intente hacer clic directamente en el cuadro combinado en lugar de desplazarse sobre él.

## Relacionados

- [Habilitar una transmisión IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Monitorear el nivel RMS de cada transmisión IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Deshabilitar una transmisión IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
- [Descripción general de DAX IQ](overview.md)
