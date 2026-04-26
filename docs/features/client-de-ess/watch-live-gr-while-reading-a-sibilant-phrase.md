# Ver la reducción de ganancia en vivo mientras lee una frase sibilante

La barra de reducción de ganancia (GR) del Aetherial De-Esser se actualiza en tiempo real mientras transmite o habla. Use este procedimiento para observar cómo responde el medidor al leer una frase sibilante, de modo que pueda confirmar que el de-esser detecta sus sonidos "S" y "T" antes de salir al aire.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado mediante el widget CHAIN. El applet permanece oculto hasta que la etapa De-Ess esté activa.
- Su micrófono debe estar enrutado a través de la cadena de audio TX y producir señal — ya sea activando el radio o utilizando un modo de monitor/prueba para que el audio fluya por el DSP.
- Abra el sub-contenedor "Aetherial De-Esser" dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa DESS del widget CHAIN para abrir el editor flotante "Aetherial De-Esser — TX".

## Pasos

1. Verifique que la etapa De-Ess esté habilitada en el widget CHAIN. El applet será visible una vez que la etapa esté activa.
2. Localice la **barra de reducción de ganancia** — la franja horizontal situada directamente debajo de la curva de respuesta del sidechain.
3. Active el radio o habilite su ruta de audio para que el audio del micrófono fluya a través del DSP de TX.
4. Pronuncie una frase con sibilancia intensa — por ejemplo, "She sells seashells by the seashore" — con su nivel y distancia de micrófono habituales.
5. Observe cómo la **barra de reducción de ganancia** se llena de derecha a izquierda en rojo suave en cada sonido "S" o "T". Si no hay relleno, el de-esser no está actuando; si el relleno alcanza el ancho completo, se están aplicando hasta 24 dB de reducción.
6. Anote el punto en que la barra alcanza típicamente su pico. La marca de graduación sobre la barra indica el punto de −6 dB, que es el valor predeterminado de **Amount** y un objetivo habitual para un de-essing transparente.
7. Si la barra nunca se mueve, reduzca **Thresh** hacia −60.0 dB hasta que comience a responder. Si la barra está pegada a la derecha en cada sílaba, aumente **Thresh** hacia 0.0 dB.
8. Repita la frase hasta que la barra responda únicamente en los picos sibilantes genuinos, no en el habla ordinaria.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|
| Curva de respuesta del sidechain | — | — | — | Dibuja la respuesta del filtro de paso de banda. Una esfera en movimiento indica la frecuencia central actual. |
| Barra de reducción de ganancia | — | 0 a 24 dB GR | — | Franja horizontal en rojo suave, rellena desde la derecha. Se actualiza a aproximadamente 30 Hz. Una marca indica el punto de −6 dB. |
| Freq | 6000 Hz | 1000 a 12000 Hz | `ClientDeEssTxFrequencyHz` | Frecuencia central de la banda de sibilancia. Utiliza mapeo logarítmico. |
| Q | 2.00 | 0.5 a 5.0 | `ClientDeEssTxQ` | Ancho de banda de la banda de sibilancia. Mayor Q = más estrecho. |
| Thresh | −30.0 dB | −60.0 a 0.0 dB | `ClientDeEssTxThresholdDb` | Nivel por encima del cual el de-esser comienza a atenuar la banda. |
| Amount | −6.0 dB | −24.0 a 0.0 dB | `ClientDeEssTxAmountDb` | Atenuación máxima aplicada en el pico de sibilancia. |

## Consejos

- El medidor funciona a aproximadamente 30 Hz, por lo que los transitorios breves e intensos pueden aparecer como destellos momentáneos. Esto es normal.
- Mantenga el control **Amount** en su valor predeterminado de −6.0 dB mientras observa el medidor por primera vez. Redúzcalo solo después de haber confirmado que el medidor se activa con los sonidos correctos.
- Si la esfera sobre la curva de respuesta del sidechain se encuentra lejos de donde se ubican sus picos de sibilancia, use **Freq** para desplazarla. El medidor solo mostrará GR cuando la energía en la banda de **Freq** actual supere **Thresh**.

## Solución de problemas

- **La barra de reducción de ganancia nunca se mueve** — El de-esser no está actuando. Verifique que la etapa De-Ess esté habilitada en el widget CHAIN, que el audio esté fluyendo por el DSP de TX y que **Thresh** no esté ajustado demasiado alto (demasiado cerca de 0.0 dB) para el nivel de su micrófono.
- **La barra de reducción de ganancia está pegada a la derecha en cada sílaba, incluso en el habla no sibilante** — **Thresh** está ajustado demasiado bajo. Auméntelo hacia 0.0 dB hasta que las vocales ordinarias dejen de activar el medidor.
- **La barra se mueve pero no escucha ningún efecto al aire** — **Amount** puede estar ajustado demasiado cerca de 0.0 dB. Redúzcalo hacia −24.0 dB para obtener una reducción más audible, o confirme que la etapa no está omitida (bypassed) en el widget CHAIN.

## Relacionados

- [Ajustar el umbral justo por debajo de los picos de "S" más intensos](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Omitir el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
