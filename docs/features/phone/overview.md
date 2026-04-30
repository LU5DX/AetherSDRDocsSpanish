# Descripción general de Phone

El applet Phone proporciona controles de TX de voz para AM, VOX, compuerta de ruido y filtrado de audio TX. Úselo para configurar cómo AetherSDR maneja su audio transmitido antes de que llegue a la FLEX-8600.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Abra el Panel de Applets si aún no está visible. Use `View > Applet Panel` para mostrarlo y, a continuación, haga clic en el botón de bandeja **PHNE** para mostrar el applet Phone.

## Cómo funciona

El applet Phone está organizado en cuatro áreas funcionales:

**AM carrier level** establece la potencia del portador para el modo de transmisión AM. El regulador **AM Carrier** funciona de 0–100 y muestra su valor actual como un número a la derecha del regulador.

**VOX (transmisión activada por voz)** tiene tres controles. El botón de alternancia **VOX** activa o desactiva VOX. Cuando VOX está activado, el regulador **VOX level** (0–100) establece el umbral de audio que dispara la transmisión. El regulador **Delay** (0–100) establece el tiempo de espera — cuánto tiempo la radio permanece en transmisión después de que su voz desciende por debajo del umbral antes de volver a recepción.

**DEXP (expansor descendente)** es una compuerta de ruido diseñada para suprimir el ruido de fondo durante pausas de transmisión. El botón de alternancia **DEXP** activa o desactiva, persistido como `DexpEnabled`. El regulador **DEXP threshold** (0–100, predeterminado 0) establece el umbral de la compuerta, persistido como `DexpLevel`. **Nota:** Ambos controles DEXP no funcionan en la versión de firmware v1.4.0.0 — la radio devuelve el error 0x5000002D. Los controles están presentes en la interfaz de usuario pero no tienen efecto hasta que una actualización de firmware resuelva el problema.

**TX audio filter** forma la banda de paso de audio transmitido. **Low Cut** ajusta el corte de baja frecuencia del filtro TX (predeterminado 50 Hz, rango 0 Hz hasta 50 Hz por debajo del valor de corte alto actual, en pasos de 50 Hz). **High Cut** ajusta el corte de alta frecuencia (predeterminado 3300 Hz, rango 50 Hz por encima del valor de corte bajo actual hasta 10000 Hz, en pasos de 50 Hz). Use los botones **<** y **>** en cada control o la rueda del ratón para cambiar el valor.

## Qué hace cada control

| Control        | Tipo                                                                | Predeterminado                                                                                                                                   |
|----------------|---------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| AM Carrier     | Regulador                                                              | —                                                                                                                                         |
| VOX            | Alterna transmisión activada por voz; llama a TransmitModel::setVoxEnable. | v0.9.3: setVoxEnable ahora emite phoneStateChanged para que el panel Phone se actualice inmediatamente cuando VOX se alterna mediante atajo de teclado (#2084). |
| VOX level      | Regulador                                                              | —                                                                                                                                         |
| Delay          | Regulador                                                              | —                                                                                                                                         |
| DEXP           | Botón de alternancia                                                       | —                                                                                                                                         |
| DEXP threshold | Regulador                                                              | 0                                                                                                                                         |
| Low Cut < / >  | Cuadro giratorio                                                             | 50 Hz                                                                                                                                     |
| High Cut < / > | Cuadro giratorio                                                             | 3300 Hz                                                                                                                                     |

## Consejos

- Los controles **DEXP** y **DEXP threshold** conservan sus valores localmente a través de `DexpEnabled` y `DexpLevel` aunque la radio rechace los comandos en la versión de firmware v1.4.0.0. Los valores guardados se aplicarán automáticamente si una versión futura de firmware resuelve el error.
- Puede ajustar **Low Cut** y **High Cut** con la rueda del ratón al pasar el cursor sobre la pantalla de valor, además de usar los botones **<** y **>**.

## Solución de problemas

- **El botón de alternancia DEXP no tiene efecto** — El firmware v1.4.0.0 devuelve el error 0x5000002D para comandos DEXP. Esta es una limitación conocida del firmware. No hay solución disponible en este momento.

## Relacionado

- [Ajuste de la potencia del portador AM para transmisión AM](adjust-am-carrier-power-for-am-transmit.md)
- [Activación de VOX y establecimiento del umbral de disparo](enable-vox-and-set-trigger-threshold.md)
- [Ajuste del tiempo de espera de VOX](tune-vox-hang-time.md)
- [Establecimiento de la frecuencia de corte bajo de audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecimiento de la frecuencia de corte alto de audio TX](set-the-tx-audio-high-cut-frequency.md)
