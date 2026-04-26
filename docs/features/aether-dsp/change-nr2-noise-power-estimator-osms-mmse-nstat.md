# Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)

El estimador de potencia de ruido (NPE) de NR2 controla cómo el motor NR2 de AetherSDR mide el piso de ruido antes de aplicar la supresión. Cambiar entre OSMS, MMSE y NSTAT puede mejorar la calidad de la reducción de ruido según si el ruido en su banda es estacionario, varía lentamente o cambia con rapidez.

## Antes de comenzar

- No se requiere conexión con el equipo. Los ajustes DSP de AetherSDR se aplican localmente y pueden modificarse con el equipo desconectado.
- NR2 debe estar activo en su slice para que los cambios sean audibles. La activación de NR2 se realiza desde los controles del slice, no desde este diálogo.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. En el grupo **NPE Method**, seleccione uno de los tres botones de opción: **OSMS**, **MMSE** o **NSTAT**.
4. Cierre el diálogo. El ajuste surte efecto de inmediato y se guarda automáticamente.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Valores válidos | Clave de ajuste |
|---|---|---|---|---|
| **OSMS** | Optimal Smoothing Minimum Statistics — rastrea el piso de ruido usando una estimación de mínimo continuo. Adecuado para ruido estacionario o con deriva lenta. | ✓ (predeterminado) | — | `NR2NpeMethod` = 0 |
| **MMSE** | Minimum Mean Squared Error — minimiza el error esperado en la estimación del ruido. Tiende a preservar la voz de forma más conservadora. | — | — | `NR2NpeMethod` = 1 |
| **NSTAT** | Non-Stationary estimation — se adapta al ruido que cambia con el tiempo. Apropiado para bandas con interferencia impulsiva o que varía rápidamente. | — | — | `NR2NpeMethod` = 2 |

El ajuste `NR2NpeMethod` se almacena como número entero: 0 = OSMS, 1 = MMSE, 2 = NSTAT.

## Consejos

- Comience con **OSMS** (el valor predeterminado) en la mayoría de las bandas HF donde el ruido de fondo es relativamente estable. Cambie a **NSTAT** si el piso de ruido fluctúa o las condiciones de la banda cambian con rapidez.
- Si desea restaurar todos los parámetros de NR2 a su estado original, haga clic en **Reset Defaults** en la pestaña NR2. Esto restablece el método NPE a **OSMS** junto con los demás valores predeterminados de NR2.

## Relacionados

- [Descripción general de AetherDSP Settings](overview.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
