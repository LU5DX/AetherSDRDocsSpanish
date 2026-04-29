# Habilitar el WebSocket del reportador de QSO de FreeDV

Conecte AetherSDR al reportador de QSO de FreeDV en `qso.freedv.org` para recibir spots de actividad FreeDV en su panadapter.

## Antes de comenzar

- La fuente WebSocket de FreeDV solo está disponible en versiones de AetherSDR compiladas con soporte para WebSocket (`HAVE_WEBSOCKETS`). Si la pestaña FreeDV no aparece en SpotHub, su versión no lo incluye.
- Los spots aparecen en el panadapter únicamente cuando la superposición maestra de spots está habilitada. Consulte [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md) si los spots no son visibles después de conectarse.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **FreeDV**.
3. Confirme que el indicador **Server:** muestra `qso.freedv.org (WebSocket)`. Este extremo es fijo y no puede modificarse.
4. Haga clic en **Start**. El indicador de estado cambia a **Connected** cuando el protocolo de enlace WebSocket se completa correctamente.
5. Opcionalmente, haga clic en **Auto-start on startup** para que la conexión se establezca de forma automática cada vez que AetherSDR se inicie.
6. Opcionalmente, haga clic en **Spot Color:** para abrir el selector de color y asignar un color distintivo a los spots de FreeDV en el panadapter. El color elegido se guarda en `FreeDvSpotColor`.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Server:** | Indicador | Extremo fijo: `qso.freedv.org (WebSocket)`. Solo lectura. | — |
| **Start / Stop** | Botón | Conecta o desconecta el WebSocket de FreeDV. | — |
| **Auto-start on startup** | Botón de alternancia | Inicia la conexión FreeDV automáticamente al lanzar la aplicación. | `FreeDvAutoStart` |
| **FreeDV Spots** | Campo de texto | Consola de solo lectura que muestra la actividad FreeDV entrante. | — |
| **Spot Color:** | Botón | Abre un selector de color para los spots de FreeDV en el panadapter. | `FreeDvSpotColor` |

## Consejos

- La actividad entrante aparece en la consola **FreeDV Spots**, así como en la tabla unificada de spots de la pestaña **Spot List**.
- Si desea que los spots de FreeDV se distingan de los spots del clúster DX o RBN, establezca un color único mediante **Spot Color:** antes de conectarse.

## Solución de problemas

- **La pestaña FreeDV no aparece** — Su versión de AetherSDR fue compilada sin soporte para WebSocket. La pestaña se oculta en tiempo de compilación y no puede habilitarse en tiempo de ejecución.
- **El estado permanece como Disconnected después de hacer clic en Start** — Verifique su conexión a internet. El extremo fijo `qso.freedv.org` debe ser accesible desde su equipo en el puerto WebSocket. Los cortafuegos o configuraciones de proxy pueden bloquear la conexión.
- **Los spots aparecen en la consola pero no en el panadapter** — Verifique que **Spots:** esté configurado como **Enabled** en la pestaña **Display** de SpotHub.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
