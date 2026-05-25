# Visión general del Compresor Aethereal (TX) / AGC-C Aethereal (RX)

AetherSDR incluye un compresor de rango dinámico del lado del cliente que se ejecuta en dos instancias independientes: **Compresor Aethereal** en la ruta de TX y **AGC-C Aethereal** en la ruta de RX. Use la instancia de TX para suavizar los picos de voz antes de transmitir; use la instancia de RX para nivelar los niveles de audio recibido.

## Antes de comenzar

- Ambas instancias residen dentro del contenedor principal **Aetherial Audio (TXDSP)** en el panel de applets. Cada mosaico permanece oculto hasta que su etapa esté habilitada; desactívelo mediante el widget CHAIN o el editor flotante en el lado correspondiente.
- No se requiere conexión de radio para configurar el compresor. Los ajustes se guardan localmente.

## Cómo funciona

Cada instancia procesa audio de forma independiente. El compresor monitorea el nivel de la señal de entrada. Cuando el nivel supera el umbral, atenúa la salida según la relación de compresión que elija. Los controles de Ataque y Liberación determinan la velocidad de reacción. La Ganancia de compensación añade ganancia para recuperar la pérdida por compresión. Un limitador opcional (configurado en el editor completo) establece un límite máximo fijo en la salida.

El mosaico del applet para cada instancia muestra:

- Una **curva de transferencia** — un gráfico estático de entrada/salida con una bola de envolvente en vivo que se desplaza a lo largo de la curva en tiempo real, mostrando el punto de operación actual.
- Una **barra de reducción de ganancia** — una franja horizontal de color ámbar que se llena desde la derecha. La escala va de 0 a 20 dB de reducción de ganancia. Una marca indica el punto de −6 dB como referencia de trabajo típica. La franja se actualiza a aproximadamente 30 Hz.

Cuando una etapa del compresor está desactivada, todo su mosaico del applet se atenúa hasta aproximadamente un 55 % de opacidad. El mosaico vuelve a la opacidad completa cuando la etapa se vuelve a habilitar. Este estado visual coincide con el comportamiento de atenuación utilizado por el applet de la curva de EQ.

Para abrir el editor completo de cualquiera de las instancias (que añade controles de rodilla y limitador no disponibles en el applet), haga doble clic en la etapa COMP en el widget CHAIN del lado TX o RX. El editor se abre con el título **Compresor Aethereal — TX** o **Compresor Aethereal — RX** según corresponda.

## Función de cada control

Los cinco mandos aparecen en una fila en la parte inferior de cada mosaico del applet. Las instancias de TX (Compresor Aethereal) y RX (AGC-C Aethereal) comparten la misma disposición de mandos con estado independiente.

Cada mando admite edición en línea del valor: haga clic en el texto del valor mostrado para abrir un campo de edición. Escriba un nuevo valor y pulse Enter o haga clic en otro lugar para confirmar el cambio. Pulse Escape para cancelar. Mientras el campo de edición está enfocado, los eventos de la rueda del ratón continúan ajustando el mando como de costumbre.

| Mando                     | Valor predeterminado                                                                                                                                                                                                                        | Rango válido                                                                                                                                                                |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Thresh                    | −18.0 dB                                                                                                                                                                                                                                    | −60.0 a 0.0 dB                                                                                                                                                              |
| Ratio                     | 3.0                                                                                                                                                                                                                                         | 1.0 a 20.0                                                                                                                                                                  |
| Attack                    | 20.0 ms                                                                                                                                                                                                                                     | 0.1 a 300.0 ms                                                                                                                                                              |
| Release                   | 200 ms                                                                                                                                                                                                                                      | 5 a 2000 ms                                                                                                                                                                 |
| Makeup                    | 0.0 dB                                                                                                                                                                                                                                      | −12.0 a 24.0 dB                                                                                                                                                             |
| Clave de ajuste (TX)      | Clave de ajuste (RX)                                                                                                                                                                                                                        | Descripción                                                                                                                                                                 |
| ---                       | ---                                                                                                                                                                                                                                         | ---                                                                                                                                                                         |
| `ClientCompTxEnabled`     | `ClientCompRxEnabled`                                                                                                                                                                                                                       | Si la etapa del compresor está activa (desvío desactivado).                                                                                                                |
| `ClientCompTxKneeDb`      | `ClientCompRxKneeDb`                                                                                                                                                                                                                        | Ancho de la rodilla suave en dB. Ajustable en el editor flotante.                                                                                                           |
| `ClientCompTxLimEnabled`  | `ClientCompRxLimEnabled`                                                                                                                                                                                                                    | Si el limitador de salida está activo.                                                                                                                                      |
| `ClientCompTxLimCeilingDb`| `ClientCompRxLimCeilingDb`                                                                                                                                                                                                                  | Límite máximo fijo aplicado por el limitador.                                                                                                                               |
| Drive                     | Aumento de ganancia previo a la compresión. Empuja más señal por encima del umbral para que el compresor actúe con más fuerza, elevando la potencia media. Combínelo con Phase para mantener los picos limpios.                              | Se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta muestra '+X.X dB'. El tooltip explica la reducción de PAPR #2887.                        |
| Phase                     | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/oct de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos de voz asimétricos antes de la compresión para reducir PAPR. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta muestra 'Off' cuando es 0, 'N stg' cuando está activo. Tooltip: 'Rotador de fase previo a la compresión (#2887). 0=desactivado, 4=predeterminado de transmisión'. |

## Consejos

- La bola de envolvente en la curva de transferencia proporciona retroalimentación visual continua. Si la bola se sitúa muy por encima de la rodilla en reposo, el umbral está demasiado bajo: suba Thresh hasta que la bola solo cruce la rodilla en los picos.
- La marca de −6 dB en la barra de reducción de ganancia es un punto de referencia útil. Un llenado ámbar constante hasta o ligeramente más allá de esa marca indica una compresión activa y moderada. Un llenado que alcanza el borde derecho de la barra significa que el compresor está trabajando a 20 dB de reducción o más.
- Cuando una etapa está desactivada, el mosaico se atenúa visiblemente. Si el mosaico aparece atenuado y los controles no responden, verifique que la etapa COMP no esté desactivada en el widget CHAIN.
- Las instancias de TX y RX son completamente independientes. Los cambios en el Compresor Aethereal (TX) no afectan al AGC-C Aethereal (RX) y viceversa.
- Los controles de rodilla y limitador no están disponibles en el mosaico del applet. Abra el editor completo para acceder a ellos.
- Para cambiar el valor de un mando escribiendo directamente, haga clic en el texto del valor mostrado. El campo de edición aparece con un fondo oscuro y un borde cian. Escriba el nuevo valor y pulse Enter o haga clic en otro lugar para aplicarlo. Pulse Escape para cancelar sin cambiar el valor.

## Relacionado

- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Establecer la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Ajustar ataque/liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Desactivar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
- [Abrir el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
