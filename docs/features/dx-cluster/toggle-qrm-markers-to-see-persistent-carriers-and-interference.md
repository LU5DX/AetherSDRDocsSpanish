# Alternar marcadores QRM para ver portadoras persistentes e interferencia

Active los marcadores QRM para resaltar portadoras estrechas persistentes e interferencia de banda ancha en el panadapter, facilitando evitar o investigar señales que pueden ser fuentes de ruido constante.

## Pasos

1. Abra **Settings > SpotHub...**.
2. Haga clic en la pestaña **Display**.
3. En la fila **QRM (Signal History)**, haga clic en el botón de alternancia para habilitarlo (valor predeterminado: Disabled). Aparecen marcadores rojos en el panadapter para las señales clasificadas como QRM.

Para deshabilitar los marcadores QRM, vuelva a hacer clic en el botón de alternancia.

## Qué hace cada control

| Control | Clave de configuración | Valor predeterminado | Comportamiento |
|---------|------------------------|----------------------|----------------|
| **QRM (Signal History)** | `SHistoryQrmEnabled` | Disabled | Alternancia principal para los marcadores QRM rojos en el panadapter. |
| **QRM Gate** (control deslizante) | `SHistoryQrmGateS` | 6 s | Tiempo que debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM. Rango: 3–30 s. Haga doble clic en la perilla del control deslizante para restablecer el valor predeterminado de 6 s. |
| **Edge Threshold** (control deslizante) | `SHistorySoftEdgeDb` | 3.0 dB | Umbral por encima del piso de ruido para la caminata del borde de pendiente que refina el borde lateral de la portadora de S-History. Rango: 1.0–10.0 dB. Un valor más bajo = más cercano a la portadora pero más sensible al ruido. Haga doble clic en la perilla del control deslizante para restablecer el valor predeterminado de 3.0 dB. |
| **Muestra de color QRM** | `SHistoryColorQrm` | #FF0000 | Abre un selector de color para cambiar el color del marcador QRM. |

## Consejos

- Los marcadores QRM son independientes de los marcadores de voz de Signal History (la alternancia `SHistoryMarkersEnabled`). Puede habilitar uno, ambos o ninguno.
- Use el control deslizante **QRM Gate** para ignorar transmisiones breves y marcar solo señales que persistan lo suficiente como para ser interferencia.
- Haga doble clic en cualquier perilla de control deslizante en la sección Signal History para restablecerla instantáneamente a su valor predeterminado de fábrica.
- El cuadro de diálogo SpotHub ahora usa colores adaptados al tema en lugar de valores fijos. Las etiquetas de estado cambian de color según el tema activo: color de acento cuando está conectado, color de etiqueta cuando está desconectado y color de peligro en caso de error.
- Los botones de alternancia **Override Colors**, **DXCC Colors**, **Spot Lines** y **Snap to Step** ahora siempre muestran su texto predeterminado ("Enabled" o "Disabled") en lugar de cambiar el texto al alternarse. El estado de alternancia se indica mediante el estado presionado del botón y el estilo de fondo, no por el texto de la etiqueta.

## Relacionado

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm-gate-and-edge-threshold)
- [Pick custom colors for voice signal and QRM markers](pick-custom-colors-for-voice-signal-and-qrm-markers)
