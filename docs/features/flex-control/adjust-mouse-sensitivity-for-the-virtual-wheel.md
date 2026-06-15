# Ajustar la sensibilidad del ratón para la rueda virtual

Cambie cuánto movimiento del ratón o trackpad se requiere para girar la rueda de sintonización virtual. Una sensibilidad más alta significa menos movimiento físico por cambio de frecuencia.

## Antes de comenzar

- El diálogo AetherControl debe estar abierto: `Settings > AetherControl...`
- La rueda virtual está disponible independientemente de si hay un FlexControl físico conectado.

## Pasos

1. Abra `Settings > AetherControl...`.
2. En la sección **Wheel Tightness / Mouse Sensitivity**, localice el control deslizante **Mouse Sensitivity**.
3. Arrastre el control deslizante al valor deseado:
   - **Less** (izquierda, valor 0): requiere más movimiento del puntero para girar la rueda.
   - **More** (derecha, valor 100): requiere menos movimiento del puntero para girar la rueda.
4. Pruebe la sensación girando su dedo o lápiz óptico alrededor del widget de la rueda virtual.
5. Cierre el diálogo para guardar la configuración.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---------|---------------------|--------------|------------------------|
| Control deslizante Mouse Sensitivity | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `sensitivity`) |

- El punto medio (50) produce una escala de 1.0x del movimiento del puntero.
- Los valores por debajo de 50 reducen la sensibilidad (se necesita más movimiento).
- Los valores por encima de 50 aumentan la sensibilidad (se necesita menos movimiento).
- Afecta solo a la rueda virtual; no cambia el comportamiento de un FlexControl físico.
- Los deltas de puntero de un solo evento se limitan a 15° (π/12 radianes) para reducir la vibración.
- El reanclaje diferido evita saltos no deseados cuando el puntero cruza la zona muerta central de la rueda.

## Comportamiento de captura/liberación

- **Haga doble clic** en la rueda virtual para capturar la entrada del ratón para sintonización circular.
- **Haga doble clic** nuevamente para liberar la captura.
- Presione **Escape** como una vía de liberación secundaria.
- Un solo clic ya no captura ni libera la rueda. Este cambio proporciona una experiencia de usuario más limpia que la asimetría anterior de clic-para-capturar con Escape-para-liberar.

## Consejos

- Si usa un trackpad, intente comenzar con el valor 65 y ajuste desde allí.
- El control deslizante complementario **Wheel Tightness** controla la sensación de deslizamiento (cuánto tiempo sigue girando la rueda después de que usted deja de moverla). Consulte [Ajustar la rigidez de la rueda (sensación de deslizamiento)](adjust-wheel-tightness-coasting-feel.md).

## Relacionado

- [Ajustar la rigidez de la rueda (sensación de deslizamiento)](adjust-wheel-tightness-coasting-feel.md)
- [Usar la rueda virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)

# Asignar acciones a la pulsación y doble toque de la rueda

Configure lo que sucede cuando pulsa o hace doble toque en la rueda virtual en el diálogo AetherControl.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`
- La rueda virtual debe estar activa.

## Pasos

1. En el cuadro combinado **Push (action)**, seleccione una acción para un solo toque en la rueda.
2. En el cuadro combinado **Double-tap (action)**, seleccione una acción para un doble toque en la rueda.

## Acciones de rueda disponibles

Las siguientes acciones se pueden asignar a la pulsación o doble toque de la rueda:

| ID de acción | Nombre mostrado |
|--------------|-----------------|
| `WheelRit` | RIT (Sintonización incremental de recepción) |
| `WheelXit` | XIT (Sintonización incremental de transmisión) |
| `WheelVolume` | Volumen maestro |
| `WheelSliceAudio` | Volumen de audio del slice |
| `WheelHeadphoneVolume` | Volumen de auriculares |
| `WheelAgcT` | AGCT (Umbral de control automático de ganancia) |
| `WheelApf` | APF (Filtro de pico de audio) |

- **WheelSlice Audio** controla el volumen de audio del slice actualmente activo. Esto es independiente del control de volumen maestro.
- Las configuraciones heredadas que usan `WheelMasterAf` se reconocen automáticamente como equivalentes a `WheelVolume`.

# Configurar botones auxiliares

Los cinco botones auxiliares en el FlexControl virtual pueden tener cada uno acciones separadas de toque simple y doble toque.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. Haga clic en uno de los cinco botones **Aux** (etiquetados con puntos) para seleccionarlo.
2. En el cuadro combinado **Aux single-tap combo**, seleccione la acción para un solo toque.
3. En el cuadro combinado **Aux double-tap combo**, seleccione la acción para un doble toque.

## Consejos

- Cada botón auxiliar recuerda sus propias asignaciones de toque simple y doble toque de forma independiente.
- El botón auxiliar seleccionado se indica mediante el estado del punto junto a su etiqueta.
