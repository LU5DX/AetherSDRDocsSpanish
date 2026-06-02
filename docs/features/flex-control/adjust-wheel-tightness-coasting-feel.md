# Ajustar la tensión de la rueda (sensación de deslizamiento)

Configure cuánto tiempo continúa girando la rueda de sintonización virtual (deslizamiento) después de dejar de mover el mouse o el trackpad. Un ajuste más firme la detiene más rápido; un ajuste más suave prolonga el deslizamiento.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. Localice el control deslizante **Wheel Tightness** en el diálogo.
2. Arrastre el control deslizante hasta la sensación de deslizamiento deseada:
   - **0** (Tight) — la rueda se detiene casi inmediatamente al dejar de moverse.
   - **100** (Loose) — la rueda se desliza por un tiempo prolongado después de detenerse.
   - **45** — valor predeterminado.
3. Cierre el diálogo. Los cambios se guardan automáticamente.

> **Nota:** Este ajuste solo afecta a la rueda virtual (sintonización con mouse/trackpad). No afecta a un dispositivo físico FlexControl.

## Función de cada control

| Control | Valor predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|---------------------|-------|-----------------|---------------|
| Control deslizante Wheel Tightness | 45 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `looseness`) | Ajusta la fricción del deslizamiento de la rueda virtual. 0 = firme (parada rápida), 100 = suave (deslizamiento prolongado). |
| Control deslizante Mouse Sensitivity | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `sensitivity`) | Ajusta cuánto movimiento capturado del mouse/trackpad hace girar la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. |

## Relacionados

- [Ajustar la sensibilidad del mouse para la rueda virtual](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Usar la rueda virtual para sintonizar la slice activa](use-the-virtual-wheel-to-tune-the-active-slice.md)
