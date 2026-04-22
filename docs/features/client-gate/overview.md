# Descripción general del Noise Gate / Expander

El Noise Gate / Expander es un expansor descendente en el lado TX que atenúa el audio que cae por debajo de un nivel establecido. Úselo para silenciar el ruido de fondo y la reverberación del entorno entre palabras, sin necesidad de activar el micrófono manualmente.

## Antes de comenzar

- El applet GATE permanece oculto hasta que se habilita la etapa Gate. Habilítela a través del widget CHAIN o del editor flotante Gate.
- El applet reside dentro del contenedor principal PooDoo Audio (TXDSP), como el subcontenedor "GATE".

## Cómo funciona

Cuando la señal del micrófono cae por debajo del umbral establecido, el gate atenúa el audio en una cantidad determinada por los ajustes de ratio y floor. Cuando la señal sube nuevamente por encima del umbral, el gate se abre a la velocidad definida por attack. Cuando vuelve a caer por debajo, se cierra a la velocidad definida por release.

Con ratios bajos (cercanos a 1.0:1), el gate actúa como un expansor descendente suave: el audio por debajo del umbral se reduce gradualmente. Con ratios altos (próximos a 10.0:1), el gate actúa más como un corte abrupto que silencia de forma inmediata todo lo que esté por debajo del umbral. El floor establece un límite máximo en la profundidad de corte del gate, evitando silencios completos poco naturales entre palabras.

El applet proporciona dos indicadores en tiempo real mientras habla:

- **Transfer curve** — gráfica de la curva estática entrada-salida del expansor, con un indicador dinámico que muestra el nivel de entrada actual y si el gate está abierto o cerrado.
- **Gain-reduction bar** — una franja horizontal de color ámbar, rellena desde la derecha, que indica cuántos dB de atenuación está aplicando el gate en ese momento. La escala va de 0 a 40 dB. Una marca a 15 dB indica el valor predeterminado de Floor.

Los cambios realizados con los controles en el applet y en el editor flotante Gate se mantienen sincronizados: girar un control en cualquiera de los dos lugares actualiza el otro.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistido | Descripción |
|---|---|---|---|---|
| Thresh | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` | Nivel por debajo del cual el gate comienza a atenuar. Ajústelo justo por encima del piso de ruido del entorno. |
| Ratio | 2.0:1 | 1.0 a 10.0 | `ClientGateTxRatio` | Valores más altos producen un corte más abrupto tipo gate; valores más bajos producen una expansión descendente más suave. |
| Attack | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` | Velocidad con la que el gate se abre cuando la entrada supera el umbral. Tiempos más cortos suenan más inmediatos; tiempos más largos generan una apertura gradual. |
| Release | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` | Velocidad con la que el gate se cierra cuando la entrada cae por debajo del umbral. Tiempos más largos evitan cortes bruscos entre sílabas. |
| Floor | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` | Atenuación máxima que puede aplicar el gate. Limita cuán bajo llega el audio cuando el gate está cerrado. |

El estado de habilitación se persiste como `ClientGateTxEnabled`.

## Consejos

- Observe la gain-reduction bar mientras no esté hablando. Si muestra un valor cercano a 0 dB, reduzca el umbral: el gate no se está cerrando.
- Si el gate corta el inicio de las palabras, aumente ligeramente el valor de Attack.
- Si el gate corta el final de las palabras, aumente el valor de Release.
- Establezca Floor en un valor moderado, como −15.0 dB en lugar de −80.0 dB, para conservar una pequeña cantidad de tono ambiental y evitar silencios robóticos.
- Para abrir el editor flotante Gate, haga doble clic en la etapa Gate del widget CHAIN. Haga clic derecho en la barra de título del subcontenedor "GATE" para flotarlo, desplegarlo o ocultarlo.

## Temas relacionados

- [Ajustar el umbral justo por encima del piso de ruido del entorno](set-threshold-just-above-room-noise-floor.md)
- [Elegir entre comportamiento de gate o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ajustar attack / release para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Configurar Floor para evitar silencios poco naturales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Observar la reducción de ganancia en tiempo real mientras no se habla](watch-live-gr-while-not-speaking.md)
- [Desactivar el gate desde la cadena](bypass-the-gate-from-the-chain.md)
