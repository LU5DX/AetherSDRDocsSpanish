# Configurar acciones de toque simple y doble para el botón PUSH

Configure lo que sucede cuando toca o toca dos veces la rueda (botón PUSH) en el diálogo AetherControl. Esto le permite cambiar rápidamente el paso de frecuencia, cambiar de banda, alternar funciones o ejecutar macros CWX sin necesidad de usar el mouse.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. Localice el cuadro combinado **Push (action)**. Este define la acción de un toque simple.
2. Haga clic en el cuadro combinado y seleccione la acción deseada de la lista.
3. Localice el cuadro combinado **Double-tap (action)** directamente debajo. Este define la acción de un doble toque.
4. Haga clic en el cuadro combinado y seleccione la acción deseada de la lista.
5. Cierre el diálogo. Los cambios se guardan automáticamente.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Cuadro combinado **Push (action)** | Asigna una acción a un toque simple (pulsación) de la rueda. | `FlexControlButtonAction_*` |
| Cuadro combinado **Double-tap (action)** | Asigna una acción a un doble toque de la rueda. | (se almacena junto con el toque simple en la misma estructura de configuración) |

Las acciones disponibles para ambos cuadros combinados incluyen:

| ID | Etiqueta |
|---|---|
| `None` | None |
| `WheelFrequency` | Tune Slice |
| `BandZoom` | Band Zoom |
| `SegmentZoom` | Segment Zoom |
| `WheelRit` | RIT (Receive Incremental Tuning) |
| `WheelXit` | XIT (Transmit Incremental Tuning) |
| `WheelVolume` | Master Volume |
| `WheelHeadphoneVolume` | Headphone Volume |
| `WheelAgcT` | AGCT (Automatic Gain Control Threshold) |
| `WheelApf` | APF (Audio Peaking Filter) |
| `ClearRit` | Clear RIT |
| `ClearXit` | Clear XIT |
| `ToggleApf` | Toggle APF |
| `NextSlice` | Change Active Slice |
| `SplitActiveSlice` | Split Active Slice |
| `ToggleMox` | MOX |
| `WheelPower` | RF Power |
| `WheelCwSpeed` | CW Speed |
| `CwxF1` a `CwxF12` | CWX Macro 1 through 12 |
| `StepUp` | Step Up |
| `StepDown` | Step Down |
| `ToggleTune` | Toggle Tune |
| `ToggleMute` | Toggle Mute |
| `ToggleLock` | Toggle Lock |
| `PrevSlice` | Previous Slice |
| `ToggleAgc` | Toggle AGC |
| `VolumeUp` | Slice AF Up |
| `VolumeDown` | Slice AF Down |

## Consejos

- Use una acción de rueda (Tune Slice, Master Volume, etc.) para el toque simple y una acción de un solo disparo (Step Up, Band Zoom, etc.) para el doble toque para lograr un comportamiento complementario.
- El tiempo de guardia del doble toque es de 230 ms. Toque dos veces dentro de esa ventana para activar la acción de doble toque.

## Relacionado

- [Map push-button and double-tap actions to the wheel](map-push-button-and-double-tap-actions-to-the-wheel.md)
- [Configure the AetherControl / FlexControl hardware controller](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
