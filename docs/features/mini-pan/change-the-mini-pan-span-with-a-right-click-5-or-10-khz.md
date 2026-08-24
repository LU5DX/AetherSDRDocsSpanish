# Cambie el alcance del mini-pan con un clic derecho (5 o 10 kHz)

Esta página le muestra cómo cambiar el alcance estrecho del mini-pan entre sus dos extensiones disponibles — ±5 kHz (10 kHz en total) y ±10 kHz (20 kHz en total) — mediante un menú de clic derecho.

## Antes de comenzar

- Su FLEX-8600 debe estar conectado a AetherSDR.
- El applet Mini-Pan debe estar abierto (consulte [Abra el alcance estrecho del mini-pan](open-the-mini-pan-narrow-scope.md)).

## Pasos

1. Haga clic derecho en cualquier parte del alcance del mini-pan.
2. En el menú contextual, elija **±5 kHz** o **±10 kHz**.
3. El alcance se re-cortará inmediatamente a la nueva extensión en el siguiente fotograma.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Configuración persistida |
|---------|----------------|--------------|--------------------------|
| **±5 kHz** (acción del menú de clic derecho) | Seleccionado | ±5 kHz (extensión de 10 kHz) | `MiniPan` |
| **±10 kHz** (acción del menú de clic derecho) | — | ±10 kHz (extensión de 20 kHz) | `MiniPan` |

- La extensión elegida se conserva entre sesiones. Los valores en el objeto AppSettings `MiniPan` fuera de las dos opciones del menú vuelven al valor predeterminado de ±5 kHz.
- La lectura del VFO y el marcador de línea fina se dibujan dentro del alcance en la misma fila que las etiquetas de extensión; la lectura se centra en el centro de la banda pasante, no en la portadora.

## Consejos

- El menú de extensión solo ofrece las dos opciones de frecuencia. Los controles de flotar, acoplar, siempre encima y cerrar se encuentran en la barra de título del contenedor que envuelve el applet.
- El rango de dBm del alcance es fijo de −130 a −40; no se ajusta automáticamente.

## Relacionado

- [Abra el alcance estrecho del mini-pan](open-the-mini-pan-narrow-scope.md)
- [Descripción general del Mini-Pan](overview.md)
