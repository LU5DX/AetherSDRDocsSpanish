# Descripción general de DAX IQ

El applet DAX IQ le permite habilitar hasta cuatro flujos de datos IQ independientes desde el FLEX-8600, establecer la tasa de muestreo de cada uno y supervisar el nivel de señal en tiempo real. Use estos flujos para alimentar software SDR externo con datos IQ sin procesar del radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet DAX IQ requiere una conexión activa con el radio.
- El applet está oculto de forma predeterminada. Haga clic en el botón **IQ** de la bandeja en la barra lateral derecha para mostrarlo.

## Cómo funciona

El FLEX-8600 admite cuatro canales DAX IQ simultáneos. Cada canal es independiente: puede ejecutarlos a diferentes tasas de muestreo, habilitar solo los que necesite y supervisar el nivel de señal de cada uno por separado.

Los flujos IQ son por sesión. El radio no conserva el estado de los flujos entre conexiones. Cuando AetherSDR se reconecta, espera a que la sesión del radio se estabilice y luego vuelve a habilitar los canales que estaban marcados como habilitados al momento de la última desconexión. La última tasa de muestreo usada en cada canal se guarda localmente y se restaura en la siguiente sesión.

Cuando un flujo está activo, el cuadro combinado de tasa se sincroniza con la tasa reportada por el radio, que puede diferir del valor guardado localmente si el radio rechaza la tasa solicitada.

Los medidores se restablecen a cero cuando se deshabilita un flujo o el radio se desconecta.

## Qué hace cada control

Cada una de las cuatro filas (etiquetadas **IQ 1:** a **IQ 4:**) contiene tres controles:

| Control | Qué hace | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|---|
| Cuadro combinado de tasa | Establece la tasa de muestreo IQ para ese canal. | `48k` | `24k` (24000), `48k` (48000), `96k` (96000), `192k` (192000) | `DaxIqRate1` – `DaxIqRate4` |
| Medidor de nivel | Muestra el nivel RMS del flujo IQ, escalado de 0 a 100. | 0 | 0–100 | — |
| Botón **Off** / **On** | Habilita o deshabilita el flujo IQ para ese canal. | **Off** | **Off**, **On** | `DaxIqEnabled1` – `DaxIqEnabled4` |

La etiqueta del botón cambia entre **Off** y **On** para reflejar el estado actual del flujo. El radio confirma la creación o eliminación del flujo; si el radio rechaza la solicitud, el estado del botón se actualiza para coincidir con el estado reportado por el radio.

## Consejos

- Habilitar un canal a una tasa de muestreo más alta (96k o 192k) aumenta la carga de red y CPU. Habilite solo los canales que esté usando activamente.
- Si cierra AetherSDR con un canal marcado como **On**, se volverá a habilitar automáticamente aproximadamente 1,5 segundos después de la siguiente conexión exitosa.
- Para evitar que un canal se vuelva a habilitar al reconectar, haga clic en su botón para ponerlo en **Off** antes de desconectarse.

## Solución de problemas

- **El botón muestra "On" pero vuelve a "Off" inmediatamente después de conectar** — El radio rechazó la solicitud del flujo. Esto puede ocurrir si la sesión no se ha inicializado completamente. AetherSDR espera 1,5 segundos después de conectar antes de volver a habilitar los flujos; si el radio sigue ocupado, intente activar el canal manualmente después de unos segundos más.
- **El cuadro combinado de tasa muestra un valor distinto al seleccionado** — El radio ha reemplazado la tasa solicitada. El cuadro combinado se sincroniza con la tasa reportada por el radio cuando un flujo está activo. Seleccione la tasa nuevamente si es necesario.
- **El medidor permanece en cero con el flujo habilitado** — No fluyen datos IQ. Confirme que su aplicación receptora haya abierto el flujo IQ en el número de canal correcto.

## Relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Supervisar el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
