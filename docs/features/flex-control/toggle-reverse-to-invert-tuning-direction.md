# Invertir inversión para cambiar la dirección de sintonización

Esta página explica cómo invertir la dirección de la rueda virtual de AetherControl / FlexControl, de modo que la rotación en el sentido de las agujas del reloj sintonice hacia frecuencias más bajas y la rotación en sentido contrario sintonice hacia frecuencias más altas.

## Antes de empezar

- Abra el diálogo de AetherControl: **Settings > AetherControl...**

## Pasos

1. En el diálogo de AetherControl, localice el botón de alternancia **Reverse**.
2. Haga clic en **Reverse** para cambiar entre la dirección de sintonización normal e invertida. El botón permanece presionado cuando la inversión está activa.

## Función de cada control

| Control | Etiqueta | Comportamiento | Clave de configuración |
|---------|----------|----------------|------------------------|
| Botón de alternancia | **Reverse** | Invierte la dirección de sintonización de la rueda. Cuando está activado, la rotación en el sentido de las agujas del reloj sintoniza hacia una frecuencia más baja y la rotación en sentido contrario sintoniza hacia una frecuencia más alta. | `FlexControlInvertDir` |

## Consejos

- La configuración **Reverse** es independiente para la rueda virtual y el dispositivo físico FlexControl; ambos usan la misma clave `FlexControlInvertDir`.
- Utilice **Reverse** si la rotación física de su controlador se siente opuesta a su modelo mental (por ejemplo, una rueda del lado izquierdo en un equipo portátil puede resultar más natural al invertirla).

## Relacionado

- [Configure the AetherControl / FlexControl hardware controller](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
- [Use the virtual wheel to tune the active slice](use-the-virtual-wheel-to-tune-the-active-slice.md)
- [Adjust mouse sensitivity for the virtual wheel](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
