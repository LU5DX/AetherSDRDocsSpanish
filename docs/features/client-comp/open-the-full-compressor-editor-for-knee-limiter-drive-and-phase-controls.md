# Abra el editor completo del compresor para los controles de Knee, Limiter, Drive y Phase

El applet compacto del compresor (que se muestra cuando habilita la etapa COMP en el widget CHAIN) le ofrece cinco perillas de ajuste: Thresh, Ratio, Attack, Release y Makeup, además de un indicador de curva de transferencia y un medidor horizontal de reducción de ganancia (20 dB máx.). Para acceder a los controles de Knee, Limiter, Drive y Phase, debe abrir el editor flotante StripCompPanel haciendo doble clic en el mosaico COMP del widget CHAIN.

## Antes de comenzar

- La etapa COMP (lado TX: "Aetherial Compressor", lado RX: "Aetherial AGC-C") debe estar habilitada en el widget CHAIN. Si el mosaico aparece atenuado (bypass), consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) para habilitarla primero.
- El mosaico COMP debe estar visible en el widget CHAIN dentro del contenedor padre Aetherial Audio (TXDSP).

## Pasos

1. Localice el mosaico de la etapa **COMP** en el widget CHAIN (lado TX o RX).
2. **Haga doble clic** en el mosaico COMP.

   Se abrirá el editor flotante con el título **"Aetherial Compressor — TX"** o **"— RX"**, según el lado en el que haya hecho doble clic. Es un panel sin bordes, con una barra de título degradada de 18 píxeles, un icono de agarre y controles de minimizar/maximizar/cerrar.

3. En el editor, verá:
   - **Columna izquierda**: la curva de transferencia (interactiva, no solo de visualización), la perilla Knee (ancho de transición soft-knee) y la perilla Make-up.
   - **Columna derecha (solo TX)**: la perilla Drive (ganancia pre-compresión de 0–18 dB con auto-makeup vinculado), la perilla Phase (0–6 etapas all-pass) y una sección **Limiter** con un botón **Enable** y una perilla Ceiling (establece el nivel de techo duro).
   - **Columna derecha (solo RX)**: una sección **Limiter** con un botón **Enable** y una perilla Ceiling.

4. Ajuste cualquier control. Los cambios surten efecto de inmediato; no hay un botón "Apply" separado.

5. Cierre el editor haciendo clic en la **X** de la barra de título, o minimícelo (botón central) para mantenerlo activo pero fuera del camino.

## Función de cada control

| Etiqueta | Función | Valor predeterminado | Rango válido |
|---|---|---|---|
| **Knee** (solo en el editor) | Ancho de transición soft-knee. Agrega una aparición gradual de la compresión en el punto de umbral en lugar de un cambio abrupto de hard-knee. | — (ver `ClientCompTxKneeDb`) | — (ver `ClientCompTxKneeDb`) |
| **Limiter Enable** (solo en el editor) | Habilita un limitador hard-knee brickwall que evita que los picos superen el valor de Ceiling. Botón de alternancia (marcado = activado). Se persiste como `ClientCompTxLimEnabled` (TX) o `ClientCompRxLimEnabled` (RX). | Desactivado | — |
| **Limiter Ceiling** (solo en el editor) | Techo de pico absoluto (dB) que aplica el limitador. Se persiste como `ClientCompTxLimCeilingDb` (TX) o `ClientCompRxLimCeilingDb` (RX). | — | — |
| **Drive** (solo TX, solo en el editor) | Aumento de ganancia pre-compresión con auto-makeup vinculado. Envía más señal a través del umbral para que el compresor actúe con más fuerza y, al mismo tiempo, agrega la misma ganancia en la salida para que el RMS promedio se eleve junto con los picos en lugar de disminuir. Combínelo con Phase para mantener los picos limpios. Se persiste como `ClientCompTxDriveDb`. | 0.0 dB | 0.0 a 18.0 dB |
| **Phase** (solo TX, solo en el editor) | Número de etapas de filtro all-pass en cascada (0 = desactivado). Cada etapa agrega 12 dB/oct de rotación de fase a frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos de voz asimétricos antes de la compresión para reducir la relación potencia pico a potencia promedio (PAPR). El valor predeterminado de radiodifusión es 4 etapas. Se persiste como `ClientCompTxPhaseRotatorStages`. | 0 etapas (etiquetado como "Off") | 0 a 6 etapas |

## Consejos

- Las cinco perillas que se muestran en el applet compacto (Thresh, Ratio, Attack, Release, Makeup) y la perilla Knee del editor controlan los mismos parámetros subyacentes del compresor; el editor simplemente los expone en un solo panel junto con los controles avanzados.
- La curva de transferencia del editor es interactiva: puede arrastrar el punto de umbral y el ángulo de relación directamente sobre el gráfico de la curva en lugar de girar las perillas.
- Los cambios realizados en el editor se reflejan inmediatamente en las perillas y el medidor de reducción de ganancia del applet compacto.
- El editor recuerda su última posición y tamaño mediante `StripCompPanelGeometry`. Si desea restablecerlo, puede borrar esa configuración del archivo de configuración.
- El tema del applet compacto se adapta al esquema de color actual. El fondo de la curva de transferencia, las líneas de la cuadrícula, las etiquetas de los ejes, el color de la curva, el brillo de la bola envolvente y el núcleo de la bola utilizan colores de la paleta `color`.

## Relacionados

- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Drive the compressor harder with pre-comp gain for PAPR reduction](drive-the-compressor-harder-with-pre-comp-gain-for-papr-reduction.md)
- [Rotate voice phase symmetry with the Phase rotator (0–6 stages)](rotate-voice-phase-symmetry-with-the-phase-rotator-0-6-stages.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
