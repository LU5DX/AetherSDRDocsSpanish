# Solucionar un espectro estático o congelado en un panadapter flotante en macOS

En macOS, al extraer un panadapter (visualizador de espectro panorámico) a una ventana flotante, el espectro puede quedar congelado: el FFT y el waterfall dejan de actualizarse aunque la radio siga conectada. Este es un problema conocido de la superficie Metal/GPU que AetherSDR resuelve automáticamente a partir de la v0.9.5.1.

## Antes de comenzar

- AetherSDR v0.9.5.1 o posterior está instalado. Las versiones anteriores no incluyen la corrección.
- Está ejecutando macOS con un FLEX-8600 conectado.
- Tiene más de un panadapter abierto (el botón ⬈ / ↩ para extraer está oculto en el modo de un solo panadapter).

## Pasos

1. En la barra de título del panadapter, haga clic en ↩ para acoplar el panadapter flotante de regreso a la ventana principal.
2. Haga clic en ⬈ para extraerlo nuevamente.

AetherSDR restablece los recursos de la GPU y vuelve a enlazar la superficie de renderizado Metal a la nueva ventana durante cada ciclo de extracción/acoplamiento. Después del paso 2, el espectro debería estar activo.

## Consejos

- Si el espectro sigue estático después de un ciclo de acoplamiento/extracción, repita el ciclo una vez más. Un estado de desconexión WAN obsoleto puede requerir ocasionalmente un segundo restablecimiento.
- Cerrar y reiniciar AetherSDR también elimina la condición. La aplicación libera los recursos de la GPU durante el cierre específicamente para evitar un fallo de desmontaje de Metal en este escenario.

## Solución de problemas

- **El botón ⬈ de extracción no es visible** — Está en el modo de un solo panadapter. Agregue un segundo panadapter para habilitar el modo multipantalla; los botones de la barra de título solo aparecen cuando hay más de un panadapter presente.
- **El espectro sigue congelado después de acoplar/desacoplar** — Confirme que está usando la v0.9.5.1 o posterior. Las versiones anteriores no ejecutan el restablecimiento de recursos de la GPU en los ciclos de extracción/acoplamiento.

## Relacionados

- [Extraer un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Descripción general del panadapter](overview.md)
