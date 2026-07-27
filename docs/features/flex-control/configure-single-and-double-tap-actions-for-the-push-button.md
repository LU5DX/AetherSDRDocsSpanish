# Configurar acciones de pulsación simple y doble para el botón PUSH

Configure qué sucede al pulsar o hacer doble clic en la rueda (botón PUSH) en el diálogo AetherControl. Esto le permite cambiar rápidamente el paso de frecuencia, cambiar de banda, alternar funciones o ejecutar macros CWX sin necesidad de usar el ratón.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. Localice el cuadro combinado **Push (action)**. Esto define la acción de pulsación simple.
2. Haga clic en el cuadro combinado y seleccione la acción deseada de la lista.
3. Localice el cuadro combinado **Double-tap (action)** justo debajo. Esto define la acción de doble pulsación.
4. Haga clic en el cuadro combinado y seleccione la acción deseada de la lista.
5. Cierre el diálogo. Los cambios se guardan automáticamente.

## Función de cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Cuadro combinado **Push (action)** | Asigna una acción a una pulsación simple de la rueda. | `FlexControlButtonAction_*` |
| Cuadro combinado **Double-tap (action)** | Asigna una acción a una doble pulsación de la rueda. | (almacenado junto con la pulsación simple en la misma estructura de configuración) |

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
| `WheelSliceAudio` | Slice Audio Volume |
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
| `CwxF1` hasta `CwxF12` | CWX Macro 1 al 12 |
| `StepUp` | Step Up |
| `StepDown` | Step Down |
| `ToggleTune` | Toggle Tune |
| `ToggleMute` | Toggle Mute |
| `ToggleLock` | Toggle Lock |
| `PrevSlice` | Previous Slice |
| `ToggleAgc` | Toggle AGC |
| `VolumeUp` | Slice AF Up |
| `VolumeDown` | Slice AF Down |

### Nuevo en v26.6.3

- **Slice Audio Volume** (`WheelSliceAudio`): Ajusta el volumen de audio del slice activo de forma independiente al volumen maestro. Esta acción se agregó a la lista de acciones disponibles en v26.6.3.

## Consejos

- Utilice una acción de rueda (Tune Slice, Master Volume, etc.) para pulsación simple y una acción instantánea (Step Up, Band Zoom, etc.) para doble pulsación para un comportamiento complementario.
- El tiempo de guardia de doble pulsación es de 230 ms. Pulse dos veces dentro de esa ventana para activar la acción de doble pulsación.
- Haga doble clic en la rueda virtual para capturar o liberar la sintonía circular usando el ratón o el trackpad. Presione Escape como liberación alternativa. La etiqueta de sugerencia de captura en la parte inferior del diálogo ahora muestra "Double-click the knob to capture circular tuning."

## Relacionado

- [Configure single- and double-tap actions for the PUSH button](configure-single--and-double-tap-actions-for-the-push-button.md)
- [Configure the AetherControl / FlexControl hardware controller](configure-the-aethercontrol-flexcontrol-hardware-controller.md)

---

# Configurar el controlador de hardware AetherControl / FlexControl

Configure el controlador rotatorio virtual o físico FlexControl en AetherSDR. El diálogo AetherControl proporciona una rueda de sintonía virtual con sintonía circular mediante ratón/táctil, mapeo de acciones del botón PUSH, cinco botones auxiliares con acciones de pulsación simple y doble, modo compacto y animación de giro externo en cambios de frecuencia.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`
- Conecte un dispositivo FlexControl físico mediante USB (opcional). Cuando esté conectado, el diálogo mostrará el nombre del puerto y el estado de la conexión.

## Configurar la rueda virtual

1. **Wheel**: Gire la rueda virtual con el ratón o táctil para sintonizar el slice activo. La frecuencia y el modo aparecen en la cara de la rueda.
2. **Tightness**: Ajuste el control deslizante **Wheel Tightness** (0–100). 0 = tenso (parada rápida), 100 = suelto (desplazamiento largo). Esto afecta solo a la rueda virtual, no a un FlexControl físico.
3. **Mouse Sensitivity**: Ajuste el control deslizante **Mouse Sensitivity** (0–100). El punto medio (50) produce una escala de 1.0x. Los valores más altos hacen que movimientos pequeños del puntero giren más la rueda. Afecta solo a la rueda virtual.
4. **Reverse**: Haga clic en **Reverse** para invertir la dirección de sintonía de la rueda.

## Configurar acciones del botón PUSH

1. **Push (action)**: Seleccione una acción del cuadro combinado para la pulsación simple de la rueda.
2. **Double-tap (action)**: Seleccione una acción del cuadro combinado para la doble pulsación de la rueda.

Consulte [Configure single- and double-tap actions for the PUSH button](configure-single--and-double-tap-actions-for-the-push-button.md) para obtener la lista completa de acciones disponibles.

## Configurar botones auxiliares

1. Haga clic en un **Aux button** (1–5) para seleccionarlo. El botón muestra un indicador de punto cuando está seleccionado.
2. Para el botón auxiliar seleccionado, configure:
   - **Aux single-tap combo**: Asigna una acción a la pulsación simple del botón auxiliar seleccionado.
   - **Aux double-tap combo**: Asigna una acción a la doble pulsación del botón auxiliar seleccionado.
3. Repita para cada botón auxiliar según sea necesario.

## Gestionar el dispositivo físico

1. El indicador **Physical** muestra el estado de la conexión y el nombre del puerto de un dispositivo FlexControl físico.
2. Haga clic en **Detect** para buscar un FlexControl físico conectado.
3. Haga clic en **Close** para desconectar el dispositivo físico.

## Modo compacto

1. Haga clic en **Compact** para alternar el modo compacto. Cuando está habilitado, los botones auxiliares se ocultan y solo permanecen visibles la rueda y la visualización de frecuencia.
2. El diálogo se redimensiona automáticamente para ajustarse al contenido. En pantallas cortas o con escala DPI, aparece una barra de desplazamiento para mantener accesible el controlador completo.
3. Haga clic en **Compact** nuevamente para volver a la vista completa.

## Giro externo

1. Haga clic en **External Spin** para habilitar la sintonía de rueda con giro externo. Cuando está habilitado, arrastrar sobre el panadapter activa gestos de sintonía de rueda giratoria.

## Función de cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Indicador **Wheel** | Rueda de sintonía virtual con indicación de frecuencia/modo. Gírela con el ratón o táctil. | None |
| Indicador **Physical** | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Los botones Detect/Close gestionan el dispositivo. | None |
| Alternador **Compact** | Alterna el modo compacto: oculta los botones auxiliares, muestra solo la rueda y la frecuencia. | None |
| Alternador **External Spin** | Habilita la sintonía de rueda con giro externo desde arrastres en el panadapter. | None |
| Alternador **Reverse** | Invierte la dirección de sintonía de la rueda. | None |
| Combinado **Push (action)** | Asigna acción a la pulsación simple de la rueda. | `FlexControlButtonAction_*` |
| Combinado **Double-tap (action)** | Asigna acción a la doble pulsación de la rueda. | (almacenado junto con la pulsación simple) |
| Control deslizante **Wheel Tightness** | Ajusta el arrastre de desplazamiento de la rueda virtual (0–100). 0 = tenso, 100 = suelto. | `FlexControlVirtualWheel` (JSON anidado, campo looseness) |
| Control deslizante **Mouse Sensitivity** | Ajusta la escala de movimiento del puntero a la rueda (0–100). 50 = 1.0x. | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) |
| **Aux buttons** (1–5) | Cinco botones auxiliares configurables con indicador de punto para la selección activa. | None |
| Combinado **Aux single-tap combo** | Asigna acción a la pulsación simple del botón auxiliar seleccionado. | None |
| Combinado **Aux double-tap combo** | Asigna acción a la doble pulsación del botón auxiliar seleccionado. | None |

## Indicadores

| Indicador | Significado |
|---|---|
| Indicación Slice / Frecuencia / Modo | Muestra qué slice está vinculado, su frecuencia actual y modo. |

## Consejos

- La rueda virtual admite sintonía circular con ratón/táctil: haga doble clic en la rueda para capturarla, luego gire su dedo o ratón en un movimiento circular. Presione Escape para liberar.
- **Wheel Tightness** y **Mouse Sensitivity** afectan principalmente a los trackpads y no afectan a un dispositivo FlexControl físico.
- En modo compacto, el diálogo se redimensiona a un tamaño mínimo. Si el contenido supera la altura disponible de la pantalla, el diálogo se desplaza verticalmente.
- Los cambios se guardan automáticamente al cerrar el diálogo.

## Relacionado

- [Configure single- and double-tap actions for the PUSH button](configure-single--and-double-tap-actions-for-the-push-button.md)
