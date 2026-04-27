# Cambiar el estimador de potencia de ruido NR2 (OSMS/MMSE/NSTAT)

El estimador de potencia de ruido (NPE) de NR2 controla cómo el motor NR2 de AetherSDR mide el nivel de ruido de fondo antes de aplicar la reducción de ganancia. Cambiar entre OSMS, MMSE y NSTAT modifica la forma en que el estimador rastrea el ruido, lo que afecta la calidad de supresión en fuentes de ruido estacionarias frente a fuentes que cambian rápidamente.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar este ajuste.
- NR2 debe estar activo en un receptor para que los cambios surtan efecto audible de inmediato.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. En el grupo **NPE Method**, seleccione uno de los tres botones de opción: **OSMS**, **MMSE** o **NSTAT**.

El ajuste surte efecto de inmediato y se guarda automáticamente en `NR2NpeMethod`.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---|---|---|---|---|---|
| **NPE Method** — **OSMS** | Botón de opción | Predeterminado (0) | — | `NR2NpeMethod` | Optimal Smoothing Minimum Statistics. Rastrea el nivel de ruido de fondo mediante una estimación de mínimo continuo. Adecuado para ruido estable y estacionario. |
| **NPE Method** — **MMSE** | Botón de opción | — | — | `NR2NpeMethod` | Minimum Mean Squared Error. Minimiza el error esperado en la estimación del ruido. Buena opción de uso general. |
| **NPE Method** — **NSTAT** | Botón de opción | — | — | `NR2NpeMethod` | Non-Stationary estimation. Se adapta al ruido que cambia con el tiempo, como QRM o interferencia variable. |

`NR2NpeMethod` se almacena como un entero: OSMS = 0, MMSE = 1, NSTAT = 2.

## Consejos

- OSMS es el valor predeterminado y funciona bien para ruido de fondo constante, como el siseo atmosférico o el ruido blanco del propio receptor.
- NSTAT es el mejor punto de partida cuando el nivel de ruido de fondo cambia rápidamente, por ejemplo, durante un concurso con condiciones de banda variables o interferencia intermitente.
- Si al cambiar el método NPE se introducen más artefactos de ruido musical, habilite **AE Filter (artifact elimination)** en la misma pestaña.
- Haga clic en **Reset Defaults** en la pestaña NR2 para volver a OSMS junto con todos los demás parámetros de NR2 a la vez.

## Solución de problemas

- **Cambiar el método NPE no produce ninguna diferencia audible** — Confirme que NR2 está habilitado en el receptor. El diálogo AetherDSP Settings ajusta los parámetros, pero no activa NR2 por sí mismo; NR2 debe activarse desde los controles del receptor.
- **NSTAT introduce más ruido residual que OSMS** — NSTAT sacrifica la precisión del nivel de fondo a favor de una adaptación más rápida. Reduzca **Reduction Depth:** o aumente **Smoothing:** en la pestaña NR2 para compensar.

## Relacionados

- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
