# Habilitar MNR en macOS y ajustar su intensidad

MNR es el motor de reducción de ruido MMSE-Wiener nativo de macOS en AetherSDR, con suavizado de ganancia asimétrico. Use esta página para activarlo y ajustar qué tan agresivamente suprime el ruido.

## Antes de comenzar

- AetherSDR debe estar ejecutándose en macOS. MNR es un motor exclusivo de macOS; el control está presente pero no tiene efecto en otras plataformas.
- No se requiere conexión a una radio para cambiar estos ajustes.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. En el diálogo AetherDSP Settings, haga clic en la pestaña **MNR**.
3. Marque **Enable MNR (macOS only)** para activar el motor.
4. Arrastre el control deslizante **Strength** hasta el nivel deseado. El rango es 0–100; 0 es reducción leve y 100 es el máximo.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| **Enable MNR (macOS only)** | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. | Leído desde el motor de audio al inicio | Activado / Desactivado | `MnrEnabled` |
| **Strength** | Ajusta la agresividad de MNR. | 100 | 0–100 | `MnrStrength` |

`MnrStrength` se almacena como un valor normalizado de 0.00–1.00, independientemente de la escala de visualización 0–100 del control deslizante.

## Consejos

- Comience con **Strength** en 100 y redúzcalo si nota artefactos en la voz o un sonido poco natural. Los valores más bajos intercambian algo de supresión de ruido por un audio más natural.

## Solución de problemas

- **Enable MNR (macOS only) no tiene efecto** — MNR es un motor exclusivo de macOS. En Linux o Windows, la casilla es visible pero el motor no se ejecuta.
- **Los ajustes no persisten después de reiniciar** — Verifique que AetherSDR tenga acceso de escritura al almacenamiento de sus ajustes. Tanto `MnrEnabled` como `MnrStrength` se guardan automáticamente cuando los modifica.

## Relacionado

- [Cómo elegir la reducción de ruido correcta: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de AetherDSP Settings](overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
