# Deshabilitar un flujo IQ para liberar ancho de banda

Cada flujo IQ activo consume ancho de banda del radio y recursos de procesamiento. Use este procedimiento para desactivar un flujo que ya no necesita.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El applet DAX IQ debe estar visible. Si no lo está, haga clic en el botón de bandeja **IQ** de la barra lateral derecha para mostrarlo.
- Identifique qué canal (IQ 1–4) desea deshabilitar verificando cuál botón de alternancia muestra **On**.

## Pasos

1. Localice la fila del canal que desea deshabilitar (IQ 1, IQ 2, IQ 3 o IQ 4).
2. Haga clic en el botón **On** ubicado en el extremo derecho de esa fila.
3. La etiqueta del botón cambia a **Off**, el estilo del botón se atenúa y el medidor de nivel se reinicia a 0.

El flujo queda cerrado en el radio. El radio no conserva el estado de los flujos entre sesiones; AetherSDR registra su elección en `DaxIqEnabled1` hasta `DaxIqEnabled4` para poder restaurar el mismo estado cuando vuelva a conectarse.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| **IQ 1..4 Off/On** (botón de alternancia) | Off | Al hacer clic mientras muestra **On**, envía una solicitud de deshabilitación al radio, restablece la etiqueta a **Off** y borra el medidor de nivel. |
| **IQ 1..4 meter** (medidor de nivel) | 0 | Muestra el nivel RMS del flujo (0–100). Se reinicia a 0 cuando el flujo se deshabilita o el radio se desconecta. |
| **IQ 1..4 rate** (cuadro combinado) | 48k | Selecciona la tasa de muestreo: 24k, 48k, 96k o 192k. Se sincroniza con la tasa reportada por el radio mientras el flujo está activo. Se guarda por canal en `DaxIqRate1` hasta `DaxIqRate4`. |

## Consejos

- Deshabilitar un flujo no modifica su tasa de muestreo guardada. La tasa que tenía seleccionada seguirá configurada al volver a habilitar el flujo.
- Si se desconecta y vuelve a conectarse, AetherSDR espera brevemente antes de rehabilitar los flujos que estaban activos. Si desea que un flujo permanezca inactivo tras la reconexión, asegúrese de que su botón muestre **Off** antes de desconectarse — las configuraciones `DaxIqEnabled1`–`DaxIqEnabled4` controlan qué flujos se restauran.
- Deshabilitar los flujos que no estén en uso antes de cambiar las tasas de muestreo en los flujos activos reduce la probabilidad de que el radio rechace el cambio de tasa.

## Solución de problemas

- **El botón muestra Off pero la aplicación SDR externa sigue reportando un flujo** — Es posible que el flujo en el lado del radio aún no haya sido eliminado. Desconéctese y vuelva a conectarse al radio para forzar un estado de sesión limpio.
- **El botón vuelve a On inmediatamente después de hacer clic en Off** — El radio rechazó la solicitud de deshabilitación. Verifique su conexión de red y confirme que ningún otro cliente SmartSDR tenga el flujo bloqueado.

## Temas relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Descripción general de DAX IQ](overview.md)
