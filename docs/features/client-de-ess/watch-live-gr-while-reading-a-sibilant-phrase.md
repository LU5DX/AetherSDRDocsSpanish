# Ver el GR en vivo mientras lee una frase sibilante

La barra de reducción de ganancia (GR) del Aetherial De-Esser se actualiza en tiempo real mientras transmite o habla. Use este procedimiento para observar la respuesta del medidor mientras lee una frase sibilante, de modo que pueda confirmar que el de-esser está capturando sus sonidos "S" y "T" antes de salir al aire.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado mediante el widget CHAIN. El applet permanece oculto hasta que la etapa De-Ess esté activa.
- Su micrófono debe estar enrutado a través de la cadena de audio de TX y generando señal, ya sea presionando la tecla del radio o usando un modo de monitoreo/prueba para que el audio fluya a través del DSP.
- Abra el subcontenedor "Aetherial De-Esser" dentro del contenedor principal Aetherial Audio (TXDSP). Tanto el bypass como la edición se manejan a través del Aetherial Audio Channel Strip; no hay un editor flotante independiente para el de-esser en la versión v0.9.7.
- El panel del de-esser admite tanto el lado TX como el RX. La instancia de RX se titula "Aetherial De-Esser — RX" y es accesible a través del Aetherial Audio Channel Strip.

## Pasos

1. Asegúrese de que la etapa De-Ess esté habilitada en el widget CHAIN. El applet será visible una vez que la etapa esté activa. Cuando la etapa está en bypass, todo el mosaico se atenúa hasta aproximadamente un 55% de opacidad.
2. Localice la **Barra de reducción de ganancia**: la franja horizontal justo debajo de la curva de respuesta de la cadena lateral.
3. Presione la tecla de su radio o active su ruta de audio para que el audio del micrófono fluya a través del DSP de TX.
4. Diga una frase que contenga mucha sibilancia, por ejemplo, "She sells seashells by the seashore", a su nivel de micrófono y distancia habituales.
5. Observe cómo la **Barra de reducción de ganancia** se llena de derecha a izquierda en un tono rojo suave en cada sonido "S" o "T". Sin relleno significa que el de-esser no se está activando; un relleno que alcanza el ancho completo significa que se está aplicando hasta 24 dB de reducción.
6. Note dónde suele alcanzar su punto máximo la barra. La marca en la barra indica el punto de −6 dB, que es el valor predeterminado de **Amount** y un objetivo común para un de-essing transparente.
7. Si la barra nunca se mueve, baje **Thresh** hacia −60.0 dB hasta que comience a responder. Si la barra está fija a la derecha en cada sílaba, suba **Thresh** hacia 0.0 dB.
8. Repita la frase hasta que la barra responda solo en los picos de sibilancia genuinos, no en el habla normal.

## Función de cada control

| Control                        | Valor predeterminado | Rango válido    | Descripción                                                                                                                          |
|--------------------------------|----------------------|-----------------|--------------------------------------------------------------------------------------------------------------------------------------|
| Curva de respuesta lateral     | —                    | —               | ClientDeEssCurveWidget en modo compacto. Dibuja la respuesta del filtro paso banda con un indicador móvil en la frecuencia central actual. |
| Barra de reducción de ganancia | —                    | 0 a 24 dB GR    | Franja horizontal roja suave, relleno desde la derecha. La escala máxima es 24 dB; una marca indica el valor típico de −6 dB. Se actualiza a ~30 Hz. |
| Freq                           | 6000 Hz              | 1000 a 12000 Hz | Mapeo logarítmico. Establece la frecuencia central de la banda de sibilancia. La etiqueta muestra "6.0 kHz" por encima de 1 kHz, "N Hz" por debajo. |
| Q                              | 2.00                 | 0.5 a 5.0       | Mapeo lineal. Establece el ancho de banda de la banda de sibilancia: Q más alto = más estrecho. La etiqueta muestra "X.XX".           |
| Thresh                         | −30.0 dB             | −60.0 a 0.0 dB  | Mapeo lineal. Nivel por encima del cual el de-esser comienza a atenuar la banda.                                                     |
| Amount                         | −6.0 dB              | −24.0 a 0.0 dB  | Mapeo lineal. Atenuación máxima aplicada en el pico de sibilancia. Los valores son negativos (o cero) porque representan reducción.   |
| Attack                         | 1.0 ms               | 0.1 a 30.0 ms   | Mapeo exponencial. Define la rapidez con la que el de-esser responde cuando la sibilancia supera el umbral. Solo presente en el panel del Channel Strip. |
| Release                        | 100 ms               | 10.0 a 500.0 ms | Mapeo exponencial. Define la rapidez con la que la ganancia vuelve a la normalidad después de que la sibilancia cae por debajo del umbral. Solo presente en el panel del Channel Strip. |

**Nota:** Los controles de Attack y Release están disponibles en el StripDeEssPanel del Channel Strip (tanto en instancias RX como TX). El ClientDeEssApplet acoplado omite estos dos mandos.

## Indicadores

| Indicador              | Estados                         | Significado                                                                    |
|------------------------|----------------------------------|--------------------------------------------------------------------------------|
| Bola de frecuencia central | En reposo sobre el pico de la curva | Marca la frecuencia central de sibilancia actualmente sintonizada en la curva de respuesta. |
| Franja de reducción de ganancia | Vacía o relleno rojo suave       | Atenuación actual aplicada a la banda de sibilancia.                           |

## Consejos

- El medidor funciona a aproximadamente 30 Hz, por lo que los transitorios cortos y agudos pueden aparecer como destellos breves. Esto es normal.
- Mantenga el mando **Amount** en su valor predeterminado de −6.0 dB mientras observa el medidor por primera vez. Ajústelo a la baja solo después de haber confirmado que el medidor se activa con los sonidos correctos.
- Si la bola en la curva de respuesta de la cadena lateral está lejos de donde alcanzan su punto máximo sus sibilancias, use **Freq** para moverla. El medidor solo mostrará GR cuando la energía en la banda actual de **Freq** supere **Thresh**.
- Cuando la etapa De-Ess está en bypass en el widget CHAIN, todo el mosaico del applet se atenúa visiblemente. Si el mosaico parece descolorido, confirme que la etapa no esté en bypass antes de interpretar el medidor.
- Para acceder a la instancia del de-esser de RX (titulada "Aetherial De-Esser — RX"), ábrala desde el Aetherial Audio Channel Strip en lugar del panel del applet acoplado.
- Las etiquetas del eje de frecuencia en la curva de respuesta de la cadena lateral usan "100", "500", "1k", etc. para mayor claridad y se renderizan con un tamaño de fuente de 8 píxeles. El widget de la curva almacena en caché estas etiquetas para mejorar el rendimiento de renderizado.

## Solución de problemas

- **La barra de reducción de ganancia nunca se mueve** — El de-esser no se está activando. Verifique que la etapa De-Ess esté habilitada en el widget CHAIN, que el audio fluya a través del DSP de TX y que **Thresh** no esté configurado demasiado alto (demasiado cerca de 0.0 dB) para el nivel de su micrófono.
- **La barra de reducción de ganancia está fija a la derecha en cada sílaba, incluido el habla no sibilante** — **Thresh** está configurado demasiado bajo. Súbalo hacia 0.0 dB hasta que las vocales normales ya no activen el medidor.
- **La barra se mueve pero no se escucha ningún efecto al aire** — **Amount** puede estar configurado demasiado cerca de 0.0 dB. Bájelo hacia −24.0 dB para una reducción más audible, o confirme que la etapa no esté en bypass en el widget CHAIN.
- **El mosaico del applet parece atenuado** — La etapa De-Ess está en bypass. Haga clic una vez en la etapa DESS en el widget CHAIN para volver a habilitarla. El mosaico volverá a la opacidad completa cuando la etapa esté activa.

## Relacionados

- [Establecer el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Pasar por alto el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
