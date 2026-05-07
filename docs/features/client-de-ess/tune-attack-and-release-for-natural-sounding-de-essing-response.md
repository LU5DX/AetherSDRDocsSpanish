# Ajuste de Ataque y Liberación para una respuesta de de-esser natural

Esta página le ayuda a ajustar los mandos de Ataque (Attack) y Liberación (Release) en el editor De-Ess del lado RX o TX para que el de-esser responda a la sibilancia rápidamente sin sonar entrecortado o artificial.

## Antes de comenzar

- La etapa De-Ess debe estar habilitada en el widget CHAIN (haga clic en DESS una vez para habilitar; haga doble clic para abrir el editor).
- Para TX: el applet acoplado **Aetherial De-Esser** muestra los cuatro mandos cotidianos (Freq, Q, Thresh, Amount). **Attack** y **Release** solo están disponibles en la ventana del editor sin marco que se abre al hacer doble clic en DESS en el widget CHAIN (o al abrir el Aetherial Audio Channel Strip).
- Para RX: abra el Aetherial Audio Channel Strip y haga doble clic en DESS en la cadena RX para abrir el editor De-Ess de RX, que incluye Attack y Release.
- Los mandos de Attack y Release solo están presentes en el **StripDeEssPanel** (dentro del Channel Strip), no en el ClientDeEssApplet acoplado.

## Pasos

1. Abra el editor De-Ess que incluye Attack y Release:
   - **TX:** Haga doble clic en la etapa DESS en el widget CHAIN para abrir el editor sin marco titulado **Aetherial De-Esser — TX**.
   - **RX:** Abra el **Aetherial Audio Channel Strip** y haga doble clic en **DESS** en la cadena RX para abrir el editor De-Ess de RX.

2. Entrene el de-esser con habla sibilante:
   - Barra el mando **Freq** para localizar su pico de sibilancia (consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)).
   - Ajuste **Thresh** justo por debajo de los picos de 'S' más fuertes (consulte [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)).
   - Ajuste **Amount** para una reducción transparente (consulte [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)).

3. Ajuste **Attack**:
   - Valor predeterminado: **1.0 ms**
   - Rango: **0.1 a 30.0 ms** (mapeo exponencial)
   - Gire **en el sentido de las agujas del reloj** para ralentizar el ataque (tiempo de reacción más largo; puede dejar pasar algo de sibilancia antes de atenuar).
   - Gire **en el sentido contrario a las agujas del reloj** para acelerar el ataque (reacción más rápida; atrapa la sibilancia rápidamente pero puede sonar a clic si es demasiado rápido).

4. Ajuste **Release**:
   - Valor predeterminado: **100 ms**
   - Rango: **10.0 a 500.0 ms** (mapeo exponencial)
   - Gire **en el sentido de las agujas del reloj** para alargar la liberación (la ganancia vuelve lentamente después de que cesa la sibilancia; puede sonar "bombeado" en habla rápida).
   - Gire **en el sentido contrario a las agujas del reloj** para acortar la liberación (la ganancia vuelve rápidamente; puede sonar entrecortado en sonidos 'S' sostenidos).

5. Pruebe con una frase sibilante mientras observa la **barra de reducción de ganancia** (la tira roja suave en la parte inferior del widget de curva De-Ess):
   - Busque reducciones suaves y breves en cada pico de 'S' (la barra debe llenarse y vaciarse limpiamente con cada sílaba).
   - Si la barra "se queda" después de que la sibilancia se detiene, aumente **Release** (sostenido más largo).
   - Si la barra reacciona lentamente a la primera 'S' de una palabra, disminuya **Attack** (respuesta más rápida).

6. Escuche al aire o grabe una muestra corta y ajuste iterativamente hasta que el de-essing suene transparente.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Mapeo | Clave de configuración |
|---|---|---|---|---|---|
| Attack | mando | 1.0 ms | 0.1–30.0 ms | Exponencial (`0.1 * 300^n`) | `ClientDeEssTxAttackMs` o `ClientDeEssRxAttackMs` |
| Release | mando | 100 ms | 10.0–500.0 ms | Exponencial (`10 * 50^n`) | `ClientDeEssTxReleaseMs` o `ClientDeEssRxReleaseMs` |

Estos dos controles existen solo en los editores de tira sin marco (StripDeEssPanel). El ClientDeEssApplet acoplado los omite.

## Consejos

- Para voces SSB típicas, **Attack 0.5–2 ms** y **Release 80–150 ms** funcionan bien. El habla muy rápida (p. ej., concursos) puede necesitar valores más cortos en ambos extremos.
- La marca **-6 dB** en la barra de reducción de ganancia indica el nivel predeterminado de Amount; es una referencia útil para ver cuánto está reduciendo realmente el de-esser.
- Los ajustes de Attack y Release se almacenan por ruta (TX y RX) y persisten entre sesiones.

## Relacionados

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
