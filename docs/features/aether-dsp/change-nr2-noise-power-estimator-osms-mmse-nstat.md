# Cambiar el estimador de potencia de ruido NR2 (OSMS/MMSE/NSTAT)

El estimador de potencia de ruido (NPE) de NR2 controla cómo el motor NR2 de AetherSDR mide el piso de ruido antes de aplicar ganancia. Cambiar entre OSMS, MMSE y NSTAT permite adaptar el estimador al tipo de ruido con el que se trabaja: estable, promediado o de variación rápida.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar esta configuración.
- NR2 debe estar activo en su slice para que el cambio tenga efecto audible.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. En el grupo **NPE Method**, haga clic en uno de los tres botones de opción: **OSMS**, **MMSE** o **NSTAT**.

La selección surte efecto de inmediato y se guarda en `NR2NpeMethod`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Valores válidos | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| **NPE Method** | Botones de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido utilizado por NR2. Se almacena como entero 0–2. |

**OSMS** — Optimal Smoothing Minimum Statistics. Rastrea el piso de ruido mediante una estimación de mínimo continuo. Ideal para ruido estable y de variación lenta.

**MMSE** — Minimum Mean Squared Error. Minimiza el error esperado en la estimación del ruido. Una opción equilibrada de propósito general.

**NSTAT** — Non-Stationary estimation. Se adapta al ruido que cambia con el tiempo. Úselo cuando el ruido de fondo sea variable o intermitente.

## Consejos

- Si escucha artefactos de ruido musical tras cambiar de estimador, habilite **AE Filter (artifact elimination)** en la misma pestaña. Su clave de configuración es `NR2AeFilter` y está activado de forma predeterminada.
- Si cambia el método NPE y no queda satisfecho, haga clic en **Reset Defaults** en la pestaña NR2 para restaurar OSMS junto con todos los demás parámetros de NR2 a sus valores predeterminados (Gamma / OSMS / AE activado / 1.50 / 0.85 / 0.20).

## Relacionados

- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
