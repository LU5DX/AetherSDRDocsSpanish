# Utilice AGC-G en RX para suprimir el ruido de banda por debajo de un piso seleccionado

El AGC-G del lado RX (expansor descendente del lado cliente) atenúa el audio recibido que cae por debajo de un umbral que usted configura, permitiéndole silenciar el ruido de fondo de banda o la estática entre señales, mientras mantiene intacto el audio deseado.

## Antes de comenzar

- Debe estar conectado a una radio FLEX-8600.
- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el Panel de Applets.
- La etapa Gate del lado RX debe estar habilitada a través del widget CHAIN (haga doble clic en la etapa GATE del lado RX para abrir su editor, o un solo clic para alternar el bypass).

## Pasos

1. En el Panel de Applets, localice el subcontenedor **Aetherial AGC-G (RX)** dentro del contenedor principal Aetherial Audio (TXDSP). Si está oculto, haga doble clic en la etapa GATE en el widget CHAIN del lado RX para abrir el editor flotante (titulado "Aetherial Gate — RX").

2. Ajuste **Thresh** (predeterminado: -40.0 dB) hacia abajo hasta que el ruido de banda que desea suprimir quede por debajo del umbral. Observe la bola de entrada en vivo en la visualización de la curva de transferencia: cuando la bola está por debajo de la línea de umbral, la puerta está cerrada y se aplica atenuación.

3. Configure **Floor** (predeterminado: -15.0 dB) a la atenuación máxima que desea aplicar al ruido de fondo. Un ajuste típico es de -15 a -20 dB, suficiente para silenciar el ruido sin que los espacios entre palabras suenen anormalmente silenciosos.

4. Ajuste **Ratio** (predeterminado: 2.0) para controlar la agresividad del corte de la puerta:
   - Relaciones bajas (1.0–3.0) actúan como un expansor descendente suave: el ruido de fondo se desvanece gradualmente.
   - Relaciones altas (5.0–10.0) crean una sensación de puerta más dura y tradicional.

5. Configure **Return** (predeterminado: 2.0 dB) para evitar aperturas y cierres rápidos cerca del umbral. Aparece una banda de histéresis cian en la curva de transferencia entre (Thresh − Return) y Thresh: la puerta permanece abierta dentro de esta zona hasta que la entrada cae por debajo de ella, luego debe superar Thresh para reabrirse.

6. Ajuste **Release** (predeterminado: 100 ms) para controlar la rapidez con que se cierra la puerta después de que la entrada caiga por debajo de Thresh − Return. Valores más largos (500–2000 ms) proporcionan un desvanecimiento más natural; valores más cortos (5–50 ms) pueden sonar abruptos.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|----------------|-------|-----------------|----------------|
| Thresh | -40.0 dB | -80.0 a 0.0 dB | `ClientGateRxThresholdDb` | Nivel por debajo del cual la puerta comienza a atenuar. Mapeo lineal. |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateRxRatio` | Relaciones más altas proporcionan un corte más duro, tipo puerta; relaciones más bajas actúan como un expansor descendente suave. Se muestra como "X.X:1". |
| Return | 2.0 dB | 0.0 a 20.0 dB | `ClientGateRxReturnDb` | Banda muerta de histéresis: la puerta se abre por encima de Thresh y permanece abierta hasta que la entrada cae por debajo de Thresh − Return. Se muestra como "X.XX dB". El widget de la curva de transferencia dibuja una banda vertical cian claro entre (Thresh − Return) y Thresh para hacer visible la zona pegajosa. |
| Release | 100 ms | 5 a 2000 ms | `ClientGateRxReleaseMs` | Rapidez con que se cierra la puerta después de que la entrada cae por debajo de Thresh − Return. Mapeo exponencial. Se muestra como "X.X ms" por debajo de 100 ms, "X ms" por encima. |
| Floor | -15.0 dB | -80.0 a 0.0 dB | `ClientGateRxFloorDb` | Atenuación máxima que la puerta puede aplicar. Mapeo lineal. |
| Barra de reducción de ganancia | — | 0 a 40 dB GR | — | Barra horizontal ámbar, rellena desde la derecha. La escala llega a 40 dB; una marca en -15 dB indica el Floor predeterminado. |
| Curva de transferencia | — | — | — | Grafica la curva de transferencia estática del expansor y una bola en vivo en el nivel de entrada actual. En modo compacto (cuando se usa el editor flotante), las etiquetas de los ejes se almacenan en caché como texto estático y se renderizan con un tamaño de fuente de 7 píxeles para mejorar el rendimiento. |

## Edición de valor en línea

Cada perilla de ajuste (Thresh, Ratio, Return, Release, Floor) admite la entrada numérica directa. Haga clic en el valor mostrado debajo de cualquier perilla para abrir un editor de texto en línea. Escriba un nuevo valor y presione Enter, o haga clic en otro lugar, para confirmar el cambio. La perilla se actualiza en vivo y limita el valor ingresado al rango válido. Presione Esc para cancelar la edición y volver al valor anterior. El editor utiliza un analizador con reconocimiento de configuración regional, por lo que los separadores decimales que coinciden con su configuración regional del sistema (por ejemplo, una coma en configuraciones regionales europeas) funcionan correctamente.

## Colores de perillas según el tema

Las perillas en el contenedor Aetherial AGC-G (RX) utilizan colores del espacio de nombres `color.knob.*`:
- **Anillo de fondo**: `color.knob.background`
- **Arco de primer plano**: `color.knob.foreground`
- **Indicador**: `color.knob.handle`
- **Texto de etiqueta**: `color.text.secondary`
- **Texto de valor**: `color.text.primary`

El widget de curva utiliza estos colores del tema:
- **Fondo**: `color.background.0`
- **Líneas de cuadrícula**: `color.background.1`
- **Etiquetas de ejes**: `color.text.label`
- **Curva**: `color.accent.warning` (ámbar)
- **Resplandor de la bola**: `color.accent.warning` (ámbar)
- **Núcleo de la bola**: `color.text.primary`

Los colores de las perillas siguen las anulaciones de contenedor por applet. Si crea un tema personalizado, configure los colores en el contenedor `applet/gate` para el renderizado específico de las perillas de la puerta.

## Eficiencia de animación de medidores

La barra de reducción de ganancia y otros indicadores de medidor en tiempo real en el applet de puerta utilizan interpolación suave para su animación. Para reducir el uso de CPU, la animación deja de actualizar la visualización una vez que el valor del medidor se ha estabilizado, es decir, cuando el valor suavizado ya no cambia significativamente. Se activa un repintado mínimo solo cuando el valor realmente cambia. Cuando el medidor está inactivo (sin entrada de audio), no se producen repintados hasta la próxima actualización del medidor, lo que conserva recursos en máquinas más lentas y mejora la capacidad de respuesta en sistemas alimentados por batería.

## Consejos

- Comience con Thresh justo por encima del nivel más alto de ruido de fondo que desea suprimir. Ajuste mientras escucha una señal débil: la puerta debe abrirse limpiamente cuando la señal supere el ruido.
- La barra de reducción de ganancia muestra la profundidad de atenuación en vivo. Cuando no hay señal presente, debe mostrar una GR constante igual a su configuración de Floor. Si nunca alcanza Floor, Thresh puede estar configurado demasiado bajo o el ruido de banda es demasiado alto.
- Las perillas de ajuste aquí y en el editor flotante se mantienen sincronizadas: los cambios en cualquiera de los dos lugares actualizan el otro en vivo.
- La visualización de la curva de transferencia almacena en caché las etiquetas de los ejes para un renderizado eficiente. Al cambiar entre el modo compacto (editor flotante) y el modo de tamaño completo, las etiquetas se actualizan automáticamente al tamaño de fuente adecuado.
- Para ingresar un valor preciso rápidamente, haga clic en el número mostrado debajo de cualquier perilla y escriba directamente en lugar de arrastrar la perilla.

## Relacionados

- [Configure el umbral de TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Elija el comportamiento de puerta versus expansor suave mediante la relación](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Configure Return para evitar el castañeo de la puerta cerca del umbral](set-return-to-prevent-gate-chatter-near-threshold.md)
- [Ajuste Release para un cierre de puerta natural](tune-release-for-natural-gate-close.md)
- [Configure Floor para evitar silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Pase por alto la puerta desde la cadena](bypass-the-gate-from-the-chain.md)
- [Observe la GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
