# Descripción general de Phone

El applet Phone proporciona controles de transmisión de voz para AM, VOX, puerta de ruido y filtrado de audio de TX. Úselo para configurar cómo AetherSDR maneja su audio transmitido antes de que llegue a la FLEX-8600.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión activa con la radio.
- Abra el Applet Panel si aún no está visible. Use `View > Applet Panel` para mostrarlo, luego haga clic en el botón de la bandeja **PHNE** para mostrar el applet Phone.

## Cómo funciona

El applet Phone está organizado en cuatro áreas funcionales:

**AM carrier level** establece la potencia de portadora para el modo de transmisión AM. El deslizador **AM Carrier** va de 0 a 100 y muestra su valor actual como una etiqueta de porcentaje (p. ej., "48%") a la derecha del deslizador.

**VOX (voice-operated transmit)** tiene tres controles. El botón de alternancia **VOX** activa o desactiva VOX. Cuando VOX está activado, el deslizador **VOX level** (0–100) establece el umbral de audio que activa la transmisión, mostrado como una etiqueta de porcentaje. El deslizador **Delay** (0–100) establece el tiempo de retención: cuánto tiempo permanece la radio en transmisión después de que su voz caiga por debajo del umbral antes de volver a recepción.

**DEXP (downward expander)** es una puerta de ruido diseñada para suprimir el ruido de fondo durante las pausas de transmisión. El botón de alternancia **DEXP** lo activa o desactiva, y su estado se guarda como `DexpEnabled`. El deslizador **DEXP threshold** (0–100, valor predeterminado 0) establece el umbral de la puerta, mostrado como una etiqueta de porcentaje, y su valor se guarda como `DexpLevel`. **Nota:** Ambos controles DEXP no son funcionales en la versión de firmware v1.4.0.0: la radio devuelve el error 0x5000002D. Los controles están presentes en la interfaz, pero no tienen efecto hasta que una actualización de firmware resuelva el problema.

**TX audio filter** da forma a la banda pasante del audio transmitido. **Low Cut** ajusta el corte de baja frecuencia del filtro de TX (valor predeterminado 50 Hz, rango desde 0 Hz hasta 50 Hz por debajo del valor actual de corte alto, en pasos de 50 Hz). **High Cut** ajusta el corte de alta frecuencia (valor predeterminado 3300 Hz, rango desde 50 Hz por encima del valor actual de corte bajo hasta 10000 Hz, en pasos de 50 Hz). Use los botones **<** y **>** de cada control o la rueda del ratón para cambiar el valor.

Cada paso se ajusta al múltiplo más cercano de 50 Hz en la dirección elegida, en lugar de sumar o restar 50 Hz del valor actual. Por ejemplo, si el valor actual de corte bajo es 87 Hz, presionar **>** lo mueve a 100 Hz y presionar **<** lo mueve a 50 Hz. Esto significa que una sola pulsación de botón corregirá un valor que no sea múltiplo de 50 a la cuadrícula antes de continuar avanzando por ella.

## Qué hace cada control

| Control        | Tipo           | Valor predeterminado |
|----------------|----------------|----------------------|
| AM Carrier     | Deslizador     | —                    |
| VOX            | Botón de alternancia | —                |
| VOX level      | Deslizador     | —                    |
| Delay          | Deslizador     | —                    |
| DEXP           | Botón de alternancia | —                |
| DEXP threshold | Deslizador     | 0                    |
| Low Cut < / >  | Spinbox        | 50 Hz                |
| High Cut < / > | Spinbox        | 3300 Hz              |

## Consejos

- Los deslizadores **AM Carrier**, **VOX level** y **DEXP threshold** muestran su valor actual como una etiqueta de porcentaje (p. ej., "48%" para AM Carrier, "70%" para VOX level, "30%" para DEXP threshold) a la derecha del deslizador.
- Los controles **DEXP** y **DEXP threshold** guardan sus valores localmente mediante `DexpEnabled` y `DexpLevel`, aunque la radio rechace los comandos en la versión de firmware v1.4.0.0. Los valores guardados se aplicarán automáticamente si una versión futura del firmware resuelve el error.
- Puede ajustar **Low Cut** y **High Cut** con la rueda del ratón al pasar el cursor sobre la visualización del valor, además de usar los botones **<** y **>**.
- Debido a que los botones **<** y **>** se ajustan a la cuadrícula de 50 Hz, presionar un botón una vez desde un valor fuera de la cuadrícula corrige a la cuadrícula en lugar de moverse un paso completo más allá. Este es el comportamiento esperado.
- El applet Phone ahora respeta el tema activo para sus colores. El estilo de los deslizadores y botones sigue los colores primario y de acento definidos en su tema elegido. Las pistas del deslizador AM Carrier y los deslizadores VOX level, Delay y VOX level utilizan el color de acento primario para sus manijas.

## Solución de problemas

- **El botón de alternancia DEXP no tiene efecto** — La versión de firmware v1.4.0.0 devuelve el error 0x5000002D para los comandos DEXP. Esta es una limitación conocida del firmware. No hay ninguna solución alternativa disponible en este momento.

## Relacionado

- [Adjust AM carrier power for AM transmit](adjust-am-carrier-power-for-am-transmit.md)
- [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md)
- [Tune VOX hang time](tune-vox-hang-time.md)
- [Set the TX audio low-cut frequency](set-the-tx-audio-low-cut-frequency.md)
- [Set the TX audio high-cut frequency](set-the-tx-audio-high-cut-frequency.md)
