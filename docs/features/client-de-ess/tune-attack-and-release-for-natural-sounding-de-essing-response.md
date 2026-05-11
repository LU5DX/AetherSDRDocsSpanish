# Ajuste de Ataque y Liberación para una respuesta natural del de-esser

Esta página le ayuda a ajustar los controles de Ataque y Liberación en el editor de De-Ess del lado de RX o TX para que el de-esser responda a las sibilancias rápidamente sin sonar entrecortado o artificial.

## Antes de comenzar

- La etapa De-Ess debe estar habilitada en el widget CHAIN (haga clic en DESS una vez para habilitarla; haga doble clic para abrir el editor).
- Para TX: el applet acoplado **Aetherial De-Esser** muestra los cuatro controles habituales (Freq, Q, Thresh, Amount). **Attack** y **Release** solo están disponibles en la ventana del editor sin marco que se abre al hacer doble clic en DESS en el widget CHAIN (o al abrir el Aetherial Audio Channel Strip).
- Para RX: abra el Aetherial Audio Channel Strip y haga doble clic en DESS en la cadena de RX para abrir el editor de De-Ess de RX, que incluye Attack y Release.
- Los controles Attack y Release solo están presentes en el **StripDeEssPanel** (dentro del Channel Strip), no en el applet acoplado ClientDeEssApplet.

## Pasos

1. Abra el editor de De-Ess que incluya Attack y Release:
   - **TX:** Haga doble clic en la etapa DESS en el widget CHAIN para abrir el editor sin marco titulado **Aetherial De-Esser — TX**.
   - **RX:** Abra el **Aetherial Audio Channel Strip** y haga doble clic en **DESS** en la cadena de RX para abrir el editor de De-Ess de RX.

2. Entrene el de-esser con habla sibilante:
   - Barra el control **Freq** para localizar su pico de sibilancia (consulte [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)).
   - Ajuste **Thresh** justo por debajo de los picos de 'S' más fuertes (consulte [Ajustar el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)).
   - Ajuste **Amount** para una reducción transparente (consulte [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)).

3. Ajuste **Attack**:
   - Valor predeterminado: **1.0 ms**
   - Rango: **0.1 a 30.0 ms** (mapeo exponencial)
   - Gire en **sentido horario** para ralentizar el ataque (mayor tiempo de reacción; puede dejar pasar algo de sibilancia antes de atenuar).
   - Gire en **sentido antihorario** para acelerar el ataque (reacción más rápida; capta la sibilancia rápidamente, pero puede sonar a clic si es demasiado rápido).

4. Ajuste **Release**:
   - Valor predeterminado: **100 ms**
   - Rango: **10.0 a 500.0 ms** (mapeo exponencial)
   - Gire en **sentido horario** para alargar la liberación (la ganancia vuelve lentamente después de que cesa la sibilancia; puede sonar "bombeado" en habla rápida).
   - Gire en **sentido antihorario** para acortar la liberación (la ganancia vuelve rápidamente; puede sonar entrecortado en sonidos de 'S' sostenidos).

5. Pruebe con una frase sibilante mientras observa la **barra de reducción de ganancia** (la franja roja suave en la parte inferior del widget de la curva De-Ess):
   - Busque reducciones suaves y breves en cada pico de 'S' (la barra debe llenarse y vaciarse limpiamente con cada sílaba).
   - Si la barra se "queda" después de que cesa la sibilancia, aumente **Release** (sostenimiento más largo).
   - Si la barra reacciona lentamente a la primera 'S' de una palabra, disminuya **Attack** (respuesta más rápida).

6. Escuche al aire o grabe una muestra corta y ajuste iterativamente hasta que el de-essing suene transparente.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Mapeo | Clave de configuración |
|---|---|---|---|---|---|
| Attack | control giratorio | 1.0 ms | 0.1–30.0 ms | Exponencial (`0.1 * 300^n`) | `ClientDeEssTxAttackMs` o `ClientDeEssRxAttackMs` |
| Release | control giratorio | 100 ms | 10.0–500.0 ms | Exponencial (`10 * 50^n`) | `ClientDeEssTxReleaseMs` o `ClientDeEssRxReleaseMs` |

Estos dos controles solo existen en los editores de cadena sin marco (StripDeEssPanel). El applet acoplado ClientDeEssApplet los omite.

## Consejos

- Para voces SSB típicas, **Attack de 0.5 a 2 ms** y **Release de 80 a 150 ms** funcionan bien. El habla muy rápida (p. ej., en concursos) puede necesitar valores más cortos en ambos extremos.
- La marca **-6 dB** en la barra de reducción de ganancia indica el nivel predeterminado de Amount; es una referencia útil de cuánto está reduciendo realmente el de-esser.
- La curva de respuesta del sidechain ahora muestra etiquetas del eje de frecuencia en 100, 500, 1k, 2k, 4k, 8k y 16k Hz utilizando texto estático en caché para mejorar el rendimiento. Las etiquetas de los ejes solo se muestran cuando el widget de curva está en su modo completo (no compacto). Cuando está en modo compacto (como en el applet acoplado), solo se dibujan las líneas de cuadrícula sin las etiquetas de frecuencia.
- Los ajustes de Attack y Release se almacenan por ruta (TX y RX) y persisten entre sesiones.

## Relacionados

- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Ajustar el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observar la GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
