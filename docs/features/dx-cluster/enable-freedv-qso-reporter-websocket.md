# Habilitar el WebSocket de FreeDV QSO Reporter

Conecte AetherSDR al servicio de reporte de QSO de FreeDV en `qso.freedv.org` para recibir spots de actividad FreeDV en su panadapter.

## Antes de comenzar

- La función WebSocket de FreeDV solo está presente en compilaciones que incluyen soporte para WebSocket (`HAVE_WEBSOCKETS`). Si la pestaña FreeDV no aparece en SpotHub, su compilación no lo incluye.
- La visualización de spots en el panadapter requiere que la capa de superposición principal de spots esté habilitada. Consulte [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md) para ver las opciones de visualización.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **FreeDV**.
3. Confirme que el indicador **Server:** muestre `qso.freedv.org (WebSocket)`. Este punto de conexión es fijo y no puede modificarse.
4. Haga clic en **Start**. El indicador de estado cambia a **Connected** cuando se establece la conexión WebSocket.
5. Observe la consola **FreeDV Spots** para ver la actividad entrante.
6. Para cambiar el color usado para los spots de FreeDV en el panadapter, haga clic en **Spot Color:** y elija un color del selector.
7. Para conectarse automáticamente cada vez que AetherSDR se inicia, haga clic en **Auto-start on startup** para activarlo.

## Qué hace cada control

| Control | Descripción | Ajuste persistente |
|---|---|---|
| **Server:** | Indicador de solo lectura que muestra el punto de conexión fijo `qso.freedv.org (WebSocket)`. | — |
| **Start / Stop** | Conecta o desconecta el WebSocket de FreeDV. | — |
| **Auto-start on startup** | Cuando está activo, el WebSocket se conecta automáticamente al iniciar. | `FreeDvAutoStart` |
| **FreeDV Spots** | Consola de solo lectura que muestra la actividad de spots FreeDV sin procesar. | — |
| **Spot Color:** | Abre un selector de color. El color elegido se aplica a los spots de FreeDV en el panadapter. | `FreeDvSpotColor` |

## Solución de problemas

- **La pestaña FreeDV no es visible** — Su compilación de AetherSDR fue generada sin soporte para WebSocket. La pestaña solo está presente en compilaciones con `HAVE_WEBSOCKETS`. Consulte con la fuente de su paquete o recompile con el soporte para WebSocket habilitado.
- **El estado permanece como Disconnected después de hacer clic en Start** — Confirme que su sistema tiene acceso a internet de salida hacia `qso.freedv.org`. Revise las reglas del firewall local que puedan bloquear conexiones WebSocket (normalmente por el puerto 443 o 80).

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Consultar activaciones POTA](poll-pota-activations.md)
