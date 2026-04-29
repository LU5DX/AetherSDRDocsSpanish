# Deshabilitar un flujo IQ para liberar ancho de banda

Cada flujo DAX IQ activo consume recursos DSP de la radio y ancho de banda de red. Deshabilitar un flujo que no está en uso libera esa capacidad para otras slices, flujos de audio o canales IQ.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet DAX IQ requiere una conexión activa con la radio.
- El applet DAX IQ debe estar visible. Si no lo está, haga clic en el botón IQ de la bandeja en la barra lateral derecha para mostrarlo.

## Pasos

1. Ubique la fila del canal que desea detener: IQ 1, IQ 2, IQ 3 o IQ 4.
2. Verifique que el botón de alternancia a la derecha de esa fila muestre "On". Si ya muestra "Off", el flujo ya está inactivo.
3. Haga clic en "On". La etiqueta del botón cambia a "Off", el estilo del botón se atenúa y el medidor de nivel se restablece a 0. El flujo se elimina de la radio durante esta sesión.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento | Clave persistida |
|---|---|---|---|
| IQ 1..4 Off/On | Off | Al hacer clic, alterna el flujo. Cuando se desactiva, el botón muestra "Off" y el medidor se restablece a 0. | `DaxIqEnabled1` – `DaxIqEnabled4` |
| Medidor IQ 1..4 | 0 | Muestra el nivel RMS del flujo (0–100). Se restablece a 0 cuando el flujo se deshabilita o la radio se desconecta. | — |
| Tasa IQ 1..4 | 48k | Establece la tasa de muestreo del canal (24k, 48k, 96k, 192k). No se modifica al deshabilitar el flujo. | `DaxIqRate1` – `DaxIqRate4` |

## Sugerencias

- Los flujos IQ son por sesión. La radio no conserva el estado del flujo entre conexiones. AetherSDR almacena su última elección de habilitación/deshabilitación en `DaxIqEnabled1` hasta `DaxIqEnabled4` y restaura esos flujos automáticamente aproximadamente 1.5 segundos después de reconectarse.
- Si desea que un canal permanezca desactivado después de una reconexión, deshabilitarlo aquí es suficiente: la clave persistida se establece en `False` de inmediato al hacer clic en "On" para desactivarlo.
- Deshabilitar un flujo también limpia el medidor de nivel. Si el medidor continúa mostrando un valor distinto de cero después de hacer clic en "Off", el estado de la radio aún no se ha sincronizado; el botón se actualizará nuevamente una vez que la radio confirme que el flujo fue eliminado.

## Solución de problemas

- **El botón muestra "Off" pero regresa inmediatamente a "On"** — Es posible que la radio esté restaurando un estado de flujo persistido al reconectarse. Espere a que se complete el retardo de configuración de sesión de 1.5 segundos y, a continuación, haga clic en "On" para deshabilitar el flujo nuevamente.
- **El medidor de nivel no se restablece a 0 después de deshabilitar** — La confirmación de eliminación del flujo de la radio aún no ha llegado. El medidor se restablecerá una vez que la radio informe que el flujo ya no existe.

## Relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
