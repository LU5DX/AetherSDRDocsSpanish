# Habilitar el WebSocket del reportero de QSO de FreeDV

Conecte AetherSDR al reportero de QSO de FreeDV en `qso.freedv.org` para recibir spots de actividad FreeDV en el panadapter.

## Antes de comenzar

- AetherSDR debe haberse compilado con soporte de WebSocket (`HAVE_WEBSOCKETS`). Si la pestaña FreeDV no aparece en SpotHub, su versión no incluye esta función.
- La capa de spots debe estar activa para que los spots se muestren en el panadapter. Consulte [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md) para configurar la visualización.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **FreeDV**.
3. Observe que el indicador **Server:** muestra `qso.freedv.org (WebSocket)`. El punto de conexión es fijo y no se puede modificar.
4. Haga clic en **Start**. El indicador de estado cambia a **Connected** cuando se establece el WebSocket.
5. La actividad entrante aparece en la consola **FreeDV Spots**.
6. Para cambiar el color de los spots FreeDV en el panadapter, haga clic en **Spot Color:** y elija un color en el selector. Este valor se guarda como `FreeDvSpotColor`.
7. Para conectarse automáticamente cada vez que AetherSDR se inicie, active **Auto-start on startup**. Este valor se guarda como `FreeDvAutoStart`.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Server:** | Indicador | Muestra el punto de conexión fijo `qso.freedv.org (WebSocket)`. No es editable. | — |
| **Start / Stop** | Botón | Conecta o desconecta el WebSocket de FreeDV. | — |
| **Auto-start on startup** | Botón de alternancia | Inicia el WebSocket de FreeDV automáticamente al arrancar AetherSDR. | `FreeDvAutoStart` |
| **FreeDV Spots** | Campo de texto | Consola de solo lectura con la actividad FreeDV recibida. | — |
| **Spot Color:** | Botón | Abre un selector de color para definir el color de los spots FreeDV en el panadapter. | `FreeDvSpotColor` |

## Solución de problemas

- **La pestaña FreeDV no es visible** — La pestaña solo está presente en versiones compiladas con soporte de WebSocket. Consulte con su proveedor de paquetes o revise la configuración de compilación.
- **El estado permanece en Disconnected después de hacer clic en Start** — Verifique su conexión a internet. El cliente se conecta a `qso.freedv.org` mediante WebSocket; un cortafuegos o proxy puede estar bloqueando el tráfico WebSocket saliente.
- **Los spots aparecen en la consola pero no en el panadapter** — Confirme que la capa principal de spots esté habilitada. Abra `Settings > SpotHub...`, vaya a la pestaña **Display** y verifique que **Spots:** esté configurado en **Enabled** (`IsSpotsEnabled`).

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Consultar activaciones de POTA](poll-pota-activations.md)
