# Habilitar MNR en macOS y ajustar su intensidad

MNR es el motor de reducción de ruido MMSE-Wiener de AetherSDR, disponible únicamente en macOS. Esta página muestra cómo activarlo y ajustar la agresividad con la que suprime el ruido.

## Antes de comenzar

- AetherSDR debe estar ejecutándose en macOS. La casilla "Enable MNR (macOS only)" está presente en todas las plataformas, pero el procesamiento MNR es exclusivo de macOS.
- No se requiere conexión a la radio para abrir AetherDSP Settings.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. En el diálogo **AetherDSP Settings**, haga clic en la pestaña **MNR**.
3. Marque **Enable MNR (macOS only)** para activar el motor.
4. Arrastre el control deslizante **Strength** para ajustar la agresividad. El valor predeterminado es 100 (máximo). Los valores más bajos reducen la supresión.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Enable MNR (macOS only) | Casilla | *(leído del motor de audio al iniciar)* | On / Off | `MnrEnabled` |
| Strength | Control deslizante | 100 | 0–100 | `MnrStrength` |

**Strength** se almacena internamente como un valor normalizado de 0.00–1.00. El control deslizante lo muestra en una escala de 0–100. Un valor de 0 aplica reducción de ruido mínima; 100 aplica supresión máxima.

## Consejos

- Los cambios en **Strength** surten efecto de inmediato sin necesidad de reiniciar AetherSDR ni reconectarse a la radio.
- Si desea una reducción más suave, ajuste **Strength** a un valor entre 30 y 60 para reducir el ruido preservando mayor naturalidad en la voz.

## Solución de problemas

- **La casilla "Enable MNR (macOS only)" es visible pero no tiene efecto** — El procesamiento MNR es exclusivo de macOS. Si está ejecutando AetherSDR en Linux o Windows, la casilla aparecerá pero el motor no se activará.

## Relacionados

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz en NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Establecer el límite de atenuación de DeepFilterNet3 para señales fuertes o débiles](set-deepfilternet3-attenuation-limit-for-strong-or-weak-signals.md)
