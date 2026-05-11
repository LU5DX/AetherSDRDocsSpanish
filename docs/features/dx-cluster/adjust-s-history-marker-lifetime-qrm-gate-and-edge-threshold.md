# Ajustar la duración de los marcadores de S-History, la puerta QRM y el umbral de borde

Ajuste con precisión cómo se comportan los marcadores de Historial de Señales en el panadapter — cuánto tiempo permanecen, cuán persistentemente debe mantenerse una señal para ser marcada como QRM, y cuán agresivamente el borde del marcador se ajusta a la portadora.

## Antes de comenzar

- Abra SpotHub: `Settings > SpotHub...`
- Haga clic en la pestaña **Display**.

## Pasos

1. En **Signal History**, ajuste **Marker Lifetime:** arrastrando el control deslizante. Los marcadores inactivos se eliminan después de esta cantidad de segundos (rango 15–300 seg, valor predeterminado 60).

2. Ajuste **QRM Gate:** — los segundos que una portadora estrecha o señal de banda ancha debe persistir antes de que el sistema la clasifique como QRM (rango 3–30 seg, valor predeterminado 6).

3. Ajuste **Edge Threshold:** — el nivel en dB por encima del piso de ruido para el recorrido del borde de la pendiente que refina el borde del lado de la portadora del marcador. Un valor más bajo se adhiere más firmemente a la portadora pero es más sensible al ruido (rango 1.0–10.0 dB, valor predeterminado 3.0 dB).

4. Opcionalmente, habilite **Snap to Step:** en la sección Signal History para redondear el clic para sintonizar al tamaño de paso más cercano del segmento activo.

## Qué hace cada control

| Control | Etiqueta en el control deslizante | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Marker Lifetime:** | `15 sec` – `300 sec` | 60 | 15–300 seg | `SHistoryLifetimeS` |
| **QRM Gate:** | `3 sec` – `30 sec` | 6 | 3–30 seg | `SHistoryQrmGateS` |
| **Edge Threshold:** | `1.0 dB` – `10.0 dB` | 3.0 | 1.0–10.0 dB | `SHistorySoftEdgeDb` |
| **Snap to Step:** | botón de alternancia | Deshabilitado | Habilitado / Deshabilitado | `SHistorySnapToStep` |

## Consejos

- **Marker Lifetime** controla los marcadores de señales de ancho de banda de voz (dorados por defecto). Los marcadores QRM (rojos por defecto) también siguen esta duración — no tienen un temporizador independiente.
- Para ver los marcadores de Signal History en el panadapter, habilite **Signals** y/o **QRM** bajo la fila superior de alternancia en la pestaña Display. Sus claves guardadas son `SHistoryMarkersEnabled` y `SHistoryQrmEnabled`.
- Activar **Snap to Step** oculta el pequeño desplazamiento de portadora que puede aparecer al hacer clic en un marcador de S-History; la frecuencia de sintonización se ajusta al siguiente múltiplo del tamaño de paso del segmento activo.

## Solución de problemas

- **Los marcadores desaparecen demasiado rápido** — Aumente **Marker Lifetime:** a un valor más alto.
- **Aparecen marcadores QRM en señales débiles que realmente no son interferencia** — Eleve **QRM Gate:** para que el sistema requiera un tiempo de retención más largo antes de clasificar la señal como QRM.
- **Los bordes de los marcadores oscilan o saltan** — Aumente **Edge Threshold:** ligeramente (p. ej., de 3.0 a 4.0 dB) para reducir la sensibilidad al ruido.

## Relacionado

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Toggle QRM markers to see persistent carriers and interference](toggle-qrm-markers-to-see-persistent-carriers-and-interference.md)
- [Pick custom colors for voice signal and QRM markers](pick-custom-colors-for-voice-signal-and-qrm-markers.md)
- [Enable Snap to Step for precise S-History tuning](enable-snap-to-step-for-precise-s-history-tuning.md)
