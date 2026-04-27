# Descripción general de DAX IQ

El applet DAX IQ permite habilitar hasta cuatro flujos de datos IQ independientes desde su FLEX-8600, establecer la tasa de muestreo de cada flujo y monitorear el nivel de señal de cada flujo en tiempo real. Use estos flujos para alimentar software SDR externo con datos IQ sin procesar provenientes del radio.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El applet DAX IQ requiere una conexión de radio activa.
- El panel del applet debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

El applet DAX IQ proporciona cuatro canales de flujo IQ independientes, denominados IQ 1 a IQ 4. Cada canal se controla por completo dentro de una sola fila del applet. Los flujos son por sesión: el radio no conserva el estado del flujo entre desconexiones; sin embargo, AetherSDR guarda localmente el estado habilitado y la tasa de muestreo de cada canal, y reactiva los canales previamente activos aproximadamente 1.5 segundos después de una reconexión exitosa.

Al activar un canal, AetherSDR solicita el flujo al radio. Cuando el radio confirma que el flujo está activo, el botón de activación del canal se actualiza para reflejar el estado en vivo. Si el radio rechaza o elimina un flujo, el botón y el medidor se reinician automáticamente.

El applet está oculto de manera predeterminada. Ábralo o ciérrelo usando el botón de bandeja IQ en la barra lateral derecha.

## Qué hace cada control

| Control | Función | Valor predeterminado | Valores válidos | Clave de configuración persistida |
|---|---|---|---|---|
| Tasa IQ 1..4 | Establece la tasa de muestreo para ese canal IQ. El combo se sincroniza con la tasa informada por el radio cuando un flujo está activo. | 48k | 24k (24000), 48k (48000), 96k (96000), 192k (192000) | `DaxIqRate1` – `DaxIqRate4` |
| Medidor IQ 1..4 | Muestra el nivel RMS del flujo IQ en una escala de 0 a 100 (escalado desde RMS × 200). Se reinicia a 0 al desconectarse o deshabilitar el canal. | 0 | 0–100 | — |
| IQ 1..4 Off/On | Activa o desactiva el flujo IQ para ese canal. Muestra "Off" cuando está inactivo y "On" cuando está activo. | Off | Off, On | `DaxIqEnabled1` – `DaxIqEnabled4` |

## Consejos

- Cambiar la tasa de muestreo mientras un flujo está activo envía la nueva tasa al radio de inmediato. Si el radio informa una tasa diferente, el combo se sincronizará con el valor informado por el radio.
- Al reconectar, AetherSDR espera 1.5 segundos antes de reactivar los canales persistidos, a fin de permitir que la sesión de radio se inicialice completamente antes de enviar las solicitudes de flujo.
- Desplazarse por el panel del applet no cambiará accidentalmente los combos de tasa ni otros controles; el panel del applet bloquea los controles de la barra lateral durante el desplazamiento.

## Solución de problemas

- **El canal muestra "On" pero regresa a "Off" de inmediato** — El radio rechazó la solicitud de flujo, probablemente porque la sesión no estaba completamente lista. Desconéctese y vuelva a conectarse, o espere un momento y active el canal nuevamente.
- **El combo de tasa muestra un valor diferente al seleccionado** — El radio informó una tasa de muestreo diferente para el flujo activo. El combo se sincroniza con el valor informado por el radio; este es el comportamiento esperado.
- **El medidor permanece en 0 mientras un canal está "On"** — No se están recibiendo datos IQ. Confirme que el software externo esté conectado al flujo y que el radio esté procesando audio activamente en el slice asociado.

## Relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
