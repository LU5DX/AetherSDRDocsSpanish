# Configurar el controlador de hardware AetherControl / FlexControl

Configure el controlador rotatorio FlexControl virtual o físico en AetherSDR. El diálogo AetherControl proporciona una rueda de sintonización virtual con sintonización circular mediante mouse/táctil, mapeo de acciones de botón pulsador, cinco botones auxiliares con acciones de toque simple y doble toque, modo compacto, animación de giro externa en cambios de frecuencia y reconexión automática para el dispositivo físico.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`
- Conecte un dispositivo FlexControl físico mediante USB (opcional). Cuando está conectado, el diálogo muestra el nombre del puerto y el estado de la conexión.

## Configurar la rueda virtual

1. **Wheel**: Gire la rueda virtual con el mouse o táctil para sintonizar el slice activo. La frecuencia y el modo aparecen en la cara de la rueda.
2. **Tightness**: Ajuste el control deslizante **Wheel Tightness** (0–100). 0 = firme (parada rápida), 100 = suelto (deslizamiento largo). Esto afecta solo a la rueda virtual, no a un FlexControl físico.
3. **Mouse Sensitivity**: Ajuste el control deslizante **Mouse Sensitivity** (0–100). El punto medio (50) produce una escala de 1.0x. Los valores más altos hacen que movimientos pequeños del puntero giren más la rueda. Afecta solo a la rueda virtual.
4. **Reverse**: Haga clic en **Reverse** para invertir la dirección de sintonización de la rueda.

## Configurar acciones del botón pulsador

1. **Push (action)**: Seleccione una acción del cuadro combinado para el toque simple de la rueda.
2. **Double-tap (action)**: Seleccione una acción del cuadro combinado para el doble toque de la rueda.

Consulte Configurar acciones de toque simple y doble toque para el botón PUSH para ver la lista completa de acciones disponibles.

## Configurar botones auxiliares

1. Haga clic en un **Aux button** (1–5) para seleccionarlo. El botón muestra un indicador de punto cuando está seleccionado.
2. Para el botón auxiliar seleccionado, configure:
   - **Aux single-tap combo**: Asigna una acción al toque simple del botón auxiliar seleccionado.
   - **Aux double-tap combo**: Asigna una acción al doble toque del botón auxiliar seleccionado.
3. Repita para cada botón auxiliar según sea necesario.

## Gestionar el dispositivo físico

1. El indicador **Physical** muestra el estado de la conexión y el nombre del puerto de un dispositivo FlexControl físico.
2. Haga clic en **Detect** para buscar un FlexControl físico conectado.
3. Haga clic en **Close** para desconectar el dispositivo físico.

### Reconexión automática

El dispositivo FlexControl físico ahora se reconecta automáticamente cuando la conexión USB se pierde y se restablece:

- Cuando el dispositivo se desconecta (cable USB extraído, dispositivo desenchufado o error de puerto), AetherSDR reintenta la conexión cada 2 segundos.
- Si el dispositivo sigue ausente, el intervalo de reintento aumenta de forma progresiva, duplicándose en cada intento hasta un máximo de 30 segundos.
- En cada reintento, AetherSDR vuelve a detectar el puerto en lugar de reutilizar el nombre anterior, de modo que una reenumeración USB que asigne un nuevo puerto COM aún se reconecte correctamente.
- Cuando el dispositivo regresa, la conexión se restablece automáticamente; no se necesita ninguna acción manual.
- Si cierra la conexión manualmente con **Close**, los reintentos se detienen.

## Modo compacto

1. Haga clic en **Compact** para alternar el modo compacto. Cuando está habilitado, los botones auxiliares se ocultan y solo permanecen visibles la rueda y la pantalla de frecuencia.
2. El diálogo se redimensiona automáticamente para ajustarse al contenido. En pantallas cortas o con escala DPI, aparece una barra de desplazamiento para mantener accesible el controlador completo.
3. Haga clic en **Compact** nuevamente para volver a la vista completa.

## Giro externo

1. Haga clic en **External Spin** para habilitar la sintonización de rueda con giro externo. Cuando está habilitado, arrastrar sobre el panadapter activa gestos de sintonización con rueda giratoria.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Indicador **Wheel** | Rueda de sintonización virtual con lectura de frecuencia/modo. Gire con mouse o táctil. | Ninguna |
| Indicador **Physical** | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Los botones Detect/Close gestionan el dispositivo. | Ninguna |
| Alternador **Compact** | Alterna el modo compacto: oculta los botones auxiliares, muestra solo la rueda y la frecuencia. | Ninguna |
| Alternador **External Spin** | Habilita la sintonización de rueda con giro externo desde arrastres en el panadapter. | Ninguna |
| Alternador **Reverse** | Invierte la dirección de sintonización de la rueda. | Ninguna |
| Cuadro combinado **Push (action)** | Asigna una acción al toque simple de la rueda. | `FlexControlButtonAction_*` |
| Cuadro combinado **Double-tap (action)** | Asigna una acción al doble toque de la rueda. | (almacenado junto con el toque simple) |
| Control deslizante **Wheel Tightness** | Ajusta el arrastre de deslizamiento de la rueda virtual (0–100). 0 = firme, 100 = suelto. | `FlexControlVirtualWheel` (JSON anidado, campo de soltura) |
| Control deslizante **Mouse Sensitivity** | Ajusta la escala de movimiento puntero-a-rueda (0–100). 50 = 1.0x. | `FlexControlVirtualWheel` (JSON anidado, campo de sensibilidad) |
| **Aux buttons** (1–5) | Cinco botones auxiliares configurables con indicador de punto para la selección activa. | Ninguna |
| **Aux single-tap combo** | Asigna una acción al toque simple del botón auxiliar seleccionado. | Ninguna |
| **Aux double-tap combo** | Asigna una acción al doble toque del botón auxiliar seleccionado. | Ninguna |

## Indicadores

| Indicador | Significado |
|---|---|
| Lectura de Slice / Frecuencia / Modo | Muestra qué slice está vinculado, su frecuencia actual y su modo. |
| Estado físico | Muestra el estado de conexión y el nombre del puerto del dispositivo FlexControl físico. |

## Consejos

- La rueda virtual admite sintonización circular con mouse/táctil: haga doble clic en la rueda para capturarla y luego gire el dedo o el mouse en un movimiento circular. Presione Escape para soltar.
- **Wheel Tightness** y **Mouse Sensitivity** afectan principalmente a los paneles táctiles y no afectan a un dispositivo FlexControl físico.
- En modo compacto, el diálogo se redimensiona a un tamaño mínimo. Si el contenido supera la altura disponible de la pantalla, el diálogo se desplaza verticalmente.
- Los cambios se guardan automáticamente al cerrar el diálogo.
- Si el FlexControl físico se desconecta y se reconecta, AetherSDR restablece la conexión automáticamente en unos pocos segundos.

## Relacionado

- Configurar acciones de toque simple y doble toque para el botón PUSH

---

# Configurar acciones de toque simple y doble toque para el botón PUSH

Configure qué sucede al tocar o tocar dos veces la rueda (botón PUSH) en el diálogo AetherControl. Esto le permite cambiar rápidamente el paso de frecuencia, cambiar de banda, alternar funciones o ejecutar macros CWX sin tener que usar el mouse.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. Localice el cuadro combinado **Push (action)**. Esto establece la acción de toque simple.
2. Haga clic en el cuadro combinado y seleccione la acción deseada de la lista.
3. Localice el cuadro combinado **Double-tap (action)** directamente debajo. Esto establece la acción de doble toque.
4. Haga clic en el cuadro combinado y seleccione la acción deseada de la lista.
5. Cierre el diálogo. Los cambios se guardan automáticamente.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Cuadro combinado **Push (action)** | Asigna una acción al toque simple (pulsación) de la rueda. | `FlexControlButtonAction_*` |
| Cuadro combinado **Double-tap (action)** | Asigna una acción al doble toque de la rueda. | (almacenado junto con el toque simple en la misma estructura de configuración) |

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
| `WheelApf` | APF (Filtro de Enfoque de Audio) |
| `ClearRit` | Borrar RIT |
| `ClearXit` | Borrar XIT |
| `ToggleApf` | Alternar APF |
| `NextSlice` | Cambiar Slice Activo |
| `SplitActiveSlice` | Dividir Slice Activo |
| `ToggleMox` | MOX |
| `WheelPower` | Potencia de RF |
| `WheelCwSpeed` | Velocidad CW |
| `CwxF1` a `CwxF12` | Macro CWX 1 a 12 |
| `StepUp` | Paso Arriba |
| `StepDown` | Paso Abajo |
| `ToggleTune` | Alternar Sintonía |
| `ToggleMute` | Alternar Silencio |
| `ToggleLock` | Alternar Bloqueo |
| `PrevSlice` | Slice Anterior |
| `ToggleAgc` | Alternar AGC |
| `VolumeUp` | AF del Slice Arriba |
| `VolumeDown` | AF del Slice Abajo |

### Nuevo en v26.6.3

- **Slice Audio Volume** (`WheelSliceAudio`): Ajusta el volumen de audio del slice activo de forma independiente del volumen maestro. Esta acción se agregó a la lista de acciones disponibles en v26.6.3.

## Consejos

- Use una acción de rueda (Sintonizar Slice, Volumen Maestro, etc.) para el toque simple y una acción de un solo disparo (Paso Arriba, Zoom de Banda, etc.) para el doble toque para obtener un comportamiento complementario.
- El tiempo de guardado del doble toque es de 230 ms. Toque dos veces dentro de esa ventana para activar la acción de doble toque.
- Haga doble clic en la rueda virtual para capturar o liberar la sintonización circular con el mouse o el panel táctil. Presione Escape como método alternativo para liberar. La etiqueta de sugerencia de captura en la parte inferior del diálogo ahora dice "Double-click the knob to capture circular tuning."

## Relacionado

- [Mapear acciones de botón pulsador y doble toque a la rueda](map-push-button-and-double-tap-actions-to-the-wheel.md)
- [Configurar el controlador de hardware AetherControl / FlexControl](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
