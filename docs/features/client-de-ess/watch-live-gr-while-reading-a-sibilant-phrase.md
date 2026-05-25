# Observe la ganancia de reducción (GR) en vivo mientras lee una frase sibilante

La barra de reducción de ganancia (GR) en el Aetherial De-Esser se actualiza en tiempo real mientras transmite o habla. Utilice este procedimiento para observar la respuesta del medidor mientras lee una frase sibilante, de modo que pueda confirmar que el de-esser está captando sus sonidos "S" y "T" antes de salir al aire.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado a través del widget CHAIN. El applet permanece oculto hasta que la etapa De-Ess esté activa.
- Su micrófono debe estar enrutado a través de la cadena de audio TX y generando señal (ya sea activando el equipo de radio o usando un modo de monitor/prueba para que el audio fluya a través del DSP).
- Abra el subcontenedor "Aetherial De-Esser" dentro del contenedor principal Aetherial Audio (TXDSP). El bypass y la edición se manejan a través del Aetherial Audio Channel Strip; no hay un editor flotante separado para el de-esser.
- El panel del de-esser admite ambos lados, TX y RX. La instancia RX se titula "Aetherial De-Esser — RX" y es accesible a través del Aetherial Audio Channel Strip.

## Pasos

1. Asegúrese de que la etapa De-Ess esté habilitada en el widget CHAIN. El applet será visible una vez que la esté activa. Cuando la etapa está en bypass, todo el mosaico se atenúa aproximadamente al 55% de opacidad.
2. Localice la **barra de reducción de ganancia**: la franja horizontal directamente debajo de la curva de respuesta de la cadena lateral.
3. Active su equipo de radio o active su ruta de audio para que el audio del micrófono fluya a través del DSP de TX.
4. Diga una frase que contenga una sibilancia intensa, por ejemplo, "Ella vende conchas marinas junto al mar", a su nivel de micrófono y distancia normales.
5. Observe la **barra de reducción de ganancia** llenarse de derecha a izquierda en un tono rojo suave en cada sonido "S" o "T". Sin relleno significa que el de-esser no se está activando; un relleno que alcanza el ancho completo significa que se está aplicando hasta 24 dB de reducción.
6. Observe dónde suele alcanzar el pico la barra. La marca en la barra indica el punto de −6 dB, que es el valor predeterminado de **Amount** y un objetivo común para un de-essing transparente.
7. Si la barra nunca se mueve, reduzca **Thresh** hacia −60.0 dB hasta que comience a responder. Si la barra está fijada a la derecha en cada sílaba, aumente **Thresh** hacia 0.0 dB.
8. Repita la frase hasta que la barra responda solo en los picos de sibilancia genuinos, no en el habla ordinaria.

## Función de cada control

| Control                    | Predeterminado | Rango válido       | Comportamiento                                                                                                                                                                                                                               |
|----------------------------|----------------|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva de respuesta de cadena lateral | —              | —                  | ClientDeEssCurveWidget en modo compacto. Dibuja la respuesta del filtro paso banda con un indicador móvil en la frecuencia central actual.                                                                                                      |
| Barra de reducción de ganancia       | —              | 0 a 24 dB GR       | Franja horizontal roja suave, relleno desde la derecha. La escala máxima es 24 dB; una marca indica el valor típico de -6 dB. Se actualiza a ~30 Hz desde ClientDeEss::gainReductionDb().                                                            |
| Freq                     | 6000 Hz        | 1000 a 12000 Hz    | Mapeo logarítmico (1000 * 12^n). Establece la frecuencia central de la banda de sibilancia. Etiqueta '6.0 kHz' por encima de 1 kHz, 'N Hz' por debajo.                                                                                          |
| Q                        | 2.00           | 0.5 a 5.0          | Mapeo lineal. Establece el ancho de banda de la banda de sibilancia: Q más alto = más estrecho. Etiqueta 'X.XX'.                                                                                                                               |
| Thresh                   | −30.0 dB       | −60.0 a 0.0 dB     | Mapeo lineal. Nivel por encima del cual el de-esser comienza a atenuar la banda.                                                                                                                                                            |
| Amount                   | −6.0 dB        | −24.0 a 0.0 dB     | Mapeo lineal. Atenuación máxima aplicada en el pico de sibilancia. Los valores son negativos (o cero) porque representan reducción.                                                                                                           |
| Attack                   | 1.0 ms         | 0.1 a 30.0 ms      | Mapeo exponencial (0.1 * 300^n). Solo disponible en el StripDeEssPanel del Channel Strip (RX y TX). El ClientDeEssApplet acoplado omite este control.                                                                                            |
| Release                  | 100 ms         | 10.0 a 500.0 ms    | Mapeo exponencial (10 * 50^n). Solo disponible en el StripDeEssPanel del Channel Strip (RX y TX). El ClientDeEssApplet acoplado omite este control.                                                                                             |
| Slope                    | 24 dB/oct      | 12 / 24 / 36 / 48 dB/oct (1 a 4 etapas) | Botón pulsador que recorre la cascada de paso banda de la cadena lateral. Cada etapa añade 12 dB/oct de atenuación fuera de la banda de sibilancia. Pendiente más alta = muesca efectiva más estrecha, menos daño colateral en la banda media en frases con muchas "S". Presente en ambas rutas TX y RX. Se guarda como `ClientDeEssTxSlopeStages` / `ClientDeEssRxSlopeStages`. |

**Nota:** Los controles Attack y Release están disponibles en el StripDeEssPanel del Channel Strip (tanto instancias RX como TX). El ClientDeEssApplet acoplado omite estos dos controles.

## Indicadores

| Indicador                    | Estados                       | Significado                                                               |
|------------------------------|-------------------------------|---------------------------------------------------------------------------|
| Indicador de frecuencia central | En reposo en el pico de la curva | Marca la frecuencia central de sibilancia actualmente sintonizada en la curva de respuesta. |
| Franja de reducción de ganancia | Vacía o relleno rojo suave    | Atenuación actual aplicada a la banda de sibilancia.                      |

## Edición de valores en línea

Todos los mandos del Aetherial De-Esser admiten la edición de valores en línea. En lugar de arrastrar el mando, puede hacer clic en el texto del valor debajo del mando para abrir una pequeña superposición de editor de texto. Esto es útil para establecer valores precisos rápidamente.

**Cómo usar la edición en línea:**

1. Haga clic en el texto del valor que se muestra debajo de cualquier mando (por ejemplo, "6.0 kHz" debajo de Freq).
2. Aparece un pequeño campo de texto con un fondo oscuro y un borde cian para indicar el modo de edición.
3. Escriba un nuevo valor. Puede incluir unidades o texto adicional; el editor elimina caracteres no numéricos automáticamente. Por ejemplo, puede escribir "12.5 ms" o "−6 dB" y el valor será extraído.
4. Presione Enter para confirmar el valor. El editor se cierra y el mando se actualiza al nuevo valor.
5. Haga clic en cualquier otro lugar de la interfaz o presione Tab para mover el foco; el valor también se confirma al perder el foco, igual que al presionar Enter.
6. Presione Escape para cancelar la edición y volver al valor anterior sin cambios.

**Formatos de entrada admitidos:**
- Números simples: "4500" o "3.5"
- Decimales con configuración regional: "12,5" funciona en configuraciones regionales que usan coma decimal
- Valores con unidades o símbolos: "6.0 kHz", "−30 dB", "1.00 ms"
- El editor elimina inteligentemente los caracteres no numéricos, por lo que puede ingresar los valores exactamente como aparecen en la etiqueta del mando

## Consejos

- El medidor funciona aproximadamente a 30 Hz, por lo que los transitorios cortos y agudos pueden aparecer como destellos breves. Esto es normal.
- Mantenga el mando **Amount** en su valor predeterminado de −6.0 dB mientras observa el medidor por primera vez. Ajústelo solo después de haber confirmado que el medidor se activa con los sonidos correctos.
- Si el indicador en la curva de respuesta de la cadena lateral se encuentra lejos de donde alcanzan su pico sus sibilancias, use **Freq** para moverlo. El medidor solo mostrará GR cuando la energía en la banda actual de **Freq** supere **Thresh**.
- Cuando la etapa De-Ess está en bypass en el widget CHAIN, todo el mosaico del applet se atenúa visiblemente. Si el mosaico parece desteñido, confirme que la etapa no esté en bypass antes de interpretar el medidor.
- Para acceder a la instancia RX del de-esser (titulada "Aetherial De-Esser — RX"), ábrala desde el Aetherial Audio Channel Strip en lugar del panel del applet acoplado.
- Las etiquetas del eje de frecuencia en la curva de respuesta de la cadena lateral usan "100", "500", "1k", etc. para mayor claridad y se representan con un tamaño de fuente de 8 píxeles. El widget de la curva almacena en caché estas etiquetas para mejorar el rendimiento de representación.
- Para una entrada de valor precisa, use el editor en línea haciendo clic en el valor mostrado del mando. Esto es más rápido que ajustar con arrastres del ratón y evita sobrepasar el valor deseado.
- El botón **Slope** recorre 12 → 24 → 36 → 48 dB/oct con cada clic. Las pendientes más altas crean una muesca más estrecha alrededor de la frecuencia de sibilancia, lo que reduce la atenuación colateral de la banda de habla media. El botón se encuentra en la esquina inferior izquierda del panel del de-esser en el Channel Strip, debajo del mando Thresh.

## Resolución de problemas

- **La barra de reducción de ganancia nunca se mueve** — El de-esser no se está activando. Verifique que la etapa De-Ess esté habilitada en el widget CHAIN, que el audio fluya a través del DSP de TX y que **Thresh** no esté configurado demasiado alto (demasiado cerca de 0.0 dB) para su nivel de micrófono.
- **La barra de reducción de ganancia está fijada a la derecha en cada sílaba, incluido el habla no sibilante** — **Thresh** está configurado demasiado bajo. Auméntelo hacia 0.0 dB hasta que las vocales ordinarias ya no activen el medidor.
- **La barra se mueve pero no se oye ningún efecto al aire** — Es posible que **Amount** esté configurado demasiado cerca de 0.0 dB. Redúzcalo hacia −24.0 dB para una reducción más audible, o confirme que la etapa no esté en bypass en el widget CHAIN.
- **El mosaico del applet parece atenuado** — La etapa De-Ess está en bypass. Haga un solo clic en la etapa DESS en el widget CHAIN para volver a habilitarla. El mosaico volverá a la opacidad completa cuando la etapa esté activa.
- **El editor en línea revierte al valor incorrecto después de escribir** — Asegúrese de presionar Enter para confirmar antes de hacer clic en otro lugar. Si hace clic en otro control mientras el editor está abierto, el valor se confirma automáticamente, lo que puede no coincidir con el valor deseado si no había terminado de escribir.
- **Los sonidos sibilantes siguen siendo ásperos después de ajustar Freq y Q** — Intente aumentar **Slope** a 36 o 48 dB/oct. Una pendiente más pronunciada crea una muesca más estrecha que corta la sibilancia con mayor precisión sin afectar la banda de habla de frecuencias medias.

## Relacionados

- [Establecer el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Poner en bypass el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
