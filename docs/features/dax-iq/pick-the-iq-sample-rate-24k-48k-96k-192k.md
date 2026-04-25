# Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)

Esta página explica cómo cambiar la tasa de muestreo de cualquiera de los cuatro canales DAX IQ. Haga esto para que coincida con la tasa esperada por el software SDR externo que recibe el flujo IQ.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX IQ no funciona sin una conexión de radio activa.
- El applet DAX IQ debe estar visible. Si no lo está, haga clic en el botón **IQ** de la bandeja en la barra lateral derecha para mostrarlo.

## Pasos

1. Abra el applet DAX IQ haciendo clic en el botón **IQ** de la bandeja en la barra lateral derecha, si aún no está visible.
2. Localice la fila del canal que desea cambiar: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
3. Haga clic en el cuadro combinado de tasa en esa fila. Muestra la tasa actual (predeterminada: **48k**).
4. Seleccione una de las tasas disponibles: **24k**, **48k**, **96k** o **192k**.

La nueva tasa entra en vigor de inmediato y se envía a la radio. Si el flujo de ese canal está activo, el cuadro combinado reflejará la tasa informada por la radio.

## Qué hace cada control

| Control | Descripción | Predeterminado | Valores válidos | Configuración persistida |
|---|---|---|---|---|
| Cuadro combinado de tasa (IQ 1–4) | Establece la tasa de muestreo IQ de ese canal en muestras por segundo. | 48k (48000) | 24k (24000), 48k (48000), 96k (96000), 192k (192000) | `DaxIqRate1` – `DaxIqRate4` |
| Botón de alternancia Off/On (IQ 1–4) | Habilita o deshabilita el flujo IQ de ese canal. | Off | Off, On | `DaxIqEnabled1` – `DaxIqEnabled4` |
| Medidor de nivel (IQ 1–4) | Muestra el nivel RMS del flujo IQ activo, en escala de 0 a 100. | 0 | 0–100 | — |

## Consejos

- El cuadro combinado de tasa se mantiene sincronizado con la radio. Si la radio informa una tasa diferente después de establecer el flujo, el cuadro combinado se actualiza automáticamente para coincidir.
- La tasa seleccionada se guarda entre sesiones. Cuando AetherSDR se vuelve a conectar a la radio, restaura la tasa que eligió por última vez para cada canal.
- Las tasas de muestreo más altas capturan más ancho de banda, pero aumentan la carga de CPU y red entre la radio y la computadora.

## Solución de problemas

- **El cuadro combinado de tasa vuelve a un valor diferente después de cambiarlo** — La radio informó una tasa de muestreo diferente para ese flujo activo. El cuadro combinado se sincroniza con el valor informado por la radio cuando un flujo está activo. Deshabilite el flujo con el botón **Off/On**, cambie la tasa y luego vuelva a habilitarlo.
- **El cuadro combinado de tasa está presente, pero los cambios no tienen efecto visible** — Es posible que el flujo de ese canal no esté habilitado. Haga clic en el botón **Off** para cambiarlo a **On** y que la radio abra el flujo con la tasa seleccionada.

## Relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Descripción general de DAX IQ](overview.md)
