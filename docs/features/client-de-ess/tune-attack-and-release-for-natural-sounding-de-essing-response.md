# Ajuste de Ataque y Liberación para una respuesta natural de de-essing

Esta página le ayuda a ajustar los controles de Ataque y Liberación en el editor de De-Ess del lado de RX o TX para que el de-esser responda a la sibilancia rápidamente sin sonar entrecortado o antinatural.

## Antes de comenzar

- La etapa De-Ess debe estar habilitada en el widget CHAIN (haga clic en DESS una vez para habilitar; haga doble clic para abrir el editor).
- Para TX: el applet acoplado **Aetherial De-Esser** muestra los cuatro controles habituales (Freq, Q, Thresh, Amount). **Attack** y **Release** solo están disponibles en la ventana del editor sin marco que se abre al hacer doble clic en DESS en el widget CHAIN (o al abrir el Aetherial Audio Channel Strip).
- Para RX: abra el **Aetherial Audio Channel Strip** y haga doble clic en **DESS** en la cadena de RX para abrir el editor de De-Ess de RX, que incluye Attack y Release.
- Los controles Attack y Release solo están presentes en el **StripDeEssPanel** (dentro del Channel Strip), no en el applet acoplado ClientDeEssApplet.

## Edición de valores en línea

Todos los controles en el editor De-Ess ahora admiten la entrada numérica en línea para un ajuste preciso:

1. Haga clic en el texto del valor que se muestra debajo de cualquier control para ingresar al modo de edición. El área del valor muestra un sutil fondo oscuro con un borde cian para indicar el modo de edición.
2. Escriba un valor numérico. Se admite el análisis sensible a la configuración regional (por ejemplo, "12,5" funciona en configuraciones regionales con coma decimal). Las unidades opcionales o el texto descriptivo (por ejemplo, "12.5 ms" o "−6 dB") se eliminan y analizan correctamente.
3. Presione **Enter** o haga clic en otro lugar para confirmar el valor. El valor se ajusta al rango válido del control.
4. Presione **Escape** mientras edita para cancelar y revertir al valor anterior.

## Pasos

1. Abra el editor De-Ess que incluye Attack y Release:
   - **TX:** Haga doble clic en la etapa DESS en el widget CHAIN para abrir el editor sin marco titulado **Aetherial De-Esser — TX**.
   - **RX:** Abra el **Aetherial Audio Channel Strip** y haga doble clic en **DESS** en la cadena de RX para abrir el editor De-Ess de RX.

2. Entrene el de-esser en el habla sibilante:
   - Varíe el control **Freq** para localizar su pico de sibilancia (consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)).
   - Ajuste **Thresh** justo por debajo de los picos de 'S' más fuertes (consulte [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)).
   - Ajuste **Amount** para una reducción transparente (consulte [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)).

3. Ajuste **Attack**:
   - Valor predeterminado: **1.0 ms**
   - Rango: **0.1 a 30.0 ms** (mapeo exponencial)
   - Gire en **sentido horario** para ralentizar el ataque (tiempo de reacción más largo; puede dejar pasar algo de sibilancia antes de la atenuación).
   - Gire en **sentido antihorario** para acelerar el ataque (reacción más rápida; captura la sibilancia rápidamente, pero puede sonar a clic si es demasiado rápido).

4. Ajuste **Release**:
   - Valor predeterminado: **100 ms**
   - Rango: **10.0 a 500.0 ms** (mapeo exponencial)
   - Gire en **sentido horario** para alargar la liberación (la ganancia regresa lentamente después de que cesa la sibilancia; puede sonar "bombeado" en el habla rápida).
   - Gire en **sentido antihorario** para acortar la liberación (la ganancia regresa rápidamente; puede sonar entrecortado en sonidos 'S' sostenidos).

5. Pruebe con una frase sibilante mientras observa la **barra de reducción de ganancia** (la franja roja suave en la parte inferior del widget de la curva De-Ess):
   - Busque reducciones suaves y breves en cada pico de 'S' (la barra debe llenarse y vaciarse limpiamente con cada sílaba).
   - Si la barra "se queda" después de que cesa la sibilancia, aumente **Release** (sostenimiento más largo).
   - Si la barra reacciona lentamente a la primera 'S' de una palabra, disminuya **Attack** (respuesta más rápida).

6. Escuche en el aire o grabe una muestra corta y ajuste iterativamente hasta que el de-essing suene transparente.

## Función de cada control

| Control | Tipo | Predeterminado | Rango válido | Mapeo | Clave de configuración |
|---|---|---|---|---|---|
| Attack | control giratorio | 1.0 ms | 0.1–30.0 ms | Exponencial (`0.1 * 300^n`) | `ClientDeEssTxAttackMs` o `ClientDeEssRxAttackMs` |
| Release | control giratorio | 100 ms | 10.0–500.0 ms | Exponencial (`10 * 50^n`) | `ClientDeEssTxReleaseMs` o `ClientDeEssRxReleaseMs` |

Estos dos controles existen únicamente en los editores de cadena sin marco (StripDeEssPanel). El applet acoplado ClientDeEssApplet los omite.

## Consejos

- Para voces SSB típicas, **Attack de 0.5–2 ms** y **Release de 80–150 ms** funcionan bien. El habla muy rápida (por ejemplo, en concursos) puede necesitar valores más cortos en ambos extremos.
- La **marca de -6 dB** en la barra de reducción de ganancia señala el nivel predeterminado de Amount; es una referencia útil para ver cuánto está reduciendo realmente el de-esser.
- La curva de respuesta de la cadena lateral ahora muestra etiquetas de eje de frecuencia en 100, 500, 1k, 2k, 4k, 8k y 16k Hz utilizando texto estático en caché para mejorar el rendimiento. Las etiquetas de los ejes solo se muestran cuando el widget de curva está en su modo completo (no compacto). Cuando está en modo compacto (como en el applet acoplado), solo se dibujan las líneas de la cuadrícula sin etiquetas de frecuencia.
- Los ajustes de Attack y Release se almacenan por ruta (TX y RX) y persisten entre sesiones.
- Para ingresar valores precisos, haga clic en el texto del valor de cualquier control para activar el editor en línea. Escriba el número deseado (con o sin unidades) y presione Enter para confirmar.

## Relacionado

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
