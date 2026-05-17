# Ajustar el umbral de TX justo por encima del piso de ruido ambiental

Ajustar Thresh correctamente le indica a la compuerta de TX dónde termina el ruido de fondo de su sala y comienza su voz. Un umbral justo por encima del piso de ruido mantiene el soplido del micrófono y los sonidos ambientales en silencio entre transmisiones, mientras deja pasar su voz con claridad.

## Antes de comenzar

- La etapa de compuerta de TX debe estar habilitada en el widget CHAIN del lado de TX. Si no está habilitada, el applet se oculta y los cambios en las perillas no tienen efecto. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).
- Abra el subcontenedor "Aetherial TX Gate" dentro del contenedor padre Aetherial Audio (TXDSP), o haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante "Aetherial Gate — TX".
- Cuando la etapa de compuerta está puenteada, todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente al 55% del brillo completo). Esto es solo un indicador visual: las posiciones de las perillas se conservan y surten efecto tan pronto como la etapa se vuelve a habilitar.

## Pasos

1. Póngase los auriculares y ajuste la sala a sus condiciones ambientales normales: ventilador encendido, ruido de computadora presente, lo que sea típico cuando opera.
2. No hable. Observe la bola de entrada en vivo en la curva Transfer. La bola muestra dónde se sitúa el ruido de su sala en el eje de entrada.
3. Observe la barra Gain-reduction. Si la barra no muestra relleno ámbar mientras está en silencio, Thresh ya está por debajo de su piso de ruido y la compuerta no se está cerrando: suba Thresh.
4. Gire la perilla Thresh lentamente en sentido horario hasta que la barra ámbar Gain-reduction comience a llenarse de forma consistente mientras está en silencio. Este es el piso de ruido.
5. Reduzca Thresh entre 2 y 3 dB para que la compuerta se cierre firmemente sobre el ruido sin recortar el borde inicial de su voz. La bola de entrada debe situarse claramente por debajo de la línea de umbral cuando esté en silencio.
6. Hable a volumen normal. Confirme que la barra Gain-reduction baje a cero (sin relleno) inmediatamente cuando comience a hablar, lo que indica que la compuerta se ha abierto.
7. Vuelva al silencio. Confirme que el relleno ámbar regrese rápidamente. Si la compuerta es lenta en cerrarse, reduzca Release. Consulte [Tune release for natural close](tune-attack-release-for-natural-open-close.md).

## Qué hace cada control

| Control                | Valor predeterminado                                                                                                                                                                                                                                     | Rango válido                                                                                                                                                                                                                                                     |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Thresh                 | −40.0 dB                                                                                                                                                                                                                                                 | −80.0 a 0.0 dB                                                                                                                                                                                                                                                   |
| Ratio                  | 2.0                                                                                                                                                                                                                                                      | 1.0 a 10.0                                                                                                                                                                                                                                                       |
| Return                 | 2.0 dB                                                                                                                                                                                                                                                   | 0.0 a 20.0 dB                                                                                                                                                                                                                                                    |
| Release                | 100 ms                                                                                                                                                                                                                                                   | 5 a 2000 ms                                                                                                                                                                                                                                                      |
| Floor                  | −15.0 dB                                                                                                                                                                                                                                                 | −80.0 a 0.0 dB                                                                                                                                                                                                                                                   |
| Flip (Expander / Gate) | Sin marcar = expansor descendente (suave, basado en relación). Marcado = Gate (corte duro). Ajusta ratio y floor a pares predefinidos al alternar; las demás perillas mantienen su posición. La etiqueta se actualiza en vivo entre 'Expander' y 'Gate'. | Control solo en editor (ClientGateEditor flotante). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Información sobre herramienta: 'Alterna entre modo Expander descendente (suave) y Gate (duro). Ajusta ratio + floor a pares predefinidos; las demás perillas se quedan donde las dejó.' |
| Peek (lookahead)       | Establece un retardo de prelectura para que la compuerta pueda abrirse fraccionalmente antes de que llegue un transiente, evitando bordes de ataque recortados. 'Off' desactiva la línea de retardo por completo.                                        | Control solo en editor. Valores más altos aumentan la latencia en la ruta de TX. 1 y 1.5 ms coinciden con las opciones preestablecidas de Ableton; se agregaron 3 y 5 ms para transientes muy rápidos.                                                            |
| Attack                 | Mapeo exponencial (0.1 * 1000^n). Define la rapidez con que la compuerta se abre después de que la entrada supera Thresh.                                                                                                                                | Control solo en editor. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima.                                                                                                                                                                             |
| Hold                   | Mapeo lineal (n * 500). Después de que la entrada cae por debajo de Thresh − Return, la compuerta permanece abierta este tiempo antes de comenzar a cerrarse, evitando vibraciones en material rítmico.                                                 | Control solo en editor. Etiqueta 'X.X ms'.                                                                                                                                                                                                                       |

La curva Transfer traza la relación estática entrada/salida y muestra una bola de entrada en vivo al nivel de señal actual. Cuando Return es mayor que cero, aparece una banda vertical cian suave en la curva entre (Thresh − Return) y Thresh, marcando el rango donde el estado abierto/cerrado de la compuerta es adhesivo. La barra Gain-reduction es una franja horizontal ámbar, rellena hacia la derecha, escalada de 0 a 40 dB; una marca indica la posición predeterminada de Floor a −15 dB. En v26.5.1, las etiquetas de los ejes se renderizan utilizando texto estático en caché para mejorar el rendimiento, reduciendo la sobrecarga de CPU durante la animación en vivo. Este cambio es transparente para los usuarios: la apariencia visual sigue siendo idéntica.

### Editor de valor en línea (v26.5.2.1)

En v26.5.2.1, todos los controles de perilla en el applet obtuvieron un editor de valor en línea. Haga clic en el texto del valor debajo de cualquier perilla para abrir un pequeño campo de entrada de texto que se superpone al valor mostrado. Ingrese un valor numérico (con o sin texto de unidad) y presione Enter para confirmar; la perilla se ajusta al valor escrito, limitado a su rango válido. Hacer clic en cualquier otro lugar de la interfaz también confirma la edición. Presione Escape para cancelar y revertir al valor anterior. El editor reconoce comas como separadores decimales en configuraciones regionales que las usan. Esto permite una entrada precisa sin arrastrar una perilla.

## Consejos

- Ajuste Thresh durante su condición de ruido más desfavorable (ventilador más ruidoso, mayor actividad de fondo). Un umbral calibrado para una sala silenciosa dejará pasar el ruido cuando las condiciones cambien.
- Si la compuerta corta el inicio de las palabras, baje Thresh entre 1 y 2 dB para que la compuerta se active antes.
- Aumente Return si la compuerta vibra o parpadea cuando el nivel de su voz se acerca al umbral. Cuanto más amplia sea la banda muerta, más estable será el comportamiento de apertura/cierre.
- La barra Gain-reduction y la bola de entrada se actualizan en vivo a aproximadamente 30 Hz, por lo que las ráfagas de ruido cortas serán visibles incluso si son breves.
- Los cambios en cualquier perilla se guardan inmediatamente y sobreviven a un reinicio. No es necesario confirmar ni aplicar por separado.
- Para ingresar un valor preciso de perilla, haga clic en el texto del valor debajo de la perilla y escriba el número, luego presione Enter. La perilla se mueve al valor ingresado al instante.

## Solución de problemas

- **El applet no es visible** — La etapa GATE no está habilitada. Haga clic una vez en la etapa GATE en el widget CHAIN para habilitarla, o haga doble clic para abrir el editor flotante y habilitarla allí.
- **El mosaico del applet aparece atenuado** — La etapa de compuerta está puenteada. El mosaico se renderiza con opacidad reducida cuando la etapa está deshabilitada. Vuelva a habilitar la etapa GATE en el widget CHAIN para restaurar el brillo completo y reanudar el procesamiento.
- **La barra Gain-reduction nunca se llena mientras está en silencio** — Thresh está configurado por debajo del piso de ruido. Suba Thresh hasta que aparezca un relleno ámbar constante durante el silencio.
- **La compuerta corta el principio de las palabras** — Thresh está demasiado cerca del nivel de su voz. Baje Thresh ligeramente.
- **La compuerta vibra o parpadea cerca del umbral** — Aumente Return para ampliar la banda muerta de histéresis. La banda cian en la curva Transfer crece a medida que sube Return, mostrando la zona adhesiva.
- **La compuerta no se cierra entre palabras** — Thresh es demasiado bajo para el piso de ruido actual. Suba Thresh hasta que la barra se llene de manera confiable durante las pausas.

## Relacionados

- [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md)
- [Tune attack / release for natural open/close](tune-attack-release-for-natural-open-close.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
