# Ver la salida del registro en vivo filtrada por categoría de diagnóstico

La pestaña **Logs** en Network Diagnostics muestra una vista en vivo del archivo de registro de AetherSDR, filtrada a las categorías de diagnóstico que usted elija. Utilice esta función cuando necesite observar mensajes de un subsistema específico en tiempo real sin tener que revisar salida no relacionada.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para ver el registro.
- Identifique qué categoría de diagnóstico desea observar (por ejemplo, `aether.connection`, `aether.cw`, `aether.dxcluster`).

## Pasos

1. Haga clic en `Settings > Network...` para abrir el cuadro de diálogo Network Diagnostics.
2. Haga clic en la pestaña **Logs**.
3. Revise la ruta del registro que se muestra en la etiqueta **Log path label** en la parte superior de la pestaña para confirmar qué archivo está siendo seguido.
4. Marque o desmarque las casillas de verificación por categoría en **Filter Categories** para mostrar solo las categorías que desee. De forma predeterminada, la categoría **General** está disponible; todas las categorías de diagnóstico registradas aparecen junto a ella.
5. Para mostrar todas las categorías a la vez, haga clic en **Select All**. Para ocultar todas las categorías, haga clic en **Deselect All** y luego marque únicamente las categorías específicas que necesite.
6. Observe el visor. Las nuevas entradas se desplazan automáticamente mientras el botón muestra **Live**.
7. Cuando termine, haga clic en **Close**.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| **Logs** (pestaña) | Vista en vivo del archivo de registro de AetherSDR filtrada por las casillas de categoría. Resaltado de sintaxis según nivel de registro y nombre de categoría. El selector **Timeframe** se oculta mientras esta pestaña está activa. | — |
| **Filter Categories** | Casillas de verificación por categoría. Marque una categoría para incluir sus líneas; desmárquela para ocultarlas. Incluye **General** más todas las categorías de LogManager registradas. | — |
| **Select All** | Muestra todas las categorías de registro en el visor de inmediato. | — |
| **Deselect All** | Oculta todas las categorías de registro del visor de inmediato. | — |
| **Live / Paused** | Cuando está en **Live**, el visor se desplaza automáticamente hasta la salida más reciente. Desplazarse hacia arriba cambia el estado a **Paused**. Hacer clic en el botón cuando muestra **Paused** reanuda el desplazamiento automático y salta al final del registro. | Live |
| **Log path label** | Muestra la ruta completa del sistema de archivos del archivo de registro que está siendo seguido. | — |

## Consejos

- La vista del registro se actualiza cada 500 ms, por lo que existe un breve retraso entre que un mensaje es escrito y el momento en que aparece en el visor.
- Los colores del resaltado de sintaxis ayudan a distinguir los niveles de registro de un vistazo: las líneas `INF` aparecen en azul, `WRN` en ámbar y `CRT`/`FTL` en rojo. Los nombres de categoría se muestran en negrita. Los números y los tokens de protocolo (como `UDP`, `TCP`, `RX`, `TX`) se resaltan de forma separada.
- Si desea congelar la pantalla para leer una entrada específica, desplácese hacia arriba. El visor cambia a **Paused** automáticamente. Haga clic en **Live** para volver al final del registro.
- Hacer clic en **Deselect All** y luego marcar una sola categoría es la forma más rápida de aislar la salida de un subsistema.

## Relacionado

- [Pausar el desplazamiento del registro para inspeccionar una entrada anterior](pause-log-scrolling-to-inspect-an-older-entry.md)
- [Descripción general de Network Diagnostics](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
