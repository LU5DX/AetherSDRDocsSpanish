# Descripción general: Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)

AetherSDR incluye un saturador de tubo dinámico del lado del cliente que opera de forma independiente en las rutas de audio de transmisión y recepción. Úselo para añadir riqueza armónica a su señal transmitida (Aetherial Mic-PreAmp) o para dar forma al tono del audio recibido (Aetherial Dynamic Tube), sin modificar ningún DSP del lado del radio.

## Antes de comenzar

- La etapa de tubo debe habilitarse mediante el widget CHAIN en el lado TX o RX correspondiente antes de que el applet sea visible.
- No se requiere conexión al radio para configurar los parámetros del tubo.

## Cómo funciona

AetherSDR instancia dos copias completamente independientes del saturador de tubo: una vinculada a la ruta TX (titulada **Aetherial Mic-PreAmp**) y otra vinculada a la ruta RX (titulada **Aetherial Dynamic Tube**). Cada copia tiene su propio conjunto de controles y ajustes persistidos. Los cambios realizados en el applet acoplado y los cambios realizados en el editor flotante se sincronizan automáticamente.

**Apertura del applet.** Los subcontenedores TX y RX aparecen dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets. Permanecen ocultos hasta que la etapa Tube se habilita mediante el widget CHAIN. Hacer doble clic en la etapa TUBE en el widget CHAIN abre el editor sin marco correspondiente, titulado **Aetherial Tube — TX** o **Aetherial Tube — RX**. Hacer clic derecho en la barra de título del subcontenedor permite flotarlo, extraerlo u ocultarlo.

**La curva de transferencia.** El applet muestra una curva de transferencia compacta que se dobla en tiempo real conforme se ajustan Drive, Bias y el modelo de tubo. Una bola de entrada en vivo recorre la curva al nivel de señal actual, mostrando en qué régimen de saturación opera la señal.

**Flujo de señal.** La señal pasa por Drive (ganancia de entrada hacia el modelo de tubo), luego por la función de transferencia del tubo moldeada por Bias, luego por el filtrado Tone, luego por Output (ajuste de nivel posterior al tubo), con Mix mezclando el resultado procesado (wet) con la señal sin procesar (dry).

**Sincronización de ajustes.** Los cinco controles del applet acoplado y sus equivalentes en el editor flotante se consultan mutuamente a aproximadamente 30 Hz. Ajustar un control en cualquiera de las dos ubicaciones actualiza el otro.

## Qué hace cada control

Los siguientes controles y valores predeterminados se aplican tanto a la instancia TX como a la RX. Las claves de ajuste se muestran para la instancia TX; la instancia RX utiliza las claves `ClientTubeRx*` correspondientes.

| Control | Predeterminado | Rango válido | Clave persistida (TX) | Comportamiento |
|---|---|---|---|---|
| Curva de transferencia | — | — | — | Muestra la curva de transferencia del tubo actual. La bola de entrada en vivo se desplaza a lo largo de la curva al nivel de entrada actual. Indicador de solo lectura. |
| Drive | 0.0 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` | Empuja más señal hacia la etapa de tubo. Valores más altos producen mayor saturación y curvatura. |
| Tone | 0.00 | -1.0 – 1.0 | `ClientTubeTxTone` | Da forma al carácter espectral de la señal saturada. Valores negativos oscurecen el tono; valores positivos lo aclaran. |
| Bias | 0 % | 0 – 100 % | `ClientTubeTxBiasAmount` | Desplaza el punto de operación en la curva de transferencia, cambiando el equilibrio entre armónicos pares e impares. |
| Output | 0.0 dB | -24.0 – 12.0 dB | `ClientTubeTxOutputGainDb` | Ganancia de compensación o ajuste posterior al tubo. Úsela para compensar los cambios de nivel introducidos por Drive. |
| Mix | 100 % | 0 – 100 % | `ClientTubeTxDryWet` | Mezcla la señal saturada (wet) con la señal sin procesar (dry). 100 % es completamente saturado; 0 % es completamente seco. |

Los equivalentes de la ruta RX utilizan `ClientTubeRxEnabled`, `ClientTubeRxDriveDb`, `ClientTubeRxTone`, `ClientTubeRxBiasAmount`, `ClientTubeRxOutputGainDb` y `ClientTubeRxDryWet`.

## Consejos

- Comience con Drive en 0.0 dB y auméntelo lentamente mientras observa cómo se dobla la curva de transferencia. El punto en que la curva se desvía notablemente de una línea recta marca el inicio de la saturación.
- Use Mix por debajo del 100 % para mezclar la saturación de forma sutil sin reemplazar completamente la señal seca. Esto es especialmente útil en RX para preservar la claridad mientras se añade calidez.
- Bias desplaza qué armónicos predominan. Cantidades pequeñas (10–20 %) introducen asimetría y armónicos de orden par, característicos de etapas de tubo en configuración single-ended.
- Después de aumentar Drive, reduzca Output para mantener el nivel procesado equiparado al nivel sin procesar.
- Las instancias TX y RX son completamente independientes. Los ajustes cambiados en un lado no afectan al otro.

## Relacionado

- [Ajuste Drive hasta que la curva comience a doblarse (calidez en TX o moldeado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Desplace Bias para ajustar el equilibrio de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Aclare u oscurezca la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcle la saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Omita el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
