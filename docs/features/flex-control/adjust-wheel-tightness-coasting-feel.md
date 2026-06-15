# Ajustar la rigidez de la rueda (sensación de deslizamiento)

Configure cuánto tiempo continúa girando la rueda de sintonización virtual (deslizamiento) después de dejar de mover el mouse o el trackpad. Un ajuste más tenso se detiene más rápido; uno más suelto se desliza por más tiempo.

## Antes de comenzar

- Abra el cuadro de diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. Localice el control deslizante **Wheel Tightness** en el cuadro de diálogo.
2. Arrastre el control deslizante hasta la sensación de deslizamiento que prefiera:
   - **0** (Tight) — la rueda se detiene casi inmediatamente cuando deja de moverse.
   - **100** (Loose) — la rueda se desliza durante un largo tiempo después de detenerse.
   - **45** — valor predeterminado.
3. Cierre el cuadro de diálogo. Los cambios se guardan automáticamente.

> **Nota:** Este ajuste afecta únicamente a la rueda virtual (sintonización con mouse/trackpad). No afecta a un dispositivo físico FlexControl.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|---------------|-------|-----------------|----------------|
| Control deslizante Wheel Tightness | 45 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `looseness`) | Ajusta la fricción de deslizamiento de la rueda virtual. 0 = tenso (parada rápida), 100 = suelto (deslizamiento prolongado). |
| Control deslizante Mouse Sensitivity | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `sensitivity`) | Ajusta cuánto movimiento capturado del mouse/trackpad hace girar la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. |

## Relacionados

- [Ajustar la sensibilidad del ratón para la rueda virtual](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Usar la rueda virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)

---

# Acción de rueda para volumen de audio del slice

La acción **Slice Audio Volume** le permite ajustar el volumen de audio del slice activo utilizando la rueda de AetherControl.

## Antes de comenzar

- Abra el cuadro de diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. En el cuadro de diálogo, localice el cuadro combinado **Push (action)** o **Double-tap (action)**, o uno de los cuadros combinados **Aux** de toque simple o doble toque.
2. Haga clic en el cuadro combinado y seleccione **Slice Audio Volume** de la lista.
3. Cierre el cuadro de diálogo. Los cambios se guardan automáticamente.

Al presionar el botón asignado o activar el doble toque, la rueda de sintonización cambia a controlar el volumen de audio del slice. Girar la rueda en sentido horario aumenta el volumen; en sentido antihorario lo disminuye.

> **Nota:** Esta acción se añadió en AetherSDR v26.6.3.
