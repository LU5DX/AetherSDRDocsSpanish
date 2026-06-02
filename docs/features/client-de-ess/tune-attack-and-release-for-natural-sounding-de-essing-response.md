# Ajuste de Ataque, Liberación y Pendiente para una respuesta natural del de-esser

Esta página le ayuda a ajustar los controles de Ataque, Liberación y Pendiente en el editor De-Ess del lado de RX o TX para que el de-esser responda a la sibilancia rápidamente sin sonar entrecortado o poco natural.

## Antes de comenzar

- La etapa De-Ess debe estar habilitada en el widget CHAIN (haga clic una vez en DESS para habilitar; haga doble clic para abrir el editor).
- Para TX: el applet acoplado **Aetherial De-Esser** muestra las cuatro perillas comunes (Freq, Q, Thresh, Amount). **Attack**, **Release** y **Slope** solo están disponibles en la ventana del editor sin marco que se abre al hacer doble clic en DESS en el widget CHAIN (o al abrir el Aetherial Audio Channel Strip).
- Para RX: abra el **Aetherial Audio Channel Strip** y haga doble clic en **DESS** en la cadena de RX para abrir el editor De-Ess de RX, que incluye Attack, Release y Slope.
- Los controles Attack, Release y Slope solo están presentes en el **StripDeEssPanel** (dentro del Channel Strip), no en el ClientDeEssApplet acoplado.

## Edición de valores en línea

Todas las perillas en el editor De-Ess ahora admiten entrada numérica en línea para un ajuste preciso:

1. Haga clic en el texto del valor que se muestra debajo de cualquier perilla para entrar en modo de edición. El área del valor muestra un sutil fondo oscuro con un borde cian para indicar el modo de edición.
2. Escriba un valor numérico. Se admite el análisis según la configuración regional (por ejemplo, "12,5" funciona en configuraciones regionales con coma decimal). Las unidades opcionales o el texto descriptivo (por ejemplo, "12.5 ms" o "−6 dB") se eliminan y analizan correctamente.
3. Presione **Enter** o haga clic en otro lugar para confirmar el valor. El valor se limita al rango válido de la perilla.
4. Presione **Escape** mientras edita para cancelar y revertir al valor anterior.

## Pasos

1. Abra el editor De-Ess que incluye Attack, Release y Slope:
   - **TX:** Haga doble clic en la etapa DESS en el widget CHAIN para abrir el editor sin marco titulado **Aetherial De-Esser — TX**.
   - **RX:** Abra el **Aetherial Audio Channel Strip** y haga doble clic en **DESS** en la cadena de RX para abrir el editor De-Ess de RX.

2. Entrene el de-esser con habla sibilante:
   - Barra la perilla **Freq** para localizar su pico de sibilancia (consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)).
   - Ajuste **Thresh** justo por debajo de los picos de 'S' más fuertes (consulte [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)).
   - Ajuste **Amount** para una reducción transparente (consulte [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)).

3. Ajuste **Attack**:
   - Valor predeterminado: **1.0 ms**
   - Rango: **0.1 a 30.0 ms** (mapeo exponencial)
   - Gire **en el sentido de las agujas del reloj** para ralentizar el ataque (mayor tiempo de reacción; puede dejar pasar algo de sibilancia antes de atenuar).
   - Gire **en el sentido contrario a las agujas del reloj** para acelerar el ataque (reacción más rápida; detecta la sibilancia rápidamente, pero puede sonar abrupto si es demasiado rápido).

4. Ajuste **Release**:
   - Valor predeterminado: **100 ms**
   - Rango: **10.0 a 500.0 ms** (mapeo exponencial)
   - Gire **en el sentido de las agujas del reloj** para alargar la liberación (la ganancia vuelve lentamente después de que cesa la sibilancia; puede sonar "bombeado" en habla rápida).
   - Gire **en el sentido contrario a las agujas del reloj** para acortar la liberación (la ganancia vuelve rápidamente; puede sonar entrecortado en sonidos 'S' sostenidos).

5. Ajuste **Slope**:
   - Haga clic en el botón **Slope** en la parte inferior de la columna de perillas izquierda para recorrer las pendientes disponibles.
   - Valor predeterminado: **24 dB/oct** (2 biquads de paso banda en cascada)
   - Configuraciones disponibles: **12, 24, 36, 48 dB/oct** (1 a 4 etapas)
   - Pendiente más alta = muesca efectiva más estrecha alrededor de la frecuencia sibilante = menos daño colateral en bandas medias en frases con muchas 'S'.
   - El texto del botón se actualiza para mostrar la configuración actual (por ejemplo, "24 dB/oct").

6. Pruebe con una frase sibilante mientras observa la **barra de reducción de ganancia** (la franja roja suave en la parte inferior del widget de curva De-Ess):
   - Busque reducciones suaves y breves en cada pico de 'S' (la barra debe llenarse y vaciarse limpiamente con cada sílaba).
   - Si la barra "se queda" después de que cesa la sibilancia, aumente **Release** (sostenimiento más largo).
   - Si la barra reacciona lentamente a la primera 'S' de una palabra, disminuya **Attack** (respuesta más rápida).
   - Si escucha atenuación colateral de las bandas medias del habla en frases con muchas 'S', pruebe con una configuración de **Slope** más alta.

7. Escuche al aire o grabe una muestra corta y ajuste iterativamente hasta que el de-essing suene transparente.

## Qué hace cada control

| Control | Tipo       | Valor predeterminado | Rango              | Mapeo       | Clave de configuración (TX)         | Clave de configuración (RX)         |
|---------|------------|----------------------|--------------------|-------------|-------------------------------------|-------------------------------------|
| Attack  | perilla    | 1.0 ms               | 0.1 a 30.0 ms      | Exponencial | `ClientDeEssTxAttackMs`             | `ClientDeEssRxAttackMs`             |
| Release | perilla    | 100 ms               | 10.0 a 500.0 ms    | Exponencial | `ClientDeEssTxReleaseMs`            | `ClientDeEssRxReleaseMs`            |
| Slope   | botón      | 24 dB/oct            | 12/24/36/48 dB/oct | Etapas biquad en cascada | `ClientDeEssTxSlopeStages`          | `ClientDeEssRxSlopeStages`          |

Estos controles existen solo en los editores de cadena sin marco (StripDeEssPanel). El ClientDeEssApplet acoplado los omite.

## Consejos

- Para voces SSB típicas, **Attack de 0.5 a 2 ms** y **Release de 80 a 150 ms** funcionan bien. El habla muy rápida (por ejemplo, en concursos) puede necesitar valores más cortos en ambos extremos.
- Comience con **Slope** en 24 dB/oct (el valor predeterminado). Aumente a 36 o 48 dB/oct solo si escucha atenuación no deseada de frecuencias del habla cercanas.
- La **marca de -6 dB** en la barra de reducción de ganancia marca el nivel de Amount predeterminado; es una referencia útil para saber cuánto está reduciendo realmente el de-esser.
- La curva de respuesta de la cadena lateral ahora muestra etiquetas de ejes de frecuencia en 100, 500, 1k, 2k, 4k, 8k y 16k Hz utilizando texto estático en caché para mejorar el rendimiento. Las etiquetas de los ejes solo se muestran cuando el widget de curva está en su modo completo (no compacto). Cuando está en modo compacto (como en el applet acoplado), solo se dibujan las líneas de la cuadrícula sin etiquetas de frecuencia.
- Las configuraciones de Attack, Release y Slope se almacenan por ruta (TX y RX) y persisten entre sesiones.
- Para ingresar valores precisos, haga clic en el texto del valor de cualquier perilla para activar el editor en línea. Escriba el número deseado (con o sin unidades) y presione Enter para confirmar.

## Relacionados

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
