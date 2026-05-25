# Ajustar la tensión de la rueda (sensación de deslizamiento)

Configure cuánto tiempo continúa girando la rueda de sintonización virtual (deslizamiento) después de dejar de mover el mouse o trackpad. Un ajuste más tenso detiene la rueda más rápido; un ajuste más suelto prolonga el deslizamiento.

## Antes de comenzar

- Abra el cuadro de diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. Encuentre el control deslizante **Wheel Tightness** en el diálogo.
2. Arrastre el control deslizante hasta la sensación de deslizamiento que prefiera:
   - **0** (Tight) — la rueda se detiene casi inmediatamente cuando deja de moverse.
   - **100** (Loose) — la rueda se desliza durante mucho tiempo después de detenerse.
   - **45** — valor predeterminado.
3. Cierre el diálogo. Los cambios se guardan automáticamente.

> **Nota:** Este ajuste afecta únicamente a la rueda virtual (sintonización con mouse/trackpad). No afecta a un dispositivo físico FlexControl.

## Función de cada control

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------|-------|----------------------|----------------|
| Control deslizante Wheel Tightness | 45 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `looseness`) | Ajusta la fricción de deslizamiento de la rueda virtual. 0 = tensa (parada rápida), 100 = suelta (deslizamiento prolongado). |

## Relacionado

- [Ajustar la sensibilidad del mouse para la rueda virtual](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Usar la rueda virtual para sintonizar la franja activa](use-the-virtual-wheel-to-tune-the-active-slice.md)
