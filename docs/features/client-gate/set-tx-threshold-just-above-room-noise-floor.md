# Ajuste el umbral de TX justo por encima del piso de ruido ambiental

Configurar Thresh correctamente indica a la compuerta de TX dónde termina el ruido de fondo de su sala y dónde comienza su voz. Un umbral justo por encima del piso de ruido mantiene silenciado el siseo del micrófono y el sonido ambiental entre transmisiones, mientras deja pasar su voz con claridad.

## Antes de comenzar

- La etapa de compuerta de TX debe estar habilitada en el widget CHAIN del lado TX. Si no está habilitada, el applet queda oculto y los cambios en los mandos no tienen efecto. Consulte [Omitir la compuerta desde la cadena](bypass-the-gate-from-the-chain.md).
- Abra el subcontenedor "Aetherial TX Gate" dentro del contenedor padre Aetherial Audio (TXDSP), o haga doble clic en la etapa GATE del widget CHAIN para abrir el editor flotante "Aetherial Gate — TX".

## Pasos

1. Póngase los auriculares y deje la sala en sus condiciones ambientales normales: ventilador encendido, ruido del ordenador presente, cualquier cosa que sea habitual cuando opera.
2. No hable. Observe la bola de entrada en vivo sobre la curva de transferencia (Transfer). La bola muestra dónde se ubica el ruido de su sala en el eje de entrada.
3. Observe la barra de reducción de ganancia (Gain-reduction). Si la barra no muestra relleno ámbar mientras guarda silencio, Thresh ya está por debajo de su piso de ruido y la compuerta no está cerrando — suba Thresh.
4. Gire el mando Thresh lentamente en sentido horario hasta que la barra ámbar de reducción de ganancia comience a rellenarse de forma constante mientras guarda silencio. Este es el piso de ruido.
5. Retroceda Thresh entre 2 y 3 dB para que la compuerta cierre firmemente sobre el ruido sin cortar el borde de ataque de su voz. La bola de entrada debe quedar claramente por debajo de la línea de umbral cuando guarda silencio.
6. Hable a volumen normal. Confirme que la barra de reducción de ganancia cae a cero (sin relleno) de inmediato al comenzar a hablar, lo que indica que la compuerta se ha abierto.
7. Vuelva al silencio. Confirme que el relleno ámbar regresa con rapidez. Si la compuerta tarda en cerrar, reduzca Release. Consulte [Ajustar el release para un cierre natural](tune-attack-release-for-natural-open-close.md).

## Qué hace cada control

| Control                | Valor por defecto                                                                                                                                                                                                                                     | Rango válido                                                                                                                                                                                                                                                        |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Thresh                 | −40.0 dB                                                                                                                                                                                                                                             | −80.0 a 0.0 dB                                                                                                                                                                                                                                                      |
| Ratio                  | 2.0                                                                                                                                                                                                                                                  | 1.0 a 10.0                                                                                                                                                                                                                                                          |
| Return                 | 2.0 dB                                                                                                                                                                                                                                               | 0.0 a 20.0 dB                                                                                                                                                                                                                                                       |
| Release                | 100 ms                                                                                                                                                                                                                                               | 5 a 2000 ms                                                                                                                                                                                                                                                         |
| Floor                  | −15.0 dB                                                                                                                                                                                                                                             | −80.0 a 0.0 dB                                                                                                                                                                                                                                                      |
| Flip (Expander / Gate) | Sin marcar = expansor descendente (suave, basado en ratio). Marcado = Gate (corte duro). Al conmutar, ajusta ratio y floor a pares predefinidos; los demás mandos permanecen en su posición. La etiqueta se actualiza en vivo entre 'Expander' y 'Gate'. | Control exclusivo del editor (ClientGateEditor flotante). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Tooltip: 'Flip between downward Expander (gentle) and Gate (hard) modes. Snaps ratio + floor to preset pairs; other knobs stay where you left them.' |
| Peek (lookahead)       | Establece un retardo de prelectura para que la compuerta pueda abrirse fracciones de segundo antes de que llegue un transitorio, evitando cortes en el borde de ataque. 'Off' deshabilita completamente la línea de retardo.                          | Control exclusivo del editor. Los valores más altos aumentan la latencia en la ruta TX. Los valores 1 y 1.5 ms coinciden con las opciones predefinidas de Ableton; 3 y 5 ms se añaden para transitorios muy rápidos.                                                |
| Attack                 | Mapeo exponencial (0.1 * 1000^n). Determina la rapidez con que la compuerta se abre cuando la entrada supera Thresh.                                                                                                                                 | Control exclusivo del editor. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima.                                                                                                                                                                         |
| Hold                   | Mapeo lineal (n * 500). Tras caer la entrada por debajo de Thresh − Return, la compuerta permanece abierta durante este tiempo antes de comenzar a cerrar, evitando el aleteo en material rítmico.                                                   | Control exclusivo del editor. Etiqueta 'X.X ms'.                                                                                                                                                                                                                   |

La curva de transferencia (Transfer) representa la relación estática entrada/salida y muestra una bola de entrada en vivo en el nivel de señal actual. Cuando Return es mayor que cero, aparece una banda vertical color cian suave en la curva entre (Thresh − Return) y Thresh, que marca el rango en el que el estado abierto/cerrado de la compuerta es estable. La barra de reducción de ganancia es una franja horizontal ámbar, rellena desde la derecha, escalada de 0 a 40 dB; una marca señala la posición por defecto de Floor en −15 dB.

## Consejos

- Ajuste Thresh durante su condición de ruido más desfavorable (ventilador más ruidoso, mayor actividad de fondo). Un umbral calibrado en una sala silenciosa dejará pasar el ruido cuando las condiciones cambien.
- Si la compuerta corta el inicio de las palabras, baje Thresh entre 1 y 2 dB para que la compuerta se active antes.
- Aumente Return si la compuerta traquetea o aletea cuando el nivel de su voz ronda el umbral. Cuanto mayor sea la banda muerta, más estable será el comportamiento de apertura y cierre.
- La barra de reducción de ganancia y la bola de entrada se actualizan en vivo a aproximadamente 30 Hz, por lo que ráfagas de ruido breves serán visibles aunque sean cortas.
- Los cambios en cualquier mando se guardan de inmediato y persisten tras un reinicio. No es necesario confirmar ni aplicar por separado.

## Resolución de problemas

- **El applet no es visible** — La etapa GATE no está habilitada. Haga clic simple en la etapa GATE del widget CHAIN para habilitarla, o haga doble clic para abrir el editor flotante y habilitarla desde allí.
- **La barra de reducción de ganancia nunca se rellena en silencio** — Thresh está configurado por debajo del piso de ruido. Suba Thresh hasta que aparezca un relleno ámbar constante durante el silencio.
- **La compuerta corta el inicio de las palabras** — Thresh está demasiado cerca del nivel de su voz. Baje Thresh ligeramente.
- **La compuerta traquetea o aletea cerca del umbral** — Aumente Return para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia crece al subir Return, mostrando la zona estable.
- **La compuerta no cierra entre palabras** — Thresh es demasiado bajo para el piso de ruido actual. Suba Thresh hasta que la barra se rellene de forma fiable durante las pausas.

## Relacionados

- [Omitir la compuerta desde la cadena](bypass-the-gate-from-the-chain.md)
- [Ajustar attack / release para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Configurar Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Observar la reducción de ganancia en vivo sin hablar](watch-live-gr-while-not-speaking.md)
- [Elegir el comportamiento de compuerta o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
