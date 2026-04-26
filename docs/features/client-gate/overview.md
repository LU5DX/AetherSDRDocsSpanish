# Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)

AetherSDR incluye un expansor descendente y una puerta de ruido del lado del cliente que funcionan de forma independiente en las rutas de audio de transmisión y recepción. Úselo para suprimir el ruido de fondo entre palabras en TX, o para reducir el ruido de banda por debajo de un nivel mínimo elegido en RX.

## Antes de comenzar

- La etapa Gate debe habilitarse mediante el widget CHAIN o el editor flotante en el lado correspondiente antes de que el applet sea visible.
- No se requiere conexión a una radio para configurar los ajustes de la puerta.

## Cómo funciona

AetherSDR instancia dos copias completamente independientes del procesador de puerta:

- **Aetherial TX Gate** — opera en la ruta de audio de transmisión. Atenúa el audio que cae por debajo del umbral establecido, reduciendo el ruido ambiente y los sonidos de respiración entre transmisiones.
- **Aetherial AGC-T** — opera en la ruta de audio de recepción. Atenúa el audio recibido por debajo del umbral, reduciendo el ruido continuo de banda entre señales.

Ambas copias aparecen como subcontenedores dentro del contenedor padre Aetherial Audio (TXDSP). Comparten el mismo conjunto de controles e indicadores, pero almacenan sus parámetros de forma independiente.

### Flujo de la señal

La puerta es un expansor descendente. Cuando el nivel de entrada cae por debajo de Thresh, la puerta comienza a atenuar la señal. La cantidad de atenuación depende de Ratio y está limitada por Floor — la puerta nunca corta más profundo que el valor de Floor, lo que evita un silencio muerto poco natural. Attack y Release controlan la rapidez con que la puerta se abre y cierra en respuesta a los cambios de nivel.

Con valores altos de Ratio (aproximándose a 10:1), la puerta se comporta como un corte abrupto; con valores bajos de Ratio (cerca de 1:1), actúa como un expansor descendente suave. La mayoría de los usuarios configuran Ratio entre 2:1 y 4:1 para obtener resultados de sonido natural.

### Retroalimentación visual

Cada mosaico de applet proporciona dos indicadores en tiempo real:

- **Curva de transferencia** — un gráfico estático de la función de transferencia entrada-salida del expansor, con una bola en movimiento que muestra el nivel de entrada actual. La posición de la bola indica si la puerta está actualmente abierta (bola por encima de la línea de umbral) o cerrada (bola por debajo de la línea de umbral).
- **Barra de reducción de ganancia** — una franja ámbar horizontal que se llena desde la derecha. La escala va de 0 a 40 dB de reducción de ganancia. Una marca en −15 dB indica el valor predeterminado de Floor. Una barra vacía significa que no se está aplicando atenuación.

Los mandos del mosaico de applet y del editor flotante (que se abre haciendo doble clic en la etapa GATE en el widget CHAIN) se mantienen sincronizados automáticamente.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistido (TX / RX) | Descripción |
|---|---|---|---|---|
| Thresh | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` | Nivel por debajo del cual la puerta comienza a atenuar. Configúrelo justo por encima del piso de ruido que desea suprimir. |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` / `ClientGateRxRatio` | Relación de expansión, mostrada como X.X:1. Valores más altos producen un corte más abrupto, similar a una puerta; valores más bajos producen una expansión descendente suave. |
| Attack | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` / `ClientGateRxAttackMs` | Rapidez con que la puerta se abre cuando la entrada sube por encima de Thresh. Valores más cortos abren más rápido. |
| Release | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` | Rapidez con que la puerta se cierra después de que la entrada cae por debajo de Thresh. Valores más largos producen una cola más natural. |
| Floor | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` / `ClientGateRxFloorDb` | Atenuación máxima que la puerta puede aplicar. Evita que la puerta produzca silencio total. |

El estado habilitado/deshabilitado de cada lado se persiste por separado: `ClientGateTxEnabled` (TX) y `ClientGateRxEnabled` (RX).

## Consejos

- Observe la barra de reducción de ganancia mientras no habla en TX. Si la barra no muestra ningún movimiento, es posible que Thresh esté configurado por debajo del piso de ruido y la puerta no se esté activando. Si nunca se vacía mientras habla, Thresh está demasiado alto.
- Los cambios realizados en los mandos del mosaico de applet y en el editor flotante se reflejan en ambas vistas dentro de un ciclo del medidor (aproximadamente 33 ms).
- Haga clic derecho en la barra de título del subcontenedor "Aetherial TX Gate" o "Aetherial AGC-T" para flotar, extraer u ocultar el mosaico sin deshabilitar el procesador de puerta.

## Temas relacionados

- [Configurar el umbral de TX justo por encima del piso de ruido ambiente](set-tx-threshold-just-above-room-noise-floor.md)
- [Usar AGC-T en RX para suprimir el ruido de banda por debajo de un nivel mínimo elegido](use-agc-t-on-rx-to-suppress-band-noise-below-a-chosen-floor.md)
- [Elegir entre comportamiento de puerta o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ajustar attack y release para una apertura/cierre natural](tune-attack-release-for-natural-open-close.md)
- [Configurar Floor para evitar silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Observar la reducción de ganancia en tiempo real mientras no habla](watch-live-gr-while-not-speaking.md)
- [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md)
