# Habilitar Snap to Step para una sintonización precisa del Historial de Señales

Snap to Step redondea la sintonización por clic del Historial de Señales al múltiplo más cercano del tamaño de paso de la franja activa, ocultando pequeños desplazamientos de portadora. Actívelo cuando desee sintonizar con precisión la frecuencia en la que debería escucharse una señal, en lugar de donde aparece su portadora.

## Antes de comenzar

- El Historial de Señales debe estar habilitado (consulte [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)).

## Pasos

1. Abra **Settings > SpotHub...**.
2. Haga clic en la pestaña **Display**.
3. Desplácese hasta la sección **Signal History**.
4. Haga clic en **Snap to Step** para activarlo (el control se vuelve verde cuando está marcado).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Snap to Step | Deshabilitado | Activado / Desactivado | `SHistorySnapToStep` |

## Consejos

- Snap to Step solo afecta los clics en los marcadores del Historial de Señales; no cambia la forma en que la franja sintoniza al hacer clic directamente en el espectro.
- El control deslizante Filter Match Window y los controles deslizantes Edge Threshold, Marker Lifetime y QRM Gate admiten doble clic izquierdo para restablecer su valor predeterminado almacenado.
- El diálogo SpotHub ahora utiliza los colores de su tema actual para las etiquetas de estado y el estilo de las pestañas. El estado Conectado aparece en el color de acento, Desconectado en el color de etiqueta y los mensajes de error en el color de acento de peligro.

## Solución de problemas

- **Al hacer clic en un marcador, aún sintoniza la frecuencia exacta de la portadora**: asegúrese de que el control **Snap to Step** muestre un relleno verde. Si aún está gris, haga clic una vez para activarlo.

## Relacionados

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm-gate-and-edge-threshold.md)
