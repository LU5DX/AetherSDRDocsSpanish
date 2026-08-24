# Cerrar un panadapter adicional

Cuando tiene varios panadapters abiertos en una distribución de múltiples slices, puede cerrar cualquiera de los adicionales para recuperar espacio en pantalla. Esta página explica cómo cerrar un panadapter que ya no necesita.

## Antes de comenzar

- Su radio debe estar conectada. El botón × (cerrar) solo está disponible cuando AetherSDR está conectado a una FLEX-8600.
- Debe tener más de un panadapter abierto. El botón × (cerrar) está oculto en el modo de panadapter único.

## Pasos

1. Localice la barra de título del panadapter que desea cerrar. Se encuentra en la parte superior del panadapter y muestra una etiqueta como "Slice A" o "Slice B".
2. Haga clic en el botón × en el extremo derecho de esa barra de título.

El panadapter se cierra inmediatamente. Los panadapters restantes se expanden para llenar el espacio disponible.

## Consejos

- Si no puede ver el botón ×, está en modo de panadapter único — solo hay un panadapter abierto y no se permite cerrarlo.
- Si el panadapter se ha extraído a una ventana flotante, el botón × sigue en la barra de título de la ventana flotante, en la esquina superior derecha. Haga clic allí.

## Solución de problemas

- **El botón × no es visible** — La radio está desconectada o solo hay un panadapter abierto. AetherSDR oculta el botón × en ambos casos. Conéctese a la radio y agregue un segundo panadapter antes de intentarlo nuevamente.

## Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro del panadapter y el waterfall cuando la decodificación CW está activa. Muestra el texto de código Morse decodificado, estadísticas de detección y controles para ajustar el decodificador.

### Redimensionamiento del panel CW (v26.7.4)

En v26.7.4, el panel de decodificación CW se puede redimensionar verticalmente arrastrando el delgado control de redimensionamiento en el borde superior del panel. Arrastre hacia abajo para aumentar la altura del panel y revelar más historial de texto decodificado, o arrastre hacia arriba para disminuirla. La altura del panel se conserva entre sesiones mediante el ajuste `CwDecodeSettings::panelHeight()`, limitado entre 60 y 600 píxeles.

### Tamaño de fuente del texto de decodificación CW (v26.7.4)

En v26.7.4, el tamaño de fuente del texto decodificado se puede ajustar usando los botones **A+** y **A-** en la barra de herramientas del panel CW. Cada clic aumenta o disminuye el tamaño de fuente en 1 píxel, limitado entre 8 y 32 píxeles. El tamaño de fuente se conserva entre sesiones mediante el ajuste `CwDecodeSettings::fontPx()`.

### Menú contextual del texto de decodificación CW

Hacer clic derecho en cualquier lugar dentro del área de texto de decodificación CW abre un menú contextual. Además de los comandos estándar de edición de texto (Select All, Copy, etc.), el menú incluye un elemento **Clear**. Elegir **Clear** borra todo el búfer de decodificación CW inmediatamente. Esto equivale a hacer clic en el botón **CLR** en la barra de herramientas del panel CW.

### Coloración TX/RX de decodificación CW

En el panel de decodificación CW, el texto recibido y el texto transmitido (autoenviado) se muestran en diferentes colores para que pueda distinguir su propio envío del CW entrante. Los colores son:

- **Verde**: Costo de confianza < 0.15 (alta confianza)
- **Amarillo**: Costo de confianza < 0.35
- **Naranja**: Costo de confianza < 0.60
- **Rojo**: Costo de confianza >= 0.60 (baja confianza)
- **Cian** (`#5fc8ff`): Texto decodificado de su propia transmisión

Al cambiar entre transmisión y recepción, se inserta automáticamente un espacio para evitar que las secuencias de texto de colores se fusionen.

### Controles del decodificador CW

La barra de herramientas del decodificador CW incluye los siguientes controles:

| Control | Tipo | Descripción |
|---------|------|-------------|
| Etiqueta de estadísticas CW | Indicador | Muestra el tono y la velocidad CW detectados como `<hz> Hz  <wpm> WPM` |
| Sens | Deslizador (0-100) | Filtra decodificaciones de baja confianza; valores más altos significan filtrado más estricto. Se asigna a un umbral de costo de 1.0 (0) a 0.1 (100). Clave de ajuste: `CwDecoderSensitivity` |
| 🔒P (Lock Pitch) | Botón de alternancia | Bloquea el tono del decodificador CW a la frecuencia sintonizada actual |
| 🔒S (Lock Speed) | Botón de alternancia | Bloquea la velocidad del decodificador CW al WPM actual |
| Deslizador de rango de tono | Deslizador de rango (300-1200 Hz) | Deslizador de doble manija para establecer el tono mínimo y máximo para la búsqueda del decodificador CW. Predeterminado: 500-700 Hz |
| Deslizador de rango WPM | Deslizador de rango (5-60 WPM) | Deslizador de doble manija para establecer la velocidad mínima y máxima para la búsqueda del decodificador CW. Predeterminado: 15-40 WPM |
| A- (disminuir tamaño de fuente) | Botón | Disminuye el tamaño de fuente del texto decodificado en 1 píxel (v26.7.4) |
| A+ (aumentar tamaño de fuente) | Botón | Aumenta el tamaño de fuente del texto decodificado en 1 píxel (v26.7.4) |
| CPY ALL | Botón | Copia todo el texto decodificado al portapapeles |
| CPY VIS | Botón | Copia solo el texto actualmente visible en el área de desplazamiento |
| CLR | Botón | Borra el búfer de decodificación CW |
| ✕ (cerrar CW) | Botón | Oculta el panel de decodificación CW |

### Indicador de sugerencia CW

Cuando se requiere enrutamiento de audio de PC pero no está configurado, aparece una etiqueta de sugerencia en el panel CW recordándole que "(requiere PC Audio)".

## Panel de decodificación RTTY (v26.6.3)

A partir de v26.6.3, AetherSDR incluye un panel de decodificación RTTY que aparece debajo del panadapter cuando el modo del slice activo está configurado a RTTY o DIGL. El panel funciona de manera similar al panel de decodificación CW pero para decodificación RTTY.

El panel RTTY incluye una lista desplegable para seleccionar el algoritmo del decodificador RTTY y controles para ajustar los parámetros del decodificador. El panel está oculto por defecto y solo aparece cuando el modo del slice está configurado adecuadamente.

## Título del slice con Multi-Flex

En sesiones Multi-Flex, el título del slice mostrado en la barra de título del panadapter usa la letra de índice proporcionada por la radio para que el título coincida con la insignia del slice. Esto garantiza consistencia cuando múltiples clientes están conectados a la misma radio.

## Comportamiento de congelación del waterfall

El waterfall se congela automáticamente cuando cualquier cliente en una sesión Multi-Flex comienza a transmitir. El estado de congelación está impulsado por el estado TRANSMITTING del interlock de la radio en lugar del borde local de MOX, eliminando el artefacto de estela de transmisión de 10-23 segundos que podía aparecer después de desactivar la transmisión.

Al reconectar la radio, se reafirman el FPS deseado del panadapter y la duración de línea del waterfall para evitar caer silenciosamente al valor predeterminado de 10 Hz de la radio. Además, los panadapters secundarios (Slices B–H) tienen su rango en dBm preparado al reconectar para que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que causaba espectro plano al reconectar.

## Tematización del panadapter (v26.6.1)

En v26.6.1, el panadapter y su panel de decodificación CW ahora usan estilos conscientes del tema en lugar de colores fijos. El degradado de la barra de título, los puntos del control de arrastre, el título del slice, las etiquetas de estadísticas y el fondo del panel CW hacen referencia a tokens de color del tema. Esto significa que el panadapter se adapta automáticamente a temas claros y oscuros sin requerir anulaciones de color manuales. El sistema de temas reemplaza las hojas de estilo de color fijo anteriores con valores basados en tokens como `{{color.background.1}}`, `{{color.text.secondary}}` y `{{color.accent}}`.

## Vista de espectro FFT 3D (v26.7.x)

A partir de v26.7.x, el panadapter incluye una vista opcional de espectro FFT 3D. Cuando está habilitada, el historial de señales se muestra como una superficie 3D que se desplaza hacia adelante con sombras de elevación y límites de desplazamiento suave. Las banderas de slice proyectan sombras de elevación almacenadas en caché sobre la superficie. El piso se resincroniza automáticamente después de un zoom de ancho de banda.

Use el botón de alternancia **3D FFT view** para habilitar o deshabilitar esta vista. El botón forma parte del SpectrumWidget y está deshabilitado por defecto.

## Alojamiento en lienzo (v26.8.4)

En v26.8.4, un panadapter en el lienzo del espacio de trabajo se comporta como un elemento de movimiento en vivo. Cuando el panadapter está alojado en el lienzo (en lugar de la distribución apilada anterior), arrastrar su franja de título transmite el gesto de movimiento directamente al lienzo — el mismo mecanismo utilizado por otros elementos del lienzo — en lugar del antiguo arrastre de ventana flotante. Un umbral de 6 píxeles separa un clic (que activa el panadapter) de un arrastre.

Cuando un panadapter está en el lienzo, el botón de extracción (⬈) siempre es visible, incluso si es el único panadapter presente. Esto es intencional: la ocultación del botón en modo de panadapter único se aplica solo a la distribución apilada, no a los elementos del lienzo, que siempre pueden extraerse.

## Relacionado

- [Panadapter overview](overview.md)
- [Click the spectrum to activate a panadapter (multi-slice mode)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)
- [Maximize one panadapter to fill the main area](maximize-one-panadapter-to-fill-the-main-area.md)
