# Desactivar un flujo IQ para liberar ancho de banda

Cada flujo DAX IQ activo consume recursos DSP de la radio y ancho de banda de red. Desactivar un flujo que no esté usando libera esa capacidad para otros slices, flujos de audio o canales IQ.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet DAX IQ requiere una conexión activa a la radio.
- El applet DAX IQ debe estar visible. Si no lo está, haga clic en el botón de la bandeja IQ en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice la fila del canal que desea detener — IQ 1, IQ 2, IQ 3 o IQ 4.
2. Verifique que el botón de alternancia a la derecha de esa fila muestre "On". Si ya muestra "Off", el flujo ya está inactivo.
3. Haga clic en "On". La etiqueta del botón cambia a "Off", el estilo del botón se atenúa y el medidor de nivel se restablece a 0. El flujo se elimina de la radio para esta sesión.

## Qué hace cada control

| Control | Predeterminado | Comportamiento | Clave persistida |
|---|---|---|---|
| IQ 1..4 Off/On | Off | Al hacer clic se alterna el flujo. Cuando se desactiva, el botón muestra "Off" y el medidor se restablece a 0. | `DaxIqEnabled1` – `DaxIqEnabled4` |
| Medidor IQ 1..4 | 0 | Muestra el nivel RMS del flujo (0–100). Se restablece a 0 cuando el flujo se desactiva, el pan al que está vinculado el flujo se elimina o la radio se desconecta. | — |
| Tasa IQ 1..4 | 48k | Establece la tasa de muestreo del canal (24k, 48k, 96k, 192k). No cambia al desactivar el flujo. El cuadro combinado conserva la última tasa seleccionada incluso mientras el flujo está desactivado; la tasa se aplica al flujo recién creado cuando lo vuelve a activar. | `DaxIqRate1` – `DaxIqRate4` |

## Consejos

- Los flujos IQ son por sesión. La radio no persiste el estado del flujo entre conexiones. AetherSDR almacena su última elección de activar/desactivar en `DaxIqEnabled1` a `DaxIqEnabled4` y restaura esos flujos automáticamente unos 1.5 segundos después de reconectar. Si AetherSDR se conecta antes de que se construya el applet DAX IQ, la restauración aún ocurre — el applet verifica si la radio ya está conectada cuando se inicializa.
- Si desea que un canal permanezca desactivado después de una reconexión, desactivarlo aquí es suficiente — la clave persistida se establece en `False` inmediatamente cuando hace clic en "On" para desactivarlo.
- Desactivar un flujo también borra el medidor de nivel. Si el medidor continúa mostrando una lectura distinta de cero después de hacer clic en "Off", el estado de la radio aún no se ha sincronizado; el botón se actualizará nuevamente una vez que la radio confirme que el flujo fue eliminado. El medidor también se pone a cero cuando existe un flujo pero no está vinculado a un pan (por ejemplo, el pan que estaba usando este canal IQ se cambió a otro canal IQ). En ese caso no fluyen datos IQ, por lo que la barra cae a 0 en lugar de congelarse.
- El cuadro combinado de tasa recuerda su selección incluso cuando el flujo está desactivado. Durante una activación con tasa no predeterminada, el flujo reporta brevemente 48k hasta que la radio confirma la tasa real; el cuadro combinado no cambia a 48k durante este período transitorio, preservando su intención.

## Solución de problemas

- **El botón muestra "Off" pero inmediatamente vuelve a "On"** — La radio puede estar restaurando un estado de flujo persistido al reconectar. Espere a que se complete el retardo de configuración de sesión de 1.5 segundos, luego haga clic en "On" para desactivar el flujo nuevamente.
- **El medidor de nivel no se restablece a 0 después de desactivar** — La confirmación de eliminación del flujo de la radio aún no ha llegado. El medidor se restablecerá una vez que la radio informe que el flujo ya no existe. Si el medidor muestra un valor constante distinto de cero pero el flujo parece desactivado, verifique si el flujo aún está vinculado a un pan; el medidor solo se pone a cero cuando el pan vinculado también se elimina.
- **El applet DAX IQ no aparece en Windows o Linux** — El applet está oculto por defecto. Haga clic en el botón de la bandeja IQ en la barra lateral derecha. Si aún no aparece, asegúrese de que su sistema de audio sea compatible con PulseAudio (PipeWire no es necesario). El applet se inicializa en estas plataformas independientemente del backend de audio.

## Relacionado

- [Enable an IQ stream for external SDR software](enable-an-iq-stream-for-external-sdr-software.md)
- [Monitor the RMS level of each IQ stream](monitor-the-rms-level-of-each-iq-stream.md)
- [Pick the IQ sample rate (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
