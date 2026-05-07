# Ver la salida del registro en vivo filtrada por categoría de diagnóstico

La pestaña Registros en Diagnóstico de Red muestra una cola en vivo del archivo de registro de AetherSDR, filtrada únicamente por las categorías de diagnóstico que usted elija. Utilícela cuando necesite supervisar mensajes de subsistemas específicos en tiempo real sin tener que revisar información no relevante.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para ver el registro.
- Sepa qué categoría de diagnóstico desea supervisar (por ejemplo, `aether.connection`, `aether.cw`, `aether.dxcluster`).

## Pasos

1. Haga clic en `Settings > Network...` para abrir el cuadro de diálogo Diagnóstico de Red.
2. Haga clic en la pestaña **Logs**.
3. Revise la ruta del registro que se muestra en la **etiqueta de ruta del registro** en la parte superior de la pestaña para confirmar qué archivo se está siguiendo.
4. Marque o desmarque las casillas por categoría en **Filter Categories** para mostrar únicamente las categorías que desee. De forma predeterminada, la categoría **General** está disponible; todas las categorías de diagnóstico registradas aparecen junto a ella.
5. Para mostrar todas las categorías a la vez, haga clic en **Select All**. Para ocultar todas las categorías, haga clic en **Deselect All** y luego marque solo las categorías específicas que necesite.
6. Observe el visor. Las nuevas entradas se desplazan automáticamente mientras el interruptor muestre **Live**.
7. Cuando termine, haga clic en **Close**.

## Qué hace cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| **Logs** (pestaña) | Cola en vivo del archivo de registro de AetherSDR filtrada por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector de **Timeframe** está oculto mientras esta pestaña esté activa. | — |
| **Filter Categories** | Casillas de verificación por categoría. Marque una categoría para incluir sus líneas; desmárquela para ocultarlas. Incluye **General** más todas las categorías de LogManager registradas. | — |
| **Select All** | Muestra todas las categorías de registro en el visor de inmediato. | — |
| **Deselect All** | Oculta todas las categorías de registro del visor de inmediato. | — |
| **Live / Paused** | Cuando está en **Live**, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba cambia el estado a **Paused**. Al hacer clic en el interruptor cuando muestra **Paused** se reanuda el desplazamiento automático y salta al final. | Live |
| **Etiqueta de ruta del registro** | Muestra la ruta completa del sistema de archivos del archivo de registro que se está siguiendo. | — |

## Consejos

- La vista del registro se actualiza cada 500 ms, por lo que hay un breve retardo entre que se escribe un mensaje y su aparición en el visor.
- Los colores del resaltado de sintaxis ayudan a distinguir los niveles de registro de un vistazo: las líneas `INF` aparecen en azul, `WRN` en ámbar y `CRT`/`FTL` en rojo. Los nombres de las categorías se muestran en negrita. Los números y los tokens de protocolo (como `UDP`, `TCP`, `RX`, `TX`) se resaltan por separado.
- Si desea congelar la pantalla para leer una entrada específica, desplácese hacia arriba. El visor cambia a **Paused** automáticamente. Haga clic en **Live** para volver al final.
- Hacer clic en **Deselect All** y luego marcar una sola categoría es la forma más rápida de aislar la salida de un subsistema.

## Relacionados

- [Pausar el desplazamiento del registro para inspeccionar una entrada anterior](pause-log-scrolling-to-inspect-an-older-entry.md)
- [Descripción general de Diagnóstico de Red](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
