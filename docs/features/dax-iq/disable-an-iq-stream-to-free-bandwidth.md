# Deshabilitar un flujo IQ para liberar ancho de banda

Cada flujo DAX IQ activo consume recursos DSP del radio y ancho de banda de la red. Deshabilitar un flujo que no esté usando libera esa capacidad para otras slices, flujos de audio o canales IQ.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet DAX IQ requiere una conexión activa al radio.
- El applet DAX IQ debe estar visible. Si no lo está, haga clic en el botón de la bandeja IQ en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice la fila del canal que desea detener — IQ 1, IQ 2, IQ 3 o IQ 4.
2. Verifique que el botón de alternancia a la derecha de esa fila muestre "On". Si ya muestra "Off", el flujo ya está inactivo.
3. Haga clic en "On". La etiqueta del botón cambia a "Off", el estilo del botón se atenúa y el medidor de nivel se restablece a 0. El flujo se elimina del radio para esta sesión.

## Función de cada control

| Control | Predeterminado | Comportamiento | Clave persistida |
|---|---|---|---|
| IQ 1..4 Off/On | Off | Al hacer clic se alterna el flujo. Al desactivarse, el botón muestra "Off" y el medidor se restablece a 0. | `DaxIqEnabled1` – `DaxIqEnabled4` |
| IQ 1..4 medidor | 0 | Muestra el nivel RMS del flujo (0–100). Se restablece a 0 cuando el flujo se deshabilita o el radio se desconecta. | — |
| IQ 1..4 tasa | 48k | Establece la tasa de muestreo del canal (24k, 48k, 96k, 192k). No cambia al deshabilitar el flujo. | `DaxIqRate1` – `DaxIqRate4` |

## Consejos

- Los flujos IQ son por sesión. El radio no persiste el estado del flujo entre conexiones. AetherSDR almacena su última elección de habilitar/deshabilitar en `DaxIqEnabled1` hasta `DaxIqEnabled4` y restaura esos flujos automáticamente aproximadamente 1.5 segundos después de reconectarse.
- Si desea que un canal permanezca apagado después de una reconexión, deshabilitarlo aquí es suficiente: la clave persistida se establece en `False` inmediatamente cuando hace clic en "On" para apagarlo.
- Deshabilitar un flujo también borra el medidor de nivel. Si el medidor continúa mostrando un valor distinto de cero después de hacer clic en "Off", el estado del radio aún no se ha sincronizado; el botón se actualizará nuevamente una vez que el radio confirme que el flujo fue eliminado.

## Solución de problemas

- **El botón muestra "Off" pero inmediatamente vuelve a "On"**: El radio puede estar restaurando un estado de flujo persistido al reconectarse. Espere a que se complete el retardo de configuración de sesión de 1.5 segundos, luego haga clic en "On" para deshabilitar el flujo nuevamente.
- **El medidor de nivel no se restablece a 0 después de deshabilitar**: La confirmación de eliminación del flujo del radio aún no ha llegado. El medidor se restablecerá una vez que el radio informe que el flujo ya no existe.

## Relacionados

- [Enable an IQ stream for external SDR software](enable-an-iq-stream-for-external-sdr-software.md)
- [Monitor the RMS level of each IQ stream](monitor-the-rms-level-of-each-iq-stream.md)
- [Pick the IQ sample rate (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
