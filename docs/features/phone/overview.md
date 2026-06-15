# Descripción general de Phone

El applet Phone proporciona controles de transmisión de voz para AM, VOX, compuerta de ruido y filtrado de audio de TX. Úselo para configurar cómo AetherSDR maneja su audio transmitido antes de que llegue a la FLEX-8600.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión activa a la radio.
- Abra el Applet Panel si aún no está visible. Use `View > Applet Panel` para mostrarlo, luego haga clic en el botón de bandeja **PHNE** para visualizar el applet Phone.

## Cómo funciona

El applet Phone está organizado en cuatro áreas funcionales:

**AM Carrier Level** establece la potencia de portadora para el modo de transmisión AM. El deslizador **AM Carrier** va de 0 a 100 y muestra su valor actual como una etiqueta de porcentaje (p. ej., "48") a la derecha del deslizador.

**VOX (transmisión activada por voz)** tiene tres controles. El botón de alternancia **VOX** activa o desactiva VOX. Cuando VOX está activado, el deslizador **VOX level** (0–100) establece el umbral de audio que dispara la transmisión, mostrado como una etiqueta de porcentaje. El deslizador **Delay** (0–100) establece el tiempo de retención — cuánto tiempo permanece la radio en transmisión después de que su voz cae por debajo del umbral antes de volver a recepción.

**DEXP (expansor descendente / compuerta de ruido)** suprime el ruido de fondo durante las pausas de transmisión. El botón de alternancia **DEXP** lo activa o desactiva. El deslizador **DEXP threshold** (0–100, valor predeterminado 0) establece el umbral de la compuerta, mostrado como una etiqueta de porcentaje. Los comandos DEXP se envían directamente a la radio; no se utiliza persistencia local.

**TX Audio Filter** da forma a la banda de paso del audio transmitido. **Low Cut** ajusta el corte de baja frecuencia del filtro TX (valor predeterminado 50 Hz, rango desde 0 Hz hasta 50 Hz por debajo del valor actual de corte alto, en pasos de 50 Hz). **High Cut** ajusta el corte de alta frecuencia (valor predeterminado 3300 Hz, rango desde 50 Hz por encima del valor actual de corte bajo hasta 10000 Hz, en pasos de 50 Hz). Use los botones **<** y **>** en cada control o la rueda del ratón para cambiar el valor.

Cada paso se ajusta al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar 50 Hz del valor actual. Por ejemplo, si el valor actual de corte bajo es 87 Hz, presionar **>** lo mueve a 100 Hz y presionar **<** lo mueve a 50 Hz. Esto significa que una sola pulsación de botón corregirá un valor que no sea múltiplo de 50 a la cuadrícula antes de continuar avanzando por ella.

## Qué hace cada control

| Control         | Tipo              | Valor predeterminado |
|-----------------|-------------------|----------------------|
| AM Carrier      | Deslizador        | —                    |
| VOX             | Botón de alternancia | —                  |
| VOX level       | Deslizador        | —                    |
| Delay           | Deslizador        | —                    |
| DEXP            | Botón de alternancia | —                  |
| DEXP threshold  | Deslizador        | 0                    |
| Low Cut < / >   | Spinbox           | 50 Hz                |
| High Cut < / >  | Spinbox           | 3300 Hz              |

## Consejos

- Los deslizadores **AM Carrier**, **VOX level** y **DEXP threshold** muestran su valor actual como una etiqueta numérica (p. ej., "48" para AM Carrier, "70" para VOX level, "30" para DEXP threshold) a la derecha del deslizador.
- Puede ajustar **Low Cut** y **High Cut** con la rueda del ratón al pasar el cursor sobre la visualización del valor, además de usar los botones **<** y **>**.
- Debido a que los botones **<** y **>** se ajustan a la cuadrícula de 50 Hz, presionar un botón una vez desde un valor fuera de la cuadrícula lo corrige a la cuadrícula en lugar de moverlo un paso completo más allá. Este es el comportamiento esperado.
- El applet Phone ahora respeta el tema activo para sus colores. El estilo de los deslizadores y botones sigue los colores primarios y de acento definidos en su tema elegido. Las pistas del deslizador AM Carrier y los deslizadores VOX level, Delay y VOX level utilizan el color de acento primario para sus manijas.

## Relacionados

- [Adjust AM carrier power for AM transmit](adjust-am-carrier-power-for-am-transmit.md)
- [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md)
- [Tune VOX hang time](tune-vox-hang-time.md)
- [Set the TX audio low-cut frequency](set-the-tx-audio-low-cut-frequency.md)
- [Set the TX audio high-cut frequency](set-the-tx-audio-high-cut-frequency.md)
