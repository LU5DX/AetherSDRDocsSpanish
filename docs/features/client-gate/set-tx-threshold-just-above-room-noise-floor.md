# Establecer el umbral de TX justo por encima del piso de ruido de la sala

Configurar Thresh correctamente le indica a la compuerta de TX dónde termina el ruido de fondo de su sala y comienza su voz. Un umbral justo por encima del piso de ruido mantiene el soplido del micrófono y el sonido ambiente silenciosos entre transmisiones, mientras deja pasar su voz con claridad.

## Antes de comenzar

- La etapa de compuerta de TX debe estar habilitada en el widget CHAIN del lado de TX. Si no está habilitada, el applet está oculto y los cambios en las perillas no tienen efecto. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).
- Abra el subcontenedor "Aetherial TX Gate" dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante "Aetherial Gate — TX".
- Cuando la etapa de compuerta está desviada (bypass), el mosaico del applet se renderiza con opacidad reducida (aproximadamente al 55 % del brillo completo). Esto es solo un indicador visual: las posiciones de las perillas se conservan y entran en vigor tan pronto como la etapa se vuelve a habilitar.

## Pasos

1. Póngase los auriculares y ajuste la sala a sus condiciones ambientales normales (ventilador encendido, ruido de computadora presente, lo que sea típico cuando opera).
2. No hable. Observe la bola de entrada en vivo en la curva de Transfer (Transferencia). La bola muestra dónde se ubica el ruido de su sala en el eje de entrada.
3. Observe la barra de Reducción de ganancia (Gain-reduction). Si la barra no muestra relleno ámbar mientras está en silencio, Thresh ya está por debajo de su piso de ruido y la compuerta no se cierra: suba Thresh.
4. Gire lentamente la perilla Thresh en el sentido de las agujas del reloj hasta que la barra ámbar de Reducción de ganancia comience a llenarse de manera consistente mientras está en silencio. Este es el piso de ruido.
5. Retroceda Thresh entre 2 y 3 dB para que la compuerta se cierre firmemente sobre el ruido sin recortar el borde inicial de su voz. La bola de entrada debe ubicarse claramente debajo de la línea de umbral cuando esté en silencio.
6. Hable a volumen normal. Confirme que la barra de Reducción de ganancia caiga a cero (sin relleno) inmediatamente cuando comience a hablar, lo que indica que la compuerta se ha abierto.
7. Vuelva al silencio. Confirme que el relleno ámbar regrese rápidamente. Si la compuerta es lenta al cerrarse, reduzca Release. Consulte [Tune release for natural close](tune-attack-release-for-natural-open-close.md).

## Función de cada control

| Control                | Predeterminado | Rango válido      | Comportamiento                                                                                                                                                                                                                                                                                                                                                                                     |
|------------------------|----------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Thresh                 | −40,0 dB       | −80,0 a 0,0 dB    | Mapeo lineal. Nivel por debajo del cual la compuerta comienza a atenuar.                                                                                                                                                                                                                                                                                                                           |
| Ratio                  | 2,0            | 1,0 a 10,0        | Mapeo lineal. Ratios más altos dan un corte más fuerte, similar a una compuerta; ratios más bajos actúan como un expansor descendente suave.                                                                                                                                                                                                                                                       |
| Return                 | 2,0 dB         | 0,0 a 20,0 dB     | Mapeo lineal (n * 20). Establece la banda muerta de histéresis: la compuerta se abre por encima de Thresh y no se vuelve a cerrar hasta que la entrada cae por debajo de Thresh − Return, evitando el parloteo (chatter) rápido cerca del umbral. El widget de la curva dibuja una banda vertical cian suave entre (Thresh − Return) y Thresh para hacer visible la zona de retención.           |
| Release                | 100 ms         | 5 a 2000 ms       | Mapeo exponencial (5 * 400^n). Establece la rapidez con que la compuerta se cierra después de que la entrada cae por debajo de Thresh − Return. Etiqueta 'X.X ms' por debajo de 100, 'X ms' por encima.                                                                                                                                                                                            |
| Floor                  | −15,0 dB       | −80,0 a 0,0 dB    | Mapeo lineal. Atenuación máxima que la compuerta puede aplicar.                                                                                                                                                                                                                                                                                                                                    |
| Flip (Expander / Gate) | Desmarcado     | Solo en editor    | Desmarcado = expansor descendente (suave, basado en ratio). Marcado = Compuerta (Gate, corte duro). Ajusta ratio y floor a pares predefinidos al alternar; las demás perillas permanecen donde están. La etiqueta se actualiza en vivo entre 'Expander' y 'Gate'. Color: desmarcado = verde (Expander), marcado = ámbar (Gate). Tooltip: 'Flip between downward Expander (gentle) and Gate (hard) modes. Snaps ratio + floor to preset pairs; other knobs stay where you left them.' |
| Peek (lookahead)       | Off            | Solo en editor    | Establece un retardo de pre-lectura para que la compuerta pueda abrirse fraccionalmente antes de que llegue un transitorio, evitando bordes de ataque recortados. 'Off' deshabilita la línea de retardo por completo. Los valores más altos aumentan la latencia en la ruta de TX. 1 y 1,5 ms coinciden con las opciones predefinidas de Ableton; se agregaron 3 y 5 ms para transitorios muy rápidos. |
| Attack                 | 0,3 ms         | Solo en editor    | Mapeo exponencial (0,1 * 1000^n). Establece la rapidez con que la compuerta se abre después de que la entrada supera Thresh. Etiqueta 'X,XX ms' por debajo de 10 ms, 'X,X ms' por encima.                                                                                                                                                                                                    |
| Hold                   | 0 ms           | Solo en editor    | Mapeo lineal (n * 500). Después de que la entrada cae por debajo de Thresh − Return, la compuerta permanece abierta durante este tiempo antes de comenzar a cerrarse, evitando el aleteo en material rítmico. Etiqueta 'X.X ms'.                                                                                                                                                              |

La curva de Transfer (Transfer) traza la relación estática entrada/salida y muestra una bola de entrada en vivo al nivel de señal actual. Cuando Return es mayor que cero, aparece una banda vertical cian suave en la curva entre (Thresh − Return) y Thresh, marcando el rango donde el estado abierto/cerrado de la compuerta se retiene. La barra de Reducción de ganancia es una tira horizontal ámbar, rellena hacia la derecha, escalada de 0 a 40 dB; una marca indica la posición predeterminada del piso (Floor) de −15 dB. En la v26.5.1, las etiquetas de los ejes se renderizan utilizando texto estático en caché para mejorar el rendimiento, reduciendo la sobrecarga de la CPU durante la animación en vivo. Este cambio es transparente para los usuarios: la apariencia visual permanece idéntica.

### Editor de valor en línea (v26.5.2.1)

En la v26.5.2.1, todos los controles de perilla en el applet obtuvieron un editor de valor en línea. Haga clic en el texto del valor debajo de cualquier perilla para abrir un pequeño campo de entrada de texto que se superpone al valor mostrado. Ingrese un valor numérico (con o sin unidad de texto) y presione Enter para confirmar; la perilla se mueve al valor escrito, limitado a su rango válido. Hacer clic en otro lugar de la interfaz también confirma la edición. Presione Escape para cancelar y revertir al valor anterior. El editor reconoce las comas como separadores decimales en configuraciones regionales que las utilizan. Esto permite una entrada precisa sin necesidad de arrastrar una perilla.

### Tematización (v26.6.1)

En la v26.6.1, el applet y todos sus controles secundarios (el widget de la curva de Transfer y cada perilla) se volvieron completamente tematizables. Los colores de las perillas (fondo del anillo, primer plano/arco del anillo, manija/puntero, texto de la etiqueta y texto del valor) ahora se leen de las claves del tema en el espacio de nombres `color.knob.*`. El widget de la curva de Transfer lee su fondo, cuadrícula, etiquetas de los ejes, línea de identidad, curva y colores de la bola de las claves del tema `color.background.*`, `color.text.*` y `color.accent.*`. El color de la curva se lee de `color.accent.warning`, que se renderiza en ámbar de forma predeterminada. Cuando se aplica un tema personalizado, todos los colores relacionados con la compuerta se actualizan de inmediato sin necesidad de reiniciar. La apariencia visual predeterminada no cambia.

### Rendimiento de la animación (v26.6.3)

En la v26.6.3, se mejoró la lógica de suavizado de la animación para reducir repintados innecesarios. El widget de la curva de Transfer y la barra de Reducción de ganancia ahora solo se repintan cuando el valor suavizado realmente cambia o cuando la animación se estabiliza, en lugar de repintarse en cada tic de animación. Esto reduce la sobrecarga de la CPU durante la animación en vivo, manteniendo al mismo tiempo la misma capacidad de respuesta visual.

## Consejos

- Configure Thresh durante su condición de ruido más desfavorable (ventilador más ruidoso, mayor actividad de fondo). Un umbral calibrado para una sala silenciosa dejará pasar el ruido cuando las condiciones cambien.
- Si la compuerta corta el inicio de las palabras, baje Thresh entre 1 y 2 dB para que la compuerta se active antes.
- Aumente Return si la compuerta parlotea o fluctúa cuando el nivel de su voz se acerca al umbral. Cuanto más amplia sea la banda muerta, más estable será el comportamiento de apertura/cierre.
- La barra de Reducción de ganancia y la bola de entrada se actualizan en vivo a aproximadamente 30 Hz, por lo que las ráfagas cortas de ruido serán visibles incluso si son breves.
- Los cambios en cualquier perilla se guardan inmediatamente y sobreviven a un reinicio. No es necesario confirmar ni aplicar por separado.
- Para ingresar un valor preciso en una perilla, haga clic en el texto del valor debajo de la perilla, escriba el número y presione Enter. La perilla se mueve al valor ingresado al instante.

## Solución de problemas

- **El applet no es visible**: la etapa GATE no está habilitada. Haga clic una vez en la etapa GATE en el widget CHAIN para habilitarla, o haga doble clic para abrir el editor flotante y habilitarla allí.
- **El mosaico del applet aparece atenuado**: la etapa de compuerta está desviada (bypass). El mosaico se renderiza con opacidad reducida cuando la etapa está deshabilitada. Vuelva a habilitar la etapa GATE en el widget CHAIN para restaurar el brillo completo y reanudar el procesamiento.
- **La barra de Reducción de ganancia nunca se llena mientras está en silencio**: Thresh está configurado por debajo del piso de ruido. Suba Thresh hasta que aparezca un relleno ámbar constante durante el silencio.
- **La compuerta corta el inicio de las palabras**: Thresh está demasiado cerca del nivel de su voz. Baje Thresh ligeramente.
- **La compuerta parlotea o fluctúa cerca del umbral**: aumente Return para ampliar la banda muerta de histéresis. La banda cian en la curva de Transfer crece a medida que sube Return, mostrando la zona de retención.
- **La compuerta no se cierra entre palabras**: Thresh es demasiado bajo para el piso de ruido actual. Suba Thresh hasta que la barra se llene de forma fiable durante las pausas.

## Relacionados

- [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md)
- [Tune attack / release for natural open/close](tune-attack-release-for-natural-open-close.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
