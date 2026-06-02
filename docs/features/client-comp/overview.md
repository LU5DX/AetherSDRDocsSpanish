# Descripción general del Compresor Aetherial (TX) / AGC-C Aetherial (RX)

AetherSDR incluye un compresor de rango dinámico del lado del cliente que se ejecuta en dos instancias independientes: **Compresor Aetherial** en la ruta de TX y **AGC-C Aetherial** en la ruta de RX. Use la instancia de TX para suavizar los picos de voz antes de transmitir; use la instancia de RX para nivelar los niveles de audio recibido.

## Antes de comenzar

- Ambas instancias residen dentro del contenedor principal **Aetherial Audio (TXDSP)** en el panel de applets. Cada mosaico permanece oculto hasta que su etapa esté habilitada; desvíelo (bypass) desde el widget CHAIN o desde el editor flotante del lado correspondiente.
- No se requiere conexión de radio para configurar el compresor. Los ajustes se guardan localmente.

## Cómo funciona

Cada instancia procesa audio de forma independiente. El compresor monitorea el nivel de la señal de entrada. Cuando el nivel supera el umbral, atenúa la salida según la relación de compresión que usted elija. Los controles Ataque (Attack) y Liberación (Release) determinan la velocidad de reacción. La maquillaje (Makeup) agrega ganancia para compensar la pérdida por compresión. Un limitador opcional (configurado en el editor completo) establece un techo duro en la salida.

El mosaico del applet para cada instancia muestra:

- Una **curva de transferencia** — un gráfico estático de entrada/salida con una bola de envolvente en vivo que se desplaza a lo largo de la curva en tiempo real, mostrando el punto de operación actual. La curva usa colores adaptados al tema para fondo, cuadrícula, etiquetas, línea de identidad, línea de curva y brillo/núcleo de la bola.
- Una **barra de reducción de ganancia** — una franja horizontal de color ámbar que se llena desde la derecha. La escala va de 0 a 20 dB de reducción de ganancia. Una marca indica el punto de −6 dB como referencia de trabajo típica. La franja se actualiza aproximadamente a 30 Hz. El color de relleno lo define el tema y se aplica al ámbito `applet/comp`.

Cuando una etapa del compresor está desviada (bypassed), todo su mosaico de applet se atenúa aproximadamente al 55 % de opacidad. El mosaico vuelve a la opacidad completa cuando la etapa se reactiva. Este estado visual coincide con el comportamiento de atenuación utilizado por el applet de la curva de ecualización.

Para abrir el editor completo de cualquiera de las instancias — que agrega controles de Rodilla (Knee), Limitador (Limiter), Drive y Fase (Phase) no disponibles en el applet — haga doble clic en la etapa COMP en el widget CHAIN del lado TX o RX. El editor se abre con el título **Aetherial Compressor — TX** o **Aetherial Compressor — RX** según corresponda.

## Función de cada control

Los cinco mandos aparecen en una fila en la parte inferior de cada mosaico de applet. Tanto la instancia TX (Compresor Aetherial) como la RX (AGC-C Aetherial) comparten la misma disposición de mandos con estado independiente.

Cada mando soporta la edición en línea del valor: haga clic en el texto del valor mostrado para abrir un campo de edición. Escriba un nuevo valor y presione Enter o haga clic en otro lugar para confirmar el cambio. Presione Escape para cancelar. Mientras el campo de edición está enfocado, los eventos de la rueda del ratón continúan ajustando el mando como es habitual.

| Mando (Knob) | Valor predeterminado | Rango válido | Clave de ajuste (TX) | Clave de ajuste (RX) |
|---|---|---|---|---|
| Thresh (Umbral) | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` | `ClientCompRxThresholdDb` |
| Ratio (Relación) | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` | `ClientCompRxRatio` |
| Attack (Ataque) | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` | `ClientCompRxAttackMs` |
| Release (Liberación) | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` | `ClientCompRxReleaseMs` |
| Makeup (Maquillaje) | 0.0 dB | −12.0 a 24.0 dB | `ClientCompTxMakeupDb` | `ClientCompRxMakeupDb` |

## Controles adicionales en el editor flotante

El panel flotante StripCompPanel (se abre haciendo doble clic en el mosaico COMP del widget CHAIN) agrega estos controles:

| Mando | Valor predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---|---|---|---|---|
| Knee (Rodilla) | Ajustable en el editor | Ajustable en el editor | `ClientCompTxKneeDb` / `ClientCompRxKneeDb` | Ancho de rodilla suave (soft-knee) en dB. |
| Ceiling (Techo) | Ajustable en el editor | Ajustable en el editor | `ClientCompTxLimCeilingDb` / `ClientCompRxLimCeilingDb` | Techo duro aplicado por el limitador. |
| Makeup (Maquillaje) | 0.0 dB | −12.0 a 24.0 dB | Ver arriba | Control duplicado en el editor por conveniencia. |
| Drive (Impulso) | 0.0 dB | 0.0 a 18.0 dB | `ClientCompTxDriveDb` / `ClientCompRxDriveDb` | Aumento de ganancia previo a la compresión con maquillaje automático vinculado. Empuja más señal a través del umbral para que el compresor actúe con más fuerza y, simultáneamente, agrega la misma ganancia a la salida, elevando el RMS promedio junto con los picos en lugar de reducirlo. Combínelo con Phase (Fase) para mantener los picos limpios. La etiqueta se muestra como '+X.X dB'. La información sobre herramientas explica la combinación para reducción de PAPR (#2887). |
| Phase (Fase) | 0 etapas | 0 a 6 etapas | `ClientCompTxPhaseRotatorStages` / `ClientCompRxPhaseRotatorStages` | Número de secciones de paso total (all-pass) en cascada (0 = desactivado). Cada etapa agrega 12 dB/octava de rotación de fase a frecuencias escalonadas (300/700/1500/2500 Hz, más opcionalmente 1000/2000 Hz). Simetriza los picos de voz asimétricos antes de la compresión para reducir la PAPR. La etiqueta muestra 'Off' (Desactivado) cuando es 0, 'N stg' cuando está activo. Información sobre herramientas: 'Rotador de fase previo a la compresión (#2887). Cascade de paso total que simetriza los picos de voz asimétricos antes de la compresión. 0 = desactivado, 4 = valor predeterminado de radiodifusión.' |
| Limiter enable (Habilitar limitador) | Off (Desactivado) | Off (Desactivado) / On (Activado) | `ClientCompTxLimEnabled` / `ClientCompRxLimEnabled` | Botón de alternancia para el limitador de salida. |

## Estados del indicador

| Indicador | Estados | Significado |
|---|---|---|
| Bola de envolvente (Envelope ball) | En reposo en la línea de umbral<br>Desplazándose a lo largo de la curva | Nivel de entrada en vivo graficado contra la curva de transferencia estática. |
| Franja de reducción de ganancia | Vacía<br>Relleno ámbar<br>Marca de −6 dB | Cantidad de atenuación dinámica aplicada actualmente por el compresor. |

## Consejos

- La bola de envolvente en la curva de transferencia proporciona retroalimentación visual continua. Si la bola se sitúa muy por encima de la rodilla (knee) en reposo, el umbral está demasiado bajo; suba Thresh hasta que la bola solo cruce la rodilla en los picos.
- La marca de −6 dB en la barra de reducción de ganancia es un punto de referencia útil. Un relleno ámbar constante hasta o ligeramente más allá de esa marca indica una compresión activa y moderada. Un relleno que alcanza el borde derecho de la barra significa que el compresor está trabajando con una reducción de 20 dB o más.
- Cuando una etapa está desviada (bypassed), el mosaico se atenúa visiblemente. Si el mosaico aparece atenuado y los controles no responden, verifique que la etapa COMP no esté desviada en el widget CHAIN.
- Las instancias TX y RX son completamente independientes. Los cambios en el Compresor Aetherial (TX) no afectan al AGC-C Aetherial (RX) y viceversa.
- Los controles de Rodilla (Knee), Limitador (Limiter), Drive y Fase (Phase) no están disponibles en el mosaico del applet. Abra el editor completo para acceder a ellos.
- Para cambiar un valor de mando escribiendo directamente, haga clic en el texto del valor mostrado. Aparecerá un campo de edición con fondo oscuro y borde cian. Escriba el nuevo valor y presione Enter o haga clic en otro lugar para aplicarlo. Presione Escape para cancelar sin cambiar el valor.
- El mando Drive incluye ganancia de maquillaje automática: al aumentar Drive, el compresor actúa con más fuerza mientras que la ganancia de salida se eleva simultáneamente para que el nivel RMS promedio se mantenga. Esto coincide con el modelo de radiodifusión Optimod: Drive empuja más material hacia la curva Y agrega la misma ganancia de vuelta, de modo que su mando Makeup fijo permanece como un ajuste final limpio posterior a todo.

## Relacionados

- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Establecer la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Ajustar ataque/liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de maquillaje después de la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Desviar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
- [Abrir el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
