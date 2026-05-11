# Ajuste el umbral de TX justo por encima del piso de ruido de la sala

Configurar Thresh correctamente le indica al compuerta de TX dónde termina el ruido de fondo de su sala y comienza su voz. Un umbral justo por encima del piso de ruido mantiene el soplido del micrófono y el sonido ambiente en silencio entre transmisiones, mientras deja pasar su voz con claridad.

## Antes de comenzar

- La etapa del compuerta de TX debe estar habilitada en el widget CHAIN del lado TX. Si no está habilitada, el applet está oculto y los cambios en las perillas no tienen efecto. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).
- Abra el subcontenedor "Aetherial TX Gate" dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante "Aetherial Gate — TX".
- Cuando la etapa del compuerta está desviada (bypassed), todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente al 55 % del brillo total). Esto es solo un indicador visual: las posiciones de las perillas se conservan y entran en efecto tan pronto como la etapa se vuelve a habilitar.

## Pasos

1. Póngase los auriculares y ajuste la sala a sus condiciones ambientales normales: ventilador encendido, ruido de computadora presente, cualquier ruido típico cuando opera.
2. No hable. Observe la bola de entrada en vivo en la curva de transferencia. La bola muestra dónde se ubica el ruido de su sala en el eje de entrada.
3. Observe la barra de reducción de ganancia. Si la barra no muestra relleno ámbar mientras está en silencio, Thresh ya está por debajo de su piso de ruido y el compuerta no se está cerrando; aumente Thresh.
4. Gire la perilla Thresh lentamente en el sentido de las agujas del reloj hasta que la barra de reducción de ganancia ámbar comience a llenarse de manera consistente mientras está en silencio. Este es el piso de ruido.
5. Reduzca Thresh entre 2 y 3 dB para que el compuerta se cierre firmemente sobre el ruido sin recortar el borde inicial de su voz. La bola de entrada debe situarse claramente por debajo de la línea de umbral cuando está en silencio.
6. Hable a volumen normal. Confirme que la barra de reducción de ganancia caiga a cero (sin relleno) inmediatamente cuando comience a hablar, lo que indica que el compuerta se ha abierto.
7. Vuelva al silencio. Confirme que el relleno ámbar regrese rápidamente. Si el compuerta tarda en cerrarse, reduzca Release. Consulte [Tune release for natural close](tune-attack-release-for-natural-open-close.md).

## Qué hace cada control

| Control                | Valor predeterminado                                                                                                                                                                                        | Rango válido                                                                                                                                                                                                                                                          |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Thresh                 | −40,0 dB                                                                                                                                                                                                    | −80,0 a 0,0 dB                                                                                                                                                                                                                                                        |
| Ratio                  | 2,0                                                                                                                                                                                                         | 1,0 a 10,0                                                                                                                                                                                                                                                            |
| Return                 | 2,0 dB                                                                                                                                                                                                      | 0,0 a 20,0 dB                                                                                                                                                                                                                                                         |
| Release                | 100 ms                                                                                                                                                                                                      | 5 a 2000 ms                                                                                                                                                                                                                                                            |
| Floor                  | −15,0 dB                                                                                                                                                                                                    | −80,0 a 0,0 dB                                                                                                                                                                                                                                                         |
| Flip (Expander / Gate) | Sin marcar = expansor descendente (suave, basado en ratio). Marcado = Gate (corte fuerte). Cambia instantáneamente ratio y floor a pares predefinidos al alternar; las otras perillas permanecen. La etiqueta se actualiza en vivo entre 'Expander' y 'Gate'. | Control solo del editor (flotante ClientGateEditor). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Información sobre herramientas: 'Alterna entre modo Expander descendente (suave) y Gate (fuerte). Cambia instantáneamente ratio + floor a pares predefinidos; las otras perillas se quedan donde las dejó.' |
| Peek (lookahead)       | Establece un retardo de prelectura para que el compuerta pueda abrirse fraccionalmente antes de que llegue un transitorio, evitando bordes de ataque recortados. 'Off' desactiva la línea de retardo por completo. | Control solo del editor. Valores más altos aumentan la latencia en la ruta TX. 1 y 1,5 ms coinciden con las opciones predefinidas de Ableton; se agregaron 3 y 5 ms para transitorios muy rápidos.                                                                     |
| Attack                 | Mapeo exponencial (0,1 * 1000^n). Establece la rapidez con que se abre el compuerta después de que la entrada supera Thresh.                                                                                | Control solo del editor. Etiqueta 'X,XX ms' por debajo de 10 ms, 'X,X ms' por encima.                                                                                                                                                                                |
| Hold                   | Mapeo lineal (n * 500). Después de que la entrada cae por debajo de Thresh − Return, el compuerta permanece abierto durante este tiempo antes de comenzar a cerrarse, evitando oscilaciones en material rítmico. | Control solo del editor. Etiqueta 'X,X ms'.                                                                                                                                                                                                                           |

La curva de transferencia traza la relación estática entrada/salida y muestra una bola de entrada en vivo en el nivel de señal actual. Cuando Return es mayor que cero, aparece una banda vertical cian suave en la curva entre (Thresh − Return) y Thresh, marcando el rango donde el estado abierto/cerrado del compuerta es adherente. La barra de reducción de ganancia es una franja horizontal ámbar, llena desde la derecha, escala de 0 a 40 dB; una marca indica la posición predeterminada de Floor en −15 dB. En la versión v26.5.1, las etiquetas de los ejes se renderizan usando texto estático en caché para mejorar el rendimiento, reduciendo la carga de CPU durante la animación en vivo. Este cambio es transparente para los usuarios: la apariencia visual permanece idéntica.

## Consejos

- Ajuste Thresh durante su condición de ruido más desfavorable (ventilador más ruidoso, mayor actividad de fondo). Un umbral calibrado para una sala silenciosa dejará pasar el ruido cuando las condiciones cambien.
- Si el compuerta recorta el inicio de las palabras, reduzca Thresh entre 1 y 2 dB para que el compuerta se active antes.
- Aumente Return si el compuerta traquetea u oscila cuando el nivel de su voz se acerca al umbral. Cuanto más ancha sea la banda muerta, más estable será el comportamiento de apertura/cierre.
- La barra de reducción de ganancia y la bola de entrada se actualizan en vivo a aproximadamente 30 Hz, por lo que las ráfagas cortas de ruido serán visibles incluso si son breves.
- Los cambios en cualquier perilla se guardan inmediatamente y sobreviven a un reinicio. No necesita confirmar ni aplicar por separado.

## Solución de problemas

- **El applet no es visible** — La etapa GATE no está habilitada. Haga clic una vez en la etapa GATE en el widget CHAIN para habilitarla, o haga doble clic para abrir el editor flotante y habilitarla allí.
- **El mosaico del applet aparece atenuado** — La etapa del compuerta está desviada (bypassed). El mosaico se renderiza con opacidad reducida cuando la etapa está deshabilitada. Vuelva a habilitar la etapa GATE en el widget CHAIN para restaurar el brillo total y reanudar el procesamiento.
- **La barra de reducción de ganancia nunca se llena en silencio** — Thresh está configurado por debajo del piso de ruido. Aumente Thresh hasta que aparezca un relleno ámbar constante durante el silencio.
- **El compuerta recorta el principio de las palabras** — Thresh está demasiado cerca del nivel de su voz. Reduzca Thresh ligeramente.
- **El compuerta traquetea u oscila cerca del umbral** — Aumente Return para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia crece a medida que aumenta Return, mostrando la zona adherente.
- **El compuerta no se cierra entre palabras** — Thresh es demasiado bajo para el piso de ruido actual. Aumente Thresh hasta que la barra se llene de manera confiable durante las pausas.

## Relacionados

- [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md)
- [Tune attack / release for natural open/close](tune-attack-release-for-natural-open-close.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
