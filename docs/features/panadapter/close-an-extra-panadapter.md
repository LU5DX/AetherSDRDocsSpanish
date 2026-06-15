# Cerrar un panorámico adicional

Cuando tiene varios panorámicos abiertos en una disposición de múltiples slices, puede cerrar cualquier adicional para recuperar espacio en pantalla. Esta página explica cómo cerrar un panorámico que ya no necesita.

## Antes de comenzar

- Su radio debe estar conectada. El botón × (cerrar) solo está disponible cuando AetherSDR está conectado a una FLEX-8600.
- Debe tener más de un panorámico abierto. El botón × (cerrar) está oculto en modo de un solo panorámico.

## Pasos

1. Localice la barra de título del panorámico que desea cerrar. Se encuentra en la parte superior del panorámico y muestra una etiqueta como "Slice A" o "Slice B".
2. Haga clic en el botón × en el extremo derecho de esa barra de título.

El panorámico se cierra inmediatamente. Los panorámicos restantes se expanden para llenar el espacio disponible.

## Consejos

- Si no puede ver el botón ×, está en modo de un solo panorámico; solo hay un panorámico abierto y no se permite cerrarlo.
- Si el panorámico se ha extraído a una ventana flotante, el botón × aún se encuentra en la barra de título de la ventana flotante, en la esquina superior derecha. Haga clic allí.

## Solución de problemas

- **El botón × no es visible** — La radio está desconectada o solo hay un panorámico abierto. AetherSDR oculta el botón × en ambos casos. Conéctese a la radio y agregue un segundo panorámico antes de intentarlo de nuevo.

## Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro del panorámico y el waterfall cuando la decodificación CW está activa. Muestra texto Morse decodificado, estadísticas de detección y controles para ajustar el decodificador.

### Menú contextual del texto de decodificación CW

Al hacer clic derecho en cualquier lugar dentro del área de texto de decodificación CW, se abre un menú contextual. Además de los comandos estándar de edición de texto (Seleccionar todo, Copiar, etc.), el menú incluye un elemento **Clear**. Al elegir **Clear**, se borra todo el búfer de decodificación CW de inmediato. Esto equivale a hacer clic en el botón **CLR** en la barra de herramientas del panel CW.

### Colores de TX/RX en decodificación CW

En el panel de decodificación CW, el texto recibido y el texto transmitido (auto-enviado) se muestran en diferentes colores para que pueda distinguir su propio envío del CW entrante. Los colores son:

- **Verde**: Costo de confianza < 0,15 (alta confianza)
- **Amarillo**: Costo de confianza < 0,35
- **Naranja**: Costo de confianza < 0,60
- **Rojo**: Costo de confianza >= 0,60 (baja confianza)
- **Cian** (`#5fc8ff`): Texto decodificado de su propia manipulación transmitida

Al cambiar entre transmisión y recepción, se inserta automáticamente un espacio para evitar que las secuencias de texto coloreadas se fusionen.

### Controles del decodificador CW

La barra de herramientas del decodificador CW incluye los siguientes controles:

| Control | Tipo | Descripción |
|---------|------|-------------|
| Etiqueta de estadísticas CW | Indicador | Muestra el tono y la velocidad de CW detectados como `<hz> Hz  <wpm> WPM` |
| Sens | Deslizador (0-100) | Filtra las decodificaciones de baja confianza; los valores más altos significan un filtrado más estricto. Se asigna a un umbral de costo de 1,0 (0) a 0,1 (100). Clave de configuración: `CwDecoderSensitivity` |
| 🔒P (Lock Pitch) | Botón de alternancia | Bloquea el tono del decodificador CW en la frecuencia sintonizada actual |
| 🔒S (Lock Speed) | Botón de alternancia | Bloquea la velocidad del decodificador CW en las WPM actuales |
| Deslizador de rango de tono | Deslizador de rango (300-1200 Hz) | Deslizador de doble manija para establecer el tono mínimo y máximo para la búsqueda del decodificador CW. Predeterminado: 500-700 Hz |
| Deslizador de rango de WPM | Deslizador de rango (5-60 WPM) | Deslizador de doble manija para establecer la velocidad mínima y máxima para la búsqueda del decodificador CW. Predeterminado: 15-40 WPM |
| CPY ALL | Botón | Copia todo el texto decodificado al portapapeles |
| CPY VIS | Botón | Copia solo el texto actualmente visible en el área de desplazamiento |
| CLR | Botón | Limpia el búfer de decodificación CW |
| ✕ (cerrar CW) | Botón | Oculta el panel de decodificación CW |

### Indicador de sugerencia CW

Cuando se requiere enrutamiento de audio de PC pero no está configurado, aparece una etiqueta de sugerencia en el panel CW que le recuerda que "(requires PC Audio)".

## Panel de decodificación RTTY (v26.6.3)

A partir de la v26.6.3, AetherSDR incluye un panel de decodificación RTTY que aparece debajo del panorámico cuando el modo del slice activo está configurado en RTTY o DIGL. El panel funciona de manera similar al panel de decodificación CW, pero para la decodificación RTTY.

El panel RTTY incluye un menú desplegable para seleccionar el algoritmo del decodificador RTTY y controles para ajustar los parámetros del decodificador. El panel está oculto de forma predeterminada y solo aparece cuando el modo del slice está configurado adecuadamente.

## Título del slice con Multi-Flex

En sesiones Multi-Flex, el título del slice que se muestra en la barra de título del panorámico utiliza la letra de índice proporcionada por la radio para que el título coincida con la insignia del slice. Esto garantiza la coherencia cuando varios clientes están conectados a la misma radio.

## Comportamiento de congelación del waterfall

El waterfall se congela automáticamente cuando cualquier cliente en una sesión Multi-Flex comienza a transmitir. El estado de congelación está controlado por el estado TRANSMITTING del interlock de la radio, en lugar del borde MOX local, lo que elimina el artefacto de estela TX de 10 a 23 segundos que podía aparecer después de desactivar la transmisión.

Al reconectar la radio, se reafirman los FPS deseados del panorámico y la duración de línea del waterfall para evitar caer silenciosamente al valor predeterminado de 10 Hz de la radio.

## Tematización del panorámico (v26.6.1)

En la v26.6.1, el panorámico y su panel de decodificación CW ahora utilizan un estilo consciente del tema en lugar de colores fijos. El gradiente de la barra de título, los puntos de agarre de arrastre, el título del slice, las etiquetas de estadísticas y el fondo del panel CW hacen referencia a tokens de color del tema. Esto significa que el panorámico se adapta automáticamente a los temas claro y oscuro sin necesidad de anulaciones de color manuales. El sistema de temas reemplaza las hojas de estilo de color fijo anteriores con valores basados en tokens como `{{color.background.1}}`, `{{color.text.secondary}}` y `{{color.accent}}`.

## Relacionados

- [Panadapter overview](overview.md)
- [Click the spectrum to activate a panadapter (multi-slice mode)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)
- [Maximize one panadapter to fill the main area](maximize-one-panadapter-to-fill-the-main-area.md)
