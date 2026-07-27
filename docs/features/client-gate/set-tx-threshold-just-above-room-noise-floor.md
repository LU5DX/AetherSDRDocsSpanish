# Ajustar el umbral de TX justo por encima del piso de ruido ambiental

Ajustar Thresh correctamente le indica al puerta de TX dónde termina el ruido de fondo de su sala y comienza su voz. Un umbral justo por encima del piso de ruido mantiene el soplido del micrófono y los sonidos ambientales en silencio entre transmisiones, mientras deja pasar su voz con claridad.

## Antes de comenzar

- La etapa de puerta de TX debe estar habilitada en el widget CHAIN del lado de TX. Si no está habilitada, el applet está oculto y los cambios en las perillas no tienen efecto. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).
- Abra el subcontenedor "Aetherial TX Gate" dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante "Aetherial Gate — TX".
- Cuando la etapa de puerta está omitida, todo el mosaico del applet se muestra con opacidad reducida (aproximadamente al 55% del brillo total). Esto es solo un indicador visual: las posiciones de las perillas se conservan y entran en vigor tan pronto como se vuelve a habilitar la etapa.

## Pasos

1. Póngase los auriculares y ajuste la sala a sus condiciones ambientales normales: ventilador encendido, ruido de computadora presente, cualquier cosa típica cuando opera.
2. No hable. Observe la bola de entrada en vivo en la curva de Transferencia. La bola muestra dónde se encuentra el ruido de su sala en el eje de entrada.
3. Observe la barra de Reducción de Ganancia. Si la barra no muestra relleno ámbar mientras está en silencio, Thresh ya está por debajo de su piso de ruido y la puerta no se está cerrando; suba Thresh.
4. Gire la perilla Thresh lentamente en sentido horario hasta que la barra ámbar de Reducción de Ganancia comience a llenarse de manera constante mientras está en silencio. Este es el piso de ruido.
5. Reduzca Thresh en 2–3 dB para que la puerta se cierre firmemente sobre el ruido sin recortar el borde inicial de su voz. La bola de entrada debe estar claramente por debajo de la línea de umbral cuando esté en silencio.
6. Hable a volumen normal. Confirme que la barra de Reducción de Ganancia baje a cero (sin relleno) inmediatamente cuando comience a hablar, indicando que la puerta se ha abierto.
7. Vuelva al silencio. Confirme que el relleno ámbar regrese rápidamente. Si la puerta es lenta al cerrarse, reduzca Release. Consulte [Tune release for natural close](tune-attack-release-for-natural-open-close.md).

## Qué hace cada control

| Control                | Predeterminado | Rango válido     | Comportamiento                                                                                                                                                                                                                                                                                                                                                                    |
|------------------------|----------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Thresh                 | −40.0 dB       | −80.0 a 0.0 dB   | Mapeo lineal. Nivel por debajo del cual la puerta comienza a atenuar.                                                                                                                                                                                                                                                                                                              |
| Ratio                  | 2.0            | 1.0 a 10.0       | Mapeo lineal. Ratios más altos proporcionan un corte más duro, similar a una puerta; ratios más bajos actúan como un expansor descendente suave. Etiqueta 'X.X:1'.                                                                                                                                                                                                                 |
| Return                 | 2.0 dB         | 0.0 a 20.0 dB    | Mapeo lineal (n * 20). Establece la banda muerta de histéresis: la puerta se abre por encima de Thresh y no se cierra nuevamente hasta que la entrada cae por debajo de Thresh − Return, evitando un parloteo rápido cerca del umbral. Etiqueta 'X.XX dB'. El widget de curva dibuja una banda vertical cian suave entre (Thresh − Return) y Thresh para hacer visible la zona adhesiva. |
| Release                | 100 ms         | 5 a 2000 ms      | Mapeo exponencial (5 * 400^n). Establece la rapidez con que la puerta se cierra después de que la entrada cae por debajo de Thresh − Return. Etiqueta 'X.X ms' por debajo de 100, 'X ms' por encima.                                                                                                                                                                               |
| Floor                  | −15.0 dB       | −80.0 a 0.0 dB   | Mapeo lineal. Atenuación máxima que la puerta puede aplicar.                                                                                                                                                                                                                                                                                                                        |
| Flip (Expander / Gate) | Desmarcado     | Solo editor      | Desmarcado = expansor descendente (suave, basado en ratio). Marcado = Gate (corte duro). Al alternar, ajusta ratio y floor a pares predefinidos; las otras perillas permanecen en su lugar. La etiqueta se actualiza en vivo entre 'Expander' y 'Gate'. Color: desmarcado = verde (Expander), marcado = ámbar (Gate). Tooltip: 'Cambia entre modo Expansor descendente (suave) y Puerta (duro). Ajusta ratio + floor a pares predefinidos; las otras perillas quedan donde las dejó.' |
| Peek (lookahead)       | Off            | Solo editor      | Establece un retardo de pre-lectura para que la puerta pueda abrirse fraccionalmente antes de que llegue un transitorio, evitando bordes de ataque recortados. 'Off' deshabilita completamente la línea de retardo. Los valores más altos aumentan la latencia en la ruta de TX. 1 y 1.5 ms coinciden con las opciones predefinidas de Ableton; se agregaron 3 y 5 ms para transitorios muy rápidos. |
| Attack                 | 0.3 ms         | Solo editor      | Mapeo exponencial (0.1 * 1000^n). Establece la rapidez con que la puerta se abre después de que la entrada supera Thresh. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima.                                                                                                                                                                                             |
| Hold                   | 0 ms           | Solo editor      | Mapeo lineal (n * 500). Después de que la entrada cae por debajo de Thresh − Return, la puerta permanece abierta durante este tiempo antes de comenzar a cerrarse, evitando fluctuaciones en material rítmico. Etiqueta 'X.X ms'.                                                                                                                                                  |

La curva de Transferencia representa la relación estática entrada/salida y muestra una bola de entrada en vivo al nivel de señal actual. Cuando Return es mayor que cero, aparece una banda vertical cian suave en la curva entre (Thresh − Return) y Thresh, marcando el rango donde el estado abierto/cerrado de la puerta es adhesivo. La barra de Reducción de Ganancia es una tira horizontal ámbar, rellena desde la derecha, escalada de 0 a 40 dB; una marca indica la posición predeterminada de Floor de −15 dB. En v26.5.1, las etiquetas de los ejes se renderizan usando texto estático en caché para mejorar el rendimiento, reduciendo la sobrecarga de la CPU durante la animación en vivo. Este cambio es transparente para el usuario: la apariencia visual permanece idéntica.

### Editor de valor en línea (v26.5.2.1)

En v26.5.2.1, todos los controles de perilla en el applet ganaron un editor de valor en línea. Haga clic en el texto del valor debajo de cualquier perilla para abrir un pequeño campo de entrada de texto que se superpone al valor mostrado. Ingrese un valor numérico (con o sin texto de unidad) y presione Enter para confirmar; la perilla se mueve al valor escrito, limitado a su rango válido. Hacer clic en cualquier otro lugar de la interfaz también confirma la edición. Presione Escape para cancelar y volver al valor anterior. El editor reconoce comas como separadores decimales en configuraciones regionales que las usan. Esto permite una entrada precisa sin necesidad de arrastrar una perilla.

### Tematización (v26.6.1)

En v26.6.1, el applet y todos sus controles secundarios (el widget de curva de Transferencia y cada perilla) se volvieron completamente tematizables. Los colores de las perillas (fondo del anillo, primer plano/arco del anillo, manija/puntero, texto de la etiqueta y texto del valor) ahora se leen de las claves de tema en el espacio de nombres `color.knob.*`. El widget de curva de Transferencia lee su fondo, cuadrícula, etiquetas de ejes, línea de identidad, curva y colores de la bola de las claves de tema `color.background.*`, `color.text.*` y `color.accent.*`. El color de la curva se lee de `color.accent.warning`, que se renderiza como ámbar de forma predeterminada. Cuando se aplica un tema personalizado, todos los colores relacionados con la puerta se actualizan inmediatamente sin necesidad de reiniciar. La apariencia visual predeterminada no cambia.

### Rendimiento de la animación (v26.7.4)

En v26.7.4, el widget de curva de Transferencia y la barra de Reducción de Ganancia ahora se repintan en cada tic de animación en lugar de solo cuando el valor suavizado cambia o se estabiliza. Esto garantiza un seguimiento visual más suave de la bola de entrada en vivo y del medidor de reducción de ganancia durante cambios rápidos de señal, a costa de un uso ligeramente mayor de CPU. La apariencia visual y la capacidad de respuesta mejoran para transitorios rápidos.

## Consejos

- Ajuste Thresh durante su condición de ruido más desfavorable (ventilador más ruidoso, mayor actividad de fondo). Un umbral calibrado para una sala silenciosa dejará pasar el ruido cuando las condiciones cambien.
- Si la puerta corta el inicio de las palabras, reduzca Thresh en 1–2 dB para que la puerta se active antes.
- Aumente Return si la puerta parlotea o fluctúa cuando el nivel de su voz se acerca al umbral. Cuanto más amplia sea la banda muerta, más estable será el comportamiento de apertura/cierre.
- La barra de Reducción de Ganancia y la bola de entrada se actualizan en vivo a aproximadamente 30 Hz, por lo que las ráfagas cortas de ruido serán visibles incluso si son breves.
- Los cambios en cualquier perilla se guardan inmediatamente y sobreviven a un reinicio. No es necesario confirmar ni aplicar por separado.
- Para ingresar un valor preciso de perilla, haga clic en el texto del valor debajo de la perilla y escriba el número, luego presione Enter. La perilla se mueve al valor ingresado al instante.

## Solución de problemas

- **El applet no es visible** — La etapa GATE no está habilitada. Haga clic una vez en la etapa GATE en el widget CHAIN para habilitarla, o haga doble clic para abrir el editor flotante y habilitarla allí.
- **El mosaico del applet aparece atenuado** — La etapa de puerta está omitida. El mosaico se renderiza con opacidad reducida cuando la etapa está deshabilitada. Vuelva a habilitar la etapa GATE en el widget CHAIN para restaurar el brillo completo y reanudar el procesamiento.
- **La barra de Reducción de Ganancia nunca se llena en silencio** — Thresh está configurado por debajo del piso de ruido. Suba Thresh hasta que aparezca un relleno ámbar constante durante el silencio.
- **La puerta corta el principio de las palabras** — Thresh está demasiado cerca del nivel de su voz. Reduzca Thresh ligeramente.
- **La puerta parlotea o fluctúa cerca del umbral** — Aumente Return para ampliar la banda muerta de histéresis. La banda cian en la curva de Transferencia crece a medida que sube Return, mostrando la zona adhesiva.
- **La puerta no se cierra entre palabras** — Thresh es demasiado bajo para el piso de ruido actual. Suba Thresh hasta que la barra se llene de manera confiable durante las pausas.

## Relacionados

- [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md)
- [Tune attack / release for natural open/close](tune-attack-release-for-natural-open-close.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
