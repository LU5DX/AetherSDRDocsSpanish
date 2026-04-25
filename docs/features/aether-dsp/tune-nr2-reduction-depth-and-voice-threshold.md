# Ajustar la profundidad de reducción y el umbral de voz de NR2

Configure qué tan agresivamente NR2 suprime el ruido y con qué sensibilidad detecta la voz. Estos dos controles establecen el balance entre la máxima eliminación de ruido y la preservación de pasajes de voz débiles.

## Antes de comenzar

- AetherSDR no necesita estar conectado a un equipo de radio para cambiar estos ajustes.
- NR2 debe estar activo en su slice para que los cambios sean audibles.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...` para abrir el diálogo AetherDSP Settings.
2. Haga clic en la pestaña **NR2**.
3. Localice el control deslizante **Reduction Depth:**. Arrástrelo hacia la izquierda para reducir la supresión o hacia la derecha para aumentarla. El valor predeterminado es **1.50**; el rango válido es **0.50–2.00**.
4. Localice el control deslizante **Voice Threshold:**. Arrástrelo hacia la izquierda para detectar voz más débil (puede pasar más ruido) o hacia la derecha para elevar el umbral (mayor supresión entre ráfagas de voz). El valor predeterminado es **0.20**; el rango válido es **0.05–0.50**.
5. Escuche el audio recibido y ajuste ambos controles deslizantes hasta que el balance entre supresión de ruido y claridad de voz sea aceptable.
6. Para deshacer todos los cambios en esta pestaña, haga clic en **Reset Defaults**. Esto restaura Reduction Depth a **1.50** y Voice Threshold a **0.20**, junto con todos los demás valores predeterminados de NR2.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste persistente |
|---|---|---|---|
| Control deslizante **Reduction Depth:** | 1.50 | 0.50–2.00 | `NR2GainMax` |
| Control deslizante **Smoothing:** | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| Control deslizante **Voice Threshold:** | 0.20 | 0.05–0.50 | `NR2Qspp` |
| Casilla **AE Filter (artifact elimination)** | Habilitada | — | `NR2AeFilter` |
| Botones de opción **Gain Method** | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| Botones de opción **NPE Method** | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| Botón **Reset Defaults** | — | — | — |

**Reduction Depth:** Establece la reducción de ganancia máxima que NR2 puede aplicar. Los valores más altos suprimen más ruido, pero aumentan el riesgo de distorsión de la voz.

**Smoothing:** Controla la rapidez con que la estimación de ruido sigue los cambios en el piso de ruido. Los valores más altos producen una adaptación más estable pero más lenta.

**Voice Threshold:** Establece el umbral de probabilidad de presencia de voz. Los valores más bajos hacen que NR2 trate más señal como voz y reduzca la supresión; los valores más altos aumentan la supresión durante las pausas.

**AE Filter (artifact elimination):** Aplica un postfiltro que reduce los artefactos de resonancia y ruido musical. Déjelo habilitado a menos que esté comparando la salida bruta de NR2.

## Consejos

- En una banda tranquila con ruido de fondo estable, un **Reduction Depth:** de 1.50–2.00 y un **Voice Threshold:** de 0.15–0.25 funciona bien para la mayoría de las señales SSB.
- Si las estaciones débiles se cortan al inicio de las sílabas, reduzca **Voice Threshold:** hacia 0.05 para que NR2 se abra más rápido.
- Si aparece ruido musical (artefactos tonales) tras aumentar **Reduction Depth:**, verifique que **AE Filter (artifact elimination)** esté marcado.
- Aumentar **Smoothing:** puede ayudar con pisos de ruido estables (interferencia RTTY, zumbido de la red eléctrica), pero ralentiza la reacción de NR2 ante cambios de ruido rápidos.

## Resolución de problemas

- **Los cambios en el control deslizante no tienen efecto audible** — NR2 puede no estar habilitado en el slice activo. Habilítelo desde los controles del slice y luego regrese a este diálogo.
- **La voz suena distorsionada o robótica** — **Reduction Depth:** está configurado demasiado alto. Redúzcalo hacia 1.00–1.50 y confirme que **AE Filter (artifact elimination)** esté marcado.
- **El ruido se filtra entre palabras** — **Voice Threshold:** puede estar demasiado bajo. Auméntelo gradualmente hacia 0.30–0.40 para que NR2 aplique mayor supresión durante las pausas.

## Temas relacionados

- [Elegir la reducción de ruido correcta: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
