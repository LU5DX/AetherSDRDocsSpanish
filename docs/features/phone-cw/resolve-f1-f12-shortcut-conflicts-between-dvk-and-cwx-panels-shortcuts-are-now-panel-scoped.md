# Resolver conflictos de atajos F1-F12 entre los paneles DVK y CWX (los atajos ahora tienen ámbito de panel)

Esta página explica cómo los atajos de teclado F1-F12 ahora tienen ámbito dentro del panel visible, de modo que los paneles DVK (Digital Voice Keyer) y CWX (Macros CW) ya no se activan simultáneamente cuando ambos están abiertos.

## Antes de empezar

- Tanto el panel DVK como el panel CWX deben estar abiertos en el panel de applets de la barra lateral derecha
- El botón de bandeja "P/CW" debe estar visible en la barra lateral derecha

## Pasos

1. Haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrir el applet Phone/CW.
2. El applet Phone/CW cambia automáticamente entre su panel Phone (para modos de voz) y su panel CW (para modos CW) según el modo del slice activo.
3. Presione cualquier tecla F1-F12: el atajo solo se activa para el panel que está actualmente visible (panel Phone → macros DVK; panel CW → macros CWX).

No se requiere configuración. El comportamiento es automático.

## Qué hace cada control

| Control | Comportamiento |
|---------|----------------|
| **Botón de bandeja P/CW** | Alterna la visibilidad del applet Phone/CW en la barra lateral derecha |
| **Panel apilado del applet Phone/CW** | Muestra automáticamente los controles Phone (modos de voz) o los controles CW (modo CW); solo los atajos F1-F12 del panel visible están activos |

## Consejos

- Este comportamiento se introdujo para solucionar el problema #2464/#2469. Anteriormente, tener ambos paneles DVK y CWX abiertos provocaba que ambos conjuntos de macros F1-F12 se activaran simultáneamente.
- Las macros CWX liberan automáticamente TX cuando la cola se vacía (problema #2450/#2507), por lo que no necesita detener manualmente la transmisión después de que finalice una macro.

## Relacionado

- [Descripción general](overview.md)
