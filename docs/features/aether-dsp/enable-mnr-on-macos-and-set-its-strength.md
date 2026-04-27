# Habilitar MNR en macOS y ajustar su intensidad

MNR es el motor de reducción de ruido MMSE-Wiener de AetherSDR, disponible únicamente en macOS. Esta página muestra cómo activarlo y ajustar el nivel de agresividad con que suprime el ruido.

## Antes de comenzar

- AetherSDR debe estar ejecutándose en macOS. La casilla "Enable MNR (macOS only)" solo aparece en las versiones para macOS.
- No se requiere conexión a la radio para ajustar estos parámetros.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. En el diálogo **AetherDSP Settings**, haga clic en la pestaña **MNR**.
3. Marque **Enable MNR (macOS only)** para activar el motor.
4. Arrastre el control deslizante **Strength** para ajustar la agresividad. 0 es la configuración más suave; 100 es la reducción de ruido máxima.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Enable MNR (macOS only) | Casilla | *(leído del motor de audio al inicio)* | Activado / Desactivado | `MnrEnabled` |
| Strength | Control deslizante | 100 | 0–100 | `MnrStrength` |

`MnrStrength` se almacena internamente como un valor normalizado entre 0.00 y 1.00.

## Consejos

- Comience con **Strength** en 100 y redúzcalo si nota artefactos en la voz o un sonido hueco. Los valores más bajos sacrifican supresión de ruido a cambio de una reproducción de voz más natural.
- Dado que el estado inicial de habilitación de MNR se lee en tiempo real desde el motor de audio al abrir el diálogo, la casilla refleja el estado actual del motor en lugar de un valor predeterminado guardado fijo.

## Solución de problemas

- **La pestaña MNR es visible pero "Enable MNR (macOS only)" no tiene efecto** — confirme que está ejecutando AetherSDR en macOS. La etiqueta de la casilla indica explícitamente que la disponibilidad es exclusiva de macOS; en otras plataformas el motor no está activo independientemente de esta configuración.

## Relacionado

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de AetherDSP Settings](overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
