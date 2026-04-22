# Ver la reducción de ganancia en vivo sin hablar

La barra de reducción de ganancia y la curva de transferencia se actualizan en tiempo real, de modo que puede observar exactamente cuánta atenuación está aplicando el gate, incluso cuando no está transmitiendo. Esto le permite verificar que el gate se cierra limpiamente entre palabras y se abre con suficiente rapidez cuando habla.

## Antes de comenzar

- El módulo Gate debe estar habilitado en el widget CHAIN. El subcontenedor GATE permanece oculto hasta que el módulo esté activo.
- El subcontenedor GATE debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).

## Pasos

1. Abra el contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. Localice el subcontenedor GATE. Si no está visible, habilite el módulo Gate mediante el widget CHAIN.
3. Permanezca en silencio — no hable frente al micrófono.
4. Observe la **barra de reducción de ganancia**: la franja ámbar se llena desde la derecha. Un llenado completo indica que el gate está aplicando cerca de 40 dB de atenuación. Sin llenado significa que el gate está abierto y deja pasar el audio.
5. Observe la **curva de transferencia**: la bola de nivel de entrada en vivo se desplaza hacia la izquierda a lo largo de la curva a medida que el nivel de entrada cae por debajo del punto Thresh.
6. Hable brevemente y luego vuelva al silencio. Confirme que el llenado ámbar regresa con rapidez tras dejar de hablar. Si no lo hace, puede ser necesario ajustar el tiempo de Release — consulte [Ajustar el ataque y la liberación para una apertura/cierre natural](tune-attack-release-for-natural-open-close.md).

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|---|
| Transfer curve | Indicador | — | — | — |
| Gain-reduction bar | Medidor | — | 0 a 40 dB GR | — |
| Thresh | Perilla | -40.0 dB | -80.0 a 0.0 dB | `ClientGateTxThresholdDb` |
| Ratio | Perilla | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` |
| Attack | Perilla | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` |
| Release | Perilla | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` |
| Floor | Perilla | -15.0 dB | -80.0 a 0.0 dB | `ClientGateTxFloorDb` |

**Barra de reducción de ganancia:** Franja ámbar horizontal que se llena desde la derecha. La escala va de 0 a 40 dB. Una marca en la posición de -15 dB señala el valor predeterminado de Floor. Cuando el gate está abierto (usted habla por encima del umbral), la barra está vacía.

**Curva de transferencia:** Muestra la curva de transferencia estática del expansor. La bola de nivel de entrada en vivo indica el nivel de entrada actual y si el gate está abierto o cerrado. Por debajo del punto Thresh, la bola se desplaza hacia la zona atenuada de la curva.

## Consejos

- El temporizador del medidor se actualiza aproximadamente cada 33 ms, por lo que la barra refleja la reducción de ganancia casi en tiempo real.
- Los cambios realizados en el editor flotante de Gate se reflejan en vivo en las perillas del subcontenedor GATE y viceversa — ambas vistas permanecen sincronizadas sin necesidad de reiniciar.
- La marca de -15 dB en la barra de reducción de ganancia corresponde al valor predeterminado de Floor (`ClientGateTxFloorDb`). Si la barra nunca supera esa marca en reposo, Floor está cumpliendo su función al evitar un corte inusualmente profundo.

## Relacionados

- [Establecer el umbral justo por encima del nivel de ruido ambiental](set-threshold-just-above-room-noise-floor.md)
- [Ajustar el ataque y la liberación para una apertura/cierre natural](tune-attack-release-for-natural-open-close.md)
- [Establecer Floor para evitar silencios antinaturales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Elegir el comportamiento de gate o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
