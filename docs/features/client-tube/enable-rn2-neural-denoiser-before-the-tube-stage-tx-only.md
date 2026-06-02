# Activar el denoiser neuronal RN2 antes de la etapa Tube (solo TX)

Active el denoiser RNNoise integrado para suprimir el ruido de fondo de la entrada de su micrófono antes de que llegue al saturador Tube, la puerta de ruido y el compresor. Esto limpia el ruido ambiental, el zumbido del ventilador o los soplidos al inicio de la cadena DSP de TX. RN2 está disponible solo en el lado TX y funciona en modos de voz (no en modos digitales).

## Antes de comenzar

- La etapa Tube debe estar habilitada en el widget CHAIN del lado TX (haga clic una vez en el mosaico TUBE).
- Debe estar en un modo de voz (SSB, AM, FM, etc.). Los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten automáticamente el denoiser.

## Pasos

1. Asegúrese de que la etapa TX Tube esté visible en el contenedor TXDSP. Si no, haga clic en el lado TX del widget CHAIN para activar la etapa.
2. Haga doble clic en el mosaico TUBE del widget CHAIN (lado TX). Se abre el editor sin marco, titulado "Aetherial Tube — TX".
3. En el área inferior del editor, debajo del medidor de nivel de salida, localice el botón de conmutación RN2.
4. Haga clic en RN2 para activarlo. El botón se ilumina (ámbar cuando está marcado) para indicar que el denoiser está activo.

   > RN2 es un conmutador simple de activación/desactivación. No hay controles adicionales: el modelo neuronal se ejecuta con una intensidad de supresión fija.

5. Hable con normalidad hacia el micrófono. El ruido de fondo debería reducirse notablemente antes de que la señal entre al saturador Tube y otras etapas DSP de TX.
6. Para desactivarlo, haga clic en RN2 nuevamente para que el botón vuelva al estado no marcado (apagado).

## Función de cada control

| Control | Tipo            | Valor predeterminado | Rango válido   | Clave de ajuste | Comportamiento |
|---------|-----------------|----------------------|----------------|-----------------|----------------|
| RN2     | Botón de conmutación | No marcado       | —              | — (persistido mediante AudioEngine) | Conmutador solo TX. Activa el denoiser neuronal RNNoise en la entrada del micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue a puerta/compresor/saturador. Solo modos de voz; los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. |
| Drive   | Perilla         | 0.00 dB              | 0.0 a 24.0 dB  | ClientTubeTxDriveDb | Mapeo lineal. Introduce más señal en la etapa del tubo. |
| Tone    | Perilla         | 0.00                 | -1.0 a 1.0     | ClientTubeTxTone | Mapeo lineal. Los valores negativos oscurecen, los positivos aclaran la señal saturada. |
| Bias    | Perilla         | 0 %                  | 0.0 a 1.0      | ClientTubeTxBias | Mapeo lineal. Desplaza el punto de operación en la curva de transferencia, cambiando la mezcla armónica. |
| Output  | Perilla         | 0.00 dB              | -24.0 a 12.0 dB| ClientTubeTxOutputDb | Mapeo lineal. Ganancia de compensación/recorte posterior al tubo. |
| Dry/Wet | Perilla         | 100 %                | 0.0 a 1.0      | ClientTubeTxDryWet | Mapeo lineal. Mezcla seca/húmeda (100 % = señal completamente saturada). |
| Envelope| Perilla         | 0 %                  | -1.0 a 1.0     | ClientTubeTxEnvelope | Mapeo lineal. Los valores positivos aumentan la excursión en los transitorios (el tubo se calienta más en picos fuertes); los valores negativos la reducen, comprimiendo los armónicos de forma dinámica. |
| Attack  | Perilla         | 5.00 ms              | 0.1 a 30.0 ms  | ClientTubeTxAttackMs | Mapeo exponencial (0,1 * 300^n). Establece la rapidez con la que el seguidor de envolvente responde a niveles crecientes cuando Envelope ≠ 0. |
| Release | Perilla         | 35.00 ms             | 10.0 a 500.0 ms| ClientTubeTxReleaseMs | Mapeo exponencial (10 * 50^n). Establece la rapidez con la que el seguidor de envolvente se recupera tras una caída de nivel cuando Envelope ≠ 0. |
| A       | Botón de conmutación | Marcado         | —              | ClientTubeTxModel | Selecciona el carácter de tubo Modelo A. Excluyente con B y C. |
| B       | Botón de conmutación | No marcado      | —              | ClientTubeTxModel | Selecciona el carácter de tubo Modelo B. Excluyente con A y C. |
| C       | Botón de conmutación | No marcado      | —              | ClientTubeTxModel | Selecciona el carácter de tubo Modelo C. Excluyente con A y B. |

## Modelos de carácter de tubo (A, B, C)

Los tres modelos de carácter de tubo ofrecen diferentes matices armónicos:

- **Modelo A** (predeterminado): Carácter de tubo cálido estándar.
- **Modelo B**: Perfil armónico más brillante con armónicos superiores incrementados.
- **Modelo C**: Carácter más oscuro y suave con armónicos de alta frecuencia reducidos.

Seleccione un modelo haciendo clic en el botón de conmutación correspondiente. Solo un modelo puede estar activo a la vez. El modelo seleccionado afecta la forma de la curva de transferencia que se muestra en el widget Tube curve.

## Controles del seguidor de envolvente

Cuando Envelope se ajusta a un valor distinto de cero, las perillas Attack y Release controlan la dinámica del seguidor de envolvente:

- **Attack**: Controla la rapidez con la que el seguidor de envolvente responde a niveles de señal crecientes. Los tiempos de ataque más cortos (0,1 ms) proporcionan una respuesta más rápida a los transitorios.
- **Release**: Controla la rapidez con la que el seguidor de envolvente se recupera tras una caída del nivel de la señal. Los tiempos de liberación más largos (hasta 500 ms) sostienen el efecto durante más tiempo.

Estos controles solo tienen efecto cuando Envelope no está al 0 %.

## Consejos

- Active RN2 primero, luego ajuste Drive y Bias en el Tube. El denoiser elimina el ruido antes de la saturación, por lo que puede usar más excursión del Tube sin amplificar el soplido de fondo.
- Si cambia a un modo digital (RADE, DAX, RTTY, FT8, FDV, CW), la etapa RN2 se omite automáticamente. El botón permanece en su estado actual y se reactivará cuando vuelva a un modo de voz.
- El conmutador RN2 solo aparece en el editor TX. El editor RX Tube ("Aetherial Dynamic Tube") no tiene un control RN2.
- Use el control Dry/Wet para mezclar la señal procesada con la original. Al 100 % (predeterminado), la señal está completamente procesada. Los valores más bajos mezclan señal no procesada para un efecto más sutil.
- El control Envelope permite cambios dinámicos en el carácter del tubo. Los valores positivos enfatizan los transitorios para un sonido más contundente; los valores negativos comprimen los armónicos para un tono más suave y consistente.

## Solución de problemas

- **El botón RN2 no aparece** — Abra el editor TX Tube (doble clic en TUBE en el widget CHAIN del lado TX). El botón aparece debajo del medidor de nivel de salida, solo en el lado TX.
- **El denoiser parece no tener efecto** — Verifique que esté en un modo de voz (SSB, AM, FM). RN2 se omite en modos digitales. Compruebe también que la etapa Tube no esté omitida (el mosaico del applet debe estar con opacidad completa, no atenuado).
- **El ruido de fondo sigue siendo audible tras activar RN2** — El denoiser suprime el ruido de fondo constante pero puede no eliminar ruidos impulsivos repentinos. Para mejores resultados, coloque el micrófono cerca de la boca y reduzca la ganancia en la fuente siempre que sea posible.
- **Los botones de carácter del tubo no funcionan** — Asegúrese de que solo un modelo (A, B o C) esté seleccionado a la vez. Los botones son mutuamente excluyentes.

## Relacionado

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Select a tube character (Model A, B, or C) to change harmonic flavour](select-a-tube-character-model-a-b-or-c-to-change-harmonic-flavour.md)
- [Shift Bias to tweak the harmonic balance](shift-bias-to-tweak-the-harmonic-balance.md)
