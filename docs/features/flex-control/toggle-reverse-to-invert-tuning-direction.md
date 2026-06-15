# Activar inversión para invertir la dirección de sintonización

Esta página explica cómo invertir la dirección de la rueda virtual de AetherControl / FlexControl, de modo que la rotación en el sentido de las agujas del reloj sintonice hacia abajo y la rotación en sentido contrario sintonice hacia arriba.

## Antes de comenzar

- Abra el diálogo AetherControl: **Settings > AetherControl...**

## Pasos

1. En el diálogo AetherControl, localice el botón de alternancia **Reverse**.
2. Haga clic en **Reverse** para cambiar entre la dirección de sintonización normal e invertida. El botón aparece presionado cuando la inversión está activa.

## Funcionamiento de cada control

| Control | Etiqueta | Comportamiento | Clave de configuración |
|---------|----------|----------------|------------------------|
| Botón de alternancia | **Reverse** | Invierte la dirección de sintonización de la rueda. Cuando está activado, la rotación en el sentido de las agujas del reloj sintoniza a una frecuencia más baja y la rotación en sentido contrario sintoniza a una frecuencia más alta. | `FlexControlInvertDir` |

## Consejos

- La configuración **Reverse** es independiente para la rueda virtual y el dispositivo físico FlexControl; ambos utilizan la misma clave `FlexControlInvertDir`.
- Use **Reverse** si la rotación física de su controlador se siente opuesta a su modelo mental (por ejemplo, una rueda del lado izquierdo en un equipo portátil puede sentirse más natural invertida).

## Relacionados

- [Configure el controlador hardware AetherControl / FlexControl](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
- [Use la rueda virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)
- [Ajuste la sensibilidad del ratón para la rueda virtual](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Asigne acciones de rueda en el AetherControl](assign-wheel-actions-on-the-aethercontrol.md)
