# Descripción general de DAX IQ

El applet DAX IQ le permite habilitar hasta cuatro flujos de datos IQ independientes desde el FLEX-8600, establecer la tasa de muestreo de cada flujo y monitorear su nivel de señal en tiempo real. Use estos flujos para alimentar software SDR externo con muestras IQ en bruto provenientes del radio.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El applet DAX IQ requiere una conexión activa con el radio.
- El panel del applet debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

El applet DAX IQ proporciona cuatro canales IQ independientes, numerados IQ 1 a IQ 4. Cada canal se controla de forma independiente y los cuatro comparten el mismo diseño dentro del applet.

Los flujos IQ son exclusivos de la sesión. El radio no conserva el estado de los flujos entre conexiones. Cada vez que AetherSDR se conecta al radio, los cuatro canales se inician en el estado Off.

Cuando un flujo está activo, el combo de tasa se sincroniza con la tasa de muestreo reportada por el radio. El medidor de nivel se actualiza en tiempo real basándose en el nivel RMS de los datos IQ entrantes.

**Apertura del applet:** El applet DAX IQ está oculto por defecto. Haga clic en el botón IQ de la barra lateral derecha para mostrarlo u ocultarlo.

## Qué hace cada control

Cada uno de los cuatro canales IQ (IQ 1, IQ 2, IQ 3, IQ 4) dispone de los siguientes controles:

| Control | Qué hace | Valor predeterminado | Valores válidos |
|---|---|---|---|
| Combo de tasa | Establece la tasa de muestreo del flujo IQ. Cuando el flujo está activo, se sincroniza con la tasa reportada por el radio. | 48k | 24k (24000 Hz), 48k (48000 Hz), 96k (96000 Hz), 192k (192000 Hz) |
| Medidor de nivel | Muestra el nivel RMS del flujo IQ en tiempo real, escalado de 0 a 100. Se restablece a 0 cuando el flujo se deshabilita o el radio se desconecta. | 0 | 0–100 |
| Botón Off / On | Habilita o deshabilita el flujo IQ de ese canal. El texto del botón indica el estado actual: "Off" cuando está inactivo, "On" cuando está activo. | Off | Off, On |

Ninguno de estos controles se almacena en una clave de configuración. El estado y la tasa del flujo se mantienen en el radio únicamente durante la sesión.

## Consejos

- Establezca la tasa de muestreo antes de habilitar un flujo. Una vez que el flujo esté activo, el combo de tasa reflejará la tasa confirmada por el radio.
- Las tasas de muestreo más altas (96k, 192k) consumen más ancho de banda de red. Use la tasa más baja que satisfaga los requisitos de su software.
- Si desplaza el panel del applet con la rueda del ratón, los combos de tasa no cambiarán de valor accidentalmente — el applet utiliza controles protegidos que ignoran los eventos de desplazamiento a menos que el menú desplegable esté abierto.

## Solución de problemas

- **Todos los canales muestran Off después de reconectarse al radio** — los flujos IQ son exclusivos de la sesión y el radio no los conserva. Vuelva a habilitar los canales que necesite después de cada conexión.
- **El medidor de nivel permanece en 0 con el flujo On** — confirme que su software SDR externo haya abierto el flujo IQ. El medidor solo muestra un nivel cuando los datos están siendo consumidos activamente.
- **El combo de tasa vuelve a su valor anterior después de cambiarlo** — si el flujo ya está activo, el radio puede reportar su propia tasa de vuelta, provocando que el combo se sincronice. Deshabilite el flujo, cambie la tasa y luego vuelva a habilitarlo.

## Temas relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
