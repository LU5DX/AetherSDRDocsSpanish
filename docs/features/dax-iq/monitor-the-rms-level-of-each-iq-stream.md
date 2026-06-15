# Supervisar el nivel RMS de cada flujo IQ

El applet DAX IQ incluye un medidor de nivel en tiempo real para cada uno de los cuatro flujos IQ. Use estos medidores para confirmar que un flujo está activo y recibiendo señal.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet DAX IQ requiere una conexión activa con el radio.
- Debe haber al menos un flujo IQ habilitado. Un flujo deshabilitado muestra un valor de 0 en el medidor.

## Pasos

1. Haga clic en el botón de bandeja **IQ** en la barra lateral derecha para abrir el applet DAX IQ.
2. Localice la fila del canal que desea supervisar: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
3. Confirme que el botón de alternancia de ese canal muestra **On**. Si muestra **Off**, habilite primero el flujo; consulte [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md).
4. Observe el medidor de nivel en el centro de la fila. La barra se actualiza en tiempo real a medida que los datos IQ llegan desde el radio.

## Qué hace cada control

| Control | Qué muestra | Rango | Notas |
|---|---|---|---|
| Medidor IQ 1–4 | Nivel RMS del flujo IQ, escalado para visualización | 0–100 (escalado desde RMS × 200) | Se restablece a 0 cuando el flujo está deshabilitado, el radio se desconecta o el flujo no está vinculado a un pan. El medidor usa el color de acento del tema actual para el bloque de la barra de progreso. |
| IQ 1–4 Off/On | Indica si este flujo IQ está actualmente activo | Off / On | El flujo debe estar **On** y vinculado a un pan para que el medidor avance por encima de 0 |
| Tasa IQ 1–4 | Tasa de muestreo seleccionada para el flujo IQ | 24k (24000), 48k (48000), 96k (96000), 192k (192000) | Cambiar la tasa emite una señal al radio. El cuadro combinado se sincroniza con la tasa informada por el radio cuando un flujo está activo, pero no sobrescribe la selección del usuario durante la deshabilitación del flujo o el ajuste de tasa. |

## Consejos

- Un flujo **On** puede mostrar un medidor en 0 si el radio no tiene un slice activo, el software externo aún no ha abierto el flujo o el flujo no está vinculado a un pan.
- El medidor se restablece a 0 al desconectarse y en cualquier flujo que se cambie a **Off**.
- El valor del medidor es solo un indicador visual. No tiene una clave de configuración persistente ni afecta la configuración del radio.
- El cuadro combinado de tasa conserva la tasa seleccionada por el usuario incluso cuando el flujo está apagado. Si elige una tasa no predeterminada mientras el flujo está apagado, esa tasa se aplica la próxima vez que habilite el flujo.

## Solución de problemas

- **El medidor permanece en 0 aunque el flujo esté On** — El radio restablece todos los flujos IQ por sesión. Si acaba de reconectarse, AetherSDR espera aproximadamente 1,5 segundos antes de volver a habilitar los flujos persistentes. Espere a que la alternancia se estabilice en **On**, luego verifique el medidor nuevamente.
- **El flujo vuelve a Off inmediatamente después de conectarse** — El radio no estaba listo cuando se envió la solicitud de habilitación. AetherSDR lo reintenta automáticamente después de que se estabilice la configuración de la sesión. Si el botón permanece en **Off**, haga clic manualmente para solicitar el flujo nuevamente.
- **El medidor permanece en 0 en un flujo recién habilitado con una tasa no predeterminada** — La configuración de tasa se aplica cuando se habilita el flujo. El medidor puede mostrar 0 momentáneamente mientras se ajusta la tasa. Si permanece en 0, verifique que el flujo esté vinculado a un pan (el medidor baja a 0 cuando no está vinculado).

## Relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
- [Elegir la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Descripción general de DAX IQ](overview.md)
