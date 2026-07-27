# Aplet de Panadaptador

## Descripción general

El aplet de Panadaptador proporciona un contenedor para una sola visualización de panadaptador (espectro FFT + waterfall) con una barra de título y un panel opcional de decodificación CW debajo para la decodificación de Morse fuera del aire.

## Controles de la barra de título

La barra de título contiene los siguientes controles (visibles solo en modo multipanel):

| Control | Tipo | Comportamiento |
|---------|------|---------------|
| Título de slice | Indicador | Muestra qué slice está vinculado a este panadaptador (Slice A..Slice H). Utiliza formato de texto enriquecido para la letra del slice. |
| ⬈ / ↩ (desacoplar/acoplar) | Botón pulsador | Desacopla el panadaptador en una ventana flotante o lo acopla de nuevo. En v0.9.5.1+, los recursos de GPU se restablecen en cada ciclo de flotación/acople para compatibilidad con macOS. La ventana flotante no tiene marco — arrastre mediante la tira de título. |
| □ (maximizar) | Botón pulsador | Maximiza este panadaptador en un diseño multipanel. |
| × (cerrar) | Botón pulsador | Cierra este panadaptador. |

## Espectro y Waterfall

El área principal de espectro/waterfall proporciona:
- Haga clic para activar el panadaptador
- Arrastre para sintonizar
- Desplace la rueda para hacer zoom

**Comportamiento de congelación en TX (v0.9.7+):** La congelación/descongelación del waterfall se controla mediante el estado TRANSMITTING del interlock de la radio, en lugar del borde local de MOX, eliminando el artefacto de estela de TX de 10 a 23 segundos después de dejar de pulsar la tecla. En configuraciones Multi-Flex, cualquier cliente que transmita activa la congelación.

**Comportamiento de reconexión:** Al reconectar la radio, los FPS deseados del panadaptador y la duración de la línea del waterfall se restablecen automáticamente para evitar que caigan al valor predeterminado de la radio de 10 Hz (#2465).

**Rango de dBm del panadaptador secundario:** Al reconectar, los panadaptadores secundarios (Slices B–H) tienen su rango de dBm inicializado para que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que causaba un espectro plano (#3034).

## Panel de decodificación CW

El panel de decodificación CW proporciona decodificación de Morse fuera del aire con los siguientes controles:

### Controles del decodificador

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---------|------|----------------------|-------|---------------|
| Sens | Deslizador | 30 | 0-100 | Filtra decodificaciones de baja confianza; más alto = más estricto. Asigna 0-100 a un umbral de costo de 1.0-0.1. |
| 🔒P (Bloquear tono) | Botón de alternancia | — | — | Bloquea el tono del decodificador CW en la frecuencia sintonizada actual. |
| 🔒S (Bloquear velocidad) | Botón de alternancia | — | — | Bloquea la velocidad del decodificador CW en las WPM actuales. |
| Rango de tono | Deslizador de doble mango | Bajo: 500, Alto: 700 | 300-1200 Hz | Tono mínimo y máximo que busca el decodificador CW. Los valores se limitan para que Bajo ≤ Alto. |
| Rango de WPM | Deslizador de doble mango | Bajo: 15, Alto: 40 | 5-60 WPM | Velocidad mínima y máxima que busca el decodificador CW. Los valores se limitan para que Bajo ≤ Alto. |

### Controles de visualización

| Control | Tipo | Comportamiento |
|---------|------|---------------|
| Etiqueta de estadísticas CW | Indicador | Muestra el tono y la velocidad CW detectados (ej., "700 Hz 25 WPM"). |
| A- (Reducir fuente) | Botón pulsador | Disminuye el tamaño de fuente del texto decodificado. La configuración se conserva entre sesiones. |
| A+ (Aumentar fuente) | Botón pulsador | Aumenta el tamaño de fuente del texto decodificado. La configuración se conserva entre sesiones. |
| CPY ALL | Botón pulsador | Copia todo el texto decodificado al portapapeles. |
| CPY VIS | Botón pulsador | Copia solo el texto actualmente visible en el área de desplazamiento. |
| CLR | Botón pulsador | Borra el búfer de decodificación CW. |
| ✕ (cerrar CW) | Botón pulsador | Oculta el panel de decodificación CW. |

### Redimensionamiento del panel de decodificación CW

Aparece un fino asidero de arrastre a lo largo del borde superior del panel de decodificación CW. Para redimensionar el panel:

1. Pase el cursor sobre el asidero de arrastre (el cursor cambia a una flecha de redimensionamiento vertical).
2. Haga clic y arrastre hacia arriba o abajo para ajustar la altura del panel.
3. La altura se conserva y se restaura al reiniciar.

El asidero de arrastre permite ajustar la altura del panel sin cambiar la jerarquía del widget de espectro de GPU.

### Visualización de texto decodificado

La pantalla rodante de solo lectura muestra CW decodificado con codificación de colores según la confianza:
- **Verde:** Costo de confianza < 0,15
- **Amarillo:** Costo de confianza < 0,35
- **Naranja:** Costo de confianza < 0,60
- **Rojo:** Costo de confianza ≥ 0,60

El tamaño de fuente se puede ajustar usando los botones A- y A+, manteniendo la configuración entre sesiones.

**Soporte de decodificación en TX (v0.9.7+):** Cuando tanto el CW entrante como el saliente se decodifican a través del mismo panel, el texto transmitido aparece en cian (#5fc8ff) para distinguirlo del texto recibido. Se inserta automáticamente un espacio separador entre las secuencias de TX y RX para evitar la fusión visual (#2417).

### Requisitos del decodificador

- Requiere enrutamiento de audio de PC a la radio para la decodificación fuera del aire.
- Cuando el audio de PC no está configurado, se muestra una indicación "(requires PC Audio)".

### Soporte de temas (v26.6.1+)

A partir de v26.6.1, los colores del tema del aplet de panadaptador provienen del sistema de temas. El degradado de fondo de la barra de título utiliza colores de parada `{{color.text.disabled}}`, `{{color.background.1}}` y `#1a2a38`. El asidero de arrastre utiliza `{{color.text.label}}`. El título del slice utiliza `{{color.text.secondary}}`. El fondo del panel CW utiliza `{{color.background.0}}` con un borde que usa `{{color.background.1}}`. El título CW utiliza `{{color.accent}}`. La sugerencia CW utiliza `{{color.meter.bar.fill}}`. La etiqueta de estadísticas CW utiliza `{{color.text.label}}`. La etiqueta Sens utiliza `{{color.text.label}}`. El deslizador de sensibilidad utiliza `applyPrimarySliderStyle()` para la apariencia temática. El asidero de redimensionamiento CW utiliza `{{color.background.2}}`.

## Comportamiento de ventana flotante (macOS)

**Problema de superficie GPU Metal (v0.9.5.1+):** En macOS, desacoplar un panadaptador en una ventana flotante puede dejar el espectro congelado. AetherSDR resuelve esto automáticamente restableciendo los recursos de GPU y re vinculando la superficie de renderizado Metal durante cada ciclo de flotación/acople.

### Pasos para restaurar el espectro después de una congelación

1. En la barra de título del panadaptador, haga clic en ↩ para acoplar el panadaptador flotante de vuelta a la ventana principal.
2. Haga clic en ⬈ para desacoplarlo nuevamente.

Después del paso 2, el espectro debería estar activo.

### Consejos

- Si el espectro sigue estático después de un ciclo de acople/desacople, repita el ciclo una vez más.
- Salir y reiniciar AetherSDR también soluciona la condición.

### Solución de problemas

- **El botón de desacoplar ⬈ no es visible** — Está en modo de un solo panel. Agregue un segundo panadaptador para habilitar el modo multipanel.
- **El espectro sigue congelado después de acoplar/desacoplar** — Confirme que está usando v0.9.5.1 o posterior.

## Soporte de sesión Multi-Flex (v0.9.7+)

En sesiones Multi-Flex, el título del slice utiliza la letra de índice proporcionada por la radio para que coincida con la insignia del slice. La letra opcional por cliente anula la asignación estándar A-H para garantizar que el título coincida con el slice real que se muestra (#2606).

## Panel de decodificación RTTY (v26.6.3+)

El panel de decodificación RTTY aparece automáticamente cuando el modo del slice se establece en RTTY o DIGL. Proporciona decodificación RTTY fuera del aire con los siguientes controles:

### Controles del decodificador

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---------|------|----------------------|-------|---------------|
| BAUD | Cuadro combinado | 45.45 | 45.45, 50, 75, 100, 110, 150, 200, 300 | Selecciona la velocidad en baudios RTTY. |
| SHIFT | Cuadro combinado | 170 | 170, 200, 425, 850 | Selecciona el desplazamiento de frecuencia RTTY. |
| CPY ALL | Botón pulsador | — | — | Copia todo el texto decodificado al portapapeles. |
| CPY VIS | Botón pulsador | — | — | Copia solo el texto actualmente visible en el área de desplazamiento. |
| CLR | Botón pulsador | — | — | Borra el búfer de decodificación RTTY. |
| ✕ (cerrar RTTY) | Botón pulsador | — | — | Oculta el panel de decodificación RTTY. |

### Visualización de texto decodificado

La pantalla rodante de solo lectura muestra los caracteres RTTY decodificados.

### Requisitos del decodificador

- Requiere enrutamiento de audio de PC a la radio para la decodificación fuera del aire.
- El panel solo aparece cuando el modo del slice es RTTY o DIGL.
- La configuración de velocidad en baudios y desplazamiento se guarda por slice y persiste entre sesiones.

## Relacionado

- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)
- [Panadapter overview](overview.md)
