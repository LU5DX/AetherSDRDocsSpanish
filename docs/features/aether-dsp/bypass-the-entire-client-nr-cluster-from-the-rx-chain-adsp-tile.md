# Configuración de AetherDSP

El cuadro de diálogo de Configuración de AetherDSP proporciona configuración avanzada para todos los motores de reducción de ruido del lado del cliente en AetherSDR. Incluye seis módulos DSP: NR2, NR4, MNR, DFNR, RN2 y BNR.

## Cómo abrir el cuadro de diálogo

- Desde la tira de la cadena de RX, haga doble clic en el mosaico **ADSP**.
- Desde la cuadrícula DSP del VFO, haga clic en el botón **ADSP**.

## Ventana del cuadro de diálogo

El cuadro de diálogo tiene una barra de título sin bordes con un glifo de agarre (⋮⋮) a la izquierda. La barra de título incluye tres botones:

- — (Minimizar) — Minimiza el cuadro de diálogo.
- □ (Maximizar) — Maximiza o restaura el cuadro de diálogo.
- × (Cerrar) — Cierra el cuadro de diálogo.

Arrastre la barra de título para mover el cuadro de diálogo. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. Arrastre cualquier borde o esquina para cambiar el tamaño (zona de cambio de tamaño de 6 px).

La posición y el tamaño del cuadro de diálogo se persisten automáticamente entre sesiones mediante la clave de configuración `AetherDspDialogGeometry`.

El cuadro de diálogo utiliza un estilo adaptado al tema aplicado a través de `ThemeManager`. Los colores se derivan del tema de color activo en lugar de valores fijos.

## Fila de alternancia

La parte superior del cuadro de diálogo contiene seis botones de alternancia que funcionan como selectores de pestañas y controles de activación/desactivación del motor:

- **NR2** — Motor de reducción de ruido musical
- **NR4** — Reducción de ruido espectral libspecbleach
- **MNR** — Reducción de ruido MMSE-Wiener de macOS (atenuado en Windows/Linux)
- **DFNR** — Reducción de ruido neuronal DeepFilterNet3
- **RN2** — Reducción de ruido neuronal RNNoise (solo informativo, sin parámetros ajustables)
- **BNR** — Reducción de ruido neuronal NVIDIA Broadcast (atenuado sin el SDK de NVIDIA Broadcast)

Al hacer clic en un motor, se activa y se selecciona su pestaña. Al hacer clic nuevamente, se desactiva el motor. Solo un motor puede estar activo a la vez: NR2, NR4 y DFNR son mutuamente excluyentes. MNR y BNR pueden apilarse en algunas compilaciones.

Cada botón de alternancia tiene un nombre accesible que incluye su etiqueta (por ejemplo, "método de reducción de ruido NR2") para tecnologías de asistencia y soporte del puente de automatización.

El último motor NR del cliente activo se guarda en la configuración `LastClientNr`. Si DFNR no está disponible y estaba activo previamente, la preferencia se borra automáticamente.

## Pestaña NR2

Controles para el motor de reducción de ruido musical.

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|------|----------------------|-------|------------------------|----------------|
| Método de ganancia | Botón de opción | Gamma | Lineal, Log, Gamma, Entrenado | `NR2GainMethod` | Selecciona la asignación de la curva de ganancia (almacenada como entero 0-3). |
| Método NPE | Botón de opción | OSMS | OSMS, MMSE, NSTAT | `NR2NpeMethod` | Selecciona el estimador de potencia de ruido (almacenado como entero 0-2). |
| Filtro AE (eliminación de artefactos) | Casilla de verificación | Verdadero | — | `NR2AeFilter` | Activa/desactiva el post-filtro antiartefactos. |
| Reducción: | Deslizador | 1.50 | 0.50-2.00 | `NR2GainMax` | Establece la profundidad máxima de reducción NR2. |
| Suavizado: | Deslizador | 0.85 | 0.50-0.98 | `NR2GainSmooth` | Controla la suavidad con la que la estimación de ruido sigue los cambios. |
| Umbral: | Deslizador | 0.20 | 0.05-0.50 | `NR2Qspp` | Establece el umbral de probabilidad de presencia de voz. |
| Restablecer valores predeterminados (icono ↺) | Botón pulsador | — | — | — | Restaura los valores predeterminados de NR2 (Gamma/OSMS/AE activado, 1.50/0.85/0.20). |

Los deslizadores de esta pestaña utilizan un estilo adaptado al tema mediante `applyPrimarySliderStyle()`.

En v26.7.4, se agregaron dos nuevas señales a la pestaña NR2: `nr2GainFloorChanged` y `nr2UseOriginalGeometryChanged`, lo que permite controles futuros para el piso de ganancia mínimo y los modos de geometría original.

## Pestaña NR4

Controles para el motor de reducción de ruido espectral libspecbleach.

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|------|----------------------|-------|------------------------|----------------|
| Estimación de ruido: | Botón de opción | MMSE | MMSE, Brandt, Martin | `NR4NoiseEstimationMethod` | Selecciona el estimador del piso de ruido (almacenado como entero 0-2). |
| Estimación de ruido adaptativa | Casilla de verificación | Verdadero | — | `NR4AdaptiveNoise` | Habilita la reestimación continua del piso de ruido. |
| Reducción (dB): | Deslizador | 10.0 | 0.0-40.0 | `NR4ReductionAmount` | Establece la reducción máxima de ruido NR4 en dB. |
| Suavizado (%): | Deslizador | 0 | 0-100 | `NR4SmoothingFactor` | Suavizado en el dominio temporal de la estimación de ruido NR4. |
| Blanqueamiento (%): | Deslizador | 0 | 0-100 | `NR4WhiteningFactor` | Aplana la forma espectral del ruido residual. |
| Profundidad de enmascaramiento: | Deslizador | 0.50 | 0.00-1.00 | `NR4MaskingDepth` | Controla la profundidad del enmascaramiento espectral. |
| Supresión: | Deslizador | 0.50 | 0.00-1.00 | `NR4SuppressionStrength` | Fuerza de supresión general de NR4. |
| Restablecer valores predeterminados (icono ↺) | Botón pulsador | — | — | — | Restaura los valores predeterminados de NR4 (MMSE/adaptativo activado, 10 dB, 0, 0, 0.50, 0.50). |

Los deslizadores de esta pestaña utilizan un estilo adaptado al tema mediante `applyPrimarySliderStyle()`.

**Nota:** NR4 requiere LLVM (clang-cl) en Windows. La alternancia se atenúa si LLVM no está instalado. Instale LLVM desde llvm.org y reconstruya AetherSDR para habilitar NR4.

## Pestaña MNR

Controles para el motor de reducción de ruido MMSE-Wiener de macOS. Esta pestaña y sus controles solo están disponibles en compilaciones de macOS.

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|------|----------------------|-------|------------------------|----------------|
| Habilitar MNR (solo macOS) | Casilla de verificación | — | — | `MnrEnabled` | Habilita la reducción de ruido MMSE-Wiener con suavizado de ganancia asimétrico. |
| Intensidad | Deslizador | 100 | 0-100 | `MnrStrength` | Ajusta la agresividad de MNR (0 suave, 100 máximo). |

## Pestaña DFNR

Controles para el motor de reducción de ruido neuronal DeepFilterNet3.

**Nota:** DeepFilterNet3 es un sistema avanzado de reducción de ruido basado en redes neuronales que utiliza aprendizaje profundo para suprimir el ruido mientras preserva la calidad de la voz. Puede requerir recursos significativos de CPU. DFNR requiere que DeepFilterNet esté configurado y que AetherSDR se reconstruya. Si no está disponible, la alternancia DFNR muestra una información sobre herramientas explicándolo.

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|------|----------------------|-------|------------------------|----------------|
| Límite de atenuación | Deslizador | 100 | 0-100 dB | `DfnrAttenLimit` | Establece la atenuación máxima de ruido aplicada por DeepFilterNet3. 0 = paso directo; 100 = supresión máxima. |
| Beta del post-filtro | Deslizador | 0.00 | 0.00-0.30 | `DfnrPostFilterBeta` | Aplica un post-filtro adicional para una mayor supresión. |

## Pestaña RN2

Selecciona la página de reducción de ruido neuronal RNNoise. Esta pestaña es puramente informativa y no tiene parámetros ajustables.

## Pestaña BNR

Selecciona la página de reducción de ruido neuronal NVIDIA Broadcast. La intensidad se controla desde el menú superpuesto. La alternancia se atenúa en compilaciones sin el SDK de NVIDIA Broadcast.

## Cómo omitir todos los motores NR del cliente

Para desactivar rápidamente toda la reducción de ruido del lado del cliente sin abrir el cuadro de diálogo de Configuración de AetherDSP:

1. Localice el mosaico **ADSP** en la tira de la cadena de RX.
2. Haga doble clic en el mosaico **ADSP** para abrir la Configuración de AetherDSP.
3. En la fila de alternancia en la parte superior, haga clic en cada alternancia de reducción de ruido activa (iluminada) para desactivarla.
4. Continúe hasta que todas las alternancias estén atenuadas.

El mosaico ADSP se actualiza para reflejar el estado de omisión. Ahora no hay motores NR del cliente activos, lo que devuelve el audio al flujo de audio de la porción sin procesar desde la radio.

## Consejos

- Las seis alternancias DSP (NR2, NR4, MNR, DFNR, RN2, BNR) funcionan como selectores de pestañas y controles de activación/desactivación del motor.
- NR2, NR4 y DFNR son mutuamente excluyentes: solo uno puede estar activo a la vez.
- MNR y BNR pueden apilarse con otros motores en algunas compilaciones.
- El botón Restablecer valores predeterminados (icono ↺) en cada pestaña restaura los parámetros de ese motor a sus valores predeterminados.
- Las configuraciones se persisten entre sesiones.
- El cuadro de diálogo utiliza un estilo adaptado al tema. Los colores se obtienen del tema de color activo en lugar de valores fijos.
- El último motor NR del cliente activo se guarda; si DFNR deja de estar disponible, la preferencia almacenada se borra automáticamente.
