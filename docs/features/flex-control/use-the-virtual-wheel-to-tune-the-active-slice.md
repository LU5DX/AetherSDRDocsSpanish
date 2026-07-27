# Use la rueda virtual para sintonizar el segmento activo

Use la rueda de sintonización virtual en pantalla en el cuadro de diálogo AetherControl para cambiar la frecuencia del segmento activo con gestos del mouse o trackpad, simulando la sensación de un controlador rotatorio físico.

## Antes de empezar

- Abra el cuadro de diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. En el cuadro de diálogo AetherControl, localice el control **Wheel** en la parte superior. Muestra la frecuencia y el modo del segmento actual.
2. Haga doble clic en la rueda para capturar la entrada del mouse para la sintonización circular. La rueda se activa para gestos de sintonización.
3. Arrastre en un movimiento circular alrededor de la rueda para sintonizar. Arrastre en el sentido de las agujas del reloj para aumentar la frecuencia, en sentido contrario para disminuirla.
4. Para liberar la captura del mouse, haga doble clic en la rueda nuevamente. Presione Escape como ruta de liberación secundaria.
5. (Opcional) Para invertir la dirección de sintonización, haga clic en **Reverse**.
6. (Opcional) Para habilitar la sintonización basada en el panadapter, haga clic en **External Spin**. Cuando está habilitado, arrastrar en el panadapter también activa la sintonización de la rueda giratoria.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|
| **Wheel** | — | — | Ninguna (muestra el segmento actual) |
| **Physical** | — | — | Ninguna (muestra el estado de conexión) |
| **Compact** | Off | On/Off | Ninguna |
| **External Spin** | Off | On/Off | `FlexControlVirtualExternalSpin` |
| **Reverse** | Off | On/Off | `FlexControlInvertDir` |
| **Push (action)** | — | — | `FlexControlButtonAction_*` |
| **Double-tap (action)** | — | — | Ninguna |
| **Wheel Tightness** | 45 | 0–100 (0 = ajustada, 100 = suelta) | `FlexControlVirtualWheel` (campo JSON anidado `looseness`) |
| **Mouse Sensitivity** | 50 | 0–100 (0 = menos, 100 = más) | `FlexControlVirtualWheel` (campo JSON anidado `sensitivity`) |
| **Aux buttons 1–5** | — | 5 botones | Ninguna |

## Opciones de acción de la rueda

Las siguientes acciones están disponibles para los controles basados en rueda (Push, Double-tap y combinaciones de botones auxiliares):

| ID de acción | Descripción |
|---|---|
| `WheelRit` | RIT (Sintonización Incremental de Recepción) |
| `WheelXit` | XIT (Sintonización Incremental de Transmisión) |
| `WheelVolume` | Volumen Maestro |
| `WheelSliceAudio` | Volumen de Audio del Segmento |
| `WheelHeadphoneVolume` | Volumen de Auriculares |
| `WheelAgcT` | AGCT (Umbral de Control Automático de Ganancia) |
| `WheelApf` | APF (Filtro de Pico de Audio) |

## Botones auxiliares

El cuadro de diálogo proporciona cinco botones auxiliares configurables (etiquetados con puntos auxiliares para indicar la selección activa). Cada botón tiene:

- **Aux single-tap combo**: Asigna una acción al toque simple del botón auxiliar seleccionado.
- **Aux double-tap combo**: Asigna una acción al doble toque del botón auxiliar seleccionado.

Estas configuraciones se almacenan por botón auxiliar.

## Consejos

- La captura del mouse se ha simplificado a un solo interruptor de doble clic: haga doble clic para capturar, haga doble clic nuevamente para liberar. Esto reemplaza el comportamiento anterior de clic para capturar, Escape para liberar para una experiencia de usuario más limpia.
- La rueda virtual responde a arrastres circulares del mouse o trackpad. Los deltas de puntero de un solo evento se limitan a 15° (π/12 radianes) por evento para reducir la vibración.
- Cuando su puntero cruza la zona muerta central, el ancla se reinicia. El siguiente movimiento inicia un nuevo gesto de sintonización sin calcular un delta.
- **Wheel Tightness** y **Mouse Sensitivity** se almacenan juntos en un único objeto JSON bajo `FlexControlVirtualWheel`. En versiones anteriores, Wheel Tightness se almacenaba por separado como `FlexControlVirtualWheelLooseness`; esto se migra automáticamente en la primera lectura.
- La rueda muestra la frecuencia del segmento en Hz y el modo actual (p. ej., USB, CW, AM).
- Haga clic en **Compact** para alternar el modo compacto, que oculta los botones auxiliares y muestra solo la rueda y la frecuencia para una interfaz mínima.
- El indicador **Physical** muestra el estado de conexión y el nombre del puerto del FlexControl físico. Use los botones Detect/Close para gestionar el dispositivo físico.
- La ventana del cuadro de diálogo ahora contiene un área de desplazamiento. Cuando el controlador completo excede la altura de pantalla disponible, el contenido se desplaza verticalmente para que la ventana pueda ser más pequeña que la altura total del controlador. El ancho mínimo de la ventana se establece en el ancho mínimo del contenido para evitar el recorte horizontal.
- En pantallas cortas o con escala DPI, la altura de la ventana se limita a la altura de pantalla disponible al abrirse, y el contenido se vuelve desplazable en lugar de forzarse al modo compacto.

## Relacionado

- [Ajustar la sensibilidad del mouse para la rueda virtual](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Ajustar la tensión de la rueda (sensación de deslizamiento)](adjust-wheel-tightness-coasting-feel.md)
- [Alternar Reverse para invertir la dirección de sintonización](toggle-reverse-to-invert-tuning-direction.md)
- [Alternar Auto Spin para la animación de cambio de frecuencia externo](toggle-auto-spin-for-external-frequency-change-animation.md)
