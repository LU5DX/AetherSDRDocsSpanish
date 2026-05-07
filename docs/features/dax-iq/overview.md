# Resumen de DAX IQ

El applet DAX IQ le permite habilitar hasta cuatro flujos independientes de datos IQ desde su FLEX-8600, establecer la tasa de muestreo de cada flujo y monitorear el nivel de señal de cada uno en tiempo real. Utilice estos flujos para alimentar software SDR externo con datos IQ sin procesar desde la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX IQ requiere una conexión activa con la radio.
- El panel del applet debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

El applet DAX IQ proporciona cuatro canales de flujo IQ independientes, etiquetados como IQ 1 a IQ 4. Cada canal se controla completamente dentro de una sola fila del applet. Los flujos son por sesión: la radio no conserva el estado del flujo entre desconexiones, pero AetherSDR guarda localmente el estado habilitado y la tasa de muestreo de cada canal, y vuelve a habilitar cualquier canal que estuviera activo aproximadamente 1.5 segundos después de una reconexión exitosa.

Cuando activa un canal, AetherSDR solicita el flujo a la radio. Cuando la radio confirma que el flujo está activo, el botón de activación del canal se actualiza para reflejar el estado en vivo. Si la radio rechaza o elimina un flujo, el botón y el medidor se restablecen automáticamente.

El applet está oculto por defecto. Actívelo o ciérrelo usando el botón de la bandeja IQ en la barra lateral derecha.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Valores válidos | Clave de configuración persistida |
|---|---|---|---|---|
| Tasa IQ 1..4 | Establece la tasa de muestreo para ese canal IQ. El combo se sincroniza con la tasa reportada por la radio cuando un flujo está activo. | 48k | 24k (24000), 48k (48000), 96k (96000), 192k (192000) | `DaxIqRate1` – `DaxIqRate4` |
| Medidor IQ 1..4 | Muestra el nivel RMS del flujo IQ en una escala de 0 a 100 (escalado desde RMS × 200). Se restablece a 0 al desconectar o deshabilitar. | 0 | 0–100 | — |
| IQ 1..4 Off/On | Activa o desactiva el flujo IQ para ese canal. Muestra "Off" cuando está inactivo y "On" cuando está activo. | Off | Off, On | `DaxIqEnabled1` – `DaxIqEnabled4` |

## Consejos

- Cambiar la tasa de muestreo mientras un flujo está activo envía la nueva tasa a la radio de inmediato. Si la radio reporta una tasa diferente, el combo se sincronizará con el valor reportado por la radio.
- Al reconectar, AetherSDR espera 1.5 segundos antes de re-habilitar los canales persistidos para permitir que la sesión de la radio se inicialice completamente antes de que se envíen las solicitudes de flujo.
- Al desplazarse por el panel del applet, no se cambiarán accidentalmente los combos de tasa ni otros controles; el panel del applet bloquea los controles de la barra lateral durante el desplazamiento.

## Solución de problemas

- **El canal muestra "On" pero se restablece a "Off" inmediatamente** — La radio rechazó la solicitud de flujo, probablemente porque la sesión no estaba completamente lista. Desconéctese y reconéctese, o espere un momento y vuelva a activar el canal.
- **El combo de tasa muestra un valor diferente al que seleccionó** — La radio reportó una tasa de muestreo diferente para el flujo activo. El combo se sincroniza con el valor reportado por la radio; este es un comportamiento esperado.
- **El medidor permanece en 0 mientras un canal está "On"** — No se están recibiendo datos IQ. Confirme que el software externo está conectado al flujo y que la radio está procesando activamente audio en el slice asociado.

## Relacionado

- [Enable an IQ stream for external SDR software](enable-an-iq-stream-for-external-sdr-software.md)
- [Pick the IQ sample rate (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Monitor the RMS level of each IQ stream](monitor-the-rms-level-of-each-iq-stream.md)
- [Disable an IQ stream to free bandwidth](disable-an-iq-stream-to-free-bandwidth.md)
