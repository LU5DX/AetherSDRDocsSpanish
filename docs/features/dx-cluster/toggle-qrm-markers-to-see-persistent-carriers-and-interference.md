# Activar marcadores de QRM para ver portadoras persistentes e interferencias

Active los marcadores de QRM para resaltar portadoras estrechas persistentes e interferencias de banda ancha en el panadapter, lo que facilita evitar o investigar señales que pueden ser fuentes de ruido constantes.

## Pasos

1. Abra **Settings > SpotHub...**.
2. Haga clic en la pestaña **Display**.
3. En la fila **QRM (Signal History)**, haga clic en el botón de alternancia para activarlo (predeterminado: Disabled). Aparecen marcadores rojos en el panadapter para las señales clasificadas como QRM.

Para desactivar los marcadores de QRM, haga clic nuevamente en el botón de alternancia.

## Qué hace cada control

| Control | Clave de configuración | Predeterminado | Comportamiento |
|---------|------------------------|----------------|----------------|
| **QRM (Signal History)** | `SHistoryQrmEnabled` | Disabled | Alternancia maestra para los marcadores rojos de QRM en el panadapter. |
| **QRM Gate** (control deslizante) | `SHistoryQrmGateS` | 6 s | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de ser clasificada como QRM. Rango: 3–30 s. |
| **Edge Threshold** (control deslizante) | `SHistorySoftEdgeDb` | 3.0 dB | Umbral por encima del piso de ruido para el recorrido del borde de pendiente que refina el borde del lado de la portadora en S-History. Rango: 1.0–10.0 dB. Un valor más bajo = más cercano a la portadora pero más sensible al ruido. |
| **Muestra de color QRM** | `SHistoryColorQrm` | #FF0000 | Abre un selector de color para cambiar el color del marcador de QRM. |

## Consejos

- Los marcadores de QRM son independientes de los marcadores de voz de Signal History (la alternancia `SHistoryMarkersEnabled`). Puede activar uno, ambos o ninguno.
- Use el control deslizante **QRM Gate** para ignorar transmisiones breves y marcar únicamente las señales que persisten lo suficiente como para ser interferencia.

## Relacionado

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm-gate-and-edge-threshold)
- [Pick custom colors for voice signal and QRM markers](pick-custom-colors-for-voice-signal-and-qrm-markers)
