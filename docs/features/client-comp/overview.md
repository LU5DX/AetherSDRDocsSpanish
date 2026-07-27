# Resumen del Compresor Aetherial (TX) / AGC-C Aetherial (RX)

AetherSDR incluye un compresor de rango dinámico del lado del cliente que se ejecuta en dos instancias independientes: **Compresor Aetherial** en la ruta de TX y **AGC-C Aetherial** en la ruta de RX. Use la instancia TX para suavizar los picos de voz antes de transmitir; use la instancia RX para nivelar los niveles de audio recibido.

## Antes de comenzar

- Ambas instancias residen dentro del contenedor principal **Aetherial Audio (TXDSP)** en el panel de applets. Cada mosaico permanece oculto hasta que su etapa esté habilitada; desvíela (bypass) mediante el widget CHAIN o el editor flotante en el lado correspondiente.
- No se requiere conexión de radio para configurar el compresor. La configuración se guarda localmente.

## Cómo funciona

Cada instancia procesa el audio de forma independiente. El compresor monitorea el nivel de la señal de entrada. Cuando el nivel supera el umbral, atenúa la salida según la relación de compresión que elija. Los controles de Ataque (Attack) y Liberación (Release) determinan la rapidez con la que reacciona. La ganancia de compensación (Makeup) agrega ganancia para recuperar la pérdida por compresión. Un limitador opcional (configurado en el editor completo) establece un límite máximo fijo en la salida.

El mosaico del applet para cada instancia muestra:

- Una **curva de transferencia**: un gráfico estático de entrada/salida con una bola de envolvente en vivo que se desplaza a lo largo de la curva en tiempo real, mostrando el punto de operación actual. La curva utiliza colores compatibles con el tema para el fondo, la cuadrícula, las etiquetas, la línea de identidad, la línea de la curva y el brillo/núcleo de la bola.
- Una **barra de reducción de ganancia**: una franja horizontal de color ámbar que se llena desde la derecha. La escala va de 0 a 20 dB de reducción de ganancia. Una marca indica el punto de −6 dB como referencia de trabajo típica. La franja se actualiza aproximadamente a 30 Hz con balística suavizada. El color de relleno está definido por el tema y se estiliza en el ámbito `applet/comp`.

Cuando una etapa del compresor está desviada (bypass), todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad. El mosaico vuelve a la opacidad completa cuando la etapa se reactiva. Este estado visual coincide con el comportamiento de atenuación utilizado por el applet de la curva de ecualización.

Para abrir el editor completo de cualquiera de las instancias (que añade controles de Knee (rodilla), limitador, Drive (impulso) y Phase (fase) no disponibles en el applet), haga doble clic en la etapa COMP en el widget CHAIN del lado TX o RX. El editor se abre con el título **Compresor Aetherial — TX** o **Compresor Aetherial — RX** según corresponda.

## Función de cada control

Los cinco mandos aparecen en una fila en la parte inferior de cada mosaico del applet. Tanto la instancia TX (Compresor Aetherial) como la RX (AGC-C Aetherial) comparten la misma disposición de mandos con estado independiente.

Cada mando admite la edición de valores en línea: haga clic en el texto del valor mostrado para abrir un campo de edición. Escriba un nuevo valor y presione Enter o haga clic en otro lugar para confirmar el cambio. Presione Escape para cancelar. Mientras el campo de edición está enfocado, los eventos de la rueda del ratón continúan ajustando el mando como de costumbre.

| Mando   | Valor predeterminado                                                                                                                                                                                                                                                                    | Rango válido                                                                                                                                                                                                                                                                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Thresh  | −18.0 dB                                                                                                                                                                                                                                                                                | −60.0 a 0.0 dB                                                                                                                                                                                                                                                                                                                                                                     |
| Ratio   | 3.0                                                                                                                                                                                                                                                                                     | 1.0 a 20.0                                                                                                                                                                                                                                                                                                                                                                         |
| Attack  | 20.0 ms                                                                                                                                                                                                                                                                                 | 0.1 a 300.0 ms                                                                                                                                                                                                                                                                                                                                                                     |
| Release | 200 ms                                                                                                                                                                                                                                                                                  | 5 a 2000 ms                                                                                                                                                                                                                                                                                                                                                                        |
| Makeup  | 0.0 dB                                                                                                                                                                                                                                                                                  | −12.0 a 24.0 dB                                                                                                                                                                                                                                                                                                                                                                    |
| Drive   | Aumento de ganancia previo a la compresión con compensación automática vinculada. Empuja más señal por encima del umbral para que el compresor actúe con más fuerza y, simultáneamente, añade la misma cantidad de ganancia en la salida, elevando el RMS promedio junto con los picos en lugar de reducirlo. Combínelo con Phase para mantener los picos limpios. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta aparece como '+X.X dB'. La información sobre herramientas explica el emparejamiento de reducción de PAPR #2887. La compensación automática sigue el modelo de difusión Optimod: Drive introduce más material en la curva Y añade la misma ganancia de vuelta, por lo que el mando MakeUp fijo del usuario permanece como un control de ajuste final limpio posterior a todo. |
| Phase   | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/oct de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos asimétricos de la voz antes de la compresión para reducir el PAPR. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. Información sobre herramientas: 'Rotador de fase previo a la compresión (#2887). Cascada de paso total que simetriza los picos asimétricos de la voz antes de la compresión. 0 = desactivado, 4 = valor predeterminado de difusión.' Los centros predeterminados (300/700/1500/2500 Hz con 1000/2000 Hz opcionales) cubren el rango de formantes del habla sin agruparse. |

### Detalles del comportamiento de los controles

- **Thresh**: Mapeo lineal. Establece el nivel por encima del cual comienza la compresión. La etiqueta se formatea como `-18.0 dB`.
- **Ratio**: Mapeo logarítmico (1 * 20^n). Define la intensidad con la que se contienen los picos una vez superado el umbral. La etiqueta se formatea como `X.XX:1`.
- **Attack**: Mapeo exponencial (0.1 * 3000^n). Define la rapidez con la que el compresor se activa después de superar el umbral. La etiqueta se formatea como `X.X ms` por debajo de 10 ms, `X ms` por encima.
- **Release**: Mapeo exponencial (5 * 400^n). Define la rapidez con la que la ganancia vuelve a la normalidad después de que la entrada vuelve a estar por debajo del umbral. La etiqueta se formatea como `X ms`.
- **Makeup**: Mapeo lineal. Agrega ganancia para recuperar la pérdida por compresión. La etiqueta muestra un signo `+` explícito para valores positivos.

### Indicadores de la curva de compresión

- **Curva de transferencia**: ClientCompCurveWidget en modo compacto. Dibuja la curva de transferencia entrada/salida más una bola en vivo que muestra el nivel de envolvente actual. Solo vista en el applet; editable en el ClientCompEditor flotante.
- **Barra de reducción de ganancia**: Franja horizontal de color ámbar, llena desde la derecha. La escala llega hasta 20 dB de reducción; una marca en -6 dB indica una cantidad de trabajo típica. Se actualiza a ~30 Hz desde `ClientComp::gainReductionDb()` con balística MeterSmoother (animación de 125 Hz, ataque de 30 ms / liberación de 180 ms). El relleno se actualiza en cada tick de animación para mantener una lectura coherente y receptiva en todas las superficies de medición.

## Controles adicionales en el editor flotante

El panel flotante StripCompPanel (se abre haciendo doble clic en el mosaico COMP en el widget CHAIN) añade estos controles:

| Control     | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|-------------|----------------------|--------------|------------------------|----------------|
| Knee        | Ajustable en el editor | Ajustable en el editor | `ClientCompTxKneeDb` / `ClientCompRxKneeDb` | Ancho de la rodilla suave en dB. |
| Ceiling     | Ajustable en el editor | Ajustable en el editor | `ClientCompTxLimCeilingDb` / `ClientCompRxLimCeilingDb` | Límite máximo fijo aplicado por el limitador. |
| Makeup      | 0.0 dB               | −12.0 a 24.0 dB | `ClientCompTxMakeupDb` / `ClientCompRxMakeupDb` | Control duplicado en el editor por comodidad. |
| Drive       | 0.0 dB               | 0.0 a 18.0 dB | `ClientCompTxDriveDb` / `ClientCompRxDriveDb` | Aumento de ganancia previo a la compresión con compensación automática vinculada. Empuja más señal por encima del umbral para que el compresor actúe con más fuerza y, simultáneamente, añade la misma cantidad de ganancia en la salida, elevando el RMS promedio junto con los picos en lugar de reducirlo. La etiqueta aparece como `+X.X dB`. La información sobre herramientas explica el emparejamiento de reducción de PAPR #2887. |
| Phase       | 0 etapas             | 0 a 6 etapas | `ClientCompTxPhaseRotatorStages` / `ClientCompRxPhaseRotatorStages` | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/oct de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos asimétricos de la voz antes de la compresión para reducir el PAPR. Etiqueta `Off` cuando es 0, `N stg` cuando está activo. Información sobre herramientas: `Rotador de fase previo a la compresión (#2887). Cascada de paso total que simetriza los picos asimétricos de la voz antes de la compresión. 0 = desactivado, 4 = valor predeterminado de difusión.` |
| Limiter enable | Desactivado | Desactivado / Activado | `ClientCompTxLimEnabled` / `ClientCompRxLimEnabled` | Botón de alternancia para el limitador de salida. |

## Estados del indicador

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Bola de envolvente | en reposo en la línea de umbral<br>moviéndose a lo largo de la curva | Nivel de entrada en vivo representado frente a la curva de transferencia estática. |
| Franja de reducción de ganancia | vacía<br>relleno ámbar<br>marca de −6 dB | Cantidad de atenuación dinámica aplicada actualmente por el compresor. |

## Consejos

- La bola de envolvente en la curva de transferencia proporciona retroalimentación visual continua. Si la bola se sitúa muy por encima de la rodilla en reposo, el umbral está demasiado bajo: suba Thresh hasta que la bola solo cruce la rodilla en los picos.
- La marca de −6 dB en la barra de reducción de ganancia es un punto de referencia útil. Un relleno ámbar constante hasta o ligeramente más allá de esa marca indica una compresión activa y moderada. Un relleno que alcanza el borde derecho de la barra significa que el compresor está trabajando con 20 dB de reducción o más.
- Cuando una etapa está desviada (bypass), el mosaico se atenúa visiblemente. Si el mosaico parece atenuado y los controles no responden, verifique que la etapa COMP no esté desviada en el widget CHAIN.
- Las instancias TX y RX son completamente independientes. Los cambios en el Compresor Aetherial (TX) no afectan al AGC-C Aetherial (RX) y viceversa.
- Los controles de Knee, limitador, Drive y Phase no están disponibles en el mosaico del applet. Abra el editor completo para acceder a ellos.
- Para cambiar el valor de un mando escribiendo directamente, haga clic en el texto del valor mostrado. Aparece un campo de edición con fondo oscuro y borde cian. Escriba el nuevo valor y presione Enter o haga clic en otro lugar para aplicarlo. Presione Escape para cancelar sin cambiar el valor.
- El mando Drive incluye ganancia de compensación automática: a medida que aumenta Drive, el compresor actúa con más fuerza mientras que la ganancia de salida se eleva simultáneamente para que el nivel RMS promedio se mantenga. Esto coincide con el modelo de difusión Optimod: Drive introduce más material en la curva Y añade la misma ganancia de vuelta, por lo que su mando MakeUp fijo permanece como un ajuste final limpio posterior a todo.
- La balística del medidor de reducción de ganancia (animación de 125 Hz, ataque de 30 ms / liberación de 180 ms) asegura que el relleno se lea de forma idéntica en todas las superficies de medición para una retroalimentación visual coherente.

## Relacionados

- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Establecer la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Ajustar ataque/liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Desviar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
- [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
