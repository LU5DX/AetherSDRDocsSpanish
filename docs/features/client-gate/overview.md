# Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)

AetherSDR incluye un expansor descendente y puerta de ruido del lado del cliente que opera de forma independiente en las rutas de audio de transmisión y recepción. Úselo para suprimir el ruido de fondo entre palabras en TX, o para reducir el ruido de banda por debajo de un nivel mínimo elegido en RX.

## Antes de comenzar

- La etapa Gate debe habilitarse mediante el widget CHAIN o el editor flotante del lado correspondiente antes de que el applet sea visible.
- AetherSDR no necesita estar conectado a un radio para ajustar los controles de la puerta, pero el audio debe estar en funcionamiento para que los indicadores en tiempo real sean significativos.

## Cómo funciona

AetherSDR instancia dos copias completamente independientes del applet de puerta:

- **Aetherial TX Gate** — actúa sobre el audio de transmisión saliente. Se encuentra en el contenedor principal Aetherial Audio (TXDSP).
- **Aetherial AGC-T** — actúa sobre el audio de recepción entrante. Se encuentra en el mismo contenedor principal como un subcontenedor separado.

Ambas copias comparten controles e indicadores idénticos. Los ajustes de cada lado se almacenan de forma independiente. Los cambios realizados en el mosaico del applet acoplado y los cambios realizados en el editor flotante permanecen sincronizados; el applet consulta el motor aproximadamente cada 33 ms y actualiza las posiciones de los mandos y la barra de reducción de ganancia para reflejar el lado activo.

### Flujo de señal

La puerta es un **expansor descendente**. Cuando el nivel de entrada cae por debajo del punto Thresh, la puerta atenúa la señal. La cantidad de atenuación depende de Ratio, y el corte máximo permitido se establece con Floor. Attack controla la rapidez con que la puerta se abre cuando la señal sube por encima de Thresh; Release controla la rapidez con que se cierra cuando la señal vuelve a caer por debajo de él.

Ajustar Ratio a un valor bajo (cerca de 1.0:1) produce un efecto suave de expansor gradual que reduce el nivel progresivamente. Ajustar Ratio a un valor alto (cerca de 10.0:1) produce una puerta dura que corta de forma agresiva.

### Abrir el applet

Haga doble clic en la etapa GATE en el widget CHAIN del lado TX o RX para abrir el editor sin marco correspondiente, titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**. Las barras de título de los subcontenedores acoplados de **Aetherial TX Gate** y **Aetherial AGC-T** pueden recibir clic derecho para flotar, desprender u ocultar el mosaico.

## Qué hace cada control

Los controles que se enumeran a continuación aparecen de forma idéntica en los applets de TX y RX. Las claves de ajuste mostradas corresponden al lado TX; el lado RX utiliza las claves equivalentes `ClientGateRx*`.

| Control | Tipo | Valor predeterminado | Rango válido | Clave de ajuste TX | Comportamiento |
|---|---|---|---|---|---|
| Curva de transferencia | Indicador | — | — | — | Traza la curva de transferencia estática del expansor. Una bola en tiempo real marca el nivel de entrada actual e indica si la puerta está abierta o cerrada. |
| Barra de reducción de ganancia | Medidor | — | 0 a 40 dB GR | — | Franja ámbar horizontal, rellena desde la derecha. La escala llega hasta 40 dB. Una marca en −15 dB señala el nivel mínimo predeterminado del expansor suave. |
| Thresh | Mando | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` | Nivel por debajo del cual la puerta comienza a atenuar. |
| Ratio | Mando | 2.0:1 | 1.0 a 10.0 | `ClientGateTxRatio` | Valores más altos producen un corte de puerta más duro; valores más bajos actúan como expansor descendente suave. |
| Return | Mando | 2.0 dB | 0.0 a 20.0 dB | — | Histéresis por encima de Thresh en la que la puerta vuelve a abrirse. |
| Release | Mando | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` | Rapidez con que la puerta se cierra después de que la entrada cae por debajo del umbral. |
| Floor | Mando | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` | Atenuación máxima que la puerta puede aplicar. |

El estado habilitado/omitido de cada lado se guarda en `ClientGateTxEnabled` (TX) y `ClientGateRxEnabled` (RX).

## Consejos

- Observe la barra de reducción de ganancia mientras no habla (TX) o durante un momento de solo ruido de banda (RX). Si la barra no se llena, Thresh está ajustado por debajo del piso de ruido y la puerta no se está activando. Consulte [Observar la RG en tiempo real mientras no habla](watch-live-gr-while-not-speaking.md).
- La marca de −15 dB en la barra de reducción de ganancia señala el valor predeterminado de Floor. Si la barra se llena completamente más allá de esa marca, Floor está ajustado por debajo de −15 dB o Ratio es lo suficientemente alto como para superar ese valor.
- Los cambios en cualquier mando tienen efecto inmediato y se guardan automáticamente. No se necesita ningún botón Apply.

## Solución de problemas

- **El applet no es visible** — La etapa Gate no ha sido habilitada en ese lado. Habilítela mediante el widget CHAIN o el editor flotante del lado TX o RX.
- **La puerta no atenúa el ruido entre palabras** — Es posible que Thresh esté ajustado demasiado bajo, por debajo del piso de ruido ambiental. Suba Thresh hasta que la barra de reducción de ganancia muestre movimiento durante el silencio. Consulte [Ajustar el umbral TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md).
- **La puerta corta el inicio del habla** — Attack es demasiado lento en relación con el inicio de su voz, o Thresh está demasiado alto. Baje Thresh ligeramente o reduzca Attack. Consulte [Ajustar attack / release para una apertura/cierre natural](tune-attack-release-for-natural-open-close.md).
- **Silencio antinatural entre palabras** — Floor está ajustado demasiado profundo. Suba Floor hacia 0 dB para que algo de audio residual pase durante los períodos de cierre. Consulte [Ajustar Floor para evitar silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md).
- **Las posiciones de los mandos en el mosaico no coinciden con el editor flotante** — El mosaico se sincroniza cada ~33 ms. Si aparecen desincronizados inmediatamente después de abrir el editor, espere un ciclo de actualización o mueva un mando para forzar la sincronización.

## Relacionados

- [Ajustar el umbral TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Usar AGC-T en RX para suprimir el ruido de banda por debajo de un nivel mínimo elegido](use-agc-t-on-rx-to-suppress-band-noise-below-a-chosen-floor.md)
- [Elegir comportamiento de puerta o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ajustar attack / release para una apertura/cierre natural](tune-attack-release-for-natural-open-close.md)
- [Ajustar Floor para evitar silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Observar la RG en tiempo real mientras no habla](watch-live-gr-while-not-speaking.md)
- [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md)
