# Desactivar un flujo IQ para liberar ancho de banda

Cada flujo DAX IQ activo consume recursos DSP de la radio y ancho de banda de red. Desactivar un flujo que no esté utilizando libera esa capacidad para otros slices, flujos de audio o canales IQ.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El applet DAX IQ requiere una conexión de radio activa.
- El applet DAX IQ debe estar visible. Si no lo está, haga clic en el botón de la bandeja IQ en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice la fila del canal que desea detener: IQ 1, IQ 2, IQ 3 o IQ 4.
2. Verifique que el botón de activación a la derecha de esa fila muestre "On". Si ya muestra "Off", el flujo ya está inactivo.
3. Haga clic en "On". La etiqueta del botón cambia a "Off", el estilo del botón se atenúa y el medidor de nivel se reinicia a 0. El flujo se elimina de la radio para esta sesión.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento | Clave persistente |
|---|---|---|---|
| IQ 1..4 Off/On | Off | Al hacer clic se alterna el flujo. Cuando se desactiva, el botón muestra "Off" y el medidor se reinicia a 0. | `DaxIqEnabled1` – `DaxIqEnabled4` |
| Medidor IQ 1..4 | 0 | Muestra el nivel RMS del flujo (0–100). Se reinicia a 0 cuando el flujo se desactiva o la radio se desconecta. | — |
| Tasa IQ 1..4 | 48k | Establece la frecuencia de muestreo del canal (24k, 48k, 96k, 192k). No se modifica al desactivar el flujo. | `DaxIqRate1` – `DaxIqRate4` |

## Consejos

- Los flujos IQ son por sesión. La radio no persiste el estado del flujo entre conexiones. AetherSDR almacena su última elección de activación/desactivación en `DaxIqEnabled1` a `DaxIqEnabled4` y restaura esos flujos automáticamente aproximadamente 1,5 segundos después de reconectar.
- Si desea que un canal permanezca desactivado después de una reconexión, basta con desactivarlo aquí; la clave persistente se establece en `False` inmediatamente cuando hace clic en "On" para apagarlo.
- Desactivar un flujo también borra el medidor de nivel. Si el medidor continúa mostrando un valor distinto de cero después de hacer clic en "Off", el estado de la radio aún no se ha sincronizado; el botón se actualizará nuevamente una vez que la radio confirme que el flujo se eliminó.

## Solución de problemas

- **El botón muestra "Off" pero inmediatamente vuelve a "On"** — La radio puede estar restaurando un estado de flujo persistente al reconectar. Espere a que se complete el retardo de configuración de sesión de 1,5 segundos, luego haga clic en "On" para desactivar el flujo nuevamente.
- **El medidor de nivel no se reinicia a 0 después de desactivar** — La confirmación de eliminación del flujo de la radio aún no ha llegado. El medidor se reiniciará una vez que la radio informe que el flujo ya no existe.
- **El applet DAX IQ no aparece en Windows o Linux** — El applet está oculto por defecto. Haga clic en el botón de la bandeja IQ en la barra lateral derecha. Si aún no aparece, asegúrese de que su sistema de audio sea compatible con PulseAudio (no se requiere PipeWire). El applet se inicializa en estas plataformas independientemente del backend de audio.

## Relacionado

- [Enable an IQ stream for external SDR software](enable-an-iq-stream-for-external-sdr-software.md)
- [Monitor the RMS level of each IQ stream](monitor-the-rms-level-of-each-iq-stream.md)
- [Pick the IQ sample rate (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
