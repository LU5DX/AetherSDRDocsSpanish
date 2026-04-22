# Cambiar el estimador de potencia de ruido NR2 (OSMS/MMSE/NSTAT)

El estimador de potencia de ruido (NPE) de NR2 determina cómo AetherSDR modela el piso de ruido de fondo antes de aplicar la reducción de ganancia. Cambiar entre OSMS, MMSE y NSTAT puede mejorar la supresión de ruido en señales cuyo carácter de ruido es estacionario, varía lentamente o cambia de forma rápida.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para cambiar esta configuración.
- La reducción de ruido NR2 debe estar activa en un receptor slice para que el cambio tenga efecto audible.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. En **NPE Method**, haga clic en uno de los tres botones de opción: **OSMS**, **MMSE** o **NSTAT**.
4. La configuración surte efecto de inmediato y se guarda automáticamente en `NR2NpeMethod`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Valores válidos | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| **NPE Method** | Botón de opción | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido utilizado por NR2. Se almacena como entero 0 (OSMS), 1 (MMSE) o 2 (NSTAT). |

**OSMS** — Estadísticas mínimas con suavizado óptimo. Rastrea el piso de ruido mediante una estimación de mínimo continuo. Funciona bien con ruido estacionario o que cambia lentamente, típico del ruido de banda e interferencias.

**MMSE** — Error cuadrático medio mínimo. Minimiza el error de estimación de ruido esperado. Generalmente produce curvas de ganancia más suaves y puede reducir los artefactos de ruido musical en señales de voz.

**NSTAT** — Estimación no estacionaria. Se adapta al ruido que cambia con el tiempo. Utilícelo cuando haya ráfagas de ruido, QRM u otras interferencias que varíen rápidamente.

## Consejos

- Si escucha ruido musical o borboteo residual después de que NR2 procesa una señal, intente cambiar de OSMS a MMSE y, a continuación, active **AE Filter (artifact elimination)** si no está marcado todavía.
- En condiciones de pile-up o concurso donde las interferencias cambian rápidamente, NSTAT puede rastrear el piso de ruido con mayor precisión que OSMS.
- Cambiar el método NPE interactúa con el control deslizante **Smoothing:** (`NR2GainSmooth`, valor predeterminado 0.85). Un valor de suavizado más bajo permite que cualquier estimador se adapte más rápido; un valor más alto lo estabiliza.
- Para restaurar OSMS junto con todos los demás valores predeterminados de NR2, haga clic en **Reset Defaults** en la pestaña NR2.

## Relacionados

- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
