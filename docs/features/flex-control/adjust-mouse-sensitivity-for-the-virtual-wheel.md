# Diálogo de AetherControl / FlexControl

El diálogo de AetherControl ofrece configuración tanto para el hardware físico FlexControl como para la rueda de sintonización virtual. Incluye una visualización de rueda virtual, configuración de botones auxiliares y ajustes de sensibilidad de sintonización.

## Abrir el diálogo

- Seleccione `Settings > AetherControl...`

## Visualización de la rueda virtual

La rueda virtual muestra el slice activo actual, su frecuencia y modo. Puede girarla con el mouse o con el tacto para sintonizar el slice activo.

## FlexControl físico

El diálogo muestra el estado de conexión y el nombre del puerto del FlexControl físico. Use los botones **Detect** y **Close** para administrar el dispositivo físico.

Si la conexión con un FlexControl físico se pierde — por ejemplo, si se desconecta el cable USB — AetherSDR reintenta la conexión automáticamente. Los reintentos comienzan después de 2 segundos y aumentan progresivamente hasta un intervalo máximo de 30 segundos hasta que el dispositivo se detecte nuevamente. El controlador vuelve a detectar el nombre del puerto en cada reintento, por lo que un dispositivo que se reenumera en un puerto COM diferente se reconecta correctamente. La falla se registra una vez por interrupción en lugar de en cada reintento.

## Modo compacto

Active **Compact** para ocultar los botones auxiliares y mostrar solo la rueda y la lectura de frecuencia para una interfaz mínima.

## Giro externo

Active **External Spin** para permitir gestos de arrastre en el panadapter que activen el comportamiento de sintonización de la rueda giratoria.

## Dirección inversa

Active **Reverse** para invertir la dirección de sintonización de la rueda.

## Acciones de la rueda

Asigne acciones al presionar o tocar dos veces la rueda:

| Control | Descripción |
|---------|-------------|
| **Push (action)** | Seleccione una acción para un toque simple en la rueda |
| **Double-tap (action)** | Seleccione una acción para un doble toque en la rueda |

Acciones de rueda disponibles:

| ID de acción | Nombre mostrado |
|-----------|--------------|
| `WheelRit` | RIT (Receive Incremental Tuning) |
| `WheelXit` | XIT (Transmit Incremental Tuning) |
| `WheelVolume` | Master Volume |
| `WheelSliceAudio` | Slice Audio Volume |
| `WheelHeadphoneVolume` | Headphone Volume |
| `WheelAgcT` | AGCT (Automatic Gain Control Threshold) |
| `WheelApf` | APF (Audio Peaking Filter) |

**WheelSlice Audio** controla el volumen de audio del slice activo actual, independiente del control de volumen maestro. Los ajustes heredados que usan `WheelMasterAf` se reconocen automáticamente como equivalentes a `WheelVolume`.

## Botones auxiliares

Configure cinco botones auxiliares, cada uno con acciones separadas de toque simple y doble toque:

1. Haga clic en uno de los cinco botones **Aux** (etiquetados con puntos) para seleccionarlo.
2. En el **combo de toque simple de Aux**, seleccione la acción para un toque simple.
3. En el **combo de doble toque de Aux**, seleccione la acción para un doble toque.

Cada botón auxiliar recuerda sus propias asignaciones de forma independiente. El botón auxiliar seleccionado se indica mediante el estado del punto junto a su etiqueta.

## Control deslizante de tensión de la rueda

Ajusta el arrastre de inercia de la rueda virtual:

| Control | Predeterminado | Rango | Clave de ajuste |
|---------|---------|-------|-------------|
| Control deslizante Wheel Tightness | 45 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `looseness`) |

- **Tight** (izquierda, valor 0): detención rápida después de soltar la rueda.
- **Loose** (derecha, valor 100): inercia prolongada después de soltar la rueda.
- Afecta principalmente el uso del trackpad; no afecta un FlexControl físico.
- Antes se almacenaba bajo la clave plana heredada `FlexControlVirtualWheelLooseness`; se migra automáticamente en la primera lectura.

## Control deslizante de sensibilidad del mouse

Ajusta cuánto movimiento del puntero gira la rueda virtual:

| Control | Predeterminado | Rango | Clave de ajuste |
|---------|---------|-------|-------------|
| Control deslizante Mouse Sensitivity | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `sensitivity`) |

- **Less** (izquierda, valor 0): requiere más movimiento del puntero.
- **More** (derecha, valor 100): requiere menos movimiento del puntero.
- El punto medio (50) produce una escala de 1.0x.
- Los deltas de puntero de evento único se limitan a 15° (π/12 radianes) para reducir la vibración.
- El reanclaje diferido evita saltos no deseados cuando el puntero cruza la zona muerta central de la rueda.
- Afecta solo la rueda virtual; no cambia el comportamiento de un FlexControl físico.

### Consejos

- Si usa un trackpad, intente comenzar con Mouse Sensitivity en el valor 65 y ajuste desde allí.
- Use el control deslizante complementario **Wheel Tightness** para controlar la sensación de inercia.

## Comportamiento de captura/liberación

- **Doble clic** en la rueda virtual para capturar la entrada del mouse para sintonización circular.
- **Doble clic** nuevamente para liberar la captura.
- Presione **Escape** como vía secundaria de liberación.
- Un solo clic ya no captura ni libera la rueda.

## Tamaño de la ventana

El diálogo de AetherControl se adapta al tamaño de su pantalla. Cuando se abre en modo no compacto en una pantalla más baja, el área de contenido se desplaza verticalmente para que todos los controles permanezcan accesibles. El diálogo nunca se abre más alto que la altura disponible del espacio de trabajo.
