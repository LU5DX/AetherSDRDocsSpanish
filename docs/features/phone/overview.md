# Descripción general de Phone

El applet Phone proporciona controles de transmisión de voz para AM, VOX, puerta de ruido y filtrado de audio en TX. Úselo para configurar cómo AetherSDR procesa el audio transmitido antes de que llegue al FLEX-8600.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Abra el panel de applets si no está visible. Use `View > Applet Panel` para mostrarlo y luego haga clic en el botón de bandeja **PHNE** para mostrar el applet Phone.

## Cómo funciona

El applet Phone está organizado en cuatro áreas funcionales:

**Nivel de portadora AM** establece la potencia de portadora para el modo de transmisión AM. El control deslizante **AM Carrier** va de 0 a 100 y muestra su valor actual como número a la derecha del control.

**VOX (transmisión activada por voz)** tiene tres controles. El botón de alternancia **VOX** habilita o deshabilita el VOX. Cuando el VOX está activado, el control deslizante **VOX level** (0–100) establece el umbral de audio que activa la transmisión. El control deslizante **Delay** (0–100) establece el tiempo de retención — cuánto tiempo permanece el radio en transmisión después de que su voz cae por debajo del umbral antes de volver a recepción.

**DEXP (expansor descendente)** es una puerta de ruido destinada a suprimir el ruido de fondo durante las pausas en la transmisión. El botón de alternancia **DEXP** lo habilita o deshabilita, y su estado se guarda como `DexpEnabled`. El control deslizante **DEXP threshold** (0–100, valor predeterminado 0) establece el umbral de la puerta, guardado como `DexpLevel`. **Nota:** Ambos controles DEXP no funcionan en el firmware v1.4.0.0 — el radio devuelve el error 0x5000002D. Los controles están presentes en la interfaz pero no tienen efecto hasta que una actualización de firmware resuelva el problema.

**Filtro de audio TX** da forma a la banda de paso del audio transmitido. **Low Cut** ajusta la frecuencia de corte inferior del filtro TX (valor predeterminado 50 Hz, rango desde 0 Hz hasta 50 Hz por debajo del valor actual de corte superior, en pasos de 50 Hz). **High Cut** ajusta la frecuencia de corte superior (valor predeterminado 3300 Hz, rango desde 50 Hz por encima del valor actual de corte inferior hasta 10000 Hz, en pasos de 50 Hz). Use los botones **<** y **>** de cada control o la rueda del ratón para avanzar el valor.

Cada paso se ajusta al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar 50 Hz al valor actual. Por ejemplo, si el valor actual de corte inferior es 87 Hz, presionar **>** lo mueve a 100 Hz y presionar **<** lo mueve a 50 Hz. Esto significa que una sola pulsación del botón corregirá un valor que no sea múltiplo de 50 al punto de la cuadrícula antes de continuar avanzando por ella.

## Qué hace cada control

| Control        | Tipo                  | Valor predeterminado |
|----------------|-----------------------|----------------------|
| AM Carrier     | Control deslizante    | —                    |
| VOX            | Botón de alternancia  | —                    |
| VOX level      | Control deslizante    | —                    |
| Delay          | Control deslizante    | —                    |
| DEXP           | Botón de alternancia  | —                    |
| DEXP threshold | Control deslizante    | 0                    |
| Low Cut < / >  | Spinbox               | 50 Hz                |
| High Cut < / > | Spinbox               | 3300 Hz              |

## Consejos

- Los controles **DEXP** y **DEXP threshold** guardan sus valores localmente mediante `DexpEnabled` y `DexpLevel` aunque el radio rechace los comandos en el firmware v1.4.0.0. Los valores guardados se aplicarán automáticamente si una versión futura del firmware resuelve el error.
- Puede ajustar **Low Cut** y **High Cut** con la rueda del ratón al pasar el cursor sobre el indicador de valor, además de usar los botones **<** y **>**.
- Dado que los botones **<** y **>** se ajustan a la cuadrícula de 50 Hz, presionar un botón una vez desde un valor fuera de la cuadrícula lo corrige a la cuadrícula en lugar de avanzar un paso completo más allá. Este es el comportamiento esperado.

## Solución de problemas

- **El botón de alternancia DEXP no tiene efecto** — El firmware v1.4.0.0 devuelve el error 0x5000002D para los comandos DEXP. Esta es una limitación conocida del firmware. Por el momento no hay solución alternativa disponible.

## Relacionados

- [Ajustar la potencia de portadora AM para transmisión en AM](adjust-am-carrier-power-for-am-transmit.md)
- [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Ajustar el tiempo de retención del VOX](tune-vox-hang-time.md)
- [Establecer la frecuencia de corte inferior del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte superior del audio TX](set-the-tx-audio-high-cut-frequency.md)
