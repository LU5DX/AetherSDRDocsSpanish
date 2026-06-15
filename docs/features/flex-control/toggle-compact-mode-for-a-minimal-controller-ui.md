# Activar modo compacto para una interfaz de control minimalista

Esta página le guía en la activación del modo compacto del diálogo AetherControl, que oculta los botones auxiliares y muestra solo la rueda virtual y el indicador de frecuencia para una apariencia simplificada.

## Antes de empezar

- Abra el diálogo AetherControl: `Settings > AetherControl…`

## Pasos

1. En el diálogo AetherControl, localice el botón de activación **Compact**.
2. Haga clic en **Compact** para activar el modo compacto. Los botones auxiliares y sus cuadros combinados de acción se ocultarán, dejando solo la rueda y el indicador de frecuencia/modo.
3. Para salir del modo compacto, haga clic en **Compact** nuevamente para restaurar la vista completa.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---------|---------------------|--------------|------------------------|
| Compact (botón de activación) | Off | — | `FlexControlCompactMode` |
| Wheel (indicador) | — | — | — |
| Physical (indicador) | — | — | — |
| External Spin (botón de activación) | Off | — | — |
| Reverse (botón de activación) | Off | — | — |
| Push (action) (cuadro combinado) | — | — | `FlexControlButtonAction_*` |
| Double-tap (action) (cuadro combinado) | — | — | — |
| Wheel Tightness (control deslizante) | 45 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo looseness) |
| Mouse Sensitivity (control deslizante) | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) |
| Aux buttons 1–5 (pulsador) | — | — | — |
| Aux single-tap combo (cuadro combinado) | — | — | — |
| Aux double-tap combo (cuadro combinado) | — | — | — |

## Acciones de rueda disponibles (para pulsaciones Push, Double-tap y botones auxiliares)

Las siguientes acciones pueden asignarse a las pulsaciones de la rueda y los toques en los botones auxiliares:

| ID de acción | Nombre mostrado |
|--------------|----------------|
| ModeCycle | Mode Cycle |
| StepZoom | Step Zoom |
| ZoomReset | Zoom Reset |
| BandUp | Band Up |
| BandDown | Band Down |
| WheelRit | RIT (Receive Incremental Tuning) |
| WheelXit | XIT (Transmit Incremental Tuning) |
| WheelVolume | Master Volume |
| **WheelSliceAudio** | **Slice Audio Volume** |
| WheelHeadphoneVolume | Headphone Volume |
| WheelAgcT | AGCT (Automatic Gain Control Threshold) |
| WheelApf | APF (Audio Peaking Filter) |

**Nota:** La acción **Slice Audio Volume** (WheelSliceAudio) es nueva en la versión v26.6.3. Ajusta el volumen de audio del slice activo de forma independiente de los volúmenes maestro y de auriculares.

## Relacionado

- [AetherControl / FlexControl overview](overview.md)
- [Configure the AetherControl / FlexControl hardware controller](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
- [Use the virtual wheel to tune the active slice](use-the-virtual-wheel-to-tune-the-active-slice.md)
