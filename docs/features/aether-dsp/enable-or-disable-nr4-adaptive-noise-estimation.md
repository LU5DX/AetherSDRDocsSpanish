# Configuración de AetherDSP

El diálogo de Configuración de AetherDSP permite ajustar los parámetros avanzados de los motores de reducción de ruido del lado del cliente de AetherSDR (NR2, NR4, MNR, DFNR, RN2, BNR), permitiendo a los operadores encontrar el equilibrio entre la supresión de ruido y la fidelidad de la voz. Los seis módulos DSP se seleccionan mediante una fila de conmutadores en la parte superior; al hacer clic en un conmutador también se activa o desvía ese motor.

## Antes de comenzar

- AetherSDR no necesita estar conectado a una radio para ajustar la configuración DSP.
- El motor NR seleccionado debe estar activo en su slice de recepción para que estos cambios tengan un efecto audible.
- Algunos motores DSP (MNR, BNR, RN2, NR4) dependen de la plataforma o son solo informativos. Para más detalles, consulte [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md).

## Abrir Configuración de AetherDSP

1. Abra `Settings > AetherDSP Settings...`.

Aparece el diálogo con una barra de título degradada de 18 px sin marco que muestra un glifo de agarre (⋮⋮) a la izquierda y el título del diálogo. Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar entre maximizar/restaurar. Haga clic y arrastre cualquier borde o esquina para cambiar el tamaño del diálogo. La zona de ajuste de tamaño de 6 px rodea el widget de contenido interior; el cursor cambia para indicar la dirección del redimensionamiento.

La barra de título contiene tres controles de ventana:
- **— (Minimizar)**: Minimiza el diálogo.
- **□ (Maximizar)**: Maximiza o restaura el diálogo.
- **× (Cerrar)**: Cierra el diálogo.

La geometría del diálogo se guarda automáticamente en la configuración `AetherDspDialogGeometry` y se restaura en el próximo inicio.

## Seleccionar un motor DSP

En la parte superior del diálogo, seis pestañas conmutables actúan tanto como selector como controles de activación/desactivación:

- **NR2** – Motor de reducción de ruido musical
- **NR4** – Supresión de ruido libspecbleach (atenuado en compilaciones de Windows sin LLVM/clang-cl)
- **MNR** – MMSE-Wiener de macOS (atenuado en compilaciones de Windows/Linux)
- **DFNR** – Supresión de ruido neuronal DeepFilterNet3
- **RN2** – RNNoise (solo informativo, sin parámetros ajustables)
- **BNR** – NVIDIA Broadcast (atenuado en compilaciones sin NVIDIA Broadcast SDK)

Haga clic en un conmutador para seleccionar su página de parámetros y activar o desviar ese motor. Cuando se activa NR2, el motor AudioEngine aplica exclusión en cascada, desactivando DFNR y otros módulos mutuamente excluyentes.

## Parámetros de NR2

| Control | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|
| **Método de Ganancia** | Gamma | Linear \| Log \| Gamma \| Trained | `NR2GainMethod` |
| **Método NPE** | OSMS | OSMS \| MMSE \| NSTAT | `NR2NpeMethod` |
| **Filtro AE (eliminación de artefactos)** | Activado (marcado) | Marcado / desmarcado | `NR2AeFilter` |
| **Reducción:** | 1.50 | 0.50–2.00 | `NR2GainMax` |
| **Suavizado:** | 0.85 | 0.50–0.98 | `NR2GainSmooth` |
| **Umbral:** | 0.20 | 0.05–0.50 | `NR2Qspp` |

Haga clic en **Restablecer valores predeterminados (icono ↺)** para restaurar los valores predeterminados de NR2 (Gamma/OSMS/AE activado, 1.50/0.85/0.20).

## Parámetros de NR4

| Control | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|
| **Estimación de Ruido:** | MMSE | MMSE \| Brandt \| Martin | `NR4NoiseEstimationMethod` |
| **Estimación Adaptativa de Ruido** | Activado (marcado) | Marcado / desmarcado | `NR4AdaptiveNoise` |
| **Reducción (dB):** | 10.0 | 0.0–40.0 dB | `NR4ReductionAmount` |
| **Suavizado (%):** | 0 | 0–100 | `NR4SmoothingFactor` |
| **Blanqueo (%):** | 0 | 0–100 | `NR4WhiteningFactor` |
| **Profundidad de Enmascaramiento:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` |
| **Supresión:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` |

Haga clic en **Restablecer valores predeterminados (icono ↺)** para restaurar los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50).

### Activar o desactivar la estimación adaptativa de ruido NR4

Con la estimación adaptativa de ruido activada, NR4 rastrea los cambios en el entorno de ruido en tiempo real; desactivarla fija la estimación del piso de ruido a una instantánea estática, lo que puede ser adecuado para condiciones de ruido muy estables.

1. Abra `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Marque o desmarque **Adaptive Noise Estimation** para activar o desactivar la reestimación continua del piso de ruido.

El cambio surte efecto de inmediato y se guarda automáticamente en `NR4AdaptiveNoise`.

#### Consejos

- Si el piso de ruido en su banda es estable y consistente, desmarcar **Adaptive Noise Estimation** puede evitar que el estimador siga los cambios en el nivel de la señal y clasifique erróneamente el habla como ruido.
- Si el piso de ruido varía rápidamente — como durante aperturas de banda o con ruido impulsivo — deje **Adaptive Noise Estimation** marcado para que NR4 pueda rastrear las condiciones cambiantes.
- El selector **Método de Estimación de Ruido** (MMSE, Brandt, Martin) determina cómo NR4 construye su modelo de ruido, independientemente de si el modo adaptativo está activado o desactivado. Cambiar el método puede afectar qué tan bien la estimación estática o adaptativa rastrea su piso de ruido.
- Haga clic en **Restablecer valores predeterminados** en la pestaña NR4 para devolver todos los controles de NR4 a sus valores de fábrica (adaptativo activado, MMSE, 10 dB, 0, 0, 0.50, 0.50).

### Disponibilidad de NR4 en Windows

NR4 utiliza la biblioteca libspecbleach, que requiere el compilador clang-cl en Windows. Si la pestaña NR4 está atenuada, instale LLVM desde llvm.org y reconstruya AetherSDR para habilitar la compatibilidad con NR4.

## Parámetros de MNR (solo macOS)

| Control | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|
| **Activar MNR (solo macOS)** | Desactivado | Marcado / desmarcado | `MnrEnabled` |
| **Intensidad** | 100 | 0–100 | `MnrStrength` |

El conmutador MNR está atenuado en las compilaciones de Windows/Linux. La casilla **Activar MNR** habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico.

## Parámetros de DFNR

| Control | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|
| **Límite de Atenuación** | 100 | 0–100 dB | `DfnrAttenLimit` |
| **Beta de Post-Filtro** | 0.00 | 0.00–0.30 | `DfnrPostFilterBeta` |

**Límite de Atenuación** establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = máximo.

**Beta de Post-Filtro** aplica un post-filtro adicional para una supresión extra.

## Pestaña RN2

Seleccionar la pestaña RN2 muestra solo contenido informativo. No hay parámetros ajustables para RN2.

## Pestaña BNR

Seleccionar la pestaña BNR muestra los controles de reducción de ruido de NVIDIA Broadcast. El conmutador BNR está atenuado en compilaciones sin el SDK de NVIDIA Broadcast. La intensidad se controla desde el menú superpuesto.

## Relacionados

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Ajustar la profundidad de enmascaramiento y la fuerza de supresión de NR4](tune-nr4-masking-depth-and-suppression-strength.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Cómo elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
