# Ajustar la duración de los marcadores de S-History, puerta de QRM y umbral de borde

Ajuste finamente cómo se comportan los marcadores de Signal History en el panadapter: cuánto tiempo permanecen, cuán persistentemente debe mantenerse una señal para ser marcada como QRM, y con qué agresividad el borde del marcador se ajusta a la portadora.

## Antes de comenzar

- Abra SpotHub: `Settings > SpotHub...`
- Haga clic en la pestaña **Display**.

## Pasos

1. En **Signal History**, ajuste **Marker Lifetime:** arrastrando el control deslizante. Los marcadores inactivos se eliminan después de esta cantidad de segundos (rango 15–300 seg, predeterminado 60). Haga doble clic izquierdo en el control deslizante para restablecerlo a 60.

2. Ajuste **QRM Gate:** — los segundos que una portadora estrecha o una señal de banda ancha debe persistir antes de que el sistema la clasifique como QRM (rango 3–30 seg, predeterminado 6). Haga doble clic izquierdo en el control deslizante para restablecerlo a 6.

3. Ajuste **Edge Threshold:** — el nivel en dB por encima del piso de ruido para la caminata de borde de pendiente que refina el borde del lado de la portadora de un marcador. Un valor más bajo se ajusta más estrechamente a la portadora, pero es más sensible al ruido (rango 1.0–10.0 dB, predeterminado 3.0). Haga doble clic izquierdo en el control deslizante para restablecerlo a 3.0.

4. Opcionalmente, active **Snap to Step:** en la sección Signal History para redondear el clic para sintonizar al tamaño de paso de la slice activa más cercano.

## Función de cada control

| Control | Etiqueta en el deslizador | Predeterminado | Rango válido | Clave de configuración | Notas |
|---|---|---|---|---|---|
| **Marker Lifetime:** | `15 sec` – `300 sec` | 60 | 15–300 seg | `SHistoryLifetimeS` | Doble clic izquierdo restablece a 60 |
| **QRM Gate:** | `3 sec` – `30 sec` | 6 | 3–30 seg | `SHistoryQrmGateS` | Doble clic izquierdo restablece a 6 |
| **Edge Threshold:** | `1.0 dB` – `10.0 dB` | 3.0 | 1.0–10.0 dB | `SHistorySoftEdgeDb` | Doble clic izquierdo restablece a 3.0 |
| **Snap to Step:** | botón de alternancia | Deshabilitado | Habilitado / Deshabilitado | `SHistorySnapToStep` | |

## Consejos

- **Marker Lifetime** controla los marcadores de señales de ancho de banda de voz (dorados por predeterminado). Los marcadores de QRM (rojos por predeterminado) también siguen esta duración; no tienen un temporizador separado.
- Para ver los marcadores de Signal History en el panadapter en primer lugar, active **Signals** y/o **QRM** bajo la fila de alternancia superior en la pestaña Display. Sus claves persistidas son `SHistoryMarkersEnabled` y `SHistoryQrmEnabled`.
- Activar **Snap to Step** oculta el pequeño desplazamiento de portadora que puede aparecer al hacer clic en un marcador de S-History; la frecuencia de sintonización se ajusta al siguiente múltiplo del tamaño de paso de la slice activa.
- Hacer doble clic izquierdo en cualquier control deslizante lo restablece a su valor predeterminado, proporcionando una forma rápida de restaurar el comportamiento de fábrica sin arrastrar.

## Solución de problemas

- **Los marcadores desaparecen demasiado rápido** — Aumente **Marker Lifetime:** a un valor más alto. Haga doble clic izquierdo en el control deslizante para restablecerlo al predeterminado de 60 segundos.
- **Aparecen marcadores de QRM en señales débiles que no son realmente interferencia** — Aumente **QRM Gate:** para que el sistema requiera un tiempo de retención más largo antes de clasificar la señal como QRM. Haga doble clic izquierdo en el control deslizante para restablecerlo al predeterminado de 6 segundos.
- **Los bordes de los marcadores oscilan o saltan** — Aumente ligeramente **Edge Threshold:** (por ejemplo, de 3.0 a 4.0 dB) para reducir la sensibilidad al ruido. Haga doble clic izquierdo en el control deslizante para restablecerlo al predeterminado de 3.0 dB.

## Relacionados

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Toggle QRM markers to see persistent carriers and interference](toggle-qrm-markers-to-see-persistent-carriers-and-interference.md)
- [Pick custom colors for voice signal and QRM markers](pick-custom-colors-for-voice-signal-and-qrm-markers.md)
- [Enable Snap to Step for precise S-History tuning](enable-snap-to-step-for-precise-s-history-tuning.md)
- [Add startup commands for DX cluster connection](add-startup-commands-for-dx-cluster-connection.md)
