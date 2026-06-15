# Resumen del Compresor Aterial (TX) / AGC-C Aterial (RX)

AetherSDR incluye un compresor de rango dinámico del lado del cliente que se ejecuta en dos instancias independientes: **Compresor Aterial** en la ruta de TX y **AGC-C Aterial** en la ruta de RX. Use la instancia de TX para controlar los picos de voz antes de transmitir; use la instancia de RX para nivelar los niveles de audio recibido.

## Antes de empezar

- Ambas instancias residen dentro del contenedor principal **Aetherial Audio (TXDSP)** en el panel de applets. Cada mosaico permanece oculto hasta que su etapa esté habilitada; desactívela mediante el widget CHAIN o el editor flotante en el lado correspondiente.
- No se requiere conexión de radio para configurar el compresor. Los ajustes se guardan localmente.

## Cómo funciona

Cada instancia procesa el audio de forma independiente. El compresor monitorea el nivel de la señal de entrada. Cuando el nivel supera el umbral, atenúa la salida según la relación de compresión que usted elija. Los controles de Ataque y Liberación determinan la velocidad de reacción. La Ganancia de Maquillaje añade la ganancia perdida por la compresión. Un limitador opcional (configurado en el editor completo) establece un límite máximo de salida.

El mosaico del applet para cada instancia muestra:

- Una **curva de transferencia**: un gráfico estático de entrada/salida con una bola de envolvente animada que se desplaza a lo largo de la curva en tiempo real, mostrando el punto de operación actual. La curva utiliza colores adaptables al tema para fondo, cuadrícula, etiquetas, línea de identidad, línea de curva y el resplandor/núcleo de la bola.
- Una **barra de reducción de ganancia**: una tira horizontal de color ámbar que se llena desde la derecha. La escala va de 0 a 20 dB de reducción de ganancia. Una marca indica el punto de −6 dB como referencia de trabajo típica. La tira se actualiza a aproximadamente 30 Hz con balística suavizada. El color de relleno lo define el tema y se estiliza en el ámbito `applet/comp`.

Cuando una etapa del compresor está desactivada, todo su mosaico del applet se atenúa aproximadamente al 55 % de opacidad. El mosaico vuelve a la opacidad completa cuando la etapa se reactiva. Este estado visual coincide con el comportamiento de atenuación utilizado por el applet de la curva de EQ.

Para abrir el editor completo de cualquiera de las instancias (que añade controles de Rodilla, Limitador, Drive y Fase no disponibles en el applet), haga doble clic en la etapa COMP en el widget CHAIN del lado TX o RX. El editor se abre con el título **Compresor Aterial — TX** o **Compresor Aterial — RX** según corresponda.

## Función de cada control

Los cinco mandos aparecen en una fila en la parte inferior de cada mosaico del applet. Tanto la instancia de TX (Compresor Aterial) como la de RX (AGC-C Aterial) comparten la misma disposición de mandos con estado independiente.

Cada mando admite la edición en línea del valor: haga clic en el texto del valor mostrado para abrir un campo de edición. Escriba un nuevo valor y presione Enter o haga clic en otro lugar para confirmar el cambio. Presione Escape para cancelar. Mientras el campo de edición está enfocado, los eventos de la rueda del ratón continúan ajustando el mando normalmente.

| Mando   | Valor predeterminado | Rango válido      | Clave de configuración |
|---------|----------------------|-------------------|-------------------------|
| Thresh  | −18.0 dB             | −60.0 a 0.0 dB    | `ClientCompTxThresholdDb` |
| Ratio   | 3.0                  | 1.0 a 20.0        | `ClientCompTxRatio` |
| Attack  | 20.0 ms              | 0.1 a 300.0 ms    | `ClientCompTxAttackMs` |
| Release | 200 ms               | 5 a 2000 ms       | `ClientCompTxReleaseMs` |
| Makeup  | 0.0 dB               | −12.0 a 24.0 dB   | `ClientCompTxMakeupDb` |

### Detalles del comportamiento de los controles

- **Thresh**: Mapeo lineal. Establece el nivel por encima del cual comienza la compresión. La etiqueta se formatea como `-18.0 dB`.
- **Ratio**: Mapeo logarítmico (1 * 20^n). Establece cuán firmemente se contienen los picos una vez superado el umbral. La etiqueta se formatea como `X.XX:1`.
- **Attack**: Mapeo exponencial (0.1 * 3000^n). Establece la rapidez con la que el compresor reacciona después de superar el umbral. La etiqueta se formatea como `X.X ms` por debajo de 10 ms, `X ms` por encima.
- **Release**: Mapeo exponencial (5 * 400^n). Establece la rapidez con la que la ganancia se recupera después de que la entrada vuelve a estar por debajo del umbral. La etiqueta se formatea como `X ms`.
- **Makeup**: Mapeo lineal. Añade la ganancia perdida por la compresión. La etiqueta muestra el signo `+` explícito para valores positivos.

### Indicadores de la curva de compresión

- **Curva de transferencia**: ClientCompCurveWidget en modo compacto. Dibuja la curva de transferencia de entrada/salida más una bola animada que muestra el nivel de envolvente actual. Solo vista en el applet; editable en el ClientCompEditor flotante.
- **Barra de reducción de ganancia**: Tira horizontal de color ámbar, relleno desde la derecha. La escala máxima es de 20 dB de reducción; una marca en −6 dB señala una cantidad de trabajo típica. Se actualiza a ~30 Hz desde `ClientComp::gainReductionDb()` con balística de MeterSmoother. El algoritmo de suavizado utiliza un sistema de marcas con estado: la barra se vuelve a pintar solo cuando el valor suavizado cambia realmente, lo que reduce el uso de CPU manteniendo una retroalimentación visual suave.

## Controles adicionales en el editor flotante

El panel StripCompPanel flotante (abra haciendo doble clic en el mosaico COMP en el widget CHAIN) añade estos controles:

| Control   | Valor predeterminado | Rango válido           | Clave de configuración | Comportamiento |
|-----------|----------------------|------------------------|------------------------|----------------|
| Knee      | Ajustable en el editor | Ajustable en el editor | `ClientCompTxKneeDb` / `ClientCompRxKneeDb` | Anchura de la rodilla suave en dB. |
| Ceiling   | Ajustable en el editor | Ajustable en el editor | `ClientCompTxLimCeilingDb` / `ClientCompRxLimCeilingDb` | Límite máximo aplicado por el limitador. |
| Makeup    | 0.0 dB               | −12.0 a 24.0 dB        | `ClientCompTxMakeupDb` / `ClientCompRxMakeupDb` | Control duplicado en el editor por comodidad. |
| Drive     | 0.0 dB               | 0.0 a 18.0 dB          | `ClientCompTxDriveDb` / `ClientCompRxDriveDb` | Aumento de ganancia previo a la compresión con maquillaje automático vinculado. Empuja más señal a través del umbral para que el compresor trabaje más, y simultáneamente añade ganancia igual en la salida para que el nivel RMS promedio se eleve junto con los picos en lugar de caer. La etiqueta muestra `+X.X dB`. La información sobre herramientas explica la combinación de reducción de PAPR #2887. |
| Phase     | 0 etapas             | 0 a 6 etapas           | `ClientCompTxPhaseRotatorStages` / `ClientCompRxPhaseRotatorStages` | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/octava de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos de voz asimétricos antes de la compresión para reducir la PAPR. La etiqueta muestra `Off` cuando es 0, `N stg` cuando está activo. Información sobre herramientas: `Rotador de fase previo a la compresión (#2887). Cascada de paso total que simetriza los picos de voz asimétricos antes de la compresión. 0 = desactivado, 4 = valor por defecto de radiodifusión.` |
| Limiter enable | Desactivado | Desactivado / Activado | `ClientCompTxLimEnabled` / `ClientCompRxLimEnabled` | Botón de alternancia para el limitador de salida. |

## Estados de los indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Bola de envolvente | en reposo en la línea de umbral<br>moviéndose a lo largo de la curva | Nivel de entrada en vivo trazado contra la curva de transferencia estática. |
| Tira de reducción de ganancia | vacía<br>relleno ámbar<br>marca de −6 dB | Cantidad de atenuación dinámica aplicada actualmente por el compresor. |

## Consejos

- La bola de envolvente en la curva de transferencia proporciona una retroalimentación visual continua. Si la bola se sitúa muy por encima de la rodilla en reposo, el umbral está demasiado bajo; suba Thresh hasta que la bola solo cruce la rodilla en los picos.
- La marca de −6 dB en la barra de reducción de ganancia es un punto de referencia útil. Un relleno ámbar consistente hasta ese punto o ligeramente más allá indica una compresión activa y moderada. Un relleno que llegue al borde derecho de la barra significa que el compresor está trabajando en o más allá de 20 dB de reducción.
- Cuando una etapa está desactivada, el mosaico se atenúa visiblemente. Si el mosaico parece atenuado y los controles no responden, verifique que la etapa COMP no esté desactivada en el widget CHAIN.
- Las instancias de TX y RX son completamente independientes. Los cambios en el Compresor Aterial (TX) no afectan al AGC-C Aterial (RX) y viceversa.
- Los controles de Rodilla, Limitador, Drive y Fase no están disponibles en el mosaico del applet. Abra el editor completo para acceder a ellos.
- Para cambiar el valor de un mando escribiendo directamente, haga clic en el texto del valor mostrado. El campo de edición aparece con un fondo oscuro y un borde cian. Escriba el nuevo valor y presione Enter o haga clic en otro lugar para aplicarlo. Presione Escape para cancelar sin cambiar el valor.
- El mando Drive incluye ganancia de maquillaje automática: al aumentar Drive, el compresor trabaja más mientras que la ganancia de salida se eleva simultáneamente, por lo que el nivel RMS promedio se mantiene. Esto coincide con el modelo de radiodifusión Optimod: Drive empuja más material a la curva Y añade la misma ganancia de vuelta, así que su mando Makeup fijo sigue siendo un ajuste final limpio posterior a todo.
- El medidor de reducción de ganancia utiliza un algoritmo de suavizado eficiente que solo se vuelve a pintar cuando el valor suavizado cambia, reduciendo el uso de CPU mientras mantiene una retroalimentación visual suave.

## Relacionados

- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Establecer la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Ajustar ataque/liberación para una compresión con sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de maquillaje después de la compresión](apply-make-up-gain-after-compression.md)
- [Ver la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Desactivar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
- [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
