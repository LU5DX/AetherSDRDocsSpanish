# Habilitar Snap to Step para un ajuste preciso del S-History

Snap to Step redondea el clic para sintonizar del S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando pequeños desplazamientos de portadora. Actívelo cuando desee sintonizar con precisión la frecuencia donde debería escucharse una señal, en lugar de donde aparece su portadora.

## Antes de comenzar

- Signal History debe estar habilitada (consulte [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)).

## Pasos

1. Abra **Settings > SpotHub...**.
2. Haga clic en la pestaña **Display**.
3. Desplácese hasta la sección **Signal History**.
4. Haga clic en **Snap to Step** para habilitarlo (el alternador se llena de verde cuando está marcado).

## Descripción de cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Snap to Step | Deshabilitado | Activado / Desactivado | `SHistorySnapToStep` |

## Consejos

- Snap to Step solo afecta los clics en los marcadores de Signal History — no cambia la forma en que el slice sintoniza al hacer clic directamente en el espectro.
- Los controles deslizantes Filter Match Window, Edge Threshold, Marker Lifetime y QRM Gate admiten doble clic izquierdo para restablecer su valor predeterminado almacenado.

## Solución de problemas

- **Al hacer clic en un marcador, aún se sintoniza la frecuencia exacta de la portadora** — Asegúrese de que el alternador **Snap to Step** muestre un relleno verde. Si aún está gris, haga clic una vez para habilitarlo.

## Relacionados

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm-gate-and-edge-threshold.md)
