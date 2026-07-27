# Habilitar el eliminador de ruido neuronal RN2 antes de la etapa Tube (solo TX)

Active el eliminador de ruido RNNoise integrado para suprimir el ruido de fondo en la entrada de su micrófono antes de que llegue al saturador Tube, la puerta de ruido y el compresor. Esto limpia el ruido ambiental, el zumbido de ventiladores o los chasquidos de la respiración al principio de la cadena de DSP de TX. RN2 está disponible solo en el lado TX y funciona en modos de voz (no en modos digitales).

## Antes de comenzar

- La etapa Tube debe estar habilitada en el widget CHAIN del lado TX (haga un solo clic en el mosaico TUBE).
- Debe estar en un modo de voz (SSB, AM, FM, etc.). Los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten el eliminador de ruido automáticamente.

## Pasos

1. Asegúrese de que la etapa TX Tube sea visible en el contenedor TXDSP. Si no es así, haga clic en el lado TX del widget CHAIN para activar la etapa.
2. Haga doble clic en el mosaico TUBE en el widget CHAIN (lado TX). Se abrirá el editor sin marco, titulado "Aetherial Tube — TX".
3. En el área inferior del editor, debajo del medidor de nivel de salida, localice el botón de conmutación RN2.
4. Haga clic en RN2 para activarlo. El botón se iluminará (ámbar cuando está marcado) para indicar que el eliminador de ruido está activo.

   > RN2 es una simple activación/desactivación. No hay controles adicionales: el modelo neuronal se ejecuta con una intensidad de supresión fija.

5. Hable con normalidad en el micrófono. El ruido de fondo debería reducirse notablemente antes de que la señal entre al saturador Tube y otras etapas de DSP de TX.
6. Para desactivarlo, haga clic en RN2 nuevamente para que el botón vuelva al estado desmarcado (apagado).

## Función de cada control

| Control  | Tipo            | Valor predeterminado | Rango válido       | Clave de configuración    |
|----------|-----------------|----------------------|--------------------|---------------------------|
| RN2      | Botón de alternancia | Desmarcado        | —                  | (persistido vía AudioEngine) |
| Dry/Wet  | Perilla         | 100 %                | 0.0 a 1.0         | `ClientTubeTxDryWet`      |
| Drive    | Perilla         | 0.00 dB              | 0.0 a 24.0 dB      | `ClientTubeTxDriveDb`     |
| Tone     | Perilla         | 0.00                 | -1.0 a 1.0         | `ClientTubeTxTone`        |
| Bias     | Perilla         | 0 %                  | 0.0 a 1.0          | `ClientTubeTxBias`        |
| Output   | Perilla         | 0.00 dB              | -24.0 a 12.0 dB    | `ClientTubeTxOutputDb`    |
| Envelope | Perilla         | 0 %                  | -1.0 a 1.0         | `ClientTubeTxEnvelope`    |
| Attack   | Perilla         | 5.00 ms              | 0.1 a 30.0 ms      | `ClientTubeTxAttackMs`    |
| Release  | Perilla         | 35.00 ms             | 10.0 a 500.0 ms    | `ClientTubeTxReleaseMs`   |
| A        | Botón de alternancia | Marcado          | —                  | `ClientTubeTxModel`       |
| B        | Botón de alternancia | Desmarcado       | —                  | `ClientTubeTxModel`       |
| C        | Botón de alternancia | Desmarcado       | —                  | `ClientTubeTxModel`       |

## Modelos de carácter de tubo (A, B, C)

Los tres modelos de carácter de tubo ofrecen diferentes matices armónicos:

- **Modelo A** (predeterminado): Carácter de tubo cálido estándar.
- **Modelo B**: Perfil armónico más brillante con armónicos superiores aumentados.
- **Modelo C**: Carácter más oscuro y suave con armónicos de alta frecuencia reducidos.

Seleccione un modelo haciendo clic en el botón de alternancia correspondiente. Solo un modelo puede estar activo a la vez. El modelo seleccionado afecta la forma de la curva de transferencia que se muestra en el widget de curva de Tube.

## Controles del seguidor de envolvente

Cuando Envelope se ajusta a un valor distinto de cero, las perillas Attack y Release controlan la dinámica del seguidor de envolvente:

- **Attack**: Controla la rapidez con la que el seguidor de envolvente responde a los niveles de señal crecientes. Los tiempos de ataque más cortos (0.1 ms) proporcionan una respuesta más rápida a los transitorios.
- **Release**: Controla la rapidez con la que el seguidor de envolvente se recupera después de que los niveles de señal caen. Los tiempos de liberación más largos (hasta 500 ms) mantienen el efecto durante más tiempo.

Estos controles solo tienen efecto cuando Envelope no está al 0%.

## Consejos

- Active RN2 primero, luego ajuste Drive y Bias en Tube. El eliminador de ruido elimina el ruido antes de la saturación, por lo que puede usar más Drive de Tube sin amplificar el silbido de fondo.
- Si cambia a un modo digital (RADE, DAX, RTTY, FT8, FDV, CW), la etapa RN2 se omite automáticamente. El botón permanece en su estado actual y se reactivará cuando vuelva a un modo de voz.
- La alternancia RN2 aparece solo en el editor TX. El editor RX Tube ("Aetherial Dynamic Tube") no tiene un control RN2.
- Use el control Dry/Wet para mezclar la señal procesada con la original. Al 100% (predeterminado), la señal está completamente procesada. Los valores más bajos mezclan la señal sin procesar para un efecto más sutil.
- El control Envelope permite cambios dinámicos en el carácter del tubo. Los valores positivos enfatizan los transitorios para un sonido más contundente; los valores negativos comprimen los armónicos para un tono más suave y uniforme.

## Solución de problemas

- **Falta el botón RN2** — Abra el editor TX Tube (haga doble clic en TUBE en el widget CHAIN del lado TX). El botón aparece debajo del medidor de nivel de salida, solo en el lado TX.
- **El eliminador de ruido parece no tener efecto** — Verifique que esté en un modo de voz (SSB, AM, FM). RN2 se omite en los modos digitales. También compruebe que la etapa Tube en sí no esté omitida (el mosaico del applet debe tener opacidad completa, no atenuada).
- **El ruido de fondo sigue audible después de activar RN2** — El eliminador de ruido suprime el ruido de fondo constante, pero puede no eliminar los ruidos de impulso repentinos. Para obtener los mejores resultados, coloque el micrófono cerca de la boca y reduzca la ganancia en la fuente siempre que sea posible.
- **Los botones de carácter de Tube no funcionan** — Asegúrese de que solo un modelo (A, B o C) esté seleccionado a la vez. Los botones son mutuamente excluyentes.

## Relacionados

- [Ajuste Drive hasta que la curva comience a doblarse (calidez TX o modelado de tono RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Seleccione un carácter de tubo (Modelo A, B o C) para cambiar el matiz armónico](select-a-tube-character-model-a-b-or-c-to-change-harmonic-flavour.md)
- [Desplace Bias para ajustar el equilibrio armónico](shift-bias-to-tweak-the-harmonic-balance.md)
