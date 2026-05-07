# Configurar el umbral de TX justo por encima del suelo de ruido de la sala

Ajustar correctamente el control Thresh (umbral) le indica a la compuerta de TX dónde termina el ruido de fondo de su sala y comienza su voz. Un umbral justo por encima del suelo de ruido mantiene el soplido del micrófono y el sonido ambiente silenciosos entre transmisiones, mientras deja pasar su voz con claridad.

## Antes de comenzar

- La etapa de la compuerta de TX debe estar habilitada en el widget CHAIN del lado TX. Si no está habilitada, el applet está oculto y los cambios en los mandos no tienen efecto. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).
- Abra el subcontenedor "Aetherial TX Gate" dentro del contenedor principal "Aetherial Audio (TXDSP)", o haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante "Aetherial Gate — TX".
- Cuando la etapa de la compuerta está puenteada (bypass), el mosaico completo del applet se muestra con opacidad reducida (aproximadamente al 55% del brillo total). Esto es solo un indicador visual: las posiciones de los mandos se conservan y entran en vigor en cuanto la etapa se vuelve a habilitar.

## Pasos

1. Póngase los auriculares y ajuste la sala a sus condiciones ambientales normales (ventilador encendido, ruido de computadora presente, lo que sea típico cuando opera).
2. No hable. Observe la bola de entrada en vivo en la curva de transferencia. La bola muestra dónde se sitúa el ruido de su sala en el eje de entrada.
3. Observe la barra de reducción de ganancia (Gain-reduction). Si la barra no muestra relleno ámbar mientras está en silencio, Thresh ya está por debajo de su suelo de ruido y la compuerta no se cierra; suba Thresh.
4. Gire el mando Thresh lentamente en sentido horario hasta que la barra ámbar de reducción de ganancia comience a llenarse de forma constante mientras está en silencio. Ese es el suelo de ruido.
5. Reduzca Thresh entre 2 y 3 dB para que la compuerta se cierre firmemente sobre el ruido sin recortar el borde inicial de su voz. La bola de entrada debe situarse claramente por debajo de la línea de umbral cuando esté en silencio.
6. Hable a volumen normal. Confirme que la barra de reducción de ganancia baje a cero (sin relleno) inmediatamente cuando comience a hablar, lo que indica que la compuerta se ha abierto.
7. Vuelva al silencio. Confirme que el relleno ámbar regrese rápidamente. Si la compuerta tarda en cerrarse, reduzca Release. Consulte [Tune release for natural close](tune-attack-release-for-natural-open-close.md).

## Función de cada control

| Control                | Valor predeterminado                                                                                                                                                                                                                                                      | Rango válido                                                                                                                                                                                                                                                          |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Thresh                 | −40,0 dB                                                                                                                                                                                                                                                                  | −80,0 a 0,0 dB                                                                                                                                                                                                                                                        |
| Ratio                  | 2,0                                                                                                                                                                                                                                                                       | 1,0 a 10,0                                                                                                                                                                                                                                                            |
| Return                 | 2,0 dB                                                                                                                                                                                                                                                                    | 0,0 a 20,0 dB                                                                                                                                                                                                                                                         |
| Release                | 100 ms                                                                                                                                                                                                                                                                    | 5 a 2000 ms                                                                                                                                                                                                                                                           |
| Floor                  | −15,0 dB                                                                                                                                                                                                                                                                  | −80,0 a 0,0 dB                                                                                                                                                                                                                                                        |
| Flip (Expander / Gate) | Sin marcar = expansor descendente (suave, basado en ratio). Marcado = Gate (corte duro). Ajusta el ratio y Floor a pares predefinidos al alternar; los demás mandos permanecen en su lugar. La etiqueta se actualiza en vivo entre 'Expander' y 'Gate'.                     | Control solo en el editor (ClientGateEditor flotante). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Información sobre herramienta: 'Cambia entre modo expansor descendente (suave) y compuerta (fuerte). Ajusta ratio + Floor a pares predefinidos; los demás mandos se quedan donde los dejó.' |
| Peek (lookahead)       | Establece un retardo de prelectura para que la compuerta pueda abrirse una fracción antes de que llegue un transitorio, evitando bordes de ataque recortados. 'Off' desactiva por completo la línea de retardo.                                                           | Control solo en el editor. Los valores más altos aumentan la latencia en la ruta de TX. 1 y 1,5 ms coinciden con las opciones preestablecidas de Ableton; se añadieron 3 y 5 ms para transitorios muy rápidos.                                                         |
| Attack                 | Mapeo exponencial (0,1 * 1000^n). Define la rapidez con que se abre la compuerta después de que la entrada supere Thresh.                                                                                                                                                | Control solo en el editor. Etiqueta 'X,XX ms' por debajo de 10 ms, 'X,X ms' por encima.                                                                                                                                                                              |
| Hold                   | Mapeo lineal (n * 500). Después de que la entrada caiga por debajo de Thresh − Return, la compuerta permanece abierta este tiempo antes de comenzar a cerrarse, evitando vibraciones en material rítmico.                                                                | Control solo en el editor. Etiqueta 'X,X ms'.                                                                                                                                                                                                                         |

La curva de transferencia representa la relación estática entrada/salida y muestra una bola de entrada en vivo al nivel de señal actual. Cuando Return es mayor que cero, aparece una banda vertical cian suave en la curva entre (Thresh − Return) y Thresh, que marca el rango donde el estado abierto/cerrado de la compuerta es estable. La barra de reducción de ganancia es una franja horizontal ámbar, rellena hacia la derecha, escalada de 0 a 40 dB; una marca indica la posición predeterminada de Floor en −15 dB.

## Consejos

- Ajuste Thresh en la condición de ruido más desfavorable (ventilador más fuerte, mayor actividad de fondo). Un umbral calibrado para una sala silenciosa dejará pasar ruido cuando las condiciones cambien.
- Si la compuerta corta el inicio de las palabras, reduzca Thresh entre 1 y 2 dB para que la compuerta se active antes.
- Aumente Return si la compuerta vibra o tiembla cuando el nivel de su voz se acerca al umbral. Cuanto más amplia sea la banda muerta, más estable será el comportamiento de apertura/cierre.
- La barra de reducción de ganancia y la bola de entrada se actualizan en vivo a aproximadamente 30 Hz, por lo que los breves estallidos de ruido serán visibles incluso si son cortos.
- Los cambios en cualquier mando se guardan de inmediato y sobreviven a un reinicio. No es necesario confirmar ni aplicar por separado.

## Solución de problemas

- **El applet no es visible** — La etapa GATE no está habilitada. Haga clic una vez en la etapa GATE en el widget CHAIN para habilitarla, o haga doble clic para abrir el editor flotante y habilitarla allí.
- **El mosaico del applet aparece atenuado** — La etapa de la compuerta está puenteada (bypass). El mosaico se muestra con opacidad reducida cuando la etapa está deshabilitada. Vuelva a habilitar la etapa GATE en el widget CHAIN para restaurar el brillo completo y reanudar el procesamiento.
- **La barra de reducción de ganancia nunca se llena en silencio** — Thresh está ajustado por debajo del suelo de ruido. Suba Thresh hasta que aparezca un relleno ámbar constante durante el silencio.
- **La compuerta corta el principio de las palabras** — Thresh está demasiado cerca del nivel de su voz. Reduzca Thresh ligeramente.
- **La compuerta vibra o tiembla cerca del umbral** — Aumente Return para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia crece a medida que sube Return, mostrando la zona estable.
- **La compuerta no se cierra entre palabras** — Thresh es demasiado bajo para el suelo de ruido actual. Suba Thresh hasta que la barra se llene de forma fiable durante las pausas.

## Relacionados

- [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md)
- [Tune attack / release for natural open/close](tune-attack-release-for-natural-open-close.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
