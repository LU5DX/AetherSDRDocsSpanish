# Invertir el giro para cambiar la dirección de sintonía

Esta página explica cómo invertir la dirección de la rueda virtual de AetherControl / FlexControl, de modo que el giro en el sentido de las agujas del reloj sintonice hacia frecuencias más bajas y el giro en sentido contrario las sintonice hacia frecuencias más altas.

## Antes de comenzar

- Abra el cuadro de diálogo de AetherControl: **Settings > AetherControl...**

## Pasos

1. En el cuadro de diálogo de AetherControl, localice el botón de alternancia **Reverse**.
2. Haga clic en **Reverse** para cambiar entre la dirección de sintonía normal e invertida. El botón aparece presionado cuando la inversión está activa.

## Función de cada control

| Control | Etiqueta | Comportamiento | Clave de configuración |
|---------|----------|----------------|------------------------|
| Botón de alternancia | **Reverse** | Invierte la dirección de sintonía de la rueda. Al activarlo, el giro en el sentido de las agujas del reloj sintoniza a una frecuencia más baja y el giro en sentido contrario sintoniza a una frecuencia más alta. | `FlexControlInvertDir` |

## Consejos

- El ajuste **Reverse** es independiente para la rueda virtual y el dispositivo físico FlexControl; ambos usan la misma clave `FlexControlInvertDir`.
- Use **Reverse** si la rotación física de su controlador se siente opuesta a su modelo mental (por ejemplo, una rueda en el lado izquierdo de un equipo portátil podría sentirse más natural invertida).

## Relacionados

- [Configure the AetherControl / FlexControl hardware controller](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
- [Use the virtual wheel to tune the active slice](use-the-virtual-wheel-to-tune-the-active-slice.md)
- [Adjust mouse sensitivity for the virtual wheel](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
