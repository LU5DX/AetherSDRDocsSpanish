# Abra el editor completo del compresor para los controles de Knee, Limiter, Drive y Phase

El applet compacto del compresor (que se muestra cuando habilita la etapa COMP en el widget CHAIN) le proporciona cinco perillas de ajuste: Thresh, Ratio, Attack, Release y Makeup, además de un indicador de curva de transferencia y un medidor horizontal de reducción de ganancia (20 dB máx.). Para acceder a los controles de Knee, Limiter, Drive y Phase, debe abrir el editor flotante StripCompPanel haciendo doble clic en el mosaico COMP en el widget CHAIN.

## Antes de comenzar

- La etapa COMP (lado TX: "Aetherial Compressor", lado RX: "Aetherial AGC-C") debe estar habilitada en el widget CHAIN. Si el mosaico está atenuado (omitido), consulte [Omitir el compresor de la cadena](bypass-the-compressor-from-the-chain.md) para habilitarlo primero.
- El mosaico COMP debe ser visible en el widget CHAIN dentro del contenedor principal Aetherial Audio (TXDSP).

## Pasos

1. Localice el mosaico de la etapa **COMP** en el widget CHAIN (lado TX o RX).
2. **Haga doble clic** en el mosaico COMP.

   Se abre el editor flotante con el título **"Aetherial Compressor — TX"** o **"— RX"**, dependiendo del lado en el que haya hecho doble clic. Es un panel sin marco con una barra de título degradada de 18 píxeles, un glifo de agarre y controles de minimizar/maximizar/cerrar.

3. En el editor, verá:
   - **Columna izquierda**: la curva de transferencia (interactiva, no solo de visualización), la perilla Knee (ancho de transición de soft-knee) y la perilla Make-up.
   - **Columna derecha (solo TX)**: la perilla Drive (ganancia previa a la compresión de 0–18 dB con auto-makeup vinculado), la perilla Phase (0–6 etapas de paso total) y una sección **Limiter** con un botón **Enable** y una perilla Ceiling (establece el nivel de techo duro).
   - **Columna derecha (solo RX)**: una sección **Limiter** con un botón **Enable** y una perilla Ceiling.

4. Ajuste cualquier control. Los cambios surten efecto de inmediato; no hay un botón "Apply" separado.

5. Cierre el editor haciendo clic en la **X** de la barra de título, o minimícelo (botón central) para mantenerlo activo pero fuera del camino.

## Qué hace cada control

| Etiqueta | Función | Valor predeterminado | Rango válido |
|---|---|---|---|
| **Knee** (solo en el editor) | Ancho de transición de soft-knee. Agrega una aparición gradual de la compresión en el punto de umbral en lugar de un cambio abrupto de hard-knee. | — (consulte `ClientCompTxKneeDb`) | — (consulte `ClientCompTxKneeDb`) |
| **Limiter Enable** (solo en el editor) | Habilita un limitador hard-knee que evita que los picos superen el valor de Ceiling. Botón de alternancia (marcado = activado). Se conserva como `ClientCompTxLimEnabled` (TX) o `ClientCompRxLimEnabled` (RX). | Desactivado | — |
| **Limiter Ceiling** (solo en el editor) | Techo de pico absoluto (dB) que aplica el limitador. Se conserva como `ClientCompTxLimCeilingDb` (TX) o `ClientCompRxLimCeilingDb` (RX). | — | — |
| **Drive** (solo TX, solo en el editor) | Aumento de ganancia previa a la compresión con auto-makeup vinculado. Envía más señal a través del umbral para que el compresor actúe con más fuerza y, al mismo tiempo, agrega una ganancia igual en la salida para que el RMS promedio suba junto con los picos en lugar de caer. Combínelo con Phase para mantener los picos limpios. Se conserva como `ClientCompTxDriveDb`. | 0.0 dB | 0.0 a 18.0 dB |
| **Phase** (solo TX, solo en el editor) | Número de etapas de filtro de paso total en cascada (0 = desactivado). Cada etapa agrega 12 dB/oct de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos asimétricos de voz antes de la compresión para reducir la relación de potencia pico a promedio (PAPR). El valor predeterminado de transmisión es 4 etapas. Se conserva como `ClientCompTxPhaseRotatorStages`. | 0 etapas (etiquetado "Off") | 0 a 6 etapas |

## Consejos

- Las cinco perillas que se muestran en el applet compacto (Thresh, Ratio, Attack, Release, Makeup) y la perilla Knee en el editor controlan los mismos parámetros subyacentes del compresor; el editor simplemente los expone en un solo panel junto con los controles avanzados.
- La curva de transferencia del editor es interactiva: puede arrastrar el punto de umbral y el ángulo de relación directamente en el gráfico de la curva en lugar de girar las perillas.
- Los cambios realizados en el editor se reflejan inmediatamente en las perillas del applet compacto y en el medidor de reducción de ganancia.
- El editor recuerda su última posición y tamaño a través de `StripCompPanelGeometry`. Si desea restablecerlo, puede borrar esa configuración del archivo de configuración.
- El tema del applet compacto se adapta al esquema de color actual. El fondo de la curva de transferencia, las líneas de la cuadrícula, las etiquetas de los ejes, el color de la curva, el brillo de la bola de la envolvente y el núcleo de la bola utilizan colores del tema de la paleta `color`.
- El medidor de reducción de ganancia y la animación de la bola de la envolvente se actualizan continuamente mientras el compresor está activo; el temporizador de animación se detiene cuando el medidor se estabiliza, pero continúa repintándose mientras la bola de la envolvente se mueve, lo que garantiza que la bola se deslice a lo largo de la curva de transferencia sin sacudidas.

## Relacionado

- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Aplicar ganancia de make-up después de la compresión](apply-make-up-gain-after-compression.md)
- [Impulsar el compresor con más fuerza con ganancia previa a la compresión para reducir la PAPR](drive-the-compressor-harder-with-pre-comp-gain-for-papr-reduction.md)
- [Rotar la simetría de fase de la voz con el rotador de fase (0–6 etapas)](rotate-voice-phase-symmetry-with-the-phase-rotator-0-6-stages.md)
- [Ajustar attack/release para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Observar la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
