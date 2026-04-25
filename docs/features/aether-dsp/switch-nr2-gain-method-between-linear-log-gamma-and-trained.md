# Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained

El método de ganancia de NR2 controla cómo AetherSDR aplica la ganancia estimada de reducción de ruido sobre la señal de audio. Elegir el método adecuado afecta el equilibrio entre la supresión de ruido y la naturalidad de la voz.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a un radio para cambiar esta configuración.
- NR2 debe estar activo en el slice que desea afectar.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. En **Gain Method**, haga clic en uno de los cuatro botones de opción: **Linear**, **Log**, **Gamma** o **Trained**.
4. Cierre el cuadro de diálogo. La configuración surte efecto de inmediato y se guarda automáticamente.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Valores válidos | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| **Gain Method** | Botones de opción | Gamma | Linear, Log, Gamma, Trained | `NR2GainMethod` | Selecciona la curva de ganancia utilizada por NR2. Se almacena como entero 0–3 según el orden indicado. |

**Opciones de Gain Method:**

- **Linear** — Aplica la ganancia en una escala de amplitud lineal. Directa, sin compresión del rango dinámico.
- **Log** — Utiliza una escala de amplitud logarítmica, comprimiendo el rango dinámico de la ganancia aplicada.
- **Gamma** — Modela la amplitud de la voz como una distribución Gamma. Es el valor predeterminado y se adapta bien a los patrones de voz típicos.
- **Trained** — Utiliza un modelo de reducción de ruido entrenado con muestras reales de voz y ruido.

## Consejos

- **Gamma** es el valor predeterminado y funciona bien para la mayoría de los contactos de voz en SSB. Comience aquí si no está seguro.
- **Trained** puede sonar más natural con voz clara, pero puede comportarse de forma diferente con señales muy distorsionadas o débiles.
- **Log** reduce la agresividad de las transiciones de ganancia y puede ser útil si **Gamma** o **Trained** producen un efecto de bombeo audible.
- Haga clic en **Reset Defaults** en la pestaña NR2 para devolver **Gain Method** a **Gamma** junto con todos los demás parámetros de NR2.

## Solución de problemas

- **Cambiar el método de ganancia no produce ningún efecto audible** — Confirme que NR2 está habilitado en el slice activo. El cuadro de diálogo AetherDSP Settings solo ajusta parámetros; NR2 debe activarse por separado desde los controles del slice.
- **La voz suena distorsionada después de cambiar a Trained** — Intente reducir **Reduction Depth:** desde su valor predeterminado de 1.50 o aumente ligeramente **Voice Threshold:**. Consulte [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md).

## Temas relacionados

- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el estimador de potencia de ruido de NR2 (OSMS/MMSE/NSTAT)](change-nr2-noise-power-estimator-osms-mmse-nstat.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
