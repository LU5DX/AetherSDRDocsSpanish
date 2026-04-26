# Elegir entre comportamiento de gate y expansor suave mediante el Ratio

El control **Ratio** determina la agresividad con que el gate atenúa el audio por debajo del umbral. Los valores bajos producen una expansión descendente suave; los valores altos producen un gate duro que corta casi por completo. Ajustando este único control es posible seleccionar cualquier punto de ese espectro sin modificar ningún otro ajuste.

## Antes de comenzar

- La etapa Gate debe estar habilitada. Si el subcontenedor GATE no es visible en el panel PooDoo Audio (TXDSP), habilite la etapa Gate mediante el widget CHAIN o haga doble clic en la etapa Gate en el widget CHAIN para abrir el editor flotante Gate.
- Debe ser capaz de producir audio cerca del nivel de ruido de fondo (ventiladores, ambiente de la sala) para que el efecto sea audible mientras realiza los ajustes.

## Pasos

1. Localice el subcontenedor GATE dentro del panel PooDoo Audio (TXDSP).
2. Encuentre el control etiquetado como **Ratio** — muestra su valor como `X.X:1`.
3. Gire **Ratio** hacia **1.0** (mínimo) para obtener expansión descendente suave: el audio por debajo del umbral se atenúa gradualmente, con fundidos de sonido natural entre palabras.
4. Gire **Ratio** hacia **10.0** (máximo) para obtener un comportamiento de gate duro: el audio por debajo del umbral se corta de forma brusca, aproximándose a un silenciamiento total.
5. Observe la barra de reducción de ganancia mientras habla y luego guarda silencio. Un relleno ámbar moderado confirma que la atenuación está ocurriendo. Un relleno de ancho completo con valores de ratio altos indica que un corte duro está en efecto.
6. Verifique la curva de transferencia — la pendiente de la curva por debajo del umbral se hace más pronunciada a medida que aumenta el ratio, mostrando visualmente el corte más duro.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` | Controla la pendiente de atenuación por debajo del umbral. Los valores más bajos actúan como un expansor descendente suave; los valores más altos actúan como un gate duro. Se muestra como `X.X:1`. |
| Thresh | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` | Nivel por debajo del cual el gate comienza a atenuar. El ratio se aplica en relación con este punto. |
| Floor | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` | Atenuación máxima que el gate puede aplicar, independientemente del ratio. La barra de reducción de ganancia incluye una marca en −15 dB que señala este valor predeterminado. |
| Barra de reducción de ganancia | — | 0 a 40 dB GR | — | Franja ámbar horizontal, rellena desde la derecha. Muestra la profundidad actual de atenuación mientras el gate está activo. |
| Curva de transferencia | — | — | — | Representa la curva estática de entrada a salida. La pendiente por debajo del umbral refleja el ajuste actual del ratio. La bola de entrada en tiempo real indica si el gate está actualmente abierto o cerrado. |

## Consejos

- Un ratio de 2.0:1 (el valor predeterminado) es un punto de partida razonable para voz: reduce el ruido de fondo de forma notable sin el corte artificial de un gate duro.
- Si la voz suena recortada o entrecortada con ratios altos, aumente el valor de Floor hacia 0 dB para limitar el corte máximo, o reduzca el ratio.
- El control Floor limita la atenuación independientemente de cuán alto se configure el ratio. Si un gate duro no corta con suficiente profundidad, verifique que Floor esté configurado lo suficientemente bajo (por ejemplo, −40 dB o menor) para permitir el corte completo.
- Los cambios realizados en el editor flotante Gate se reflejan en los controles del applet GATE dentro de un ciclo de actualización, y viceversa.

## Solución de problemas

- **El Ratio está en 10.0:1 pero el ruido de fondo sigue siendo audible entre palabras** — el valor de Floor puede estar limitando la atenuación antes de que el gate alcance su máxima profundidad. Reduzca `ClientGateTxFloorDb` (por ejemplo, a −40.0 dB o por debajo) para permitir cortes más profundos.
- **La voz suena artificialmente entrecortada incluso con ratios moderados** — el umbral puede estar demasiado alto, lo que provoca que el gate se active con voz baja además de con ruido. Reduzca `ClientGateTxThresholdDb` hasta que solo el ruido de fondo genuino quede por debajo de él.
- **La curva de transferencia no se actualiza al girar el control Ratio** — la etapa GATE puede no estar habilitada. Habilítela mediante el widget CHAIN.

## Temas relacionados

- [Establecer el umbral justo por encima del nivel de ruido de sala](set-threshold-just-above-room-noise-floor.md)
- [Establecer Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Ajustar ataque y liberación para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Observar la reducción de ganancia en tiempo real sin hablar](watch-live-gr-while-not-speaking.md)
- [Descripción general del Noise Gate / Expansor](overview.md)
