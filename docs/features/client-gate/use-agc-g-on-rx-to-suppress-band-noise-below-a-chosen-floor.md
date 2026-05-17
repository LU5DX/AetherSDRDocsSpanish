# Uso de AGC-G en RX para suprimir el ruido de banda por debajo de un umbral seleccionado

El AGC-G de RX (expansor descendente del lado del cliente) atenúa el audio recibido que se encuentra por debajo de un umbral que usted configura, permitiéndole silenciar el ruido de fondo de la banda o la estática entre señales, mientras mantiene intacto el audio deseado.

## Antes de comenzar

- Debe estar conectado a una radio FLEX-8600.
- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el Panel de Applets.
- La etapa Gate del lado RX debe estar habilitada mediante el widget CHAIN (haga doble clic en la etapa GATE del lado RX para abrir su editor, o haga clic simple para activar/desactivar el bypass).

## Pasos

1. En el Panel de Applets, localice el subcontenedor **Aetherial AGC-G (RX)** dentro del contenedor principal Aetherial Audio (TXDSP). Si está oculto, haga doble clic en la etapa GATE del widget CHAIN en el lado RX para abrir el editor flotante (titulado "Aetherial Gate — RX").

2. Ajuste **Thresh** (valor predeterminado: -40.0 dB) hacia abajo hasta que el ruido de banda que desea suprimir se sitúe por debajo del umbral. Observe la bola de entrada en vivo en la visualización de la curva de transferencia; cuando la bola esté debajo de la línea de umbral, la compuerta está cerrada y se aplica atenuación.

3. Establezca **Floor** (valor predeterminado: -15.0 dB) en la atenuación máxima que desea aplicar al ruido de fondo. Un valor típico es de -15 a -20 dB, suficiente para silenciar el ruido sin que los espacios entre palabras suenen antinaturalmente silenciosos.

4. Ajuste **Ratio** (valor predeterminado: 2.0) para controlar la agresividad con la que corta la compuerta:
   - Relaciones más bajas (1.0–3.0) actúan como un expansor descendente suave: el ruido de fondo se desvanece gradualmente.
   - Relaciones más altas (5.0–10.0) crean una sensación de compuerta más dura y tradicional.

5. Establezca **Return** (valor predeterminado: 2.0 dB) para evitar aperturas y cierres rápidos cerca del umbral. Aparece una banda de histéresis de color cian en la curva de transferencia entre (Thresh − Return) y Thresh: la compuerta permanece abierta dentro de esta zona hasta que la entrada cae por debajo de ella, luego debe superar Thresh para volver a abrirse.

6. Ajuste **Release** (valor predeterminado: 100 ms) para controlar la rapidez con que se cierra la compuerta después de que la entrada caiga por debajo de Thresh − Return. Valores más largos (500–2000 ms) proporcionan una atenuación más natural; valores más cortos (5–50 ms) pueden sonar abruptos.

## Función de cada control

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| Thresh | -40.0 dB | -80.0 a 0.0 dB | `ClientGateRxThresholdDb` | Nivel por debajo del cual la compuerta comienza a atenuar. Mapeo lineal. |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateRxRatio` | Relaciones más altas proporcionan un corte más duro, similar a una compuerta; relaciones más bajas actúan como un expansor descendente suave. Se muestra como "X.X:1". |
| Return | 2.0 dB | 0.0 a 20.0 dB | `ClientGateRxReturnDb` | Banda muerta de histéresis: la compuerta se abre por encima de Thresh y permanece abierta hasta que la entrada cae por debajo de Thresh − Return. Se muestra como "X.XX dB". El widget de curva de transferencia dibuja una banda vertical cian suave entre (Thresh − Return) y Thresh para hacer visible la zona de retención. |
| Release | 100 ms | 5 a 2000 ms | `ClientGateRxReleaseMs` | Rapidez con que se cierra la compuerta después de que la entrada caiga por debajo de Thresh − Return. Mapeo exponencial. Se muestra como "X.X ms" por debajo de 100 ms, "X ms" por encima. |
| Floor | -15.0 dB | -80.0 a 0.0 dB | `ClientGateRxFloorDb` | Atenuación máxima que la compuerta puede aplicar. Mapeo lineal. |
| Barra de reducción de ganancia | — | 0 a 40 dB GR | — | Franja horizontal ámbar, rellena desde la derecha. La escala máxima es de 40 dB; una marca en -15 dB indica el Floor predeterminado. |
| Curva de transferencia | — | — | — | Representa la curva de transferencia estática del expansor y una bola en vivo en el nivel de entrada actual. En modo compacto (cuando se usa el editor flotante), las etiquetas de los ejes se almacenan en caché como texto estático y se renderizan con un tamaño de fuente de 7 píxeles para mejorar el rendimiento. |

## Edición de valores en línea

Cada perilla de ajuste (Thresh, Ratio, Return, Release, Floor) admite la entrada numérica directa. Haga clic en el valor mostrado debajo de cualquier perilla para abrir un editor de texto en línea. Escriba un nuevo valor y presione Enter, o haga clic en otro lugar, para confirmar el cambio. La perilla se actualiza en vivo y limita el valor ingresado al rango válido. Presione Esc para cancelar la edición y volver al valor anterior. El editor utiliza un analizador que reconoce la configuración regional, por lo que los separadores decimales que coinciden con la configuración regional de su sistema (por ejemplo, una coma en las configuraciones regionales europeas) funcionan correctamente.

## Consejos

- Comience con Thresh justo por encima del nivel más alto de ruido de fondo que desea suprimir. Ajuste mientras escucha una señal débil: la compuerta debe abrirse limpiamente cuando la señal supere el ruido.
- La barra de reducción de ganancia muestra la profundidad de atenuación en vivo. Cuando no hay señal presente, debe mostrar una GR constante igual a su configuración de Floor. Si nunca alcanza Floor, es posible que Thresh esté configurado demasiado bajo o que el ruido de banda sea demasiado fuerte.
- Las perillas de ajuste aquí y en el editor flotante se mantienen sincronizadas: los cambios en un lugar actualizan el otro en vivo.
- La visualización de la curva de transferencia almacena en caché las etiquetas de los ejes para un renderizado eficiente. Al cambiar entre el modo compacto (editor flotante) y el modo de tamaño completo, las etiquetas se actualizan automáticamente al tamaño de fuente apropiado.
- Para ingresar un valor preciso rápidamente, haga clic en el número mostrado debajo de cualquier perilla y escriba directamente en lugar de arrastrar la perilla.

## Relacionados

- [Establecer umbral de TX justo por encima del nivel de ruido ambiente de la sala](set-tx-threshold-just-above-room-noise-floor.md)
- [Elegir comportamiento de compuerta vs. expansor suave mediante la relación](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Establecer Return para evitar el traqueteo de la compuerta cerca del umbral](set-return-to-prevent-gate-chatter-near-threshold.md)
- [Ajustar Release para un cierre natural de la compuerta](tune-release-for-natural-gate-close.md)
- [Establecer Floor para evitar silencios antinaturales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Pasar por alto la compuerta desde la cadena](bypass-the-gate-from-the-chain.md)
- [Observar la GR en vivo mientras no se habla](watch-live-gr-while-not-speaking.md)
