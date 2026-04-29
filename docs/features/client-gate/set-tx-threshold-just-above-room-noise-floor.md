# Ajuste el umbral de TX justo por encima del nivel de ruido ambiental

Configurar Thresh correctamente le indica a la puerta de TX dónde termina el ruido de fondo de su sala y dónde comienza su voz. Un umbral situado justo por encima del nivel de ruido mantiene el silencio entre transmisiones —sin siseo del micrófono ni sonido ambiental— y deja pasar su voz con claridad.

## Antes de comenzar

- La etapa de puerta de TX debe estar habilitada en el widget CHAIN del lado TX. Si no está habilitada, el applet queda oculto y los cambios en los controles no tienen efecto. Consulte [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md).
- Abra el subcontenedor "Aetherial TX Gate" dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa GATE del widget CHAIN para abrir el editor flotante "Aetherial Gate — TX".

## Pasos

1. Póngase los auriculares y deje la sala en sus condiciones ambientales normales: ventilador encendido, ruido del equipo presente y cualquier otro factor habitual durante la operación.
2. No hable. Observe la bola de entrada en vivo sobre la curva Transfer. La bola muestra dónde se sitúa el ruido de la sala en el eje de entrada.
3. Observe la barra Gain-reduction. Si la barra no muestra relleno ámbar mientras usted está en silencio, Thresh ya está por debajo del nivel de ruido y la puerta no se está cerrando — suba Thresh.
4. Gire el control Thresh lentamente en el sentido de las agujas del reloj hasta que la barra ámbar Gain-reduction comience a llenarse de forma consistente mientras usted está en silencio. Este es el nivel de ruido.
5. Reduzca Thresh entre 2 y 3 dB para que la puerta cierre firmemente sobre el ruido sin recortar el borde inicial de su voz. La bola de entrada debe quedar claramente por debajo de la línea de umbral cuando usted está en silencio.
6. Hable a volumen normal. Confirme que la barra Gain-reduction cae a cero (sin relleno) de inmediato al comenzar a hablar, lo que indica que la puerta se ha abierto.
7. Vuelva al silencio. Confirme que el relleno ámbar regresa con prontitud. Si la puerta tarda en cerrarse, reduzca Release. Consulte [Ajustar el tiempo de cierre para una respuesta natural](tune-attack-release-for-natural-open-close.md).

## Qué hace cada control

| Control                | Valor predeterminado                                                                                                                                                                                                                      | Rango válido                                                                                                                                                                                                                                                        |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Thresh                 | −40.0 dB                                                                                                                                                                                                                                  | −80.0 a 0.0 dB                                                                                                                                                                                                                                                      |
| Ratio                  | 2.0                                                                                                                                                                                                                                       | 1.0 a 10.0                                                                                                                                                                                                                                                          |
| Return                 | 2.0 dB                                                                                                                                                                                                                                    | 0.0 a 20.0 dB                                                                                                                                                                                                                                                       |
| Release                | 100 ms                                                                                                                                                                                                                                    | 5 a 2000 ms                                                                                                                                                                                                                                                         |
| Floor                  | −15.0 dB                                                                                                                                                                                                                                  | −80.0 a 0.0 dB                                                                                                                                                                                                                                                      |
| Flip (Expander / Gate) | Sin marcar = expansor descendente (suave, basado en ratio). Marcado = Gate (corte abrupto). Al conmutar, ajusta ratio y floor a pares preestablecidos; los demás controles permanecen en su posición. La etiqueta alterna entre 'Expander' y 'Gate' en tiempo real. | Control exclusivo del editor (ClientGateEditor flotante). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Información emergente: 'Flip between downward Expander (gentle) and Gate (hard) modes. Snaps ratio + floor to preset pairs; other knobs stay where you left them.' |
| Peek (lookahead)       | Establece un retardo de prelectura para que la puerta pueda abrirse de forma fraccionaria antes de que llegue un transitorio, evitando el recorte del borde de ataque. 'Off' desactiva completamente la línea de retardo.                  | Control exclusivo del editor. Los valores más altos incrementan la latencia en la ruta TX. Los valores 1 y 1.5 ms coinciden con las opciones preestablecidas de Ableton; 3 y 5 ms se agregaron para transitorios muy rápidos.                                        |
| Attack                 | Mapeo exponencial (0.1 * 1000^n). Define la rapidez con que la puerta se abre después de que la entrada supere Thresh.                                                                                                                    | Control exclusivo del editor. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima.                                                                                                                                                                         |
| Hold                   | Mapeo lineal (n * 500). Tras bajar la entrada por debajo de Thresh − Return, la puerta permanece abierta durante este tiempo antes de comenzar a cerrarse, evitando el aleteo en material rítmico.                                        | Control exclusivo del editor. Etiqueta 'X.X ms'.                                                                                                                                                                                                                   |

La curva Transfer representa la relación estática entrada/salida y muestra una bola de entrada en vivo con el nivel de señal actual. Cuando Return es mayor que cero, aparece una banda vertical de color cian suave entre (Thresh − Return) y Thresh, que delimita el rango donde el estado abierto/cerrado de la puerta es estable. La barra Gain-reduction es una franja horizontal ámbar, rellena de derecha a izquierda, escalada de 0 a 40 dB; una marca indica la posición predeterminada de Floor en −15 dB.

## Consejos

- Ajuste Thresh bajo la condición de mayor ruido posible (ventilador al máximo, máxima actividad de fondo). Un umbral calibrado en una sala silenciosa permitirá que el ruido pase cuando las condiciones cambien.
- Si la puerta corta el inicio de las palabras, reduzca Thresh entre 1 y 2 dB para que la puerta se active antes.
- Aumente Return si la puerta traquetea o aletea cuando el nivel de su voz ronda el umbral. Cuanto más amplia sea la zona muerta, más estable será el comportamiento de apertura y cierre.
- La barra Gain-reduction y la bola de entrada se actualizan en vivo a aproximadamente 30 Hz, de modo que los pulsos de ruido breves serán visibles aunque sean cortos.
- Los cambios en cualquier control se guardan de inmediato y se conservan tras un reinicio. No es necesario confirmar ni aplicar por separado.

## Solución de problemas

- **El applet no está visible** — La etapa GATE no está habilitada. Haga clic una vez en la etapa GATE del widget CHAIN para habilitarla, o haga doble clic para abrir el editor flotante y habilitarla desde allí.
- **La barra Gain-reduction nunca se llena en silencio** — Thresh está configurado por debajo del nivel de ruido. Suba Thresh hasta que aparezca un relleno ámbar consistente durante el silencio.
- **La puerta corta el inicio de las palabras** — Thresh está demasiado cerca del nivel de su voz. Reduzca Thresh ligeramente.
- **La puerta traquetea o aletea cerca del umbral** — Aumente Return para ampliar la zona de histéresis. La banda cian en la curva Transfer crece a medida que sube Return, mostrando la zona estable.
- **La puerta no se cierra entre palabras** — Thresh está demasiado bajo para el nivel de ruido actual. Suba Thresh hasta que la barra se llene de forma fiable durante las pausas.

## Relacionados

- [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md)
- [Ajustar ataque y cierre para una respuesta natural](tune-attack-release-for-natural-open-close.md)
- [Ajustar Floor para evitar silencios antinaturales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Observar la reducción de ganancia en vivo sin hablar](watch-live-gr-while-not-speaking.md)
- [Elegir entre comportamiento de puerta o expansor suave mediante ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
