# Resumen de DAX IQ

El applet DAX IQ le permite habilitar hasta cuatro flujos de datos IQ independientes desde su FLEX-8600, configurar la frecuencia de muestreo de cada flujo y monitorear el nivel de señal de cada flujo en tiempo real. Utilice estos flujos para alimentar software SDR externo con datos IQ puros desde la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX IQ requiere una conexión activa con la radio.
- El panel del applet debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

El applet DAX IQ proporciona cuatro canales de flujo IQ independientes, etiquetados IQ 1 a IQ 4. Cada canal se controla completamente dentro de una sola fila del applet. Los flujos son por sesión: la radio no conserva el estado del flujo entre desconexiones, pero AetherSDR guarda localmente el estado habilitado y la frecuencia de muestreo de cada canal, y vuelve a habilitar cualquier canal previamente activo aproximadamente 1,5 segundos después de una reconexión exitosa.

Cuando activa un canal, AetherSDR solicita el flujo a la radio. Cuando la radio confirma que el flujo está activo, el botón de activación del canal se actualiza para reflejar el estado activo. Si la radio rechaza o elimina un flujo, el botón y el medidor se restablecen automáticamente.

El applet está oculto por defecto. Actívelo o ciérrelo usando el botón de la bandeja IQ en la barra lateral derecha.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Valores válidos | Clave de configuración persistida |
|---|---|---|---|---|
| Tasa IQ 1..4 | Establece la frecuencia de muestreo para ese canal IQ. El combo se sincroniza con la tasa informada por la radio cuando un flujo está activo. | 48k | 24k (24000), 48k (48000), 96k (96000), 192k (192000) | `DaxIqRate1` – `DaxIqRate4` |
| Medidor IQ 1..4 | Muestra el nivel RMS del flujo IQ en una escala de 0–100 (escalado desde RMS × 200). Se restablece a 0 al desconectar o deshabilitar. | 0 | 0–100 | — |
| IQ 1..4 Off/On | Activa o desactiva el flujo IQ para ese canal. Muestra "Off" cuando está inactivo y "On" cuando está activo. | Off | Off, On | `DaxIqEnabled1` – `DaxIqEnabled4` |

## Apariencia

El applet DAX IQ se adapta al tema actual. El fondo y el color de acento de la barra de progreso del medidor están controlados por los valores `color.background.0`, `color.background.1` y `color.accent` del tema activo, en lugar de colores fijos. Esto garantiza que el applet coincida visualmente con el resto de la interfaz de AetherSDR, independientemente del tema seleccionado.

## Consejos

- Cambiar la frecuencia de muestreo mientras un flujo está activo envía la nueva tasa a la radio inmediatamente. Si la radio informa una tasa diferente, el combo se sincronizará con el valor informado por la radio.
- Al reconectar, AetherSDR espera 1,5 segundos antes de volver a habilitar los canales persistidos para permitir que la sesión de la radio se inicialice completamente antes de enviar solicitudes de flujo.
- Desplazar el panel del applet no cambiará accidentalmente los combos de tasa u otros controles; el panel del applet bloquea los controles de la barra lateral durante el desplazamiento.
- El applet DAX IQ reconoce el tema: las barras del medidor usarán el color de acento de su tema actual en lugar del azul fijo anterior.

## Solución de problemas

- **El canal muestra "On" pero se restablece a "Off" inmediatamente** — La radio rechazó la solicitud de flujo, probablemente porque la sesión no estaba completamente lista. Desconecte y reconecte, o espere un momento y active el canal nuevamente.
- **El combo de tasa muestra un valor diferente al que seleccionó** — La radio informó una frecuencia de muestreo diferente para el flujo activo. El combo se sincroniza con el valor informado por la radio; esto es un comportamiento esperado.
- **El medidor permanece en 0 mientras un canal está "On"** — No se están recibiendo datos IQ. Confirme que el software externo esté conectado al flujo y que la radio esté procesando activamente audio en el slice asociado.

## Relacionado

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la frecuencia de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
