# Activar el modo compacto para una interfaz de control minimalista

Esta página explica cómo cambiar el cuadro de diálogo AetherControl al modo compacto, que oculta los botones auxiliares y muestra solo la rueda virtual y el indicador de frecuencia para una apariencia simplificada.

## Antes de comenzar

- Abra el cuadro de diálogo AetherControl: `Settings > AetherControl…`

## Pasos

1. En el cuadro de diálogo AetherControl, localice el botón de alternancia **Compact**.
2. Haga clic en **Compact** para activar el modo compacto. Los botones auxiliares y sus cuadros combinados de acción quedarán ocultos, mostrando solo la rueda y el indicador de frecuencia/modo.
3. Para salir del modo compacto, haga clic en **Compact** nuevamente para restaurar la vista completa.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---------|---------------------|--------------|------------------------|
| Compact (botón de alternancia) | Off | — | `FlexControlCompactMode` |
| Wheel (indicador) | — | — | — |
| Physical (indicador) | — | — | — |
| External Spin (botón de alternancia) | Off | — | — |
| Reverse (botón de alternancia) | Off | — | — |
| Push (acción) (cuadro combinado) | — | — | `FlexControlButtonAction_*` |
| Double-tap (acción) (cuadro combinado) | — | — | — |
| Wheel Tightness (control deslizante) | 45 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo looseness) |
| Mouse Sensitivity (control deslizante) | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) |
| Aux buttons 1–5 (botón de pulsación) | — | — | — |
| Aux single-tap combo (cuadro combinado) | — | — | — |
| Aux double-tap combo (cuadro combinado) | — | — | — |

## Acciones de rueda disponibles (para acciones Push, Double-tap y botones auxiliares)

Las siguientes acciones pueden asignarse a las pulsaciones de la rueda y a los toques de los botones auxiliares:

| ID de acción | Nombre mostrado |
|--------------|-----------------|
| ModeCycle | Mode Cycle |
| StepZoom | Step Zoom |
| ZoomReset | Zoom Reset |
| BandUp | Band Up |
| BandDown | Band Down |
| WheelRit | RIT (Receive Incremental Tuning) |
| WheelXit | XIT (Transmit Incremental Tuning) |
| WheelVolume | Master Volume |
| WheelSliceAudio | Slice Audio Volume |
| WheelHeadphoneVolume | Headphone Volume |
| WheelAgcT | AGCT (Automatic Gain Control Threshold) |
| WheelApf | APF (Audio Peaking Filter) |

**Nota:** La acción **Slice Audio Volume** (WheelSliceAudio) ajusta el volumen de audio de la franja activa de forma independiente de los volúmenes maestro y de auriculares.

## Comportamiento del tamaño de ventana (v26.7.4)

El cuadro de diálogo AetherControl ahora utiliza un diseño desplazable. Cuando el modo compacto está desactivado, la ventana garantiza que el controlador completo esté disponible incluso en pantallas cortas o con escalado DPI. El área de contenido se desplaza verticalmente cuando su altura intrínseca supera la altura disponible de la pantalla. El ancho mínimo de la ventana sigue el ancho mínimo del contenido para evitar el recorte horizontal.

## Relacionados

- [AetherControl / FlexControl overview](overview.md)
- [Configure the AetherControl / FlexControl hardware controller](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
- [Use the virtual wheel to tune the active slice](use-the-virtual-wheel-to-tune-the-active-slice.md)
