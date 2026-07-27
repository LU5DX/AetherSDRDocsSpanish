# Diálogo de AetherControl / FlexControl

El diálogo de AetherControl permite configurar tanto el hardware físico FlexControl como la rueda de sintonización virtual. Incluye una visualización de rueda virtual, configuración de botones auxiliares y ajustes de sensibilidad de sintonización.

## Abrir el diálogo

- Seleccione `Settings > AetherControl...`

## Visualización de la rueda virtual

La rueda virtual muestra el slice activo actual, su frecuencia y modo. Puede girarla con el ratón o el tacto para sintonizar el slice activo.

## FlexControl físico

El diálogo muestra el estado de conexión y el nombre del puerto del FlexControl físico. Use los botones **Detect** y **Close** para gestionar el dispositivo físico.

## Modo compacto

Active **Compact** para ocultar los botones auxiliares y mostrar solo la rueda y la lectura de frecuencia, obteniendo una interfaz mínima.

## Giro externo

Active **External Spin** para permitir que los gestos de arrastre sobre el panadapter activen el comportamiento de sintonización con rueda giratoria.

## Invertir dirección

Active **Reverse** para invertir la dirección de giro de la rueda.

## Acciones de la rueda

Asigne acciones al pulsar o hacer doble clic en la rueda:

| Control | Descripción |
|---------|-------------|
| **Push (action)** | Seleccione una acción para un solo clic en la rueda |
| **Double-tap (action)** | Seleccione una acción para un doble clic en la rueda |

Acciones disponibles para la rueda:

| ID de acción | Nombre mostrado |
|--------------|-----------------|
| `WheelRit` | RIT (Sintonización Incremental en Recepción) |
| `WheelXit` | XIT (Sintonización Incremental en Transmisión) |
| `WheelVolume` | Volumen Maestro |
| `WheelSliceAudio` | Volumen de Audio del Slice |
| `WheelHeadphoneVolume` | Volumen de Auriculares |
| `WheelAgcT` | AGCT (Umbral de Control Automático de Ganancia) |
| `WheelApf` | APF (Filtro de Enfoque de Audio) |

**WheelSlice Audio** controla el volumen de audio del slice activo actual, independientemente del control de volumen maestro. Las configuraciones heredadas que usan `WheelMasterAf` se reconocen automáticamente como equivalentes a `WheelVolume`.

## Botones auxiliares

Configure cinco botones auxiliares, cada uno con acciones separadas para un solo clic y doble clic:

1. Haga clic en uno de los cinco botones **Aux** (marcados con puntos) para seleccionarlo.
2. En el **Aux single-tap combo**, seleccione la acción para un solo clic.
3. En el **Aux double-tap combo**, seleccione la acción para un doble clic.

Cada botón auxiliar recuerda sus propias asignaciones de forma independiente. El botón auxiliar seleccionado se indica mediante el estado del punto junto a su etiqueta.

## Control deslizante de tensión de la rueda

Ajusta el arrastre por inercia de la rueda virtual:

| Control | Valor predeterminado | Rango | Clave de configuración |
|---------|----------------------|-------|------------------------|
| Control deslizante Wheel Tightness | 45 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `looseness`) |

- **Tight** (izquierda, valor 0): se detiene rápidamente al soltar la rueda.
- **Loose** (derecha, valor 100): se desliza largo tiempo al soltar la rueda.
- Afecta principalmente el uso del trackpad; no afecta a un FlexControl físico.
- Anteriormente se almacenaba bajo la clave plana heredada `FlexControlVirtualWheelLooseness`; se migra automáticamente en la primera lectura.

## Control deslizante de sensibilidad del ratón

Ajusta cuánto movimiento del puntero gira la rueda virtual:

| Control | Valor predeterminado | Rango | Clave de configuración |
|---------|----------------------|-------|------------------------|
| Control deslizante Mouse Sensitivity | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `sensitivity` field) |

- **Less** (izquierda, valor 0): requiere más movimiento del puntero.
- **More** (derecha, valor 100): requiere menos movimiento del puntero.
- El punto medio (50) produce una escala de 1.0x.
- Los deltas del puntero de evento único se limitan a 15° (π/12 radianes) para reducir la inestabilidad.
- El reanclaje diferido evita saltos no deseados cuando el puntero cruza la zona muerta central de la rueda.
- Afecta solo a la rueda virtual; no cambia el comportamiento de un FlexControl físico.

### Consejos

- Si usa un trackpad, pruebe comenzar con Mouse Sensitivity en el valor 65 y ajuste desde allí.
- Use el control deslizante complementario **Wheel Tightness** para controlar la sensación de deslizamiento.

## Comportamiento de captura/liberación

- **Haga doble clic** en la rueda virtual para capturar la entrada del ratón para sintonización circular.
- **Haga doble clic** nuevamente para liberar la captura.
- Presione **Escape** como ruta de liberación secundaria.
- Un solo clic ya no captura ni libera la rueda.

## Tamaño de la ventana

El diálogo de AetherControl se adapta al tamaño de su pantalla. Cuando se abre en modo no compacto en una pantalla de poca altura, el área de contenido se desplaza verticalmente para que todos los controles sigan siendo accesibles. El diálogo nunca se abre con una altura mayor que la altura disponible del espacio de trabajo.
