# Ajuste de Return y Release para una apertura/cierre natural

Ajuste los controles **Return** y **Release** para controlar la banda muerta de histéresis del gate y la velocidad con que se cierra cuando el audio cae por debajo del umbral. Una configuración correcta evita el traqueteo rápido cerca del umbral y los cortes abruptos entre palabras.

## Antes de comenzar

- La etapa Gate debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el gate de la cadena](bypass-the-gate-from-the-chain.md) si la etapa aún no está activa.
- Abra el subcontenedor "Aetherial TX Gate" o "Aetherial AGC-T" dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante de ese lado.
- Reproduzca audio o hable al micrófono para que la barra de reducción de ganancia se mueva mientras realiza los ajustes.

## Pasos

1. Localice la fila de controles en la parte inferior del applet. Encuentre el control etiquetado **Return** (tercer control desde la izquierda en TX; misma posición en RX).
2. Gire **Return** hacia la derecha (valores más altos) para ampliar la banda muerta de histéresis: el gate se abre cuando la entrada sube por encima de Thresh y no se cerrará de nuevo hasta que la entrada caiga por debajo de Thresh − Return. Gírelo hacia la izquierda (hacia 0.0 dB) para reducir la banda muerta y que el gate se cierre antes después de que la señal caiga. El valor predeterminado es 2.0 dB. El rango válido es de 0.0 a 20.0 dB.
3. Observe la curva de transferencia. Aparece una banda vertical de color cian suave entre (Thresh − Return) y Thresh, que muestra la zona de estabilidad. Una banda más ancha significa que el gate permanece abierto en un rango de señal mayor antes de cerrarse.
4. Observe la bola de entrada en vivo sobre la curva de transferencia. Cuando el nivel de señal se mantiene cerca del umbral, la bola debe quedar dentro de la banda cian sin provocar que el gate se abra y cierre intermitentemente.
5. Localice el control etiquetado **Release** (cuarto control desde la izquierda).
6. Gire **Release** hacia la derecha (valores más altos) para que el gate se cierre más lentamente después de que el audio caiga por debajo de Thresh − Return; esto suaviza la cola entre palabras. Gírelo hacia la izquierda para cerrarlo más rápido y suprimir el ruido de fondo con mayor agresividad. El valor predeterminado es 100 ms. El rango válido es de 5 a 2000 ms.
7. Pronuncie una frase con pausas naturales y observe la barra de reducción de ganancia. El relleno ámbar debe crecer suavemente durante el silencio y retroceder limpiamente cuando retome el habla, sin bombeo ni saltos bruscos.
8. Si el gate se cierra bruscamente en medio de una palabra, aumente **Release**. Si el ruido de fondo se cuela entre oraciones, disminuya **Release**.
9. Si el gate se abre y cierra rápidamente con señales cerca del umbral, aumente **Return** para ampliar la banda muerta.

## Qué hace cada control

| Control                   | Valor predeterminado                                                                                                                                                                                                                | Rango válido                                                                                                                                                                                                                                                                                                          |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Return                    | 2.0 dB                                                                                                                                                                                                                              | 0.0 – 20.0 dB                                                                                                                                                                                                                                                                                                         |
| Release                   | 100 ms                                                                                                                                                                                                                              | 5 – 2000 ms                                                                                                                                                                                                                                                                                                           |
| Flip (Expander / Gate)    | Sin marcar = expansor descendente (suave, basado en ratio). Marcado = Gate (corte duro). Al conmutar, ajusta el ratio y el floor a pares preestablecidos; los demás controles quedan en su posición. La etiqueta alterna en vivo entre 'Expander' y 'Gate'. | Control exclusivo del editor (ClientGateEditor flotante). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Descripción emergente: 'Flip between downward Expander (gentle) and Gate (hard) modes. Snaps ratio + floor to preset pairs; other knobs stay where you left them.' |
| Peek (lookahead)          | Establece un retardo de prelectura para que el gate pueda abrirse levemente antes de que llegue un transitorio, evitando bordes de ataque recortados. 'Off' deshabilita completamente la línea de retardo.                           | Control exclusivo del editor. Los valores más altos incrementan la latencia en el camino TX. 1 y 1.5 ms coinciden con las opciones preestablecidas de Ableton; 3 y 5 ms se añaden para transitorios muy rápidos.                                                                                                      |
| Attack                    | Mapeo exponencial (0.1 * 1000^n). Establece la rapidez con que el gate se abre cuando la entrada supera Thresh.                                                                                                                     | Control exclusivo del editor. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima.                                                                                                                                                                                                                           |
| Hold                      | Mapeo lineal (n * 500). Después de que la entrada cae por debajo de Thresh − Return, el gate permanece abierto durante este tiempo antes de comenzar a cerrarse, evitando el aleteo en material rítmico.                            | Control exclusivo del editor. Etiqueta 'X.X ms'.                                                                                                                                                                                                                                                                     |

## Consejos

- La barra de reducción de ganancia alcanza un máximo de 40 dB y la marca de referencia en la posición −15 dB corresponde al valor predeterminado de Floor. Use esta marca como referencia visual: si el relleno ámbar raramente llega a la marca, el límite operativo es la configuración de Floor, no el ratio ni los tiempos.
- Los cambios realizados en los controles del applet acoplado y en el editor flotante se sincronizan automáticamente. No es necesario reabrir ninguna de las dos vistas tras ajustar una de ellas.
- Para voz en SSB, un Release de 150–300 ms suele evitar que el gate se cierre durante las breves pausas entre palabras. Para tonos de audio CW, un Release mucho más corto (10–30 ms) ofrece un resultado más limpio.
- Si la banda de histéresis cian desaparece, Return está ajustado en 0.0 dB y el gate no tiene banda muerta. Cualquier señal que caiga por debajo de Thresh iniciará inmediatamente la secuencia de cierre.

## Resolución de problemas

- **El gate traquetea o fluctúa entre abierto y cerrado** — Release es demasiado corto o Return es demasiado estrecho. Aumente **Return** para que el gate permanezca abierto ante pequeñas fluctuaciones de señal cerca del umbral, o aumente **Release** para ralentizar el tiempo de cierre.
- **El gate permanece abierto demasiado tiempo después de que termina el habla** — Return es demasiado amplio o Release es demasiado largo. Reduzca **Return** para que el gate se cierre antes después de que la señal caiga, o gire **Release** hacia la izquierda para acortar la cola.
- **El ruido de fondo es audible entre palabras** — Release es demasiado largo. Gire **Release** hacia la izquierda para acortar la cola. Verifique también que **Floor** esté configurado con un valor suficientemente negativo para atenuar el ruido mientras el gate está cerrado.
- **La posición del control no coincide con la ajustada en el editor flotante** — El applet se sincroniza con el motor aproximadamente cada 33 ms. Espere un momento; la posición del control se actualizará para reflejar el valor actual del motor.

## Relacionados

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Ajustar el umbral TX justo por encima del ruido de fondo del entorno](set-tx-threshold-just-above-room-noise-floor.md)
- [Ajustar Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Elegir entre comportamiento de gate o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Observar la reducción de ganancia en vivo sin hablar](watch-live-gr-while-not-speaking.md)
