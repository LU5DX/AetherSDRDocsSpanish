# Vea la reducción de ganancia en vivo mientras lee una frase sibilante

La barra de reducción de ganancia (GR) del Aetherial De-Esser se actualiza en tiempo real mientras transmite o habla. Utilice este procedimiento para observar cómo responde el medidor mientras lee una frase sibilante, de modo que pueda confirmar que el de-esser está capturando sus sonidos "S" y "T" antes de salir al aire.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado mediante el widget CHAIN. El applet permanece oculto hasta que la etapa De-Ess esté activa.
- Su micrófono debe estar enrutado a través de la cadena de audio de TX y produciendo señal, ya sea presionando PTT en la radio o usando un modo de monitoreo/prueba para que el audio fluya a través del DSP.
- Abra el subcontenedor "Aetherial De-Esser" dentro del contenedor principal Aetherial Audio (TXDSP). El bypass y la edición se manejan a través del Aetherial Audio Channel Strip — no hay un editor flotante separado para el de-esser en la versión 0.9.7.
- El panel del de-esser admite tanto el lado TX como el RX. La instancia RX se titula "Aetherial De-Esser — RX" y es accesible a través del Aetherial Audio Channel Strip.

## Pasos

1. Asegúrese de que la etapa De-Ess esté habilitada en el widget CHAIN. El applet será visible una vez que la etapa esté activa. Cuando la etapa está en bypass, todo el mosaico se atenúa aproximadamente al 55% de opacidad.
2. Localice la **barra de reducción de ganancia** — la franja horizontal directamente debajo de la curva de respuesta de la cadena lateral.
3. Presione PTT en su radio o active su ruta de audio para que el audio del micrófono fluya a través del DSP de TX.
4. Pronuncie una frase que contenga sibilancia intensa — por ejemplo, "She sells seashells by the seashore" — a su nivel y distancia normales del micrófono.
5. Observe cómo la **barra de reducción de ganancia** se llena de derecha a izquierda en rojo suave en cada sonido "S" o "T". Sin llenado significa que el de-esser no se está disparando; un llenado que alcanza el ancho completo significa que se está aplicando hasta 24 dB de reducción.
6. Observe dónde alcanza típicamente su punto máximo la barra. La marca en la barra indica el punto de −6 dB, que es el valor predeterminado de **Amount** y un objetivo común para un de-essing transparente.
7. Si la barra nunca se mueve, baje **Thresh** hacia −60.0 dB hasta que comience a responder. Si la barra llega al tope derecho en cada sílaba, suba **Thresh** hacia 0.0 dB.
8. Repita la frase hasta que la barra responda solo en los picos de sibilancia genuinos, no en el habla normal.

## Qué hace cada control

| Control                          | Valor predeterminado | Rango válido     | Descripción                                                                                                                                    |
|----------------------------------|----------------------|------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva de respuesta de cadena lateral | —                    | —                | ClientDeEssCurveWidget en modo compacto. Dibuja la respuesta del filtro pasabanda con una bola en vivo en la frecuencia central actual.             |
| Barra de reducción de ganancia   | —                    | 0 a 24 dB GR     | Franja horizontal rojo suave, llenado desde la derecha. Escala máxima en 24 dB; una marca señala los −6 dB típicos. Se actualiza a ~30 Hz.      |
| Freq                             | 6000 Hz              | 1000 a 12000 Hz  | Mapeo logarítmico. Establece la frecuencia central de la banda de sibilancia. La etiqueta muestra "6.0 kHz" por encima de 1 kHz, "N Hz" por debajo. |
| Q                                | 2.00                 | 0.5 a 5.0        | Mapeo lineal. Establece el ancho de banda de la banda de sibilancia — Q más alto = más estrecho. La etiqueta muestra "X.XX".                        |
| Thresh                           | −30.0 dB             | −60.0 a 0.0 dB   | Mapeo lineal. Nivel por encima del cual el de-esser comienza a atenuar la banda.                                                                 |
| Amount                           | −6.0 dB              | −24.0 a 0.0 dB   | Mapeo lineal. Atenuación máxima aplicada en el pico de sibilancia. Los valores son negativos (o cero) porque representan reducción.                |
| Attack                           | 1.0 ms               | 0.1 a 30.0 ms    | Mapeo exponencial. Establece la rapidez con la que el de-esser responde una vez que la sibilancia supera el umbral. Solo presente en el panel del Channel Strip. |
| Release                          | 100 ms               | 10.0 a 500.0 ms  | Mapeo exponencial. Establece la rapidez con la que la ganancia regresa después de que la sibilancia cae por debajo del umbral. Solo presente en el panel del Channel Strip. |

**Nota:** Los controles Attack y Release están disponibles en el StripDeEssPanel del Channel Strip (tanto instancias RX como TX). El ClientDeEssApplet acoplado omite estos dos mandos.

## Indicadores

| Indicador              | Estados                         | Significado                                                               |
|------------------------|----------------------------------|---------------------------------------------------------------------------|
| Bola de frecuencia central | En reposo sobre el pico de la curva | Marca la frecuencia central de sibilancia actualmente sintonizada en la curva de respuesta. |
| Franja de reducción de ganancia | Vacía o llenado rojo suave     | Atenuación actual aplicada a la banda de sibilancia.                      |

## Consejos

- El medidor funciona a aproximadamente 30 Hz, por lo que los transitorios cortos y agudos pueden aparecer como destellos breves. Esto es normal.
- Mantenga el mando **Amount** en su valor predeterminado de −6.0 dB mientras observa el medidor por primera vez. Ajústelo solo después de haber confirmado que el medidor se está disparando con los sonidos correctos.
- Si la bola en la curva de respuesta de la cadena lateral está lejos de donde alcanza su pico su sibilancia, use **Freq** para moverla. El medidor solo mostrará GR cuando la energía en la banda de **Freq** actual supere **Thresh**.
- Cuando la etapa De-Ess está en bypass en el widget CHAIN, todo el mosaico del applet se atenúa visiblemente. Si el mosaico aparece atenuado, confirme que la etapa no esté en bypass antes de interpretar el medidor.
- Para acceder a la instancia RX del de-esser (titulada "Aetherial De-Esser — RX"), ábrala desde el Aetherial Audio Channel Strip, no desde el panel del applet acoplado.

## Solución de problemas

- **La barra de reducción de ganancia nunca se mueve** — El de-esser no se está disparando. Verifique que la etapa De-Ess esté habilitada en el widget CHAIN, que el audio fluya a través del DSP de TX y que **Thresh** no esté configurado demasiado alto (demasiado cerca de 0.0 dB) para su nivel de micrófono.
- **La barra de reducción de ganancia llega al tope derecho en cada sílaba, incluido el habla no sibilante** — **Thresh** está configurado demasiado bajo. Súbalo hacia 0.0 dB hasta que las vocales normales ya no disparen el medidor.
- **La barra se mueve pero no se escucha ningún efecto al aire** — **Amount** puede estar configurado demasiado cerca de 0.0 dB. Bájelo hacia −24.0 dB para una reducción más audible, o confirme que la etapa no esté en bypass en el widget CHAIN.
- **El mosaico del applet aparece atenuado** — La etapa De-Ess está en bypass. Haga clic una vez en la etapa DESS en el widget CHAIN para volver a habilitarla. El mosaico volverá a la opacidad completa cuando la etapa esté activa.

## Relacionados

- [Ajuste el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajuste Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Varíe Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Ponga en bypass el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
