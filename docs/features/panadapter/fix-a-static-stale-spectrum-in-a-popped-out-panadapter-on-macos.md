# Applet Panadáptico

## Resumen

El applet Panadáptico proporciona un contenedor para una única pantalla de panadáptico (espectro FFT + waterfall) con una barra de título y un panel opcional de decodificación CW debajo para la decodificación de Morse fuera del aire.

## Controles de la Barra de Título

La barra de título contiene los siguientes controles (visibles solo en modo multi-pan):

| Control | Tipo | Comportamiento |
|---------|------|---------------|
| Título de slice | Indicador | Muestra qué slice está vinculado a este panadáptico (Slice A..Slice H). Usa formato de texto enriquecido para la letra del slice. |
| ⬈ / ↩ (emergente/acoplar) | Botón pulsador | Saca el panadáptico a una ventana flotante o lo acopla de nuevo. En v0.9.5.1+, los recursos de GPU se reinician en cada ciclo de flotación/acople para compatibilidad con macOS. La ventana flotante no tiene marco — arrastre mediante la barra de título. |
| □ (maximizar) | Botón pulsador | Maximiza este panadáptico en un diseño multi-pan. |
| × (cerrar) | Botón pulsador | Cierra este panadáptico. |

## Espectro y Waterfall

El área principal de espectro/waterfall proporciona:
- Haga clic para activar el panadáptico
- Arrastre para sintonizar
- Desplácese para hacer zoom

**Comportamiento de congelación en TX (v0.9.7+):** La congelación/descongelación del waterfall se rige por el estado TRANSMITTING del interlock del radio en lugar del borde MOX local, eliminando el artefacto de estela de TX de 10 a 23 segundos después de desactivar la tecla. En configuraciones Multi-Flex, cualquier cliente que transmita activa la congelación.

**Comportamiento de reconexión:** Al reconectarse al radio, los FPS deseados del panadáptico y la duración de la línea del waterfall se reafirman automáticamente para evitar caer al valor predeterminado de 10 Hz del radio (#2465).

## Panel de Decodificación CW

El panel de decodificación CW proporciona decodificación de Morse fuera del aire con los siguientes controles:

### Controles del Decodificador

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---------|------|----------------|-------|---------------|
| Sens | Deslizador | 30 | 0-100 | Filtra decodificaciones de baja confianza; más alto = más estricto. Asigna 0-100 a un umbral de costo de 1.0-0.1. |
| 🔒P (Bloquear Tono) | Botón de alternancia | — | — | Bloquea el tono del decodificador CW a la frecuencia sintonizada actual. |
| 🔒S (Bloquear Velocidad) | Botón de alternancia | — | — | Bloquea la velocidad del decodificador CW a las WPM actuales. |
| Rango de tono | Deslizador de doble manija | Bajo: 500, Alto: 700 | 300-1200 Hz | Tono mínimo y máximo que busca el decodificador CW. Los valores se fijan para que Bajo ≤ Alto. |
| Rango de WPM | Deslizador de doble manija | Bajo: 15, Alto: 40 | 5-60 WPM | Velocidad mínima y máxima que busca el decodificador CW. Los valores se fijan para que Bajo ≤ Alto. |

### Controles de Visualización

| Control | Tipo | Comportamiento |
|---------|------|---------------|
| Etiqueta de estadísticas CW | Indicador | Muestra el tono y la velocidad CW detectados (ej., "700 Hz 25 WPM"). |
| CPY ALL | Botón pulsador | Copia todo el texto decodificado al portapapeles. |
| CPY VIS | Botón pulsador | Copia solo el texto actualmente visible en el área de desplazamiento. |
| CLR | Botón pulsador | Limpia el búfer de decodificación CW. |
| ✕ (cerrar CW) | Botón pulsador | Oculta el panel de decodificación CW. |

### Visualización de Texto Decodificado

La pantalla rodante de solo lectura muestra CW decodificado con codificación de colores por confianza:
- **Verde:** costo de confianza < 0.15
- **Amarillo:** costo de confianza < 0.35
- **Naranja:** costo de confianza < 0.60
- **Rojo:** costo de confianza ≥ 0.60

**Soporte de decodificación en TX (v0.9.7+):** Cuando tanto el CW entrante como el saliente se decodifican a través del mismo panel, el texto transmitido aparece en cian (#5fc8ff) para distinguirlo del texto recibido. Se inserta automáticamente un espacio separador entre las ejecuciones de TX y RX para evitar la fusión visual (#2417).

### Requisitos del Decodificador

- Requiere enrutamiento de audio de PC al radio para la decodificación fuera del aire.
- Cuando el audio de PC no está configurado, se muestra una sugerencia "(requires PC Audio)".

### Soporte de Temas (v26.6.1+)

A partir de v26.6.1, los colores del tema del applet panadáptico provienen del sistema de temas. El gradiente de fondo de la barra de título utiliza colores de parada `{{color.text.disabled}}`, `{{color.background.1}}` y `#1a2a38`. El agarre de arrastre utiliza `{{color.text.label}}`. El título del slice usa `{{color.text.secondary}}`. El fondo del panel CW usa `{{color.background.0}}` con un borde que usa `{{color.background.1}}`. El título CW usa `{{color.accent}}`. La sugerencia CW usa `{{color.meter.bar.fill}}`. La etiqueta de estadísticas CW usa `{{color.text.label}}`. La etiqueta Sens usa `{{color.text.label}}`. El deslizador de sensibilidad usa `applyPrimarySliderStyle()` para una apariencia temática.

## Comportamiento de Ventana Flotante (macOS)

**Problema de superficie GPU Metal (v0.9.5.1+):** En macOS, al sacar un panadáptico a una ventana flotante, el espectro puede quedar congelado. AetherSDR resuelve esto automáticamente reiniciando los recursos de GPU y reenlazando la superficie de renderizado Metal durante cada ciclo de flotación/acople.

### Pasos para restaurar el espectro después de la congelación

1. En la barra de título del panadáptico, haga clic en ↩ para acoplar el panadáptico flotante de vuelta a la ventana principal.
2. Haga clic en ⬈ para sacarlo de nuevo.

Después del paso 2, el espectro debería estar activo.

### Consejos

- Si el espectro aún está estático después de un ciclo de acople/emergencia, repita el ciclo una vez más.
- Salir y reiniciar AetherSDR también elimina la condición.

### Solución de Problemas

- **El botón de emergencia ⬈ no es visible** — Está en modo de un solo pan. Agregue un segundo panadáptico para habilitar el modo multi-pan.
- **El espectro aún está congelado después de acoplar/desacoplar** — Confirme que está usando v0.9.5.1 o posterior.

## Soporte de Sesiones Multi-Flex (v0.9.7+)

En sesiones Multi-Flex, el título del slice usa la letra de índice proporcionada por el radio para coincidir con la insignia del slice. La letra opcional por cliente anula la asignación estándar A-H para asegurar que el título coincida con el slice real que se muestra (#2606).

## Panel de Decodificación RTTY (v26.6.3+)

El panel de decodificación RTTY aparece automáticamente cuando el modo del slice se establece en RTTY o DIGL. Proporciona decodificación RTTY fuera del aire con los siguientes controles:

### Controles del Decodificador

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---------|------|----------------|-------|---------------|
| BAUD | Cuadro combinado | 45.45 | 45.45, 50, 75, 100, 110, 150, 200, 300 | Selecciona la velocidad en baudios RTTY. |
| SHIFT | Cuadro combinado | 170 | 170, 200, 425, 850 | Selecciona el desplazamiento de frecuencia RTTY. |
| CPY ALL | Botón pulsador | — | — | Copia todo el texto decodificado al portapapeles. |
| CPY VIS | Botón pulsador | — | — | Copia solo el texto actualmente visible en el área de desplazamiento. |
| CLR | Botón pulsador | — | — | Limpia el búfer de decodificación RTTY. |
| ✕ (cerrar RTTY) | Botón pulsador | — | — | Oculta el panel de decodificación RTTY. |

### Visualización de Texto Decodificado

La pantalla rodante de solo lectura muestra los caracteres RTTY decodificados.

### Requisitos del Decodificador

- Requiere enrutamiento de audio de PC al radio para la decodificación fuera del aire.
- El panel solo aparece cuando el modo del slice es RTTY o DIGL.
- La configuración de velocidad en baudios y desplazamiento se guarda por slice y persiste entre sesiones.

## Relacionado

- [Sacar un panadáptico a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Resumen del panadáptico](overview.md)
