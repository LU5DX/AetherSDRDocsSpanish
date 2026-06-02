# Activar marcadores QRM para ver portadoras persistentes e interferencias

Active los marcadores QRM para resaltar portadoras estrechas persistentes e interferencias de banda ancha en el panadaptador, lo que facilita evitar o investigar señales que pueden ser fuentes de ruido constante.

## Pasos

1. Abra **Settings > SpotHub...**.
2. Haga clic en la pestaña **Display**.
3. En la fila **QRM (Signal History)**, haga clic en el botón de activación para habilitarlo (predeterminado: Disabled). Aparecen marcadores rojos en el panadaptador para las señales clasificadas como QRM.

Para deshabilitar los marcadores QRM, haga clic nuevamente en el botón de activación.

## Función de cada control

| Control | Clave de configuración | Predeterminado | Comportamiento |
|---------|------------------------|----------------|----------------|
| **QRM (Signal History)** | `SHistoryQrmEnabled` | Disabled | Activación principal para los marcadores QRM rojos en el panadaptador. |
| **QRM Gate** (control deslizante) | `SHistoryQrmGateS` | 6 s | Tiempo que una portadora estrecha o señal de banda ancha debe persistir antes de clasificarse como QRM. Rango: 3–30 s. Haga doble clic en la perilla del control deslizante para restablecer al valor predeterminado de 6 s. |
| **Edge Threshold** (control deslizante) | `SHistorySoftEdgeDb` | 3.0 dB | Umbral sobre el piso de ruido para el recorrido del borde de pendiente que refina el borde lateral de la portadora en S-History. Rango: 1.0–10.0 dB. Un valor más bajo = más cercano a la portadora pero más sensible al ruido. Haga doble clic en la perilla del control deslizante para restablecer al valor predeterminado de 3.0 dB. |
| **Muestra de color QRM** | `SHistoryColorQrm` | #FF0000 | Abre un selector de color para cambiar el color del marcador QRM. |

## Consejos

- Los marcadores QRM son independientes de los marcadores de voz de Signal History (el interruptor `SHistoryMarkersEnabled`). Puede habilitar uno, ambos o ninguno.
- Use el control deslizante **QRM Gate** para ignorar transmisiones breves y solo marcar señales que persistan lo suficiente como para ser interferencia.
- Haga doble clic en cualquier perilla de control deslizante en la sección Signal History para restablecerla instantáneamente a su valor predeterminado de fábrica.
- El cuadro de diálogo SpotHub ahora usa colores acordes al tema en lugar de valores codificados. Las etiquetas de estado cambian de color según el tema activo: color de acento cuando está conectado, color de etiqueta cuando está desconectado y color de peligro en caso de error.

## Relacionado

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm-gate-and-edge-threshold)
- [Pick custom colors for voice signal and QRM markers](pick-custom-colors-for-voice-signal-and-qrm-markers)
