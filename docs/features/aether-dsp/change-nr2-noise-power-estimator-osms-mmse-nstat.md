# Cambiar el estimador de potencia de ruido NR2 (OSMS/MMSE/NSTAT)

El estimador de potencia de ruido (NPE) de NR2 controla cómo el motor NR2 de AetherSDR mide el piso de ruido de fondo antes de aplicar la reducción de ganancia. Cambiar entre OSMS, MMSE y NSTAT modifica la forma en que el estimador rastrea el ruido, lo que afecta la calidad de la supresión en fuentes de ruido estacionarias frente a las que cambian rápidamente.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- NR2 debe estar activo en un receptor para que los cambios tengan efecto audible de inmediato.

## Pasos

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR2**.
3. En el grupo **NPE Method**, seleccione uno de los tres botones de opción: **OSMS**, **MMSE** o **NSTAT**.

La configuración surte efecto de inmediato y se guarda automáticamente en `NR2NpeMethod`.

## Función de cada control

| Control                         | Tipo                                                                                                      | Valor predeterminado                                                                                         |
|---------------------------------|-----------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| **Gain Method**                 | Botón de opción (Linear, Log, Gamma, Trained)                                                              | Gamma                                                                                                         |
| **NPE Method** — **OSMS**       | Botón de opción                                                                                           | Predeterminado (0)                                                                                            |
| **NPE Method** — **MMSE**       | Botón de opción                                                                                           | —                                                                                                             |
| **NPE Method** — **NSTAT**      | Botón de opción                                                                                           | —                                                                                                             |
| **AE Filter (eliminación de artefactos)** | Casilla de verificación                                                                              | True                                                                                                          |
| Reduction:                      | Deslizador, 0.50–2.00                                                                                     | 1.50                                                                                                          |
| Smoothing:                      | Deslizador, 0.50–0.98                                                                                     | 0.85                                                                                                          |
| Threshold:                      | Deslizador, 0.05–0.50                                                                                     | 0.20                                                                                                          |
| Reset Defaults (icono ↺)       | Restaura los valores predeterminados de NR2 (Gamma/OSMS/AE activado, 1.50/0.85/0.20).                     | Se representa como un botón de icono plano que muestra una flecha en sentido antihorario (U+21BA).            |
| Barra de título — AetherDSP Settings | Barra de título degradada de 18 px sin marco con glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. | Coincide con la familia de estilo de NetworkDiagnosticsDialog y AetherialAudioStrip. Añadido en v0.9.8 (refactorización #2425). |
| — (Minimizar)                   | Minimiza el diálogo.                                                                                      |                                                                                                               |
| □ (Maximizar)                   | Maximiza o restaura el diálogo.                                                                          |                                                                                                               |
| × (Cerrar)                      | Cierra el diálogo.                                                                                        |                                                                                                               |
| NR4 (pestaña)                   | Selecciona la página NR4 (libspecbleach).                                                                 |                                                                                                               |
| Noise Estimation:               | Botón de opción (MMSE, Brandt, Martin)                                                                    | MMSE                                                                                                          |
| Adaptive Noise Estimation       | Casilla de verificación                                                                                   | True                                                                                                          |
| Reduction (dB):                 | Deslizador, 0.0–40.0                                                                                      | 10.0                                                                                                          |
| Smoothing (%):                  | Deslizador, 0–100                                                                                         | 0                                                                                                             |
| Whitening (%):                  | Deslizador, 0–100                                                                                         | 0                                                                                                             |
| Masking Depth:                  | Deslizador, 0.00–1.00                                                                                     | 0.50                                                                                                          |
| Suppression:                    | Deslizador, 0.00–1.00                                                                                     | 0.50                                                                                                          |
| Reset Defaults (icono ↺)       | Restaura los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50).          | Se representa como un botón de icono plano que muestra una flecha en sentido antihorario (U+21BA).            |
| MNR (pestaña)                   | Selecciona la página MNR (macOS MMSE-Wiener). La alternancia MNR está atenuada en compilaciones Windows/Linux — el motor no tiene backend en esas plataformas. |                                               |
| Enable MNR (solo macOS)        | Casilla de verificación                                                                                   | Se lee en vivo desde AudioEngine                                                                              |
| Strength                        | Deslizador, 0–100                                                                                         | 100                                                                                                           |
| RN2 (pestaña)                   | Selecciona la página RN2 (RNNoise) — puramente informativa, sin parámetros ajustables.                    |                                                                                                               |
| BNR (pestaña)                   | Selecciona la página BNR (NVIDIA) — la intensidad se controla desde el menú superpuesto. La alternancia BNR está atenuada en compilaciones sin el SDK de NVIDIA Broadcast. |                                                                               |
| DFNR (pestaña)                  | Selecciona la página DeepFilterNet3.                                                                      |                                                                                                               |
| Attenuation Limit               | Deslizador, 0–100 dB                                                                                      | 100                                                                                                           |
| Post-Filter Beta                | Deslizador, 0.00–0.30                                                                                     | 0.00                                                                                                          |
| Arrastrar para mover            | Haga clic y arrastre la barra de título para mover el diálogo.                                           | Haga doble clic en la barra de título para alternar entre maximizar y restaurar.                              |
| Redimensionamiento de 8 ejes    | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. | Zona de redimensionamiento de 6 px alrededor del widget de contenido interno.                                 |

`NR2NpeMethod` se almacena como un entero: OSMS = 0, MMSE = 1, NSTAT = 2.

## Notas

- Los seis conmutadores DSP (NR2, NR4, MNR, DFNR, RN2, BNR) actúan como selectores exclusivos y controles de activación/desactivación del motor. Cuando se activa NR2, AudioEngine aplica una exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.
- El diálogo ahora usa `PersistentDialog`, que guarda y restaura automáticamente su geometría entre sesiones. La posición y el tamaño del diálogo se conservan mediante la clave de configuración `AetherDspDialogGeometry`.

## Consejos

- OSMS es el valor predeterminado y funciona bien para ruido de fondo constante, como el silbido atmosférico o el ruido blanco del propio receptor.
- NSTAT es un mejor punto de partida cuando el piso de ruido cambia rápidamente, por ejemplo, durante un concurso con condiciones de banda variables o interferencia intermitente.
- Si cambiar el método NPE introduce más artefactos de ruido musical, active **AE Filter (eliminación de artefactos)** en la misma pestaña.
- Haga clic en **Reset Defaults** en la pestaña NR2 para volver a OSMS junto con todos los demás parámetros de NR2 a la vez.

## Solución de problemas

- **Cambiar el método NPE no produce diferencia audible** — Confirme que NR2 está habilitado en el receptor. El diálogo AetherDSP Settings ajusta los parámetros pero no activa NR2 por sí mismo; NR2 debe activarse desde los controles del receptor.
- **NSTAT introduce más ruido residual que OSMS** — NSTAT intercambia precisión del piso por una adaptación más rápida. Reduzca **Reduction:** o aumente **Smoothing:** en la pestaña NR2 para compensar.

## Relacionados

- [Ajustar la profundidad de reducción y el umbral de voz de NR2](tune-nr2-reduction-depth-and-voice-threshold.md)
- [Cambiar el método de ganancia de NR2 entre Linear, Log, Gamma y Trained](switch-nr2-gain-method-between-linear-log-gamma-and-trained.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
