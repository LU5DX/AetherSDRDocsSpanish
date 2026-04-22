# Ajuste el umbral justo por encima del nivel de ruido de la sala

Ajuste el mando **Thresh** de modo que la gate comience a atenuar justo por encima del nivel de ruido ambiente de su sala. Esto mantiene el ruido de fondo silenciado entre transmisiones y permite que su voz pase con claridad.

## Antes de comenzar

- La etapa Gate debe estar habilitada en el widget CHAIN. Consulte [Omitir la gate desde la cadena](bypass-the-gate-from-the-chain.md) si el applet GATE no está visible.
- Permanezca en una sala silenciosa, en su posición normal de operación, para que la lectura del nivel de ruido sea representativa.

## Pasos

1. Abra el subcontenedor GATE dentro del contenedor principal PooDoo Audio (TXDSP). Si no está visible, haga doble clic en la etapa Gate del widget CHAIN para abrir el editor flotante Gate, o haga clic derecho en la barra de título del subcontenedor GATE y elija mostrarlo.
2. Observe el display **Transfer curve**. El punto de entrada en tiempo real muestra su nivel de entrada actual. Sin hablar, el punto debe ubicarse en el nivel de ruido de su sala.
3. No hable. Anote dónde reposa el punto en la curva — ese es su nivel de ruido.
4. Gire el mando **Thresh** hacia arriba (hacia 0 dB) hasta que quede entre 2 y 6 dB por encima de la posición de reposo del punto. La gate comenzará a atenuar cada vez que usted no esté hablando.
5. Confirme observando la **barra de reducción de ganancia** (Gain-reduction bar): debe mostrar relleno ámbar durante el silencio y volver a vacía cuando usted habla a un nivel normal.
6. Hable al micrófono. Verifique que el punto cruce el umbral, que la barra de reducción de ganancia caiga a vacío y que su audio pase sin cortes.
7. Si la gate se abre con demasiada lentitud o recorta el inicio de las palabras, baje **Thresh** ligeramente o ajuste **Attack**. Consulte [Ajustar ataque/liberación para una apertura y cierre natural](tune-attack-release-for-natural-open-close.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Thresh | -40.0 dB | -80.0 a 0.0 dB | `ClientGateTxThresholdDb` | Nivel por debajo del cual la gate comienza a atenuar. Ajústelo justo por encima del nivel de ruido. |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` | Valores más altos producen un corte más abrupto; valores más bajos actúan como un expansor descendente suave. |
| Attack | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` | Rapidez con la que la gate se abre cuando la entrada supera el umbral. |
| Release | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` | Rapidez con la que la gate se cierra cuando la entrada cae por debajo del umbral. |
| Floor | -15.0 dB | -80.0 a 0.0 dB | `ClientGateTxFloorDb` | Atenuación máxima que la gate puede aplicar. |

`ClientGateTxEnabled` controla si la etapa gate está activa.

## Consejos

- La escala de la **barra de reducción de ganancia** va de 0 a 40 dB. La marca en -15 dB corresponde al valor predeterminado de **Floor** — un punto de referencia útil para la operación como expansor suave.
- Los mandos del applet GATE y los del editor flotante Gate permanecen sincronizados. Los cambios realizados en cualquiera de las dos ubicaciones tienen efecto de inmediato y se guardan automáticamente.
- Ajuste **Thresh** de forma conservadora, por debajo en lugar de demasiado alto. Un umbral excesivamente alto recortará el inicio de las palabras.

## Solución de problemas

- **El punto nunca cruza el umbral durante el habla** — Thresh está ajustado demasiado alto. Gire el mando **Thresh** hacia -80 dB hasta que el habla normal empuje el punto por encima de la línea de umbral.
- **La gate no silencia el ruido de la sala entre palabras** — Thresh está ajustado demasiado bajo. Suba **Thresh** hasta que quede por encima de la posición de reposo del punto durante el silencio.
- **La gate recorta el inicio de las palabras** — **Attack** es demasiado lento o **Thresh** está demasiado cerca del nivel del habla. Baje **Thresh** ligeramente o reduzca el valor de **Attack**. Consulte [Ajustar ataque/liberación para una apertura y cierre natural](tune-attack-release-for-natural-open-close.md).
- **Silencio antinatural entre palabras** — **Floor** está aplicando demasiada atenuación. Suba **Floor** hacia 0 dB. Consulte [Ajustar Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md).

## Temas relacionados

- [Descripción general de Noise Gate / Expansor](overview.md)
- [Ver la reducción de ganancia en tiempo real sin hablar](watch-live-gr-while-not-speaking.md)
- [Ajustar ataque/liberación para una apertura y cierre natural](tune-attack-release-for-natural-open-close.md)
- [Ajustar Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Elegir entre gate y expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Omitir la gate desde la cadena](bypass-the-gate-from-the-chain.md)
