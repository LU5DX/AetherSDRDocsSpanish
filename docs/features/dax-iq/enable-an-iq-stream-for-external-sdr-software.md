# Habilitar un flujo IQ para software SDR externo

El applet DAX IQ permite activar hasta cuatro flujos IQ desde su FLEX-8600 y enrutarlos hacia software SDR externo. Habilite un canal aquí para iniciar el flujo en la radio; su aplicación externa se conecta luego a ese flujo para recibir muestras IQ.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet DAX IQ requiere una conexión de radio activa.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de bandeja **IQ** en la barra lateral derecha para abrir el applet DAX IQ.
2. Ubique la fila del canal que desea usar: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
3. Seleccione una tasa de muestreo en el cuadro combinado de tasa de esa fila. El valor predeterminado es **48k**. Las tasas disponibles son 24k, 48k, 96k y 192k.
4. Haga clic en el botón **Off** en el extremo derecho de la fila. El botón cambia a **On** y el flujo queda activo en la radio.
5. Configure su software SDR externo para conectarse al canal DAX IQ correspondiente. El medidor de nivel de esa fila mostrará actividad de señal una vez que las muestras estén fluyendo.

## Qué hace cada control

| Control | Descripción | Predeterminado | Valores válidos |
|---|---|---|---|
| Cuadro combinado de tasa (IQ 1–4) | Establece la tasa de muestreo IQ del canal. El cuadro combinado se sincroniza con la tasa informada por la radio cuando un flujo está activo. | 48k | 24k (24000), 48k (48000), 96k (96000), 192k (192000) |
| Medidor de nivel (IQ 1–4) | Muestra el nivel RMS del flujo IQ activo, escalado de 0 a 100. Se reinicia a 0 al desconectar o deshabilitar. | 0 | 0–100 |
| Botón Off / On (IQ 1–4) | Habilita o deshabilita el flujo IQ de ese canal. | Off | Off, On |

## Consejos

- Los flujos IQ son por sesión y no los persiste la radio. Sin embargo, AetherSDR guarda el estado habilitado de cada canal de forma local (claves `DaxIqEnabled1` a `DaxIqEnabled4`) y restaura los flujos activos automáticamente aproximadamente 1.5 segundos después de reconectarse a la radio.
- El cuadro combinado de tasa también se guarda localmente por canal (`DaxIqRate1` a `DaxIqRate4`), de modo que su tasa de muestreo preferida se restaura en el siguiente inicio.
- Si desplaza el panel de applets sin intención de cambiar valores, el mecanismo de bloqueo de controles de AetherSDR evita cambios accidentales de tasa durante el desplazamiento.

## Solución de problemas

- **El botón muestra "On" tras reconectarse pero no llegan muestras a la aplicación externa** — AetherSDR solicita los flujos aproximadamente 1.5 segundos después de conectarse para permitir que la configuración de sesión se complete. Espere un momento y luego verifique que su software externo esté conectado al número de canal DAX IQ correcto.
- **El cuadro combinado de tasa muestra un valor distinto al seleccionado** — Cuando un flujo está activo, el cuadro combinado se sincroniza con la tasa informada por la radio, lo que puede anular su selección. Deshabilite el flujo, cambie la tasa y luego vuelva a habilitarlo.

## Relacionado

- [Descripción general de DAX IQ](overview.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
