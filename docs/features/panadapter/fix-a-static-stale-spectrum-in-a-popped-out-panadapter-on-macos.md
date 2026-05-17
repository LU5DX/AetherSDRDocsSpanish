# Applet de Panadapter

## Descripción general

El applet de Panadapter proporciona un contenedor para una sola visualización de panadapter (espectro FFT + waterfall) con una barra de título y un panel opcional de decodificación CW debajo para la decodificación de Morse fuera del aire.

## Controles de la barra de título

La barra de título contiene los siguientes controles (visibles solo en modo multi-pan):

| Control | Tipo | Comportamiento |
|---------|------|---------------|
| Título del slice | Indicador | Muestra qué slice está vinculado a este panadapter (Slice A..Slice H). Usa formato de texto enriquecido para la letra del slice. |
| ⬈ / ↩ (emergente/acoplar) | Botón pulsador | Saca el panadapter a una ventana flotante o lo acopla de nuevo. En v0.9.5.1+, los recursos de GPU se restablecen en cada ciclo de flotación/acoplamiento para compatibilidad con macOS. La ventana flotante no tiene marco — arrastre mediante la barra de título. |
| □ (maximizar) | Botón pulsador | Maximiza este panadapter en un diseño multi-pan. |
| × (cerrar) | Botón pulsador | Cierra este panadapter. |

## Espectro y Waterfall

El área principal de espectro/waterfall proporciona:
- Haga clic para activar el panadapter
- Arrastre para sintonizar
- Desplace la rueda para hacer zoom

**Comportamiento de congelación en TX (v0.9.7+):** La congelación/descongelación del waterfall se controla mediante el estado de TRANSMISIÓN del interlock de la radio en lugar del borde MOX local, eliminando el artefacto de estela de TX de 10 a 23 segundos después de desactivar la transmisión. En configuraciones Multi-Flex, cualquier cliente que transmita activa la congelación.

**Comportamiento de reconexión:** Al reconectar la radio, los FPS deseados del panadapter y la duración de la línea del waterfall se reafirman automáticamente para evitar que caigan al valor predeterminado de 10 Hz de la radio (#2465).

## Panel de decodificación CW

El panel de decodificación CW proporciona decodificación de Morse fuera del aire con los siguientes controles:

### Controles del decodificador

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---------|------|----------------|-------|---------------|
| Sens | Deslizador | 30 | 0-100 | Filtra decodificaciones de baja confianza; más alto = más estricto. Mapea 0-100 al umbral de costo 1.0-0.1. |
| 🔒P (Bloquear tono) | Botón de alternancia | — | — | Bloquea el tono del decodificador CW a la frecuencia sintonizada actual. |
| 🔒S (Bloquear velocidad) | Botón de alternancia | — | — | Bloquea la velocidad del decodificador CW a las PPM actuales. |
| Lo (tono mínimo) | Deslizador | 500 | 300-1200 Hz | Tono mínimo que busca el decodificador CW; limitado ≤ Hi. |
| Hi (tono máximo) | Deslizador | 700 | 300-1200 Hz | Tono máximo que busca el decodificador CW; limitado ≥ Lo. |

### Controles de visualización

| Control | Tipo | Comportamiento |
|---------|------|---------------|
| Etiqueta de estadísticas CW | Indicador | Muestra el tono y la velocidad de CW detectados (ej., "700 Hz 25 WPM"). |
| CPY ALL | Botón pulsador | Copia todo el texto decodificado al portapapeles. |
| CPY VIS | Botón pulsador | Copia solo el texto actualmente visible en el área de desplazamiento. |
| CLR | Botón pulsador | Limpia el búfer de decodificación CW. |
| ✕ (cerrar CW) | Botón pulsador | Oculta el panel de decodificación CW. |

### Visualización de texto decodificado

La pantalla rodante de solo lectura muestra CW decodificado con código de colores según la confianza:
- **Verde:** Costo de confianza < 0.15
- **Amarillo:** Costo de confianza < 0.35
- **Naranja:** Costo de confianza < 0.60
- **Rojo:** Costo de confianza ≥ 0.60

**Soporte de decodificación en TX (v0.9.7+):** Cuando tanto el CW entrante como el saliente se decodifican a través del mismo panel, el texto transmitido aparece en cian (#5fc8ff) para distinguirlo del texto recibido. Se inserta automáticamente un espacio separador entre las ejecuciones de TX y RX para evitar la fusión visual (#2417).

### Requisitos del decodificador

- Requiere enrutamiento de audio de PC a la radio para la decodificación fuera del aire.
- Cuando el audio de PC no está configurado, se muestra una sugerencia "(requires PC Audio)".

## Comportamiento de ventana flotante (macOS)

**Problema de superficie GPU Metal (v0.9.5.1+):** En macOS, sacar un panadapter a una ventana flotante puede dejar el espectro congelado. AetherSDR resuelve esto automáticamente restableciendo los recursos de GPU y reasociando la superficie de renderizado Metal durante cada ciclo de flotación/acoplamiento.

### Pasos para restaurar el espectro después de una congelación

1. En la barra de título del panadapter, haga clic en ↩ para acoplar el panadapter flotante de vuelta a la ventana principal.
2. Haga clic en ⬈ para sacarlo de nuevo.

Después del paso 2, el espectro debería estar activo.

### Consejos

- Si el espectro sigue estático después de un ciclo de acoplamiento/emergente, repita el ciclo una vez más.
- Salir y reiniciar AetherSDR también soluciona la condición.

### Solución de problemas

- **El botón emergente ⬈ no es visible** — Está en modo de un solo pan. Agregue un segundo panadapter para habilitar el modo multi-pan.
- **El espectro sigue congelado después de acoplar/desacoplar** — Confirme que está usando v0.9.5.1 o posterior.

## Soporte de sesión Multi-Flex (v0.9.7+)

En sesiones Multi-Flex, el título del slice utiliza la letra de índice proporcionada por la radio para coincidir con la insignia del slice. La letra opcional por cliente anula la asignación estándar A-H para garantizar que el título coincida con el slice real que se muestra (#2606).

## Relacionados

- [Sacar un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Descripción general del panadapter](overview.md)
