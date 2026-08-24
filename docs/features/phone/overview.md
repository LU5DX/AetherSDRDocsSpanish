# Descripción general de Phone

El applet Phone proporciona controles de transmisión de voz para AM, VOX, compuerta de ruido y filtrado de audio de TX. Úselo para configurar cómo AetherSDR maneja su audio transmitido antes de que llegue a la FLEX-8600.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Abra el Applet Panel si no está visible. Use `View > Applet Panel` para mostrarlo y luego haga clic en el botón de bandeja **PHNE** para mostrar el applet Phone.

## Cómo funciona

El applet Phone está organizado en cuatro áreas funcionales:

**Nivel de portadora AM** establece la potencia de portadora para el modo de transmisión AM. El control deslizante **AM Carrier** va de 0 a 100 y muestra su valor actual como una etiqueta de porcentaje (por ejemplo, "48") a la derecha del control.

**VOX (transmisión activada por voz)** tiene tres controles. El botón de alternancia **VOX** activa o desactiva el VOX. Cuando el VOX está activado, el control deslizante **VOX level** (0–100) establece el umbral de audio que activa la transmisión, mostrado como etiqueta de porcentaje. El control deslizante **Delay** (0–100) establece el tiempo de retención: cuánto tiempo permanece la radio en transmisión después de que su voz cae por debajo del umbral antes de volver a recepción.

**DEXP (expansor descendente / compuerta de ruido)** suprime el ruido de fondo durante las pausas de transmisión. El botón de alternancia **DEXP** lo activa o lo desactiva. El control deslizante **DEXP threshold** (0–100, predeterminado 0) establece el umbral de la compuerta, mostrado como etiqueta de porcentaje. Los comandos DEXP se envían directamente a la radio; no se usa persistencia local. Tenga en cuenta que DEXP no funciona en el firmware v1.4.0.0: la radio devuelve el error 0x5000002D cuando se emite un comando DEXP.

**Filtro de audio TX** da forma a la banda de paso del audio transmitido. **Low Cut** ajusta el corte de baja frecuencia del filtro TX (predeterminado 50 Hz, rango desde 0 Hz hasta 50 Hz por debajo del valor de corte alto actual, en pasos de 50 Hz). **High Cut** ajusta el corte de alta frecuencia (predeterminado 3300 Hz, rango desde 50 Hz por encima del valor de corte bajo actual hasta 10000 Hz, en pasos de 50 Hz). Use los botones **<** y **>** en cada control o la rueda del mouse para cambiar el valor.

Cada paso se ajusta al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar 50 Hz al valor actual. Por ejemplo, si el valor actual de corte bajo es 87 Hz, al presionar **>** se mueve a 100 Hz y al presionar **<** se mueve a 50 Hz. Esto significa que una sola pulsación de botón corregirá un valor que no sea múltiplo de 50 a la cuadrícula antes de continuar avanzando por ella. Cuando la radio publica una lista de pasos explícita para los pasos del filtro, los botones de paso respetan esa lista en su lugar.

## Qué hace cada control

| Control        | Tipo                                                                                                                               | Predeterminado                                              |
|----------------|------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------|
| AM Carrier     | Control deslizante: establece el nivel de potencia de portadora AM, 0–100.                                                         | —                                                           |
| VOX            | Botón de alternancia: activa o desactiva la transmisión activada por voz.                                                          | —                                                           |
| VOX level      | Control deslizante: establece el umbral de activación de VOX, 0–100.                                                               | —                                                           |
| Delay          | Control deslizante: establece el tiempo de retención de VOX antes de volver a recepción, 0–100.                                    | —                                                           |
| DEXP           | Botón de alternancia: activa o desactiva el expansor descendente (compuerta de ruido).                                             | —                                                           |
| DEXP threshold | Control deslizante: establece el umbral de la compuerta DEXP, 0–100.                                                               | 0                                                           |
| Low Cut < / >  | Campo de texto: < / > o rueda del mouse ajusta el corte bajo del filtro TX en 50 Hz (o según la cuadrícula de pasos publicada por la radio). | 50 Hz                                                      |
| High Cut < / > | Campo de texto: < / > o rueda del mouse ajusta el corte alto del filtro TX en 50 Hz (o según la cuadrícula de pasos publicada por la radio). | 3300 Hz                                                    |

### Entrada numérica directa

Haga doble clic en el valor de **Low Cut** o **High Cut** para abrir un campo de texto editable y escriba un valor exacto en Hz. El campo acepta cualquier número entero dentro de los límites que la radio reporta para ese borde del filtro.

- Un valor escrito se trata como una solicitud de ese valor exacto, no como un paso. Si escribe un valor fuera de rango, se rechaza y se restaura el valor anterior; el campo nunca limita un número escrito.
- Los botones de paso, en cambio, siempre se limitan en el límite del rango, porque un paso es una solicitud de moverse un incremento y detenerse en el límite es el único resultado sensato.
- En radios que publican una cuadrícula de pasos discreta, un valor escrito debe estar en esa cuadrícula; las entradas fuera de la cuadrícula se rechazan. En radios que aceptan valores continuos en Hz, se acepta cualquier número entero dentro del rango.
- Si escribe un valor que cruzaría el borde opuesto del filtro (por ejemplo, escribir un corte bajo por encima del corte alto actual), la entrada se rechaza en lugar de empujar el otro borde fuera del camino. Esto mantiene los botones de paso como la única forma de mover deliberadamente un borde de la banda de paso.

## Consejos

- Los controles deslizantes **AM Carrier**, **VOX level** y **DEXP threshold** muestran su valor actual como una etiqueta numérica (por ejemplo, "48" para AM Carrier, "70" para VOX level, "30" para DEXP threshold) a la derecha del control.
- Puede ajustar **Low Cut** y **High Cut** con la rueda del mouse al pasar el cursor sobre la pantalla de valores, además de usar los botones **<** y **>**.
- Debido a que los botones **<** y **>** se ajustan a la cuadrícula de 50 Hz, presionar un botón una vez desde un valor fuera de la cuadrícula corrige a la cuadrícula en lugar de moverse un paso completo más allá. Este es el comportamiento esperado.
- La entrada numérica directa es la forma de solicitar una frecuencia de filtro exacta. Los botones de paso se ajustan a la cuadrícula, por lo que pueden aterrizar en un valor ligeramente diferente al que intentaba solicitar.
- El applet Phone ahora respeta el tema activo para sus colores. El estilo de controles deslizantes y botones sigue los colores primario y de acento definidos en su tema elegido. Las pistas del control deslizante AM Carrier y los controles VOX level, Delay y VOX level usan el color de acento primario para sus manijas.

## Relacionado

- [Adjust AM carrier power for AM transmit](adjust-am-carrier-power-for-am-transmit.md)
- [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md)
- [Tune VOX hang time](tune-vox-hang-time.md)
- [Set the TX audio low-cut frequency](set-the-tx-audio-low-cut-frequency.md)
- [Set the TX audio high-cut frequency](set-the-tx-audio-high-cut-frequency.md)
