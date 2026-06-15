# Habilitar el eliminador de ruido neuronal RN2 antes de la etapa de válvula (solo TX)

Active el eliminador de ruido RNNoise integrado para suprimir el ruido de fondo en la entrada de su micrófono antes de que llegue al saturador de válvula, compuerta y compresor. Esto limpia el ruido ambiental, el zumbido de ventiladores o los chasquidos de la respiración al inicio de la cadena de DSP de TX. RN2 está disponible solo en el lado de TX y funciona en modos de voz (no en modos digitales).

## Antes de comenzar

- La etapa de válvula debe estar habilitada en el widget CHAIN del lado de TX (haga clic una vez en el mosaico TUBE).
- Debe estar en un modo de voz (SSB, AM, FM, etc.). Los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten el eliminador de ruido automáticamente.

## Pasos

1. Asegúrese de que la etapa de válvula TX sea visible en el contenedor TXDSP. Si no, haga clic en el lado TX del widget CHAIN para activar la etapa.
2. Haga doble clic en el mosaico TUBE en el widget CHAIN (lado TX). Se abrirá el editor sin marco, titulado "Aetherial Tube — TX".
3. En el área inferior del editor, debajo del medidor de nivel de salida, localice el botón de conmutación RN2.
4. Haga clic en RN2 para activarlo. El botón se ilumina (ámbar cuando está marcado) para indicar que el eliminador de ruido está activo.

   > RN2 es una simple activación/desactivación. No hay controles adicionales: el modelo neuronal funciona con una intensidad de supresión fija.

5. Hable con normalidad hacia el micrófono. El ruido de fondo debería reducirse notablemente antes de que la señal entre al saturador de válvula y otras etapas de DSP de TX.
6. Para desactivarlo, haga clic en RN2 nuevamente para que el botón vuelva al estado desmarcado (apagado).

## Función de cada control

| Control  | Tipo            | Valor predeterminado |
|----------|-----------------|----------------------|
| RN2      | Botón de conmutación | Desmarcado          |
| Drive    | Perilla         | 0.00 dB              |
| Tone     | Perilla         | 0.00                 |
| Bias     | Perilla         | 0 %                  |
| Output   | Perilla         | 0.00 dB              |
| Dry/Wet  | Perilla         | 100 %                |
| Envelope | Perilla         | 0 %                  |
| Attack   | Perilla         | 5.00 ms              |
| Release  | Perilla         | 35.00 ms             |
| A        | Botón de conmutación | Marcado            |
| B        | Botón de conmutación | Desmarcado          |
| C        | Botón de conmutación | Desmarcado          |

## Modelos de carácter de válvula (A, B, C)

Los tres modelos de carácter de válvula proporcionan diferentes matices armónicos:

- **Modelo A** (predeterminado): Carácter de válvula cálido estándar.
- **Modelo B**: Perfil armónico más brillante con armónicos superiores aumentados.
- **Modelo C**: Carácter más oscuro y suave con armónicos de alta frecuencia reducidos.

Seleccione un modelo haciendo clic en el botón de conmutación correspondiente. Solo un modelo puede estar activo a la vez. El modelo seleccionado afecta la forma de la curva de transferencia que se muestra en el widget de curva de válvula.

## Controles del seguidor de envolvente

Cuando Envelope se configura en un valor distinto de cero, las perillas Attack y Release controlan la dinámica del seguidor de envolvente:

- **Attack**: Controla la rapidez con la que el seguidor de envolvente responde a niveles de señal crecientes. Tiempos de ataque más cortos (0.1 ms) proporcionan una respuesta más rápida a los transitorios.
- **Release**: Controla la rapidez con la que el seguidor de envolvente se recupera después de que los niveles de señal disminuyen. Tiempos de liberación más largos (hasta 500 ms) mantienen el efecto por más tiempo.

Estos controles solo tienen efecto cuando Envelope no está en 0%.

## Consejos

- Active RN2 primero, luego ajuste Drive y Bias en la válvula. El eliminador de ruido elimina el ruido antes de la saturación, por lo que puede usar más drive de válvula sin amplificar el soplido de fondo.
- Si cambia a un modo digital (RADE, DAX, RTTY, FT8, FDV, CW), la etapa RN2 se omite automáticamente. El botón permanece en su estado actual y se reactivará cuando vuelva a un modo de voz.
- El conmutador RN2 aparece solo en el editor TX. El editor de válvula RX ("Aetherial Dynamic Tube") no tiene un control RN2.
- Use el control Dry/Wet para mezclar la señal procesada con la original. Al 100% (predeterminado), la señal está completamente procesada. Los valores más bajos mezclan señal sin procesar para un efecto más sutil.
- El control Envelope permite cambios dinámicos en el carácter de la válvula. Los valores positivos enfatizan los transitorios para un sonido más contundente; los valores negativos comprimen los armónicos para un tono más suave y consistente.

## Solución de problemas

- **Falta el botón RN2** — Abra el editor de válvula TX (haga doble clic en TUBE en el widget CHAIN del lado TX). El botón aparece debajo del medidor de nivel de salida, solo en el lado TX.
- **El eliminador de ruido parece no tener efecto** — Verifique que esté en un modo de voz (SSB, AM, FM). RN2 se omite en modos digitales. También compruebe que la etapa de válvula en sí no esté omitida (el mosaico del applet debe tener opacidad completa, no atenuada).
- **El ruido de fondo aún se escucha después de activar RN2** — El eliminador de ruido suprime el ruido de fondo constante, pero puede no eliminar los ruidos de impulso repentinos. Para obtener los mejores resultados, coloque el micrófono cerca de la boca y reduzca la ganancia en la fuente cuando sea posible.
- **Los botones de carácter de válvula no funcionan** — Asegúrese de que solo un modelo (A, B o C) esté seleccionado a la vez. Los botones son mutuamente excluyentes.

## Relacionados

- [Ajuste Drive hasta que la curva comience a doblarse (calidez TX o modelado de tono RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Seleccione un carácter de válvula (Modelo A, B o C) para cambiar el matiz armónico](select-a-tube-character-model-a-b-or-c-to-change-harmonic-flavour.md)
- [Desplace Bias para ajustar el equilibrio armónico](shift-bias-to-tweak-the-harmonic-balance.md)
