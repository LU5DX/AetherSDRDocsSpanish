# Observe la reducción de ganancia en vivo mientras habla o escucha

El ClientCompApplet muestra un medidor de reducción de ganancia en vivo y una curva de transferencia animada mientras el audio pasa por el compresor. Utilice estos indicadores para ver en tiempo real la intensidad del trabajo del compresor — tanto al transmitir (lado TX) como al recibir audio (lado RX) — sin necesidad de abrir el editor flotante.

Cada perilla del compresor admite edición de valor en línea: haga clic en el texto del valor para ingresar directamente un número preciso, luego presione Enter o haga clic en otro lugar para confirmarlo.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa del compresor que desea monitorear (TX o RX) debe estar habilitada; el mosaico se renderiza con opacidad reducida cuando la etapa está desviada. Consulte [Desviar el compresor de la cadena](bypass-the-compressor-from-the-chain.md) si el mosaico aparece atenuado.

## Pasos

1. Localice el subcontenedor "Aetherial Compressor" (lado TX) o "Aetherial AGC-C" (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Hable por su micrófono (TX) o deje que se reproduzca el audio recibido (RX).
3. Observe la **Barra de reducción de ganancia** — la franja horizontal ámbar debajo de la curva de transferencia. La franja se llena desde la derecha a medida que aumenta la reducción de ganancia, hasta un máximo de 20 dB.
4. Observe la **Curva de transferencia** — la bola de envolvente en vivo se mueve a lo largo de la curva estática para mostrar el nivel de entrada actual en relación con el umbral y la configuración de relación.
5. Use la marca de -6 dB en la **Barra de reducción de ganancia** como referencia. Un llenado que alcanza o supera ligeramente esa marca de forma constante es una cantidad de compresión de trabajo típica.

## Ingresar valores precisos directamente

Haga clic en el texto del valor mostrado de cualquier perilla para abrir un editor en línea. Escriba un número y presione Enter, o haga clic en otro lugar para aplicar el valor. El editor se cierra automáticamente y la perilla se actualiza.

- El editor acepta formatos decimales según la configuración regional (por ejemplo, "12,5" en locales con coma decimal).
- Ingrese números simples sin unidades (por ejemplo, escriba "5" o "5.0" para 5.0 ms de Ataque).
- Presione Escape para cancelar la edición y restaurar el valor anterior.
- El editor aparece como una superposición transparente que coincide con la apariencia normal de la etiqueta. Cuando está enfocado, un fondo oscuro sutil y un borde cian indican el modo de edición.

## Qué hace cada control

| Control            | Tipo                                                                                                                                                                                                                                                                     | Lo que ve                                                                                                                                                                                                                                                |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva de transferencia | Indicador                                                                                                                                                                                                                                                               | Curva estática de entrada/salida con una bola en vivo en el nivel de envolvente actual. Los colores de la curva, la cuadrícula, la bola y las etiquetas de los ejes siguen el tema activo a través de `ThemeManager`.                                      |
| Barra de reducción de ganancia | Medidor                                                                                                                                                                                                                                                                 | Franja horizontal ámbar, llenada desde la derecha. La escala va de 0 a 20 dB de reducción de ganancia. Una marca señala el punto de -6 dB. El relleno del control deslizante se estiliza a través del contenedor de tema `applet/comp`.                  |
| Thresh (Umbral)    | Perilla                                                                                                                                                                                                                                                                  | Umbral actual. Predeterminado -18.0 dB; rango -60.0 a 0.0 dB. Haga clic en el valor para escribir un umbral preciso. La configuración se almacena como `ClientCompTxThresholdDb` o `ClientCompRxThresholdDb`.                                            |
| Ratio (Relación)   | Perilla                                                                                                                                                                                                                                                                  | Relación actual. Predeterminado 3.0; rango 1.0 a 20.0. Se muestra como X.XX:1. Haga clic en el valor para escribir una relación precisa. La configuración se almacena como `ClientCompTxRatio` o `ClientCompRxRatio`.                                    |
| Attack (Ataque)    | Perilla                                                                                                                                                                                                                                                                  | Tiempo de ataque actual. Predeterminado 20.0 ms; rango 0.1 a 300.0 ms. Haga clic en el valor para escribir un tiempo de ataque preciso. La configuración se almacena como `ClientCompTxAttackMs` o `ClientCompRxAttackMs`.                               |
| Release (Liberación) | Perilla                                                                                                                                                                                                                                                                  | Tiempo de liberación actual. Predeterminado 200 ms; rango 5 a 2000 ms. Haga clic en el valor para escribir un tiempo de liberación preciso. La configuración se almacena como `ClientCompTxReleaseMs` o `ClientCompRxReleaseMs`.                         |
| Makeup (Compensación) | Perilla                                                                                                                                                                                                                                                                  | Ganancia de compensación actual. Predeterminado 0.0 dB; rango -12.0 a 24.0 dB. Haga clic en el valor para escribir una ganancia de compensación precisa. Muestra el signo '+' explícito para valores positivos. La configuración se almacena como `ClientCompTxMakeupDb` o `ClientCompRxMakeupDb`.                    |
| Drive (Impulso)    | Aumento de ganancia previo a la compresión con compensación automática vinculada. Empuja más señal más allá del umbral para que el compresor actúe con más fuerza y, simultáneamente, agrega la misma ganancia en la salida, de modo que el RMS promedio se eleve junto con los picos en lugar de caer. Combínelo con Phase (Fase) para mantener los picos limpios. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta se muestra como '+X.X dB'. Rango 0.0 a 18.0 dB. El tooltip explica la combinación de reducción de PAPR #2887. La configuración se almacena como `ClientCompTxDriveDb`. |
| Phase (Fase)       | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa agrega 12 dB/octava de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos asimétricos de la voz antes de la compresión para reducir el PAPR. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. Rango de 0 a 6 etapas. La configuración se almacena como `ClientCompTxPhaseRotatorStages`. Tooltip: 'Rotador de fase previo a la compresión (#2887). 0=off, 4=valor por defecto de broadcast.' |

## Consejos

- Si la **Barra de reducción de ganancia** nunca se mueve, el nivel de entrada no está superando el umbral. Baje la perilla Thresh o aumente la ganancia de su micrófono.
- Si la **Barra de reducción de ganancia** está fijada en 20 dB o cerca de ese valor de forma continua, la relación o el umbral se han configurado de forma muy agresiva. Suba el valor de Thresh o baje la perilla Ratio para aliviar la compresión.
- La bola de envolvente en la **Curva de transferencia** descansa en la línea de umbral cuando no hay audio presente. Durante el audio, viaja a lo largo de la curva; una bola situada en la parte curvada de la curva confirma la compresión activa.
- Los mosaicos TX y RX se actualizan de forma independiente. Puede monitorear ambos simultáneamente si ambos subcontenedores están expandidos.
- Las etiquetas de los ejes de la curva de transferencia utilizan texto estático en caché para mejorar el rendimiento del renderizado. La caché se reconstruye automáticamente al cambiar entre modos de visualización compacto y completo.
- Para ingresar un valor preciso, haga clic en el texto del valor mostrado. El editor en línea acepta entrada numérica con separadores decimales según la configuración regional. Use signos negativos cuando corresponda (por ejemplo, "-24.0" para el umbral).
- Los colores de la curva de transferencia y la barra de reducción de ganancia se adaptan al tema activo. La curva usa el color del tema `color.accent.dim`, el brillo de la bola usa `color.accent.warning` y la cuadrícula usa `color.background.1`.
- La compensación automática de la perilla Drive sigue el modelo Optimod de broadcast: empuja más material hacia la curva Y agrega la misma ganancia de retorno, de modo que la perilla Makeup fija del usuario permanezca como una perilla de ajuste limpia posterior a todo.
- El rotador de fase predeterminado de 4 etapas (estándar de broadcast) utiliza frecuencias centrales escalonadas de 300/700/1500/2500 Hz con 1000/2000 Hz opcionales para cubrir el rango de formantes del habla sin agruparlos.
- Las animaciones del medidor de reducción de ganancia y la bola de envolvente se ejecutan a una frecuencia de actualización suave y eficiente. El temporizador de animación se detiene automáticamente cuando la señal se estabiliza y se reinicia cuando se reanuda la actividad de audio. La pantalla se vuelve a pintar solo cuando es necesario, ya sea cuando el suavizador alcanza un estado estable o cuando el valor actual justifica una actualización visual.

## Solución de problemas

- **El mosaico aparece atenuado** — La etapa del compresor está desviada. El mosaico ahora se renderiza con aproximadamente un 55 % de opacidad cuando la etapa está deshabilitada, coincidiendo con el efecto de atenuación utilizado en la curva EQ. Habilite la etapa desde el widget CHAIN (un solo clic en la etapa COMP) o consulte [Desviar el compresor de la cadena](bypass-the-compressor-from-the-chain.md).
- **La Barra de reducción de ganancia no muestra movimiento durante el audio** — El nivel de entrada no está alcanzando el umbral. Reduzca el valor de la perilla Thresh o verifique que el dispositivo de audio correcto esté activo y produciendo señal.
- **La bola de envolvente no se mueve** — El applet no está conectado a un motor de audio activo. Verifique que la radio esté conectada y que el audio fluya a través de la cadena de procesamiento TX o RX correspondiente.
- **El editor en línea no aparece** — Haga clic directamente en el texto del valor numérico debajo de cada perilla. El editor solo aparece al hacer clic en el valor, no en el cuerpo de la perilla.

## Relacionado

- [Descripción general del Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Establecer la relación de compresión para la voz (TX) o para el audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Ajustar ataque/liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Abrir el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
