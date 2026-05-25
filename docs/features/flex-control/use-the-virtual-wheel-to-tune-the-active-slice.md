# Usar la rueda virtual para sintonizar la franja activa

Use la rueda de sintonización virtual en pantalla en el diálogo AetherControl para cambiar la frecuencia de la franja actualmente activa con gestos del mouse o trackpad, simulando la sensación de un control rotatorio físico.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. En el diálogo AetherControl, localice el control **Wheel** en la parte superior. Muestra la frecuencia y el modo de la franja actual.
2. Haga clic y arrastre en un movimiento circular alrededor de la rueda para sintonizar. Arrastre en sentido horario para aumentar la frecuencia, en sentido antihorario para disminuirla.
3. (Opcional) Para invertir la dirección de sintonización, haga clic en **Reverse**.
4. (Opcional) Para habilitar la sintonización basada en el panadapter, haga clic en **External Spin**. Cuando está activado, arrastrar sobre el panadapter también activa la sintonización con la rueda.

## Qué hace cada control

| Control | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|
| **Wheel** | — | — | Ninguna (muestra la franja actual) |
| **Reverse** | Apagado | On/Off | `FlexControlInvertDir` |
| **External Spin** | Apagado | On/Off | `FlexControlVirtualExternalSpin` |
| **Wheel Tightness** | 45 | 0–100 (0 = ajustado, 100 = suelto) | `FlexControlVirtualWheel` (campo JSON anidado `looseness`) |
| **Mouse Sensitivity** | 50 | 0–100 (0 = menor, 100 = mayor) | `FlexControlVirtualWheel` (campo JSON anidado `sensitivity`) |

## Consejos

- La rueda virtual responde a arrastres circulares del mouse o trackpad. Los deltas de puntero de un solo evento se limitan a 15° (π/12 radianes) por evento para reducir la vibración.
- Cuando su puntero cruza la zona muerta central, el anclaje se restablece. El siguiente movimiento inicia un nuevo gesto de sintonización sin calcular un delta.
- **Wheel Tightness** y **Mouse Sensitivity** se almacenan juntos en un único objeto JSON bajo `FlexControlVirtualWheel`. En versiones anteriores, Wheel Tightness se almacenaba por separado como `FlexControlVirtualWheelLooseness`; esto se migra automáticamente en la primera lectura.
- La rueda muestra la frecuencia de la franja en Hz y el modo actual (por ejemplo, USB, CW, AM).

## Relacionado

- [Adjust mouse sensitivity for the virtual wheel](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Adjust wheel tightness (coasting feel)](adjust-wheel-tightness-coasting-feel.md)
- [Toggle Reverse to invert tuning direction](toggle-reverse-to-invert-tuning-direction.md)
- [Toggle Auto Spin for external frequency change animation](toggle-auto-spin-for-external-frequency-change-animation.md)
