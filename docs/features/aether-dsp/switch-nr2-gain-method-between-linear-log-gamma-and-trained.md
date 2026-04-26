# Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained

El método de ganancia de NR2 controla cómo AetherSDR mapea el piso de ruido estimado hacia una curva de ganancia de supresión. Cambiar esta configuración permite equilibrar entre voz de sonido natural y eliminación agresiva de ruido.

## Antes de comenzar

- No se requiere conexión a radio. El diálogo AetherDSP Settings funciona sin conexión.
- NR2 debe estar activo en su receptor para que los cambios sean audibles.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. En el grupo **Gain Method**, haga clic en uno de los cuatro botones de opción: **Linear**, **Log**, **Gamma** o **Trained**.
4. Cierre el diálogo. La configuración surte efecto de inmediato y se guarda automáticamente.

## Qué hace cada control

| Control | Tipo | Predeterminado | Valores válidos | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| **Gain Method** | Botones de opción | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` | Selecciona el mapeo de curva de ganancia utilizado por NR2. Se almacena como entero 0–3 según el orden mostrado. |

### Descripciones de los métodos de ganancia

- **Linear** — Aplica una escala de amplitud de audio lineal al cálculo de ganancia.
- **Log** — Utiliza una escala de amplitud logarítmica, comprimiendo el rango dinámico.
- **Gamma** — Modela los patrones de amplitud de voz mediante una distribución Gamma. Es el valor predeterminado y se adapta bien al trabajo en SSB y CW.
- **Trained** — Aplica un modelo de reducción de ruido entrenado con muestras reales de voz y ruido.

## Consejos

- **Gamma** es el valor predeterminado de fábrica y funciona bien para señales SSB típicas. Pruebe **Log** si Gamma suprime en exceso las estaciones débiles.
- **Trained** puede rendir mejor en señales con ruido de fondo constante, pero puede sonar menos natural con pisos de ruido que varían rápidamente.
- Si cambia el método de ganancia y la voz suena peor, haga clic en **Reset Defaults** para restaurar Gamma junto con todos los demás parámetros de NR2.

## Solución de problemas

- **Los botones de opción de Gain Method aparecen pero cambiarlos no tiene efecto** — Verifique que NR2 esté habilitado en el receptor. La configuración del método de ganancia se guarda de todas formas, pero solo se aplica cuando NR2 está activo.

## Relacionados

- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
