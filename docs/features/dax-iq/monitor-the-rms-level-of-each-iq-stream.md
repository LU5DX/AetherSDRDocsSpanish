# Monitoree el nivel RMS de cada flujo IQ

El applet DAX IQ incluye un medidor de nivel en tiempo real para cada uno de los cuatro flujos IQ. Utilice estos medidores para confirmar que un flujo está activo y recibiendo señal.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo de radio. El applet DAX IQ requiere una conexión activa con el radio.
- Al menos un flujo IQ debe estar habilitado. Un flujo deshabilitado muestra un valor de medidor de 0.

## Pasos

1. Haga clic en el botón de bandeja **IQ** en la barra lateral derecha para abrir el applet DAX IQ.
2. Localice la fila del canal que desea monitorear: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
3. Confirme que el botón de alternancia para ese canal muestre **On**. Si muestra **Off**, habilite primero el flujo — consulte [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md).
4. Observe el medidor de nivel en el centro de la fila. La barra se actualiza en tiempo real a medida que llegan datos IQ desde el radio.

## Qué hace cada control

| Control | Qué muestra | Rango | Notas |
|---|---|---|---|
| Medidor IQ 1–4 | Nivel RMS del flujo IQ, escalado para visualización | 0–100 (escalado desde RMS × 200) | Se restablece a 0 cuando el flujo se deshabilita o el radio se desconecta. El medidor usa el color de acento del tema actual para la barra de progreso. |
| IQ 1–4 Off/On | Indica si este flujo IQ está actualmente activo | Off / On | El flujo debe estar en **On** para que el medidor avance por encima de 0 |
| Tasa IQ 1–4 | Tasa de muestreo seleccionada para el flujo IQ | 24k (24000), 48k (48000), 96k (96000), 192k (192000) | Cambiar la tasa emite una señal al radio. El cuadro combinado se sincroniza con la tasa reportada por el radio cuando un flujo está activo. |

## Consejos

- Un medidor que permanece en 0 en un flujo **On** puede indicar que el radio no tiene una franja activa o que el software externo aún no ha abierto el flujo.
- El medidor se restablece a 0 al desconectarse y en cualquier flujo que se cambie a **Off**.
- El valor del medidor es solo un indicador visual. No tiene una clave de configuración persistente ni ningún efecto en la configuración del radio.

## Solución de problemas

- **El medidor permanece en 0 aunque el flujo esté en On** — El radio restablece todos los flujos IQ por sesión. Si acaba de reconectarse, AetherSDR espera aproximadamente 1.5 segundos antes de re-habilitar los flujos persistentes. Espere a que el interruptor se estabilice en **On** y luego revise el medidor nuevamente.
- **El flujo vuelve a Off inmediatamente después de conectarse** — El radio no estaba listo cuando se envió la solicitud de habilitación. AetherSDR reintenta automáticamente después de que se estabilice la configuración de la sesión. Si el botón permanece en **Off**, haga clic manualmente para solicitar el flujo nuevamente.

## Relacionado

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
- [Elegir la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Descripción general de DAX IQ](overview.md)
