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
4. Pruebe la sensación girando el dedo o el lápiz alrededor del widget de la rueda virtual.
5. Cierre el diálogo para guardar la configuración.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---------|---------------------|--------------|------------------------|
| Control deslizante Mouse Sensitivity | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `sensitivity`) |

- El punto medio (50) produce una escala 1.0x del movimiento del puntero.
- Los valores por debajo de 50 reducen la sensibilidad (se necesita más movimiento).
- Los valores por encima de 50 aumentan la sensibilidad (se necesita menos movimiento).
- Afecta solo a la rueda virtual; no cambia el comportamiento de un FlexControl físico.
- Los deltas del puntero de un solo evento se limitan a 15° (π/12 radianes) para reducir la vibración.
- El reanclaje diferido evita saltos no deseados cuando el puntero cruza la zona muerta central de la rueda.

## Comportamiento de captura/liberación

- **Doble clic** en la rueda virtual para capturar la entrada del ratón para sintonización circular.
- **Doble clic** nuevamente para liberar la captura.
- Presione **Escape** como ruta de liberación secundaria.
- Un solo clic ya no captura ni libera la rueda. Este cambio proporciona una experiencia de usuario más limpia que la asimetría anterior de hacer clic para capturar y Escape para liberar.

## Consejos

- Si usa un trackpad, intente comenzar con el valor 65 y ajuste desde allí.
- El control deslizante complementario **Wheel Tightness** controla la sensación de deslizamiento (cuánto tiempo sigue girando la rueda después de que usted deja de moverla). Consulte [Ajustar la rigidez de la rueda (sensación de deslizamiento)](adjust-wheel-tightness-coasting-feel.md).

## Relacionados

- [Ajustar la rigidez de la rueda (sensación de deslizamiento)](adjust-wheel-tightness-coasting-feel.md)
- [Usar la rueda virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)
