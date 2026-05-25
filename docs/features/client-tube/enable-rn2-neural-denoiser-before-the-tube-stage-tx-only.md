# Habilitar el denoiser neuronal RN2 antes de la etapa Tube (solo TX)

Active el denoiser RNNoise integrado para suprimir el ruido de fondo en la entrada de su micrófono antes de que llegue al saturador Tube, puerta y compresor. Esto limpia el ruido ambiente, el zumbido del ventilador o los golpes de respiración al principio de la cadena DSP de TX. RN2 está disponible solo en el lado TX y funciona en modos de voz (no en modos digitales).

## Antes de empezar

- La etapa Tube debe estar habilitada en el widget CHAIN del lado TX (haga un solo clic en el mosaico TUBE).
- Debe estar en un modo de voz (SSB, AM, FM, etc.). Los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten el denoiser automáticamente.

## Pasos

1. Asegúrese de que la etapa TX Tube sea visible en el contenedor TXDSP. Si no es así, haga clic en el lado TX del widget CHAIN para activar la etapa.
2. Haga doble clic en el mosaico TUBE en el widget CHAIN (lado TX). Se abrirá el editor sin marco, titulado "Aetherial Tube — TX".
3. En el área inferior del editor, debajo del medidor de nivel de salida, localice el botón de alternancia RN2.
4. Haga clic en RN2 para habilitarlo. El botón se ilumina (ámbar cuando está marcado) para indicar que el denoiser está activo.

   > RN2 es una activación/desactivación simple de encendido/apagado. No hay controles adicionales: el modelo neuronal funciona con una intensidad de supresión fija.

5. Hable con normalidad hacia el micrófono. El ruido de fondo debería reducirse notablemente antes de que la señal entre al saturador Tube y otras etapas DSP de TX.
6. Para deshabilitarlo, haga clic en RN2 nuevamente para que el botón vuelva al estado desmarcado (apagado).

## Qué hace cada control

| Control | Tipo       | Valor predeterminado | Notas                                                                                                                                                                                                  |
|---------|------------|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RN2     | Botón de alternancia | Desmarcado           | Habilita el denoiser neuronal RNNoise en la entrada del micrófono, antes de la cadena DSP de TX (puerta, compresor, Tube). Se conserva mediante AudioEngine. |

## Consejos

- Habilite RN2 primero, luego ajuste Drive y Bias en el Tube. El denoiser elimina el ruido antes de la saturación, así que puede usar más drive del Tube sin amplificar el soplido de fondo.
- Si cambia a un modo digital (RADE, DAX, RTTY, FT8, FDV, CW), la etapa RN2 se omite automáticamente. El botón permanece en su estado actual y se reactivará cuando vuelva a un modo de voz.
- La alternancia RN2 aparece solo en el editor de TX. El editor de RX Tube ("Aetherial Dynamic Tube") no tiene un control RN2.

## Solución de problemas

- **El botón RN2 no aparece** — Abra el editor de TX Tube (haga doble clic en TUBE en el widget CHAIN del lado TX). El botón aparece debajo del medidor de nivel de salida, solo en el lado TX.
- **El denoiser parece no tener efecto** — Verifique que esté en un modo de voz (SSB, AM, FM). RN2 se omite en modos digitales. También compruebe que la etapa Tube no esté omitida (el mosaico del applet debe tener opacidad completa, no atenuada).
- **El ruido de fondo aún es audible después de habilitar RN2** — El denoiser suprime el ruido de fondo constante, pero puede no eliminar ruidos impulsivos repentinos. Para mejores resultados, coloque su micrófono cerca de su boca y reduzca la ganancia en la fuente cuando sea posible.

## Relacionado

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Select a tube character (Model A, B, or C) to change harmonic flavour](select-a-tube-character-model-a-b-or-c-to-change-harmonic-flavour.md)
- [Shift Bias to tweak the harmonic balance](shift-bias-to-tweak-the-harmonic-balance.md)
