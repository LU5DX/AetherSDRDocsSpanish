# Descripción general de DAX IQ

El applet DAX IQ le permite habilitar hasta cuatro flujos de datos IQ independientes desde su FLEX-8600, configurar la frecuencia de muestreo de cada flujo y monitorear el nivel de señal de cada flujo en tiempo real. Utilice estos flujos para alimentar software SDR externo con datos IQ en bruto desde la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX IQ requiere una conexión activa con la radio.
- El panel del applet debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

El applet DAX IQ proporciona cuatro canales de flujo IQ independientes, etiquetados IQ 1 a IQ 4. Cada canal se controla completamente dentro de una sola fila del applet. Los flujos son por sesión: la radio no conserva el estado del flujo al desconectarse, pero AetherSDR guarda localmente el estado habilitado y la frecuencia de muestreo de cada canal, y vuelve a habilitar cualquier canal previamente activo aproximadamente 1.5 segundos después de una reconexión exitosa.

Cuando activa un canal, AetherSDR solicita el flujo a la radio. Cuando la radio confirma que el flujo está activo, el botón de activación del canal se actualiza para reflejar el estado en vivo. Si la radio rechaza o elimina un flujo, el botón y el medidor se restablecen automáticamente. Si existe un flujo pero no está vinculado a un pan (por ejemplo, el `daxiq_channel` del pan fue reasignado), el medidor cae a cero ya que no fluyen datos.

El applet está oculto por defecto. Actívelo o desactívelo usando el botón IQ en la barra lateral derecha.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Valores válidos | Clave de ajuste persistido |
|---|---|---|---|---|
| Tasa IQ 1..4 | Establece la frecuencia de muestreo para ese canal IQ. El combinado se sincroniza con la tasa reportada por la radio cuando un flujo está activo y no está estabilizando la tasa. Cualquier tasa seleccionada mientras el flujo está desactivado se aplica en la próxima activación. | 48k | 24k (24000), 48k (48000), 96k (96000), 192k (192000) | `DaxIqRate1` – `DaxIqRate4` |
| Medidor IQ 1..4 | Muestra el nivel RMS del flujo IQ en una escala de 0 a 100 (escalado de RMS × 200). Se restablece a 0 cuando el flujo está deshabilitado o no está vinculado a un pan. | 0 | 0–100 | — |
| IQ 1..4 Off/On | Activa o desactiva el flujo IQ para ese canal. Muestra "Off" cuando está inactivo y "On" cuando está activo. | Off | Off, On | `DaxIqEnabled1` – `DaxIqEnabled4` |

## Apariencia

El applet DAX IQ se adapta al tema actual. El fondo de la barra de progreso y el color de acento están controlados por los valores `color.background.0`, `color.background.1` y `color.accent` del tema activo, en lugar de colores fijos. Esto asegura que el applet coincida visualmente con el resto de la interfaz de AetherSDR independientemente del tema seleccionado.

## Consejos

- Cambiar la frecuencia de muestreo mientras un flujo está activo envía la nueva tasa a la radio inmediatamente. Si la radio reporta una tasa diferente (después de que se complete la estabilización), el combinado se sincronizará con el valor reportado por la radio.
- Al reconectar, AetherSDR espera 1.5 segundos antes de volver a habilitar los canales persistidos para permitir que la sesión de la radio se inicialice completamente antes de enviar solicitudes de flujo. La lógica idempotente evita solicitudes de habilitación duplicadas si ocurren múltiples eventos de reconexión cercanos.
- Si la radio ya está conectada cuando se carga el applet, los canales persistidos se restauran inmediatamente sin esperar un evento de cambio de estado de conexión.
- Desplazarse por el panel del applet no cambiará accidentalmente los combinados de tasa u otros controles; el panel del applet bloquea los controles de la barra lateral durante el desplazamiento.
- El applet DAX IQ es consciente del tema: las barras del medidor usarán el color de acento de su tema actual en lugar del azul fijo anterior.

## Solución de problemas

- **El canal muestra "On" pero se restablece a "Off" inmediatamente** — La radio rechazó la solicitud de flujo, probablemente porque la sesión no estaba completamente lista. Desconéctese y reconéctese, o espere un momento y vuelva a activar el canal.
- **El combinado de tasa muestra un valor diferente al que seleccionó** — Si el flujo está estabilizando la tasa, el combinado mantiene el valor deseado y se sincronizará una vez que se complete la estabilización. Si el flujo no existe, el combinado conserva su última selección.
- **El medidor permanece en 0 mientras un canal está "On"** — No se reciben datos IQ. Esto puede ocurrir si el flujo existe pero no está vinculado a un pan (el `daxiq_channel` del pan se movió a otro lugar). Confirme que el software externo esté conectado al flujo y que la radio esté procesando activamente audio en el slice asociado.

## Relacionado

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la frecuencia de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
