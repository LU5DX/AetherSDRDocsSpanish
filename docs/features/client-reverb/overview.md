# Resumen de Aetherial FreeVerb

Aetherial FreeVerb añade una cola de reverberación basada en Freeverb al audio de su transmisión, proporcionando a su voz una sensación de ambiente de sala o auditorio. Se aplica únicamente a la ruta de TX — no tiene contraparte en RX.

## Antes de comenzar

- La etapa de Reverb debe estar habilitada en el widget CHAIN dentro del applet Aetherial Audio (TXDSP). El subcontenedor "Aetherial FreeVerb" y sus controles permanecen ocultos hasta que la etapa esté activada.
- No se requiere una conexión de radio para ajustar la configuración de reverberación.

## Cómo funciona

Aetherial FreeVerb inserta un procesador de reverberación Freeverb en la cadena de audio de TX del lado del cliente, después de cualquier etapa DSP previa. Cuando la etapa VERB está activa, los cinco mandos — Size, Decay, Damp, Pre y Mix — moldean el carácter y el nivel de la cola de reverberación añadida a su voz transmitida.

Los controles aparecen en dos lugares que se mantienen sincronizados a aproximadamente 30 Hz:

- **El subcontenedor "Aetherial FreeVerb"** — una fila compacta de cinco mandos integrada dentro del contenedor principal Aetherial Audio (TXDSP) en el panel del applet.
- **El editor flotante titulado "Aetherial FreeVerb — TX"** — una versión más grande de los mismos controles, que se abre haciendo doble clic en la etapa VERB en el widget CHAIN. También puede hacer clic derecho en la barra de título del subcontenedor "Aetherial FreeVerb" para flotarlo, desacoplarlo u ocultarlo.

Girar cualquier mando en una vista actualiza inmediatamente la otra. La configuración se guarda automáticamente al cambiar un mando.

### Visualización de reverberación en vivo

El editor flotante incluye una visualización compacta en vivo (90 px de altura) que se actualiza en tiempo real mientras gira los mandos. Representa tres componentes de señal sobre un fondo de cuadrícula oscura:

- **Cian** — el paquete de señal seca, con degradado que se desvanece hacia la derecha.
- **Amarillo** — reflexiones de primer orden, espaciadas y amortiguadas según los valores actuales de Size y Damp.
- **Magenta** — la cola reverberante, cuya longitud y envolvente de decaimiento siguen los mandos Decay y Damp.

El mando Pre desplaza el punto en el que comienzan las reflexiones y la cola en relación con la señal seca. El mando Mix escala la amplitud tanto de los componentes húmedos como del desvanecimiento del paquete seco. La visualización coincide con el diseño utilizado por el panel de reverberación lateral de la tira, por lo que ambas vistas se leen de manera consistente.

### Edición de valor en línea

Cada mando en el subcontenedor y editor flotante de Aetherial FreeVerb admite la edición de valor en línea. Haga clic en la etiqueta de valor de un mando para ingresar al modo de edición — un sutil borde cian indica que el editor está activo. Escriba un nuevo valor usando las mismas unidades que se muestran en la etiqueta del mando (por ejemplo, "2.50" para Decay, "75" para Size), luego presione Enter o haga clic en otro lugar para confirmar. El valor se limita automáticamente al rango válido del mando. Presione Escape para cancelar la edición y revertir al valor anterior.

El desplazamiento con la rueda del ratón continúa funcionando mientras el editor tiene el foco, por lo que puede ajustar finamente desplazándose después de escribir un valor aproximado.

## Qué hace cada control

| Mando                | Predeterminado | Rango válido | Clave de configuración        |
|----------------------|----------------|--------------|-------------------------------|
| Size                 | 50 %           | 0–100 %      | `ClientReverbTxSize`          |
| Decay                | 1.20 s         | 0.3–5.0 s    | `ClientReverbTxDecayS`        |
| Damp                 | 50 %           | 0–100 %      | `ClientReverbTxDamping`       |
| Pre                  | 20 ms          | 0–100 ms     | `ClientReverbTxPreDelayMs`    |
| Mix                  | 15 %           | 0–100 %      | `ClientReverbTxMix`           |

| Indicador                 | Comportamiento                                                          |
|---------------------------|-------------------------------------------------------------------------|
| Visualización de reverberación | ReverbVizBox — visualización en vivo que muestra el paquete de señal seca (cian), reflexiones de primer orden (amarillo) y cola reverberante (magenta). Los cinco valores de los mandos alimentan la representación para que la pantalla siga las ediciones de los mandos en tiempo real. 90 px de altura. Reemplaza el widget de curva utilizado por otros applets DSP. El algoritmo de representación coincide con StripReverbPanel::GridBox. |

El estado habilitado/deshabilitado de la etapa se guarda como `ClientReverbTxEnabled`.

- **Size** — Establece el tamaño de la sala modelada. Mapeo lineal. Valores más grandes simulan un espacio más grande.
- **Decay** — Establece la longitud de la cola de reverberación. Mapeo exponencial de 0.3 a 5.0 s. Valores más altos producen una cola más larga y sostenida.
- **Damp** — Controla la rapidez con que las altas frecuencias se desvanecen en la cola. Mapeo lineal. Valores más altos amortiguan las altas frecuencias más rápido, produciendo una cola más cálida y oscura.
- **Pre** — Pre-retardo entre la señal seca y las primeras reflexiones. Mapeo lineal de 0 a 100 ms.
- **Mix** — Balance seco/húmedo. Mapeo lineal. Controla el nivel del efecto de reverberación en relación con la señal seca.

## Consejos

- Para voz, un Mix del 10–15 % es típico. El valor predeterminado del 15 % es un punto de partida razonable.
- Valores altos de Decay (por encima de 3 s) pueden embarullar el habla. Comience con el valor predeterminado de 1.20 s y aumente solo si el efecto de sala parece demasiado corto.
- Aumentar Damp reduce el brillo de las altas frecuencias en la cola, lo que puede ayudar a que la reverberación se sitúe detrás del habla en lugar de superponerse a ella.
- El editor flotante ("Aetherial FreeVerb — TX") proporciona mandos más grandes y la visualización en vivo para un ajuste preciso. Su posición y tamaño se guardan automáticamente entre sesiones.
- Use la visualización en vivo para tener una idea aproximada de la longitud de la cola y la densidad de reflexiones antes de transmitir. La longitud de la cola magenta da una aproximación visual de cómo interactúan Decay y Damp.
- Use la edición de valor en línea para ingresar valores exactos rápidamente — haga clic en la etiqueta de valor del mando, escriba el número y presione Enter. Esto es especialmente útil para Decay y Pre donde puede desear tiempos precisos.

## Relacionado

- [Bypass reverb from the chain](bypass-reverb-from-the-chain.md)
- [Dial in a subtle Mix — 10-15 % is typical for voice](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Tune decay to taste without muddying speech](tune-decay-to-taste-without-muddying-speech.md)
- [Reduce the high-end sparkle of the tail with Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Set room size for a small or large-hall feel](set-room-size-for-a-small-or-large-hall-feel.md)
- [Offset reflections from the dry signal with Pre](offset-reflections-from-the-dry-signal-with-pre.md)
