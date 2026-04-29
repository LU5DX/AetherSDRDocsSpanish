# Descripción general de Phone

El applet Phone proporciona controles de TX de voz para AM, VOX, puerta de ruido y filtrado de audio en TX. Úselo para configurar cómo AetherSDR procesa el audio transmitido antes de que llegue al FLEX-8600.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Abra el panel de applets si no está visible. Use `View > Applet Panel` para mostrarlo y, a continuación, haga clic en el botón de bandeja **PHNE** para mostrar el applet Phone.

## Cómo funciona

El applet Phone está organizado en cuatro áreas funcionales:

**AM carrier level** establece la potencia de portadora para el modo de transmisión AM. El control deslizante **AM Carrier** va de 0 a 100 y muestra su valor actual como número a la derecha del control.

**VOX (transmisión activada por voz)** tiene tres controles. El botón de alternancia **VOX** habilita o deshabilita el VOX. Cuando el VOX está activado, el control deslizante **VOX level** (0–100) establece el umbral de audio que activa la transmisión. El control deslizante **Delay** (0–100) establece el tiempo de retención: cuánto tiempo permanece la radio en transmisión después de que su voz cae por debajo del umbral antes de volver a recepción.

**DEXP (expansor descendente)** es una puerta de ruido diseñada para suprimir el ruido de fondo durante las pausas de transmisión. El botón de alternancia **DEXP** habilita o deshabilita esta función, con persistencia en `DexpEnabled`. El control deslizante **DEXP threshold** (0–100, valor predeterminado 0) establece el umbral de la puerta, con persistencia en `DexpLevel`. **Nota:** Ambos controles DEXP no son funcionales en el firmware v1.4.0.0 — la radio devuelve el error 0x5000002D. Los controles están presentes en la interfaz, pero no tienen efecto hasta que una actualización de firmware resuelva el problema.

**TX audio filter** da forma a la banda de paso del audio transmitido. **Low Cut** ajusta la frecuencia de corte inferior del filtro TX (valor predeterminado 50 Hz, rango de 0 Hz hasta 50 Hz por debajo del valor de corte alto actual, en pasos de 50 Hz). **High Cut** ajusta la frecuencia de corte superior (valor predeterminado 3300 Hz, rango desde 50 Hz por encima del valor de corte bajo actual hasta 10000 Hz, en pasos de 50 Hz). Use los botones **<** y **>** de cada control o la rueda del ratón para cambiar el valor.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Clave de persistencia |
|---|---|---|---|---|
| AM Carrier | Control deslizante | — | 0–100 | — |
| VOX | Botón de alternancia | — | Activado/Desactivado | — |
| VOX level | Control deslizante | — | 0–100 | — |
| Delay | Control deslizante | — | 0–100 | — |
| DEXP | Botón de alternancia | — | Activado/Desactivado | `DexpEnabled` |
| DEXP threshold | Control deslizante | 0 | 0–100 | `DexpLevel` |
| Low Cut < / > | Cuadro de giro | 50 Hz | 0 a (corte alto − 50 Hz), paso 50 Hz | — |
| High Cut < / > | Cuadro de giro | 3300 Hz | (corte bajo + 50 Hz) a 10000 Hz, paso 50 Hz | — |

## Sugerencias

- Los controles **DEXP** y **DEXP threshold** guardan sus valores localmente mediante `DexpEnabled` y `DexpLevel`, aunque la radio rechace los comandos en el firmware v1.4.0.0. Los valores guardados se aplicarán automáticamente si una versión futura del firmware resuelve el error.
- Puede ajustar **Low Cut** y **High Cut** con la rueda del ratón al pasar el cursor sobre el indicador de valor, además de usar los botones **<** y **>**.

## Solución de problemas

- **El interruptor DEXP no tiene efecto** — El firmware v1.4.0.0 devuelve el error 0x5000002D para los comandos DEXP. Esta es una limitación conocida del firmware. Por el momento no existe solución alternativa.

## Relacionados

- [Ajustar la potencia de portadora AM para transmisión AM](adjust-am-carrier-power-for-am-transmit.md)
- [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Ajustar el tiempo de retención del VOX](tune-vox-hang-time.md)
- [Establecer la frecuencia de corte inferior del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte superior del audio TX](set-the-tx-audio-high-cut-frequency.md)
