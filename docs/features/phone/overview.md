# Resumen de Phone

El applet Phone proporciona controles de transmisión de voz para AM, VOX, compuerta de ruido y filtrado de audio de TX. Úselo para configurar cómo AetherSDR maneja su audio transmitido antes de que llegue a la FLEX-8600.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión activa con la radio.
- Abra el Panel de Applets si aún no está visible. Use `View > Applet Panel` para mostrarlo, luego haga clic en el botón de la bandeja **PHNE** para visualizar el applet Phone.

## Cómo funciona

El applet Phone está organizado en cuatro áreas funcionales:

**Nivel de portadora AM** establece la potencia de la portadora para el modo de transmisión AM. El control deslizante **AM Carrier** va de 0 a 100 y muestra su valor actual como un número a la derecha del control deslizante.

**VOX (transmisión activada por voz)** tiene tres controles. El botón de alternancia **VOX** activa o desactiva VOX. Cuando VOX está activado, el control deslizante **VOX level** (0-100) establece el umbral de audio que activa la transmisión. El control deslizante **Delay** (0-100) establece el tiempo de retención: cuánto tiempo permanece la radio en transmisión después de que su voz caiga por debajo del umbral antes de volver a recepción.

**DEXP (expansor descendente)** es una compuerta de ruido diseñada para suprimir el ruido de fondo durante las pausas de transmisión. El botón de alternancia **DEXP** lo activa o desactiva y se conserva como `DexpEnabled`. El control deslizante **DEXP threshold** (0-100, valor predeterminado 0) establece el umbral de la compuerta y se conserva como `DexpLevel`. **Nota:** Ambos controles DEXP no son funcionales en el firmware v1.4.0.0; la radio devuelve el error 0x5000002D. Los controles están presentes en la interfaz de usuario pero no tienen efecto hasta que una actualización del firmware resuelva el problema.

**Filtro de audio de TX** da forma a la banda de paso del audio transmitido. **Low Cut** ajusta la frecuencia de corte baja del filtro de TX (valor predeterminado 50 Hz, rango 0 Hz hasta 50 Hz por debajo del valor actual de corte alto, en pasos de 50 Hz). **High Cut** ajusta la frecuencia de corte alta (valor predeterminado 3300 Hz, rango 50 Hz por encima del valor actual de corte bajo hasta 10000 Hz, en pasos de 50 Hz). Use los botones **<** y **>** en cada control o la rueda del ratón para cambiar el valor.

Cada paso se ajusta al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar 50 Hz del valor actual. Por ejemplo, si el valor actual de corte bajo es 87 Hz, presionar **>** lo mueve a 100 Hz y presionar **<** lo mueve a 50 Hz. Esto significa que una sola pulsación de botón corregirá un valor que no sea múltiplo de 50 a la cuadrícula antes de continuar avanzando por ella.

## Qué hace cada control

| Control        | Tipo             | Valor predeterminado |
|----------------|------------------|----------------------|
| AM Carrier     | Control deslizante | —                  |
| VOX            | Botón de alternancia | —                |
| VOX level      | Control deslizante | —                  |
| Delay          | Control deslizante | —                  |
| DEXP           | Botón de alternancia | —                |
| DEXP threshold | Control deslizante | 0                  |
| Low Cut < / >  | Control giratorio  | 50 Hz              |
| High Cut < / > | Control giratorio  | 3300 Hz            |

## Consejos

- Los controles **DEXP** y **DEXP threshold** conservan sus valores localmente mediante `DexpEnabled` y `DexpLevel` aunque la radio rechace los comandos en el firmware v1.4.0.0. Los valores guardados se aplicarán automáticamente si una versión futura del firmware resuelve el error.
- Puede ajustar **Low Cut** y **High Cut** con la rueda del ratón al pasar el cursor sobre la visualización del valor, además de usar los botones **<** y **>**.
- Debido a que los botones **<** y **>** se ajustan a la cuadrícula de 50 Hz, presionar un botón una vez desde un valor fuera de la cuadrícula lo corrige a la cuadrícula en lugar de moverlo un paso completo más allá. Este es el comportamiento esperado.

## Solución de problemas

- **El botón de alternancia DEXP no tiene efecto**: El firmware v1.4.0.0 devuelve el error 0x5000002D para los comandos DEXP. Esta es una limitación conocida del firmware. Actualmente no hay ninguna solución alternativa disponible.

## Relacionado

- [Adjust AM carrier power for AM transmit](adjust-am-carrier-power-for-am-transmit.md)
- [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md)
- [Tune VOX hang time](tune-vox-hang-time.md)
- [Set the TX audio low-cut frequency](set-the-tx-audio-low-cut-frequency.md)
- [Set the TX audio high-cut frequency](set-the-tx-audio-high-cut-frequency.md)
