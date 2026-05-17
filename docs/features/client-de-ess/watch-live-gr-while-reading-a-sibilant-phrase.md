# Ver el GR en vivo mientras lee una frase sibilante

La barra de reducción de ganancia (GR) del Aetherial De-Esser se actualiza en tiempo real mientras transmite o habla. Utilice este procedimiento para observar cómo responde el medidor mientras lee una frase sibilante, y así confirmar que el de-esser está capturando sus sonidos "S" y "T" antes de salir al aire.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado a través del widget CHAIN. La applet está oculta hasta que la etapa De-Ess esté activa.
- Su micrófono debe estar enrutado a través de la cadena de audio TX y produciendo señal, ya sea pulsando la radio o usando un modo de monitor/prueba para que el audio fluya a través del DSP.
- Abra el subcontenedor "Aetherial De-Esser" dentro del contenedor principal Aetherial Audio (TXDSP). El bypass y la edición se manejan a través del Aetherial Audio Channel Strip — no hay un editor flotante separado para el de-esser.
- El panel del de-esser admite ambos lados, TX y RX. La instancia RX se titula "Aetherial De-Esser — RX" y es accesible a través del Aetherial Audio Channel Strip.

## Pasos

1. Asegúrese de que la etapa De-Ess esté habilitada en el widget CHAIN. La applet será visible una vez que la etapa esté activa. Cuando la etapa está en bypass, todo el mosaico se atenúa hasta aproximadamente un 55% de opacidad.
2. Localice la **barra de reducción de ganancia** — la franja horizontal justo debajo de la curva de respuesta de la cadena lateral.
3. Pulse su radio o active su ruta de audio para que el audio del micrófono fluya a través del DSP de TX.
4. Pronuncie una frase que contenga mucha sibilancia — por ejemplo, "Ella vende conchas marinas en la orilla del mar" — a su nivel y distancia de micrófono normales.
5. Observe cómo la **barra de reducción de ganancia** se llena de derecha a izquierda en rojo suave con cada sonido "S" o "T". Sin relleno significa que el de-esser no se está disparando; un relleno que alcanza el ancho completo significa que se está aplicando hasta 24 dB de reducción.
6. Note dónde suele alcanzar su punto máximo la barra. La marca en la barra indica el punto de −6 dB, que es el valor predeterminado de **Amount** y un objetivo común para un de-essing transparente.
7. Si la barra nunca se mueve, baje **Thresh** hacia −60.0 dB hasta que comience a responder. Si la barra se queda fijada a la derecha en cada sílaba, suba **Thresh** hacia 0.0 dB.
8. Repita la frase hasta que la barra responda solo en picos sibilantes genuinos, no en el habla normal.

## Qué hace cada control

| Control                     | Predeterminado | Rango válido    | Descripción                                                                                                                             |
|-----------------------------|----------------|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| Curva de respuesta de cadena lateral | —              | —               | ClientDeEssCurveWidget en modo compacto. Dibuja la respuesta del filtro pasabanda con un punto móvil en la frecuencia central actual.   |
| Barra de reducción de ganancia       | —              | 0 a 24 dB GR    | Franja horizontal roja suave, rellena por la derecha. La escala máxima es 24 dB; una marca señala los −6 dB típicos. Se actualiza a ~30 Hz. |
| Freq                        | 6000 Hz        | 1000 a 12000 Hz | Mapeo logarítmico (1000 * 12^n). Establece la frecuencia central de la banda de sibilancia. La etiqueta muestra "6.0 kHz" por encima de 1 kHz, "N Hz" por debajo. |
| Q                           | 2.00           | 0.5 a 5.0       | Mapeo lineal. Establece el ancho de banda de la banda de sibilancia — Q más alto = más estrecho. La etiqueta muestra "X.XX".             |
| Thresh                      | −30.0 dB       | −60.0 a 0.0 dB  | Mapeo lineal. Nivel por encima del cual el de-esser comienza a atenuar la banda.                                                         |
| Amount                      | −6.0 dB        | −24.0 a 0.0 dB  | Mapeo lineal. Atenuación máxima aplicada en el pico de sibilancia. Los valores son negativos (o cero) porque representan reducción.     |
| Attack                      | 1.0 ms         | 0.1 a 30.0 ms   | Mapeo exponencial (0.1 * 300^n). Establece la rapidez con la que el de-esser responde una vez que la sibilancia cruza el umbral. Solo presente en el panel del Channel Strip. |
| Release                     | 100 ms         | 10.0 a 500.0 ms | Mapeo exponencial (10 * 50^n). Establece la rapidez con la que la ganancia vuelve después de que la sibilancia cae por debajo del umbral. Solo presente en el panel del Channel Strip. |

**Nota:** Los controles Attack y Release están disponibles en el StripDeEssPanel del Channel Strip (tanto en instancias RX como TX). La applet ClientDeEssApplet acoplada omite estos dos mandos.

## Indicadores

| Indicador                   | Estados                        | Significado                                                             |
|-----------------------------|--------------------------------|-------------------------------------------------------------------------|
| Punto de frecuencia central | Reposando en el pico de la curva | Marca la frecuencia central de sibilancia actualmente sintonizada en la curva de respuesta. |
| Franja de reducción de ganancia | Vacía o relleno rojo suave     | Atenuación actual aplicada a la banda de sibilancia.                    |

## Edición de valores en línea

Todos los controles de mando en el Aetherial De-Esser admiten la edición de valores en línea. En lugar de arrastrar el mando, puede hacer clic en el texto del valor debajo del mando para abrir una pequeña superposición de editor de texto. Esto es útil para establecer valores precisos rápidamente.

**Cómo usar la edición en línea:**

1. Haga clic en el texto del valor que se muestra debajo de cualquier mando (por ejemplo, "6.0 kHz" debajo de Freq).
2. Aparece un pequeño campo de texto con un fondo oscuro y un borde cian para indicar el modo de edición.
3. Escriba un nuevo valor. Puede incluir unidades o texto adicional — el editor elimina los caracteres no numéricos automáticamente. Por ejemplo, puede escribir "12.5 ms" o "−6 dB" y se extraerá el valor.
4. Presione Enter para confirmar el valor. El editor se cierra y el mando se actualiza al nuevo valor.
5. Haga clic en cualquier otro lugar de la interfaz o presione Tab para mover el foco — el valor también se confirma al perder el foco, igual que al presionar Enter.
6. Presione Escape para cancelar la edición y volver al valor anterior sin cambios.

**Formatos de entrada admitidos:**
- Números simples: "4500" o "3.5"
- Decimales con reconocimiento local: "12,5" funciona en configuraciones regionales con coma decimal
- Valores con unidades o símbolos: "6.0 kHz", "−30 dB", "1.00 ms"
- El editor inteligentemente elimina caracteres no numéricos, por lo que puede ingresar valores exactamente como aparecen en el formato de etiqueta del mando

## Consejos

- El medidor funciona a aproximadamente 30 Hz, por lo que los transitorios cortos y agudos pueden aparecer como destellos breves. Esto es normal.
- Mantenga el mando **Amount** en su valor predeterminado de −6.0 dB mientras observa el medidor por primera vez. Ajústelo solo después de haber confirmado que el medidor se activa con los sonidos correctos.
- Si el punto en la curva de respuesta de la cadena lateral se sitúa lejos de donde alcanzan su punto máximo sus sibilancias, use **Freq** para moverlo. El medidor solo mostrará GR cuando la energía en la banda **Freq** actual cruce **Thresh**.
- Cuando la etapa De-Ess está en bypass en el widget CHAIN, todo el mosaico de la applet se atenúa visiblemente. Si el mosaico parece atenuado, confirme que la etapa no esté en bypass antes de interpretar el medidor.
- Para acceder a la instancia RX del de-esser (titulada "Aetherial De-Esser — RX"), ábrala desde el Aetherial Audio Channel Strip en lugar del panel de la applet acoplada.
- Las etiquetas del eje de frecuencia en la curva de respuesta de la cadena lateral usan "100", "500", "1k", etc. para mayor claridad y se representan con un tamaño de fuente de 8 píxeles. El widget de la curva almacena en caché estas etiquetas para mejorar el rendimiento de renderizado.
- Para una entrada de valor precisa, use el editor en línea haciendo clic en el valor mostrado del mando. Esto es más rápido que ajustar con arrastres del ratón y evita sobrepasar el valor deseado.

## Solución de problemas

- **La barra de reducción de ganancia nunca se mueve** — El de-esser no se está activando. Verifique que la etapa De-Ess esté habilitada en el widget CHAIN, que el audio fluya a través del DSP de TX y que **Thresh** no esté configurado demasiado alto (demasiado cerca de 0.0 dB) para el nivel de su micrófono.
- **La barra de reducción de ganancia se queda fijada a la derecha en cada sílaba, incluyendo el habla no sibilante** — **Thresh** está configurado demasiado bajo. Súbalo hacia 0.0 dB hasta que las vocales normales ya no activen el medidor.
- **La barra se mueve pero no oye ningún efecto al aire** — **Amount** puede estar configurado demasiado cerca de 0.0 dB. Bájelo hacia −24.0 dB para una reducción más audible, o confirme que la etapa no esté en bypass en el widget CHAIN.
- **El mosaico de la applet aparece atenuado** — La etapa De-Ess está en bypass. Haga clic una vez en la etapa DESS en el widget CHAIN para volver a habilitarla. El mosaico volverá a la opacidad completa cuando la etapa esté activa.
- **El editor en línea vuelve al valor incorrecto después de escribir** — Asegúrese de presionar Enter para confirmar antes de hacer clic en otro lugar. Si hace clic en otro control mientras el editor está abierto, el valor se confirma automáticamente, lo que puede no coincidir con el punto de ajuste deseado si no había terminado de escribir.

## Relacionados

- [Ajustar el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Pasar por alto el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
