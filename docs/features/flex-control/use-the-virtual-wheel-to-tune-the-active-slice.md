# Uso de la rueda virtual para sintonizar la porción activa

Use la rueda de sintonización virtual en pantalla del cuadro de diálogo AetherControl para cambiar la frecuencia de la porción activa con gestos del ratón o trackpad, simulando la sensación de un control rotatorio físico.

## Antes de comenzar

- Abra el cuadro de diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. En el cuadro de diálogo AetherControl, localice el control **Wheel** en la parte superior. Muestra la frecuencia y el modo de la porción actual.
2. Haga doble clic en la rueda para capturar la entrada del ratón para sintonización circular. La rueda se activa para gestos de sintonización.
3. Arrastre en un movimiento circular alrededor de la rueda para sintonizar. Arrastre en sentido horario para aumentar la frecuencia, en sentido antihorario para disminuirla.
4. Para liberar la captura del ratón, haga doble clic nuevamente en la rueda. Presione Escape como ruta alternativa de liberación.
5. (Opcional) Para invertir la dirección de sintonización, haga clic en **Reverse**.
6. (Opcional) Para habilitar la sintonización basada en el panadapter, haga clic en **External Spin**. Cuando está habilitado, arrastrar sobre el panadapter también activa la sintonización por rueda.

## Función de cada control

| Control | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|
| **Wheel** | — | — | Ninguna (muestra la porción actual) |
| **Physical** | — | — | Ninguna (muestra el estado de conexión) |
| **Compact** | Off | On/Off | Ninguna |
| **External Spin** | Off | On/Off | `FlexControlVirtualExternalSpin` |
| **Reverse** | Off | On/Off | `FlexControlInvertDir` |
| **Push (acción)** | — | — | `FlexControlButtonAction_*` |
| **Double-tap (acción)** | — | — | Ninguna |
| **Wheel Tightness** | 45 | 0–100 (0 = ajustado, 100 = suelto) | `FlexControlVirtualWheel` (campo JSON anidado `looseness`) |
| **Mouse Sensitivity** | 50 | 0–100 (0 = menor, 100 = mayor) | `FlexControlVirtualWheel` (campo JSON anidado `sensitivity`) |
| **Aux buttons 1–5** | — | 5 botones | Ninguna |

## Botones auxiliares

El cuadro de diálogo proporciona cinco botones auxiliares configurables (etiquetados con puntos auxiliares para indicar la selección activa). Cada botón tiene:

- **Aux single-tap combo**: Asigna una acción al toque único del botón auxiliar seleccionado.
- **Aux double-tap combo**: Asigna una acción al doble toque del botón auxiliar seleccionado.

Estas configuraciones se almacenan por botón auxiliar.

## Consejos

- La captura del ratón se ha simplificado a una alternancia de doble clic: haga doble clic para capturar, haga doble clic nuevamente para liberar. Esto reemplaza el comportamiento anterior de clic para capturar y Escape para liberar para una experiencia de usuario más limpia.
- La rueda virtual responde a arrastres circulares del ratón o trackpad. Los deltas de puntero de eventos únicos se limitan a 15° (π/12 radianes) por evento para reducir la vibración.
- Cuando su puntero cruza la zona muerta central, el anclaje se reinicia. El siguiente movimiento inicia un nuevo gesto de sintonización sin calcular un delta.
- **Wheel Tightness** y **Mouse Sensitivity** se almacenan juntos en un único objeto JSON bajo `FlexControlVirtualWheel`. En versiones anteriores, Wheel Tightness se almacenaba por separado como `FlexControlVirtualWheelLooseness`; esto se migra automáticamente en la primera lectura.
- La rueda muestra la frecuencia de la porción en Hz y el modo actual (p. ej., USB, CW, AM).
- Haga clic en **Compact** para alternar el modo compacto, que oculta los botones auxiliares y muestra solo la rueda y la frecuencia para una interfaz mínima.
- El indicador **Physical** muestra el estado de conexión del FlexControl físico y el nombre del puerto. Use los botones Detect/Close para gestionar el dispositivo físico.

## Relacionado

- [Ajustar la sensibilidad del ratón para la rueda virtual](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Ajustar la rigidez de la rueda (sensación de deslizamiento)](adjust-wheel-tightness-coasting-feel.md)
- [Alternar Reverse para invertir la dirección de sintonización](toggle-reverse-to-invert-tuning-direction.md)
- [Alternar Auto Spin para la animación de cambio de frecuencia externa](toggle-auto-spin-for-external-frequency-change-animation.md)
