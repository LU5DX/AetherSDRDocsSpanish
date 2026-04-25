# Cambiar el estimador de potencia de ruido NR2 (OSMS/MMSE/NSTAT)

El estimador de potencia de ruido (NPE) de NR2 determina cómo el motor NR2 de AetherSDR mide el nivel de ruido de fondo. Cambiar entre OSMS, MMSE y NSTAT le permite adaptar el estimador al tipo de ruido con el que está trabajando.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar este ajuste.
- NR2 debe estar activo en su slice para que el cambio tenga un efecto audible.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. En el cuadro de diálogo AetherDSP Settings, haga clic en la pestaña **NR2**.
3. En **NPE Method**, haga clic en uno de los tres botones de opción: **OSMS**, **MMSE** o **NSTAT**.

El ajuste surte efecto de inmediato y se guarda automáticamente en `NR2NpeMethod`.

## Qué hace cada control

| Control | Tipo | Predeterminado | Valores válidos | Clave de ajuste | Comportamiento |
|---|---|---|---|---|---|
| NPE Method — **OSMS** | botón de opción | ✓ predeterminado | — | `NR2NpeMethod` = 0 | Optimal Smoothing Minimum Statistics. Rastrea el nivel de ruido de fondo mediante una estimación de mínimo continuo. Ideal para ruido estable y estacionario. |
| NPE Method — **MMSE** | botón de opción | — | — | `NR2NpeMethod` = 1 | Minimum Mean Squared Error. Minimiza el error esperado en la estimación del ruido. Una opción equilibrada para condiciones mixtas. |
| NPE Method — **NSTAT** | botón de opción | — | — | `NR2NpeMethod` = 2 | Non-Stationary estimation. Se adapta a ruido que cambia rápidamente con el tiempo, como QRM cuya naturaleza varía. |

`NR2NpeMethod` se almacena como un entero: 0 = OSMS, 1 = MMSE, 2 = NSTAT.

## Consejos

- OSMS es el valor predeterminado y funciona bien para ruido atmosférico o de banda constante.
- Si el nivel de ruido de fondo varía con rapidez (por ejemplo, al cambiar de estación o al cambiar las condiciones de la banda), pruebe NSTAT, que se readapta de forma más agresiva.
- MMSE es un término medio: tiende a dejar menos ruido residual que OSMS en condiciones moderadas, sin los artefactos de variación rápida que NSTAT puede introducir.
- Para restaurar todos los parámetros de NR2 a sus valores predeterminados (incluido NPE Method de vuelta a OSMS), haga clic en **Reset Defaults** en la parte inferior de la pestaña **NR2**.

## Relacionado

- [Ajustar la profundidad de reducción NR2 y el umbral de voz](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Restablecer los parámetros de NR2 o NR4 a sus valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
