# Habilitar el WebSocket del reportador de QSO FreeDV

Conecte AetherSDR al reportador de QSO de FreeDV en `qso.freedv.org` para mostrar la actividad FreeDV como spots en el panadapter.

## Antes de comenzar

- La fuente WebSocket de FreeDV solo está disponible en compilaciones con soporte WebSocket (`HAVE_WEBSOCKETS`). Si la pestaña FreeDV no aparece en SpotHub, su compilación no lo incluye.
- Los spots aparecen en el panadapter únicamente cuando la superposición maestra de spots está habilitada. Consulte [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md) si los spots no son visibles.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **FreeDV**.
3. Confirme que el indicador **Server:** muestre `qso.freedv.org (WebSocket)`. El punto de conexión es fijo y no puede editarse.
4. Haga clic en **Start**. El indicador de estado cambia a **Connected** cuando se establece el enlace WebSocket.
5. Observe la consola **FreeDV Spots** para ver la actividad entrante.
6. Para cambiar el color utilizado para los spots FreeDV en el panadapter, haga clic en **Spot Color:** y elija un color del selector.
7. Para conectarse automáticamente en cada inicio, habilite **Auto-start on startup**.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Indicador de solo lectura. Siempre muestra `qso.freedv.org (WebSocket)`. | — |
| **Start / Stop** | Conecta o desconecta el WebSocket de FreeDV. | — |
| **Auto-start on startup** | Vuelve a conectar el WebSocket de FreeDV cada vez que AetherSDR se inicia. | `FreeDvAutoStart` |
| **FreeDV Spots** | Consola de solo lectura que muestra la actividad de spots FreeDV sin procesar. | — |
| **Spot Color:** | Abre un selector de color. El color elegido se usa para los spots FreeDV en el panadapter. | `FreeDvSpotColor` |

## Solución de problemas

- **La pestaña FreeDV no aparece** — Su compilación de AetherSDR fue compilada sin soporte WebSocket. Las funciones WebSocket de FreeDV y TCI requieren una compilación con `HAVE_WEBSOCKETS`. Consulte a su proveedor del paquete o compile desde el código fuente con el soporte WebSocket habilitado.
- **El estado permanece en Disconnected después de hacer clic en Start** — Verifique que AetherSDR tenga acceso a internet de salida hacia `qso.freedv.org` en el puerto WebSocket. Un firewall o proxy puede estar bloqueando la conexión.
- **Los spots aparecen en la consola FreeDV Spots pero no en el panadapter** — Confirme que **Spots:** esté configurado en Enabled en la pestaña **Display** de SpotHub. Consulte [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md).

## Relacionado

- [Consultar activaciones POTA](poll-pota-activations.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas hacia mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
