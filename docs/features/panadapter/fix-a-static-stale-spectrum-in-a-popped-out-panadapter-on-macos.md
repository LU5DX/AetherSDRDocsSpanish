# Solucionar un espectro estático/estático en un panadapter emergido en macOS

En macOS, al emerger un panadapter en una ventana flotante, el espectro puede quedar congelado — el FFT y el waterfall dejan de actualizarse aunque la radio siga conectada. Este es un problema conocido de la superficie Metal/GPU que AetherSDR resuelve automáticamente a partir de la versión v0.9.5.1.

## Antes de comenzar

- AetherSDR v0.9.5.1 o posterior está instalado. Las versiones anteriores no incluyen la corrección.
- Está ejecutando macOS con una FLEX-8600 conectada.
- Tiene más de un panadapter abierto (el botón de emerger/regresar ↩ está oculto en el modo de un solo panadapter).

## Pasos

1. En la barra de título del panadapter, haga clic en ↩ para acoplar el panadapter flotante de vuelta en la ventana principal.
2. Haga clic en ⬈ para emergerlo nuevamente.

AetherSDR restablece los recursos de GPU y reasigna la superficie de renderizado Metal a la ventana nueva durante cada ciclo de emerger/acoplar. Después del paso 2, el espectro debería estar activo.

## Consejos

- Si el espectro sigue estático después de un ciclo de acoplar/emerger, repita el ciclo una vez más. Un estado de desconexión WAN obsoleto puede requerir ocasionalmente un segundo restablecimiento.
- Salir y reiniciar AetherSDR también soluciona la condición. La aplicación libera los recursos de GPU durante el cierre específicamente para evitar un fallo de destrucción de Metal en este escenario.

## Solución de problemas

- **El botón de emerger ↩ no es visible** — Está en modo de un solo panadapter. Agregue un segundo panadapter para habilitar el modo multipan; los botones de la barra de título aparecen solo cuando hay más de un panadapter presente.
- **El espectro sigue congelado después de acoplar/desacoplar** — Confirme que está en v0.9.5.1 o posterior. Las compilaciones anteriores no ejecutan el restablecimiento de recursos de GPU en los ciclos de emerger/acoplar.

## Relacionado

- [Emerge un panadapter en su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Resumen de panadapter](overview.md)
