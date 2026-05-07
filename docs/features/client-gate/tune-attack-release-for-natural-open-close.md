# Ajuste de Return / Release para apertura y cierre naturales

Ajuste los mandos de Return y Release para controlar la banda muerta de histéresis de la puerta y la rapidez con que se cierra cuando el audio cae por debajo del umbral. Una configuración correcta evita el aleteo rápido cerca del umbral y los cortes abruptos entre palabras.

## Antes de comenzar

- La etapa de puerta debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) si la etapa aún no está activa.
- Abra el subcontenedor "Aetherial TX Gate" o "Aetherial AGC-T" dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante de ese lado.
- Reproduzca audio o hable al micrófono para que la barra de reducción de ganancia se mueva mientras ajusta.

## Pasos

1. Localice la fila de mandos en la parte inferior del applet. Busque el mando etiquetado **Return** (tercer mando desde la izquierda en TX; misma posición en RX).
2. Gire **Return** hacia la derecha (valores más altos) para ampliar la banda muerta de histéresis: la puerta se abre cuando la entrada supera Thresh y no se cierra hasta que la entrada cae por debajo de Thresh − Return. Gírelo hacia la izquierda (hacia 0.0 dB) para reducir la banda muerta y que la puerta se cierre antes después de que la señal disminuya. El valor predeterminado es 2.0 dB. El rango válido es de 0.0 a 20.0 dB.
3. Observe la curva de transferencia. Aparece una banda vertical en color cian suave entre (Thresh − Return) y Thresh, que muestra la zona de retención. Una banda más ancha significa que la puerta permanece abierta en un rango de señal más amplio antes de cerrarse.
4. Observe la bola de entrada en vivo sobre la curva de transferencia. Cuando el nivel de su señal se sitúe cerca del umbral, la bola debe reposar dentro de la banda cian sin provocar que la puerta se abra y cierre repetidamente.
5. Localice el mando etiquetado **Release** (cuarto mando desde la izquierda).
6. Gire **Release** hacia la derecha (valores más altos) para que la puerta se cierre más lentamente después de que el audio caiga por debajo de Thresh − Release — esto suaviza la cola entre palabras. Gírelo hacia la izquierda para un cierre más rápido y un corte más agresivo del ruido de fondo. El valor predeterminado es 100 ms. El rango válido es de 5 a 2000 ms.
7. Pronuncie una frase con pausas naturales y observe la barra de reducción de ganancia. El relleno ámbar debe crecer suavemente durante el silencio y retraerse limpiamente cuando el habla se reanude, sin bombeo ni saltos bruscos.
8. Si la puerta se cierra de golpe a mitad de una palabra, aumente **Release**. Si el ruido de fondo se filtra entre frases, reduzca **Release**.
9. Si la puerta se abre y cierra rápidamente con señales cercanas al umbral, aumente **Return** para ampliar la banda muerta.

## Qué hace cada control

| Mando                  | Valor predeterminado                                                                                                                                                                                                                                                       | Rango válido                                                                                                                                                                                                                                                           |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Return                 | 2.0 dB                                                                                                                                                                                                                                                                     | 0.0 – 20.0 dB                                                                                                                                                                                                                                                          |
| Release                | 100 ms                                                                                                                                                                                                                                                                     | 5 – 2000 ms                                                                                                                                                                                                                                                            |
| Flip (Expander / Gate) | Sin marcar = expansor descendente (suave, basado en relación). Marcado = Gate (corte duro). Ajusta la relación y el piso a pares predefinidos al alternar; los demás mandos permanecen igual. La etiqueta se actualiza en vivo entre 'Expander' y 'Gate'.                 | Control solo del editor (ClientGateEditor flotante). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Información sobre herramientas: 'Alterna entre modo expansor descendente (suave) y compuerta (duro). Ajusta relación + piso a pares predefinidos; los demás mandos permanecen donde los dejó.' |
| Peek (lookahead)       | Establece un retardo de prelectura para que la puerta pueda abrirse una fracción antes de que llegue un transitorio, evitando bordes de ataque recortados. 'Off' desactiva completamente la línea de retardo.                                                              | Control solo del editor. Valores más altos aumentan la latencia en la ruta de TX. 1 y 1.5 ms coinciden con las opciones predefinidas de Ableton; se agregaron 3 y 5 ms para transitorios muy rápidos.                                                                  |
| Attack                 | Mapeo exponencial (0.1 * 1000^n). Define la rapidez con que se abre la puerta después de que la entrada supera Thresh.                                                                                                                                                     | Control solo del editor. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima.                                                                                                                                                                                   |
| Hold                   | Mapeo lineal (n * 500). Después de que la entrada cae por debajo de Thresh − Return, la puerta permanece abierta durante este tiempo antes de comenzar a cerrarse, evitando fluctuaciones en material rítmico.                                                       | Control solo del editor. Etiqueta 'X.X ms'.                                                                                                                                                                                                                             |

## Consejos

- La barra de reducción de ganancia llega a un máximo de 40 dB y la marca en la posición de −15 dB corresponde al valor de piso predeterminado. Use esta marca como referencia visual: si el relleno ámbar rara vez alcanza la marca, su ajuste de Floor es el límite que gobierna, no la relación ni la temporización.
- Los cambios realizados en los mandos del applet acoplado y en el editor flotante se mantienen sincronizados automáticamente. No es necesario volver a abrir ninguna vista después de ajustar una.
- Para voz en SSB, un Release de 150–300 ms normalmente evita que la puerta se cierre durante las pausas breves entre palabras. Para tonos de audio en CW, un Release mucho más corto (10–30 ms) da un resultado más limpio.
- Si la banda de histéresis cian desaparece, Return está en 0.0 dB y la puerta no tiene banda muerta. Cualquier señal que caiga por debajo de Thresh iniciará inmediatamente la secuencia de cierre.

## Solución de problemas

- **La puerta oscila o aletea entre abierta y cerrada** — Release es demasiado corto, o Return demasiado estrecho. Aumente **Return** para que la puerta permanezca abierta ante pequeñas fluctuaciones de señal cerca del umbral, o aumente **Release** para ralentizar el tiempo de cierre.
- **La puerta permanece abierta demasiado tiempo después de que termina el habla** — Return es demasiado amplio o Release demasiado largo. Reduzca **Return** para que la puerta se cierre antes después de que la señal disminuya, o gire **Release** hacia la izquierda para acortar la cola.
- **Ruido de fondo audible entre palabras** — Release es demasiado largo. Gire **Release** hacia la izquierda para acortar la cola. Verifique también que **Floor** esté ajustado a un valor suficientemente negativo para atenuar el ruido mientras está cerrada.
- **La posición del mando no coincide con lo establecido en el editor flotante** — El applet se sincroniza desde el motor aproximadamente cada 33 ms. Espere un momento; la posición del mando se actualizará para reflejar el valor actual del motor.

## Relacionados

- [Aetherial TX Gate / Aetherial AGC-T (RX) overview](overview.md)
- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
