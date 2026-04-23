# Activar un flujo IQ para software SDR externo

El applet DAX IQ permite activar uno o más de los cuatro flujos de datos IQ de su radio Flex. El software SDR externo puede entonces recibir muestras IQ en bruto del radio a través de la red local.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio Flex. Si no está conectado, abra primero `Settings > Connect to Radio...`.
- El panel de applets debe estar visible. Si no lo está, abra `View > Applet Panel`.

## Pasos

1. Haga clic en el botón de bandeja **IQ** en la barra lateral derecha para abrir el applet DAX IQ.
2. Localice la fila del canal que desea: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
3. Seleccione una tasa de muestreo en el cuadro combinado de tasa de esa fila. El valor predeterminado es **48k**. Consulte [Elegir la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md) para orientación sobre cómo elegir una tasa.
4. Haga clic en el botón **Off** situado a la derecha de esa fila. El botón cambia a **On** y se resalta para confirmar que el flujo está activo.
5. Configure su software SDR externo para recibir el flujo IQ en el número de canal DAX IQ correspondiente.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Comportamiento |
|---|---|---|---|
| Cuadro combinado de tasa (IQ 1–4) | 48k | 24k, 48k, 96k, 192k | Establece la tasa de muestreo enviada al radio para este canal. Se sincroniza con la tasa reportada por el radio cuando un flujo está activo. |
| Medidor de nivel (IQ 1–4) | 0 | 0–100 | Muestra el nivel RMS del flujo IQ activo. Se restablece a 0 cuando el flujo se deshabilita o el radio se desconecta. |
| Botón de alternancia Off/On (IQ 1–4) | Off | Off, On | Habilita o deshabilita el flujo IQ de ese canal. |

## Consejos

- Los flujos IQ son por sesión y el radio no los conserva. Tras reconectarse, todos los botones se restablecen a **Off** y debe volver a habilitar los flujos que necesite.
- Que el medidor de nivel suba por encima de 0 después de hacer clic en **On** confirma que los datos IQ están fluyendo. Si permanece en 0, es posible que su software externo aún no haya abierto el flujo.
- Desplazarse por el panel de applets no cambia accidentalmente el cuadro combinado de tasa; debe hacer clic en el cuadro combinado para abrirlo antes de que la rueda de desplazamiento surta efecto.

## Resolución de problemas

- **El botón muestra On pero el medidor de nivel permanece en 0** — El radio ha aceptado la solicitud de flujo, pero ningún cliente está consumiendo los datos. Verifique que su software SDR externo esté en ejecución y conectado al canal DAX IQ correcto.
- **El cuadro combinado de tasa vuelve a un valor diferente tras habilitarlo** — El radio reportó una tasa de muestreo diferente para ese canal. El cuadro combinado se sincroniza con la tasa reportada por el radio cuando un flujo se activa; seleccione la tasa deseada nuevamente antes de hacer clic en **On**, o ajústela en su software externo.
- **El botón de bandeja IQ no es visible en la barra lateral** — Es posible que el panel de applets esté oculto. Abra `View > Applet Panel` para mostrarlo y luego haga clic en el botón de bandeja **IQ**.

## Relacionado

- [Descripción general de DAX IQ](overview.md)
- [Elegir la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Supervisar el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
