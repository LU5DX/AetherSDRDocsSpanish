# Configurar acciones de un solo toque y doble toque para el botón PULSAR

Configure lo que sucede al tocar o tocar dos veces la rueda (botón PULSAR) en el diálogo de AetherControl. Esto le permite cambiar rápidamente el paso de frecuencia, cambiar de banda, alternar funciones o ejecutar macros CWX sin necesidad de usar el ratón.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. Localice el cuadro combinado **Push (action)**. Esto define la acción de un solo toque.
2. Haga clic en el cuadro combinado y seleccione la acción deseada de la lista.
3. Localice el cuadro combinado **Double-tap (action)** justo debajo. Esto define la acción de doble toque.
4. Haga clic en el cuadro combinado y seleccione la acción deseada de la lista.
5. Cierre el diálogo. Los cambios se guardan automáticamente.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Cuadro combinado **Push (action)** | Asigna una acción a un solo toque (pulsación) de la rueda. | `FlexControlButtonAction_*` |
| Cuadro combinado **Double-tap (action)** | Asigna una acción a un doble toque de la rueda. | (almacenado junto con el de un solo toque en la misma estructura de configuración) |

Las acciones disponibles para ambos cuadros combinados incluyen:

| ID | Etiqueta |
|---|---|
| `None` | Ninguna |
| `WheelFrequency` | Sintonizar Slice |
| `BandZoom` | Zoom de Banda |
| `SegmentZoom` | Zoom de Segmento |
| `WheelRit` | RIT (Sintonización Incremental de Recepción) |
| `WheelXit` | XIT (Sintonización Incremental de Transmisión) |
| `WheelVolume` | Volumen Maestro |
| `WheelSliceAudio` | Volumen de Audio del Slice |
| `WheelHeadphoneVolume` | Volumen de Auriculares |
| `WheelAgcT` | AGCT (Umbral de Control Automático de Ganancia) |
| `WheelApf` | APF (Filtro de Pico de Audio) |
| `ClearRit` | Limpiar RIT |
| `ClearXit` | Limpiar XIT |
| `ToggleApf` | Alternar APF |
| `NextSlice` | Cambiar Slice Activo |
| `SplitActiveSlice` | Dividir Slice Activo |
| `ToggleMox` | MOX |
| `WheelPower` | Potencia RF |
| `WheelCwSpeed` | Velocidad CW |
| `CwxF1` a `CwxF12` | Macro CWX 1 a 12 |
| `StepUp` | Paso Arriba |
| `StepDown` | Paso Abajo |
| `ToggleTune` | Alternar Sintonización |
| `ToggleMute` | Alternar Silencio |
| `ToggleLock` | Alternar Bloqueo |
| `PrevSlice` | Slice Anterior |
| `ToggleAgc` | Alternar AGC |
| `VolumeUp` | Subir AF del Slice |
| `VolumeDown` | Bajar AF del Slice |

### Nuevo en v26.6.3

- **Volumen de Audio del Slice** (`WheelSliceAudio`): Ajusta el volumen de audio del slice activo independientemente del volumen maestro. Esta acción se agregó a la lista de acciones disponibles en v26.6.3.

## Consejos

- Use una acción de rueda (Sintonizar Slice, Volumen Maestro, etc.) para el toque simple y una acción de un solo uso (Paso Arriba, Zoom de Banda, etc.) para el doble toque para un comportamiento complementario.
- El tiempo de protección del doble toque es de 230 ms. Toque dos veces dentro de esa ventana para activar la acción de doble toque.
- Haga doble clic en la rueda virtual para capturar o liberar la sintonización circular usando el ratón o el trackpad. Presione Escape como una alternativa para liberar. La etiqueta de sugerencia de captura en la parte inferior del diálogo ahora dice "Haga doble clic en la perilla para capturar la sintonización circular."

## Relacionado

- [Asignar acciones de botón pulsar y doble toque a la rueda](map-push-button-and-double-tap-actions-to-the-wheel.md)
- [Configurar el controlador de hardware AetherControl / FlexControl](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
