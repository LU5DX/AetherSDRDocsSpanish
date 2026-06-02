# Habilitar Snap to Step para sintonización precisa en S-History

Snap to Step redondea la sintonización con clic de S-History al múltiplo más cercano del tamaño de paso de la franja activa, ocultando pequeños desplazamientos de portadora. Actívelo cuando desee sintonizar con precisión la frecuencia donde debería escucharse una señal, en lugar de donde aparece su portadora.

## Antes de empezar

- El historial de señales debe estar habilitado (consulte [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)).

## Pasos

1. Abra **Settings > SpotHub...**.
2. Haga clic en la pestaña **Display**.
3. Desplácese hasta la sección **Signal History**.
4. Haga clic en **Snap to Step** para habilitarlo (el conmutador se llena de verde cuando está marcado).

## Controles

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Snap to Step | Deshabilitado | Activado / Desactivado | `SHistorySnapToStep` |

## Consejos

- Snap to Step solo afecta los clics en los marcadores de Signal History; no cambia la forma en que se sintoniza la franja al hacer clic directamente en el espectro.
- El control deslizante Filter Match Window y los controles deslizantes Edge Threshold, Marker Lifetime y QRM Gate admiten doble clic izquierdo para restablecer su valor predeterminado almacenado.
- El cuadro de diálogo SpotHub ahora usa los colores de su tema actual para las etiquetas de estado y el estilo de las pestañas. El estado Conectado aparece en el color de énfasis, Desconectado en el color de etiqueta y los mensajes de error en el color de énfasis de peligro.

## Solución de problemas

- **Al hacer clic en un marcador, aún se sintoniza la frecuencia exacta de la portadora** — Asegúrese de que el conmutador **Snap to Step** muestre un relleno verde. Si aún está gris, haga clic una vez para habilitarlo.

## Relacionados

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm-gate-and-edge-threshold.md)
