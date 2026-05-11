# Habilitar Snap to Step para un ajuste preciso del S-History

Snap to Step redondea el ajuste con un clic del S-History al múltiplo más cercano del tamaño de paso de la franja activa, ocultando pequeños desfases de portadora. Actívelo cuando desee sintonizar con precisión la frecuencia en la que debería escucharse una señal, en lugar de donde aparece su portadora.

## Antes de comenzar

- Signal History debe estar habilitado (consulte [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)).

## Pasos

1. Abra **Settings > SpotHub...**.
2. Haga clic en la pestaña **Display**.
3. Desplácese hasta la sección **Signal History**.
4. Haga clic en **Snap to Step** para habilitarlo (el interruptor se rellena de verde cuando está marcado).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Snap to Step | Deshabilitado | Activado / Desactivado | `SHistorySnapToStep` |

## Consejos

- Snap to Step solo afecta los clics en los marcadores de Signal History; no cambia la forma en que la franja sintoniza al hacer clic directamente en el espectro.

## Solución de problemas

- **Al hacer clic en un marcador, aún se sintoniza la frecuencia exacta de la portadora** — Asegúrese de que el interruptor **Snap to Step** muestre un relleno verde. Si todavía está gris, haga clic una vez para activarlo.

## Relacionado

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm-gate-and-edge-threshold.md)
