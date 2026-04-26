# Ajustar Attack y Release para una apertura/cierre natural

Attack y Release controlan la rapidez con que el gate se abre cuando su voz supera el umbral, y la rapidez con que se cierra cuando cae por debajo de él. Configurarlos correctamente elimina la primera sílaba recortada (Attack demasiado lento) y el corte abrupto tras cada palabra (Release demasiado rápido) que hacen que el gate suene artificial.

## Antes de comenzar

- El gate debe estar habilitado en el lado que desea ajustar (TX o RX). Consulte [Omitir el gate desde la cadena](bypass-the-gate-from-the-chain.md) para confirmar que la etapa de gate está activa.
- Abra el subcontenedor Aetherial TX Gate (lado TX) o Aetherial AGC-T (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets. Si el subcontenedor no es visible, haga doble clic en la etapa GATE del widget CHAIN del lado correspondiente para abrir el editor de gate flotante.

## Pasos

1. Localice el mando **Attack** en la fila de cinco mandos ubicada en la parte inferior del applet.
2. Gire **Attack** hacia la izquierda para abrir más rápido (mínimo 0.1 ms) o hacia la derecha para abrir más lento (máximo 100.0 ms). El valor predeterminado es 0.50 ms. Para la mayoría del trabajo de voz, valores entre 0.5 ms y 5 ms evitan recortar el borde inicial de las consonantes.
3. Hable con normalidad y observe la bola de entrada en la curva de transferencia y la barra ámbar de reducción de ganancia. Si la barra muestra un breve pico de reducción de ganancia al inicio de cada palabra, Attack es demasiado lento — gírelo hacia la izquierda.
4. Localice el mando **Release** en la misma fila.
5. Gire **Release** hacia la izquierda para cerrar más rápido (mínimo 5 ms) o hacia la derecha para cerrar más lento (máximo 2000 ms). El valor predeterminado es 100 ms. Para un habla natural, valores entre 80 ms y 400 ms permiten que el gate se desvanezca gradualmente en lugar de cortar de forma abrupta.
6. Deje de hablar y observe la barra de reducción de ganancia. Si la barra se llena rápidamente y la señal se corta de forma antinatural entre palabras, aumente Release (gire a la derecha). Si el ruido de fondo reaparece durante las pausas, disminuya Release (gire a la izquierda).
7. Repita los pasos 2–6 hasta que las pausas suenen naturales y el gate se abra limpiamente en la primera sílaba.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste persistente (TX / RX) |
|---|---|---|---|
| **Attack** | 0.50 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` / `ClientGateRxAttackMs` |
| **Release** | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |

Attack utiliza mapeo exponencial de mando (0.1 × 1000^n). Release utiliza mapeo exponencial de mando (5 × 400^n). Ambos mandos guardan los cambios de inmediato; los valores persisten entre reinicios y se comparten entre los mandos del applet y el editor flotante.

La barra de reducción de ganancia muestra de 0 a 40 dB de atenuación como una franja ámbar rellena hacia la derecha. Una marca de referencia en −15 dB corresponde al valor predeterminado de **Floor**. Use esta barra como guía en tiempo real: una apertura limpia mostrará la barra creciendo suavemente durante las pausas, en lugar de saltar al máximo de escala.

## Consejos

- Attack y Release interactúan con **Thresh** y **Ratio**. Una relación más pronunciada (valor más alto) hace que los errores de temporización sean más audibles — considere reducir Ratio hacia 2.0:1 mientras ajusta Attack/Release, y luego ajuste Ratio una vez que la temporización se sienta correcta.
- Los cambios en los mandos realizados en el editor de gate flotante y en el tile del applet se mantienen sincronizados automáticamente; no es necesario cerrar el editor para ver los valores actualizados en el applet.
- La bola de entrada en la curva de transferencia se mueve para indicar si el gate está actualmente abierto (bola por encima de la línea de umbral) o cerrado (bola por debajo). Obsérvela durante el habla natural para confirmar que el gate está siguiendo correctamente.

## Solución de problemas

- **La primera sílaba de cada palabra se recorta o suena apagada** — Attack es demasiado lento. Gire el mando **Attack** hacia la izquierda, en dirección a 0.1 ms, hasta que el gate se abra antes de que se pierda la sílaba.
- **El gate se cierra demasiado rápido, cortando el final de las palabras** — Release es demasiado corto. Gire el mando **Release** hacia la derecha. Para voz, comience alrededor de 150–200 ms.
- **Se escucha ruido de fondo entre palabras** — Release es demasiado largo, o **Thresh** está configurado por debajo del piso de ruido. Reduzca Release y/o aumente Thresh. Consulte [Ajustar el umbral de TX justo por encima del piso de ruido del entorno](set-tx-threshold-just-above-room-noise-floor.md).
- **El valor del mando en el applet no coincide con el editor flotante** — Espere un ciclo del medidor (aproximadamente 33 ms); el applet sincroniza las posiciones de los mandos desde el motor en cada ciclo y se actualizará automáticamente.

## Temas relacionados

- [Ajustar el umbral de TX justo por encima del piso de ruido del entorno](set-tx-threshold-just-above-room-noise-floor.md)
- [Elegir entre comportamiento de gate o expansor suave mediante Ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ajustar Floor para evitar silencios antinaturales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Observar la reducción de ganancia en tiempo real mientras no se habla](watch-live-gr-while-not-speaking.md)
