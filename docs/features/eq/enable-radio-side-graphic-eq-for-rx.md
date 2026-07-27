# Habilitar el ecualizador gráfico del lado de la radio para RX

Abra el applet Equalizer y active la ruta del ecualizador de RX para que la radio Flex aplique un ecualizador gráfico de 8 bandas al audio recibido dentro de la propia radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El applet EQ requiere una conexión activa a la radio.
- Si el panel del applet no está visible, actívelo mediante `View > Applet Panel`.

## Pasos

1. Haga clic en el botón EQ de la barra lateral derecha para abrir el panel Equalizer.
2. Haga clic en RX. El botón se resalta en azul y los deslizadores cambian a la ruta de recepción.
3. Haga clic en ON. El botón se resalta en verde. El ecualizador de RX está ahora activo en la radio.
4. Ajuste los deslizadores de banda (63, 125, 250, 500, 1k, 2k, 4k, 8k) según sea necesario. Cada deslizador ajusta su banda de −10 a +10 dB. La etiqueta de valor debajo de cada deslizador se actualiza en vivo. Mientras arrastra un deslizador, aparece un mensaje emergente que muestra el valor actual con un signo (+ o −) seguido de " dB". El mensaje emergente permanece brevemente después de soltar el deslizador.

## Función de cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Apagado (desmarcado) | Encendido / Apagado | Activa o desactiva el ecualizador para la ruta seleccionada actualmente. Resaltado en verde cuando está activado. |
| RX | Botón de alternancia | Apagado (desmarcado) | — | Selecciona la ruta de recepción para visualización y edición. Resaltado en azul cuando está activo. Mutuamente excluyente con TX. |
| TX | Botón de alternancia | Encendido (marcado) | — | Selecciona la ruta de transmisión. El applet se abre en la vista TX de forma predeterminada. |
| Botón Reset (arco) | Botón pulsador | — | — | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Tooltip: "Restablecer todas las bandas a 0 dB". |
| 63 | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada. El mensaje emergente de arrastre muestra el valor en dB con signo. |
| 125 | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. El mensaje emergente de arrastre muestra el valor en dB con signo. |
| 250 | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. El mensaje emergente de arrastre muestra el valor en dB con signo. |
| 500 | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. El mensaje emergente de arrastre muestra el valor en dB con signo. |
| 1k | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. El mensaje emergente de arrastre muestra el valor en dB con signo. |
| 2k | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. El mensaje emergente de arrastre muestra el valor en dB con signo. |
| 4k | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. El mensaje emergente de arrastre muestra el valor en dB con signo. |
| 8k | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. El mensaje emergente de arrastre muestra el valor en dB con signo. |
| Escala +10 / 0 / −10 dB | Indicador | — | −10 a +10 dB | Etiquetas de referencia en el lado izquierdo de la columna de deslizadores que muestran el rango de la escala. |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Etiqueta de valor por banda | −10 a +10 | Valor en dB en vivo de cada deslizador, mostrado debajo de su manija. Mientras arrastra, un mensaje emergente cerca de la manija muestra el valor con signo (por ejemplo, "+3 dB" o "−5 dB"). |

## Consejos

- El applet recuerda si usó la vista RX o TX por última vez y restaura esa selección al reabrirse. En el primer inicio, se abre mostrando la ruta TX. Haga clic en RX antes de ajustar los deslizadores para asegurarse de que está editando las bandas de recepción, no las de transmisión.
- Para comparar rápidamente el audio ecualizado y el audio plano, haga clic en ON repetidamente mientras escucha. La radio aplica o elimina el EQ de inmediato.
- Para empezar de nuevo, haga clic en el botón Reset (arco). Todas las bandas de RX vuelven a 0 dB con un solo clic.
- Mientras arrastra cualquier deslizador de EQ, aparece un mensaje emergente que muestra el valor con signo (por ejemplo, "+3 dB" o "-5 dB") cerca de la manija del deslizador. El mensaje se desvanece después de soltar el botón del ratón, dándole tiempo para leer el valor final.
- Para ajustar un deslizador con el teclado, use las teclas de flecha estándar cuando el applet EQ tenga el foco. Cuando mueva un deslizador con el teclado, aparece un mensaje emergente que muestra el nuevo valor, igual que después de un arrastre con el ratón. Este mensaje permanece brevemente para que pueda leer el valor antes de que se desvanezca.
- Los colores de los deslizadores y el fondo del applet se adaptan al tema activo. La manija del EQ usa el color de acento del tema para mayor visibilidad.

## Solución de problemas

- **El botón ON no responde** — Confirme que AetherSDR está conectado a la radio. El applet EQ requiere una conexión activa a la radio para enviar cambios.
- **Los cambios en los deslizadores afectan a TX en lugar de RX** — TX es la vista predeterminada. Haga clic en RX primero para cambiar el applet a la ruta de recepción antes de editar las bandas.
- **Los colores de los deslizadores no coinciden con el tema** — Reinicie AetherSDR para asegurarse de que todos los cambios de tema se apliquen. Los deslizadores de EQ usan los tokens de tema `color.slider.*` para una apariencia consistente.

## Relacionado

- [Descripción general del ecualizador (gráfico)](overview.md)
- [Habilitar el ecualizador gráfico del lado de la radio para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Aumentar o reducir bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Restablecer todas las bandas a plano con un solo clic](reset-all-bands-to-flat-with-one-click.md)
- [Cambiar entre dar forma al audio de RX y al audio de TX](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Comparar EQ activado vs EQ desactivado rápidamente con el botón ON](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
