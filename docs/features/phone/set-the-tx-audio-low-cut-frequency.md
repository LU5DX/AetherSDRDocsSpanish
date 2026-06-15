# Resumen de Phone

El applet Phone proporciona controles de transmisión (TX) de voz para la radio FLEX-8600. Acceda a él haciendo clic en el botón de la bandeja **PHNE** en la barra lateral derecha.

## Controles

| Control              | Tipo            | Descripción                                                                 |
|----------------------|-----------------|-----------------------------------------------------------------------------|
| **AM Carrier**       | Control deslizante | Establece el nivel de potencia de la portadora AM de 0 a 100 por ciento. Arrástrelo mientras mantiene presionado para ver una etiqueta de porcentaje (ej. "48%"). |
| **VOX**              | Botón de alternancia | Activa o desactiva la transmisión por voz.                                |
| **VOX level**        | Control deslizante | Establece el umbral de activación de VOX de 0 a 100 por ciento. Arrástrelo mientras mantiene presionado para ver una etiqueta de porcentaje. |
| **Delay**            | Control deslizante | Establece el tiempo de retención de VOX de 0 a 100 (unidades arbitrarias) antes de volver a recepción. |
| **DEXP**             | Botón de alternancia | Activa o desactiva el expansor descendente (puerta de ruido).                |
| **DEXP threshold**   | Control deslizante | Establece el umbral de la puerta DEXP de 0 a 100 por ciento. Arrástrelo mientras mantiene presionado para ver una etiqueta de porcentaje. |
| **Low Cut < / >**    | Cuadro de incremento | Ajusta la frecuencia de corte bajo del filtro TX en pasos de 50 Hz. Valor predeterminado 50 Hz. Rango: 0 Hz a (corte alto − 50 Hz). |
| **High Cut < / >**   | Cuadro de incremento | Ajusta la frecuencia de corte alto del filtro TX en pasos de 50 Hz. Valor predeterminado 3300 Hz. Rango: (corte bajo + 50 Hz) a 10000 Hz. |

## Notas

- El control deslizante AM Carrier y el control deslizante VOX level ahora muestran una etiqueta de porcentaje al arrastrarlos (ej. "48%"). Esto proporciona una retroalimentación visual más clara del valor actual.
- Los controles DEXP ahora son funcionales en la versión de firmware 4.2 de FLEX-8600. Las configuraciones de DEXP se comunican directamente a la radio y ya no se guardan como preferencias de la aplicación.
- Todos los controles deslizantes en el applet Phone utilizan la clase `GuardedSlider`, que proporciona un comportamiento de arrastre suave y retroalimentación visual.
- El applet Phone ahora admite la personalización de temas. Todos los colores se adaptan al tema activo.

## Relacionado

- [Establecer la frecuencia de corte bajo del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte alto del audio TX](set-the-tx-audio-high-cut-frequency.md)
- [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)

---

# Establecer la frecuencia de corte bajo del audio TX

Use el control Low Cut en el applet Phone para elevar el borde inferior de la banda de paso del audio TX, eliminando retumbos, ruido de respiración o interferencia de baja frecuencia de su señal transmitida.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Panel de Applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **Low Cut** en el área del filtro TX en la parte inferior del applet.
3. Haga clic en **<** para disminuir la frecuencia de corte bajo o en **>** para aumentarla. También puede desplazar la rueda del ratón sobre la pantalla de valor para avanzar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los dos botones. El valor predeterminado es **50 Hz**.

## Cómo funcionan los botones de paso

Cada clic en **<** o **>** ajusta la frecuencia de corte bajo al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el valor actual es 87 Hz, al hacer clic en **>** se establece en 100 Hz y al hacer clic en **<** se establece en 50 Hz. Si el valor ya es un múltiplo exacto de 50 Hz, los botones lo mueven al siguiente múltiplo en la dirección elegida.

Esto significa que un solo clic siempre aterriza en un límite limpio de 50 Hz, independientemente del valor inicial.

## Qué hace cada control

| Control               | Valor predeterminado | Rango válido                             |
|-----------------------|----------------------|------------------------------------------|
| **Low Cut** **<**     | —                    | Ajusta al múltiplo de 50 Hz inferior más cercano |
| **Low Cut** **>**     | —                    | Ajusta al múltiplo de 50 Hz superior más cercano |
| Pantalla de valor Low Cut | 50 Hz               | 0 Hz a (corte alto − 50 Hz), paso 50 Hz |

## Consejos

- El valor de corte bajo no se puede establecer por encima de la frecuencia de corte alto actual menos 50 Hz. Si está cerca de ese límite, primero reduzca el corte alto o auméntelo para crear espacio.
- Para voz SSB, un corte bajo típico de 100–200 Hz reduce el ruido de baja frecuencia sin afectar notablemente la inteligibilidad de la voz.
- Debido a que los botones se ajustan a múltiplos de 50 Hz, un solo clic desde cualquier valor fuera del límite puede mover la frecuencia menos de 50 Hz. Este comportamiento es esperado.

## Solución de problemas

- **Los botones Low Cut no hacen nada** — Confirme que la radio esté conectada. Los controles del filtro TX requieren una conexión de radio activa para enviar los cambios de filtro a la FLEX-8600.

## Relacionado

- [Establecer la frecuencia de corte alto del audio TX](set-the-tx-audio-high-cut-frequency.md)
- [Resumen de Phone](overview.md)
- [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)

---

# Establecer la frecuencia de corte alto del audio TX

Use el control High Cut en el applet Phone para reducir el borde superior de la banda de paso del audio TX, disminuyendo siseos, silbidos o ruido de alta frecuencia de su señal transmitida.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Panel de Applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **High Cut** en el área del filtro TX en la parte inferior del applet.
3. Haga clic en **<** para disminuir la frecuencia de corte alto o en **>** para aumentarla. También puede desplazar la rueda del ratón sobre la pantalla de valor para avanzar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los dos botones. El valor predeterminado es **3300 Hz**.

## Cómo funcionan los botones de paso

Cada clic en **<** o **>** ajusta la frecuencia de corte alto al múltiplo de 50 Hz más cercano en la dirección elegida. Por ejemplo, si el valor actual es 1234 Hz, al hacer clic en **>** se establece en 1250 Hz y al hacer clic en **<** se establece en 1200 Hz. Si el valor ya es un múltiplo exacto de 50 Hz, los botones lo mueven al siguiente múltiplo en la dirección elegida.

Esto significa que un solo clic siempre aterriza en un límite limpio de 50 Hz, independientemente del valor inicial.

## Qué hace cada control

| Control                | Valor predeterminado | Rango válido                                |
|------------------------|----------------------|---------------------------------------------|
| **High Cut** **<**     | —                    | Ajusta al múltiplo de 50 Hz inferior más cercano |
| **High Cut** **>**     | —                    | Ajusta al múltiplo de 50 Hz superior más cercano |
| Pantalla de valor High Cut | 3300 Hz            | (corte bajo + 50 Hz) a 10000 Hz, paso 50 Hz |

## Consejos

- El valor de corte alto no se puede establecer por debajo de la frecuencia de corte bajo actual más 50 Hz. Si está cerca de ese límite, primero aumente el corte bajo o redúzcalo para crear espacio.
- Para voz SSB, un corte alto típico de 2700–3000 Hz reduce el ruido de alta frecuencia mientras mantiene una buena inteligibilidad. Para AM o FM, pueden ser apropiados ajustes más altos.
- Debido a que los botones se ajustan a múltiplos de 50 Hz, un solo clic desde cualquier valor fuera del límite puede mover la frecuencia menos de 50 Hz. Este comportamiento es esperado.

## Solución de problemas

- **Los botones High Cut no hacen nada** — Confirme que la radio esté conectada. Los controles del filtro TX requieren una conexión de radio activa para enviar los cambios de filtro a la FLEX-8600.

## Relacionado

- [Establecer la frecuencia de corte bajo del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Resumen de Phone](overview.md)
- [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)

---

# Habilitar VOX y establecer el umbral de activación

Use los controles VOX en el applet Phone para habilitar la transmisión activada por voz y ajustar la sensibilidad y el tiempo de retención.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Panel de Applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Haga clic en el botón de alternancia **VOX** para habilitar la transmisión activada por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el control deslizante **VOX level** para establecer el umbral de activación:
   - Arrastre el control deslizante hacia la derecha (valor más alto) para requerir un audio más fuerte para activar la transmisión.
   - Arrastre el control deslizante hacia la izquierda (valor más bajo) para permitir que un audio más suave active la transmisión.
   - Mientras arrastra, aparece una etiqueta de porcentaje (ej. "45%") que muestra el nivel actual.
4. Ajuste el control deslizante **Delay** para establecer cuánto tiempo continúa la transmisión después de que deje de hablar:
   - Arrastre el control deslizante hacia la derecha para un tiempo de retención más largo.
   - Arrastre el control deslizante hacia la izquierda para un tiempo de retención más corto.

## Qué hace cada control

| Control         | Valor predeterminado | Rango    | Descripción                                      |
|-----------------|----------------------|----------|--------------------------------------------------|
| **VOX**         | Deshabilitado        | —        | Activa/desactiva la transmisión activada por voz |
| **VOX level**   | —                    | 0–100%   | Umbral de activación para VOX                    |
| **Delay**       | —                    | 0–100    | Tiempo de retención antes de volver a recepción (unidades arbitrarias) |

## Consejos

- Comience con un nivel de VOX alrededor del 30–50% y ajústelo según su micrófono y volumen de voz.
- Una demora más larga evita que el transmisor se detenga entre palabras o pausas cortas, pero una demora demasiado larga puede hacer que el canal parezca ocupado.
- La etiqueta de porcentaje en el control deslizante VOX level proporciona una retroalimentación precisa al ajustar el umbral.

## Solución de problemas

- **El botón VOX no se enciende** — Confirme que la radio esté conectada. VOX requiere una conexión de radio activa para funcionar.
- **VOX se activa con demasiada facilidad o no se activa en absoluto** — Ajuste el control deslizante VOX level. Auméntelo para requerir un audio más fuerte, disminúyalo para permitir un audio más suave.
- **VOX se detiene entre palabras** — Aumente el control deslizante Delay para extender el tiempo de retención.

## Relacionado

- [Resumen de Phone](overview.md)
- [Establecer la frecuencia de corte bajo del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte alto del audio TX](set-the-tx-audio-high-cut-frequency.md)

---

# Establecer el nivel de portadora AM

Use el control deslizante AM Carrier en el applet Phone para establecer el nivel de potencia de la portadora AM para el modo de operación AM.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Panel de Applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice el control deslizante **AM Carrier** en la parte superior del applet.
3. Arrastre el control deslizante al nivel deseado. El rango válido es de 0 a 100 por ciento.
4. Mientras arrastra, aparece una etiqueta de porcentaje (ej. "48%") que muestra el nivel de portadora actual.

## Consejos

- El nivel de portadora AM debe establecerse para que coincida con las capacidades de su transmisor y la profundidad de modulación que desea lograr.
- Los niveles típicos de portadora AM varían del 20% al 80% dependiendo de su radio y sistema de antena.
- La etiqueta de porcentaje proporciona una retroalimentación precisa al ajustar el nivel de portadora.

## Solución de problemas

- **El control deslizante AM Carrier no tiene efecto** — Confirme que la radio esté en modo AM. El control deslizante solo controla el nivel de portadora AM.
- **No aparece la etiqueta de porcentaje al arrastrar** — Esto indica una versión anterior del software. Actualice a v26.5.3 o posterior para ver la etiqueta.

## Relacionado

- [Resumen de Phone](overview.md)
- [Establecer la frecuencia de corte bajo del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte alto del audio TX](set-the-tx-audio-high-cut-frequency.md)
