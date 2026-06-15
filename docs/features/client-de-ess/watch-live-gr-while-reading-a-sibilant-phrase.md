# Vea la reducción de ganancia en vivo mientras lee una frase sibilante

La barra de reducción de ganancia (GR) en el Aetherial De-Esser se actualiza en tiempo real mientras transmite o habla. Use este procedimiento para observar cómo responde el medidor mientras lee una frase sibilante, para confirmar que el desempañador está capturando sus sonidos "S" y "T" antes de salir al aire.

## Antes de empezar

- El Aetherial De-Esser debe estar habilitado a través del widget CHAIN. La applet permanece oculta hasta que la etapa De-Ess esté activa.
- Su micrófono debe estar enrutado a través de la cadena de audio TX y produciendo señal, ya sea pulsando el equipo o usando un modo de monitor/prueba para que el audio fluya a través del DSP.
- Abra el subcontenedor "Aetherial De-Esser" dentro del contenedor padre Aetherial Audio (TXDSP). Tanto la omisión como la edición se manejan a través del Aetherial Audio Channel Strip — no hay un editor flotante separado para el desempañador.
- El panel del desempañador admite los lados TX y RX. La instancia RX se titula "Aetherial De-Esser — RX" y se accede a través del Aetherial Audio Channel Strip.

## Pasos

1. Asegúrese de que la etapa De-Ess esté habilitada en el widget CHAIN. La applet será visible una vez que la etapa esté activa. Cuando la etapa está omitida, todo el mosaico se atenúa aproximadamente al 55% de opacidad.
2. Localice la **Barra de reducción de ganancia** — la tira horizontal justo debajo de la curva de respuesta de la cadena lateral.
3. Pulse su radio o active su ruta de audio para que el audio del micrófono fluya a través del DSP de TX.
4. Pronuncie una frase que contenga sibilancia fuerte — por ejemplo, "She sells seashells by the seashore" — a su nivel y distancia de micrófono normales.
5. Observe cómo la **Barra de reducción de ganancia** se llena de derecha a izquierda en rojo suave en cada sonido "S" o "T". Sin relleno significa que el desempañador no está disparando; un relleno que alcanza el ancho completo significa que se están aplicando hasta 24 dB de reducción.
6. Observe dónde suele alcanzar su punto máximo la barra. La marca en la barra indica el punto de −6 dB, que es el valor predeterminado de **Amount** y un objetivo común para un desempañado transparente.
7. Si la barra nunca se mueve, baje **Thresh** hacia −60.0 dB hasta que comience a responder. Si la barra está fija a la derecha en cada sílaba, suba **Thresh** hacia 0.0 dB.
8. Repita la frase hasta que la barra responda solo en picos sibilantes genuinos, no en el habla normal.

## Qué hace cada control

| Control                     | Predeterminado | Rango válido                              |
|-----------------------------|----------------|-------------------------------------------|
| Curva de respuesta de cadena lateral | —      | —                                         |
| Barra de reducción de ganancia       | —      | 0 a 24 dB de GR                          |
| Freq                         | 6000 Hz       | 1000 a 12000 Hz                          |
| Q                            | 2.00          | 0.5 a 5.0                                |
| Thresh                       | −30.0 dB      | −60.0 a 0.0 dB                           |
| Amount                       | −6.0 dB       | −24.0 a 0.0 dB                           |
| Attack                       | 1.0 ms        | 0.1 a 30.0 ms                            |
| Release                      | 100 ms        | 10.0 a 500.0 ms                          |
| Slope                        | 24 dB/oct     | 12 / 24 / 36 / 48 dB/oct (1 a 4 etapas) |

**Nota:** Los controles Attack y Release están disponibles en el StripDeEssPanel del Channel Strip (tanto en instancias RX como TX). La applet ClientDeEssApplet acoplada omite estos dos mandos.

## Indicadores

| Indicador                     | Estados                          | Significado                                                            |
|-------------------------------|----------------------------------|------------------------------------------------------------------------|
| Bola de frecuencia central    | Reposando en el pico de la curva | Marca la frecuencia central de sibilancia actualmente sintonizada en la curva de respuesta. |
| Tira de reducción de ganancia | Vacía o relleno rojo suave       | Atenuación actual aplicada a la banda de sibilancia.                  |

## Edición de valor en línea

Todos los controles de mando en el Aetherial De-Esser admiten la edición de valor en línea. En lugar de arrastrar el mando, puede hacer clic en el texto del valor debajo del mando para abrir una pequeña superposición de editor de texto. Esto es útil para establecer valores precisos rápidamente.

**Cómo usar la edición en línea:**

1. Haga clic en el texto del valor mostrado debajo de cualquier mando (por ejemplo, "6.0 kHz" debajo de Freq).
2. Aparece un pequeño campo de texto con un fondo oscuro y un borde cian para indicar el modo de edición.
3. Escriba un nuevo valor. Puede incluir unidades o texto adicional — el editor elimina automáticamente los caracteres no numéricos. Por ejemplo, puede escribir "12.5 ms" o "−6 dB" y el valor será extraído.
4. Presione Enter para confirmar el valor. El editor se cierra y el mando se actualiza al nuevo valor.
5. Haga clic en otra parte de la interfaz de usuario o presione Tab para mover el foco — el valor también se confirma al perder el foco, igual que al presionar Enter.
6. Presione Escape para cancelar la edición y volver al valor anterior sin cambios.

**Formatos de entrada admitidos:**
- Números simples: "4500" o "3.5"
- Decimales locales: "12,5" funciona en configuraciones regionales de coma decimal
- Valores con unidades o símbolos: "6.0 kHz", "−30 dB", "1.00 ms"
- El editor elimina inteligentemente caracteres no numéricos, por lo que puede ingresar valores exactamente como aparecen en el formato de etiqueta del mando

## Consejos

- El medidor funciona a aproximadamente 30 Hz, por lo que los transitorios cortos y agudos pueden aparecer como destellos breves. Esto es normal.
- La barra de reducción de ganancia ahora se actualiza de manera más uniforme durante la sibilancia sostenida. Antes de v26.6.3, el temporizador de animación podía detenerse temprano durante un desempañado continuo. Ahora el medidor se repinta continuamente mientras la reducción de ganancia está activa, incluso si el suavizador interno se estabiliza temporalmente. Esto significa que verá una barra estable y receptiva durante un sonido "S" largo en lugar de un destello breve que desaparece.
- Mantenga el mando **Amount** en su valor predeterminado de −6.0 dB mientras observa el medidor por primera vez. Ajústelo solo después de haber confirmado que el medidor se dispara en los sonidos correctos.
- Si la bola en la curva de respuesta de la cadena lateral se sitúa lejos de donde sus picos de sibilancia alcanzan su máximo, use **Freq** para moverla. El medidor solo mostrará GR cuando la energía en la banda de **Freq** actual cruce **Thresh**.
- Cuando la etapa De-Ess está omitida en el widget CHAIN, todo el mosaico de la applet se atenúa visiblemente. Si el mosaico parece descolorido, confirme que la etapa no esté omitida antes de interpretar el medidor.
- Para acceder a la instancia RX del desempañador (titulada "Aetherial De-Esser — RX"), ábrala desde el Aetherial Audio Channel Strip en lugar del panel de applet acoplado.
- Las etiquetas del eje de frecuencia en la curva de respuesta de la cadena lateral usan "100", "500", "1k", etc. para mayor claridad y se representan en un tamaño de fuente de 8 píxeles. El widget de la curva almacena en caché estas etiquetas para mejorar el rendimiento de la representación.
- Para la entrada de valor precisa, use el editor en línea haciendo clic en el valor mostrado del mando. Esto es más rápido que ajustar con arrastres del ratón y evita sobrepasar su configuración objetivo.
- El botón **Slope** cicla a través de 12 → 24 → 36 → 48 dB/oct con cada clic. Las pendientes más altas crean una muesca más estrecha alrededor de la frecuencia sibilante, reduciendo la atenuación colateral de la banda media del habla. El botón está ubicado en la esquina inferior izquierda del panel del desempañador del Channel Strip, debajo del mando Thresh.

## Solución de problemas

- **La barra de reducción de ganancia nunca se mueve** — El desempañador no se está disparando. Verifique que la etapa De-Ess esté habilitada en el widget CHAIN, que el audio fluya a través del DSP de TX y que **Thresh** no esté configurado demasiado alto (demasiado cerca de 0.0 dB) para el nivel de su micrófono.
- **La barra de reducción de ganancia está fija a la derecha en cada sílaba, incluido el habla no sibilante** — **Thresh** está configurado demasiado bajo. Súbalo hacia 0.0 dB hasta que las vocales normales ya no activen el medidor.
- **La barra se mueve pero no escucha ningún efecto al aire** — **Amount** puede estar configurado demasiado cerca de 0.0 dB. Bájelo hacia −24.0 dB para una reducción más audible, o confirme que la etapa no esté omitida en el widget CHAIN.
- **El mosaico de la applet aparece atenuado** — La etapa De-Ess está omitida. Haga un solo clic en la etapa DESS en el widget CHAIN para volver a habilitarla. El mosaico volverá a la opacidad completa cuando la etapa esté activa.
- **El editor en línea revierte al valor incorrecto después de escribir** — Asegúrese de presionar Enter para confirmar antes de hacer clic en otro lugar. Si hace clic en otro control mientras el editor está abierto, el valor se confirma automáticamente, lo que puede no coincidir con el punto de ajuste deseado si no había terminado de escribir.
- **Los sonidos sibilantes aún son ásperos después de ajustar Freq y Q** — Intente aumentar **Slope** a 36 o 48 dB/oct. Una pendiente más pronunciada crea una muesca más estrecha que corta la sibilancia con mayor precisión sin afectar la banda de frecuencias medias del habla.

## Relacionados

- [Establezca el umbral justo por debajo de los picos 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajuste Amount para el desempañado más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Barra Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Omita el desempañador desde la cadena](bypass-the-de-esser-from-the-chain.md)
