# Applet de Panadapter

## Descripción general

El applet de Panadapter proporciona un contenedor para una sola visualización de panadapter (espectro FFT + waterfall) con una barra de título y un panel opcional de decodificación CW debajo para la decodificación de Morse fuera del aire.

## Controles de la barra de título

La barra de título contiene los siguientes controles:

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| Título de slice | Indicador | Muestra qué slice está vinculado a este panadapter (Slice A..Slice H). Usa formato de texto enriquecido para la letra del slice. |
| ⬈ / ↩ (pop-out/acoplar) | Botón pulsador | Expulsa el panadapter a una ventana flotante o lo acopla de nuevo. En v0.9.5.1+, los recursos de GPU se restablecen en cada ciclo de flotación/acople para compatibilidad con macOS. La ventana flotante no tiene marco; arrastre mediante la franja de título. |
| □ (maximizar) | Botón pulsador | Maximiza este panadapter en un diseño de múltiples pannels. |
| × (cerrar) | Botón pulsador | Cierra este panadapter. |

**Reglas de visibilidad:**
- En modo de un solo pan, los botones de maximizar y cerrar están ocultos.
- El botón de pop-out está oculto en modo de un solo pan (apilado), pero siempre está visible cuando el panadapter está alojado en el lienzo del espacio de trabajo.

## Espectro y Waterfall

El área principal de espectro/waterfall proporciona:
- Clic para activar el panadapter
- Arrastrar para sintonizar
- Desplazarse para hacer zoom

**Vista 3D FFT (v26.7.x+):** Alterne la vista de espectro 3D FFT para mostrar el historial de señales como una superficie 3D que se desplaza hacia adelante con sombras de elevación, límites de desplazamiento suave y piso resincronizado después del zoom de ancho de banda. Los indicadores de slice proyectan sombras de elevación almacenadas en caché.

**Comportamiento de congelación por TX (v0.9.7+):** La congelación/descongelación del waterfall está impulsada por el estado TRANSMITTING del interlock de la radio, en lugar del borde local de MOX, eliminando el artefacto de estela de TX de 10–23 segundos después de desactivar la transmisión. En configuraciones Multi-Flex, cualquier cliente que transmita activa la congelación.

**Comportamiento de reconexión:** Al reconectar la radio, la FPS deseada del panadapter y la duración de línea del waterfall se reafirman automáticamente para evitar que caigan a los 10 Hz predeterminados de la radio (#2465).

**Rango dBm del panadapter secundario:** Al reconectar, los panadapters secundarios (Slices B–H) tienen su rango dBm preparado para que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que causaba un espectro plano (#3034).

## Alojamiento en lienzo (v26.8.4, RFC #4887)

Cuando el panadapter está alojado como un elemento en el lienzo del espacio de trabajo, la franja de título transmite el gesto de movimiento en vivo, el mismo mecanismo que el modo de lienzo de ContainerTitleBar. Este es un gesto real que la sesión del lienzo sigue, no un fantasma de QDrag.

**Umbral de arrastre:** Un umbral de 6 px separa un clic (que activa el panadapter) de un arrastre. Todo lo que supere ese umbral se consume para que la maquinaria de arrastre flotante de la franja nunca lo vea.

**Pop-out en lienzo:** Un elemento del lienzo siempre puede expandirse, incluso como el único pan; la ocultación del botón en modo de un solo pan es una economía del modo apilado, no una regla sobre la flotación. Fuera del lienzo, el siguiente modo de diseño de la pila vuelve a aplicar su economía.

## Panel de decodificación CW

El panel de decodificación CW proporciona decodificación de Morse fuera del aire con los siguientes controles:

### Controles del decodificador

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---------|------|----------------|-------|----------------|
| Sens | Deslizador | 30 | 0-100 | Filtra decodificaciones de baja confianza; más alto = más estricto. Asigna 0-100 al umbral de costo 1.0-0.1. |
| 🔒P (Bloquear tono) | Botón de alternancia | — | — | Bloquea el tono del decodificador CW a la frecuencia sintonizada actual. |
| 🔒S (Bloquear velocidad) | Botón de alternancia | — | — | Bloquea la velocidad del decodificador CW a las WPM actuales. |
| Rango de tono | Deslizador de doble manija | Bajo: 500, Alto: 700 | 300-1200 Hz | Tono mínimo y máximo que busca el decodificador CW. Los valores se limitan para que Bajo ≤ Alto. |
| Rango de WPM | Deslizador de doble manija | Bajo: 15, Alto: 40 | 5-60 WPM | Velocidad mínima y máxima que busca el decodificador CW. Los valores se limitan para que Bajo ≤ Alto. |

### Controles de visualización

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| Etiqueta de estadísticas CW | Indicador | Muestra el tono y la velocidad CW detectados (p. ej., "700 Hz 25 WPM"). |
| A- (Reducir fuente) | Botón pulsador | Disminuye el tamaño de fuente del texto decodificado. La configuración se guarda entre sesiones. |
| A+ (Aumentar fuente) | Botón pulsador | Aumenta el tamaño de fuente del texto decodificado. La configuración se guarda entre sesiones. |
| CPY ALL | Botón pulsador | Copia todo el texto decodificado al portapapeles. |
| CPY VIS | Botón pulsador | Copia solo el texto actualmente visible en el área de desplazamiento. |
| CLR | Botón pulsador | Borra el búfer de decodificación CW. |
| ✕ (cerrar CW) | Botón pulsador | Oculta el panel de decodificación CW. |

### Redimensionamiento del panel de decodificación CW

Una fina empuñadura de arrastre aparece a lo largo del borde superior del panel de decodificación CW. Para redimensionar el panel:

1. Pase el cursor sobre la empuñadura de arrastre (el cursor cambia a una flecha de redimensionamiento vertical).
2. Haga clic y arrastre hacia arriba o hacia abajo para ajustar la altura del panel.
3. La altura se guarda y se restaura al reiniciar.

La empuñadura de arrastre permite ajustar la altura del panel sin cambiar el widget de espectro GPU de padre.

### Visualización del texto decodificado

La pantalla rodante de solo lectura muestra CW decodificado con codificación de colores por confianza:
- **Verde:** costo de confianza < 0.15
- **Amarillo:** costo de confianza < 0.35
- **Naranja:** costo de confianza < 0.60
- **Rojo:** costo de confianza ≥ 0.60

El tamaño de fuente se puede ajustar con los botones A- y A+, y la configuración se guarda entre sesiones.

**Soporte de decodificación TX (v0.9.7+):** Cuando tanto el CW entrante como el saliente se decodifican a través del mismo panel, el texto transmitido aparece en cian (#5fc8ff) para distinguirlo del texto recibido. Se inserta automáticamente un espacio separador entre las secuencias TX y RX para evitar la fusión visual (#2417).

### Requisitos del decodificador

- Requiere enrutamiento de audio de PC a la radio para la decodificación fuera del aire.
- Cuando el audio de PC no está configurado, se muestra una pista "(requires PC Audio)".

### Soporte de temas (v26.6.1+)

A partir de v26.6.1, los colores del tema del applet de panadapter provienen del sistema de temas. El degradado de fondo de la barra de título usa `{{color.text.disabled}}`, `{{color.background.1}}` y colores de parada `#1a2a38`. La empuñadura de arrastre usa `{{color.text.label}}`. El título del slice usa `{{color.text.secondary}}`. El fondo del panel CW usa `{{color.background.0}}` con un borde usando `{{color.background.1}}`. El título CW usa `{{color.accent}}`. La pista CW usa `{{color.meter.bar.fill}}`. La etiqueta de estadísticas CW usa `{{color.text.label}}`. La etiqueta Sens usa `{{color.text.label}}`. El deslizador de sensibilidad usa `applyPrimarySliderStyle()` para la apariencia temática. La empuñadura de redimensionamiento CW usa `{{color.background.2}}`.

## Comportamiento de ventana flotante (macOS)

**Problema de superficie GPU Metal (v0.9.5.1+):** En macOS, expandir un panadapter a una ventana flotante puede dejar el espectro congelado. AetherSDR resuelve esto automáticamente restableciendo los recursos de GPU y volviendo a vincular la superficie de renderizado Metal durante cada ciclo de flotación/acople.

### Pasos para restaurar el espectro después de la congelación

1. En la barra de título del panadapter, haga clic en ↩ para acoplar el panadapter flotante de nuevo a la ventana principal.
2. Haga clic en ⬈ para expandirlo de nuevo.

Después del paso 2, el espectro debería estar activo.

### Consejos

- Si el espectro sigue estático después de un ciclo de acople/expansión, repita el ciclo una vez más.
- Salir y reiniciar AetherSDR también elimina la condición.

### Solución de problemas

- **El botón de pop-out ⬈ no es visible** — Está en modo de un solo pan (apilado). Agregue un segundo panadapter para habilitar el modo de múltiples pannels, o aloje el panadapter en el lienzo del espacio de trabajo donde el pop-out siempre está disponible.
- **El espectro sigue congelado después de acoplar/desacoplar** — Confirme que está en v0.9.5.1 o posterior.

## Soporte de sesiones Multi-Flex (v0.9.7+)

En sesiones Multi-Flex, el título del slice usa la letra de índice proporcionada por la radio para coincidir con la insignia del slice. La letra opcional por cliente anula la asignación estándar A-H para garantizar que el título coincida con el slice real que se muestra (#2606).

## Panel de decodificación RTTY (v26.6.3+)

El panel de decodificación RTTY aparece automáticamente cuando el modo del slice se establece en RTTY o DIGL. Proporciona decodificación RTTY fuera del aire con los siguientes controles:

### Controles del decodificador

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---------|------|----------------|-------|----------------|
| BAUD | Cuadro combinado | 45.45 | 45.45, 50, 75, 100, 110, 150, 200, 300 | Selecciona la velocidad de baudios RTTY. |
| SHIFT | Cuadro combinado | 170 | 170, 200, 425, 850 | Selecciona el desplazamiento de frecuencia RTTY. |
| CPY ALL | Botón pulsador | — | — | Copia todo el texto decodificado al portapapeles. |
| CPY VIS | Botón pulsador | — | — | Copia solo el texto actualmente visible en el área de desplazamiento. |
| CLR | Botón pulsador | — | — | Borra el búfer de decodificación RTTY. |
| ✕ (cerrar RTTY) | Botón pulsador | — | — | Oculta el panel de decodificación RTTY. |

### Visualización del texto decodificado

La pantalla rodante de solo lectura muestra los caracteres RTTY decodificados.

### Requisitos del decodificador

- Requiere enrutamiento de audio de PC a la radio para la decodificación fuera del aire.
- El panel solo aparece cuando el modo del slice es RTTY o DIGL.
- La velocidad de baudios y la configuración de desplazamiento se guardan por slice y persisten entre sesiones.

## Relacionado

- [Expandir un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Descripción general del panadapter](overview.md)
