# Activar MNR en macOS y ajustar su intensidad

MNR (reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico) es un motor de reducción de ruido exclusivo de macOS integrado en la cadena de audio de AetherSDR. Esta página explica cómo activarlo y ajustar con qué agresividad suprime el ruido.

## Antes de comenzar

- Debe estar ejecutando AetherSDR en macOS. La casilla "Enable MNR (macOS only)" no tiene efecto en Linux ni en Windows.
- No se requiere una conexión de radio para cambiar estos ajustes.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...` para abrir el diálogo AetherDSP Settings.
2. Haga clic en la pestaña **MNR**.
3. Marque **Enable MNR (macOS only)** para activar el motor.
4. Arrastre el control deslizante **Strength** para definir con qué agresividad MNR suprime el ruido. El valor predeterminado es 100 (máximo). Muévalo hacia la izquierda para reducir la agresividad y conservar más del carácter original del audio.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| Enable MNR (macOS only) | Casilla | *(leído del motor de audio al inicio)* | Activado / Desactivado | `MnrEnabled` |
| Strength | Deslizador | 100 | 0–100 | `MnrStrength` |

**Enable MNR (macOS only)** — Activa la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. El estado inicial de la casilla refleja el estado en vivo del motor de audio en el momento en que se abre el diálogo.

**Strength** — Controla la agresividad de MNR. 0 corresponde a supresión leve; 100 corresponde a supresión máxima. El valor se almacena internamente como una cifra normalizada de 0.00 a 1.00.

## Consejos

- Comience con **Strength** cerca de 100 y redúzcalo si nota que la señal suena hueca o excesivamente procesada. Las voces se vuelven más suaves al disminuir la agresividad.
- Dado que el estado inicial de **Enable MNR (macOS only)** se lee en vivo desde el motor de audio, puede diferir de lo que guardó por última vez si el estado del motor cambió al inicio.

## Temas relacionados

- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Descripción general de AetherDSP Settings](overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
