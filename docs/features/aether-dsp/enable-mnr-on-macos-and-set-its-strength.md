# Activar MNR en macOS y ajustar su intensidad

MNR es un motor de reducción de ruido MMSE-Wiener disponible únicamente en macOS. Use esta página para activarlo y ajustar con qué agresividad suprime el ruido.

## Antes de comenzar

- AetherSDR debe estar ejecutándose en macOS. La casilla "Enable MNR (macOS only)" no tiene efecto en Linux ni en Windows.
- No se requiere conexión a una radio para cambiar estos ajustes.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **MNR**.
3. Marque **Enable MNR (macOS only)** para activar el motor.
4. Arrastre el control deslizante **Strength** hasta el nivel deseado. Los valores bajos aplican una reducción de ruido suave; los valores altos aplican la supresión máxima.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| Enable MNR (macOS only) | Activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial se lee desde el motor de audio al abrir el diálogo. | — | On / Off | `MnrEnabled` |
| Strength | Ajusta la agresividad de MNR. 0 es suave; 100 es el máximo. Se almacena internamente como un valor normalizado (0.00–1.00). | 100 | 0–100 | `MnrStrength` |

## Consejos

- Si desea una reducción de ruido que funcione en todas las plataformas, considere usar NR2 o NR4 en su lugar. MNR es exclusivo de macOS y no estará activo en Linux ni en Windows, independientemente del valor guardado en `MnrEnabled`.
- Los cambios surten efecto de inmediato — no hay botón Apply ni OK que presionar.

## Relacionado

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Descripción general de AetherDSP Settings](overview.md)
