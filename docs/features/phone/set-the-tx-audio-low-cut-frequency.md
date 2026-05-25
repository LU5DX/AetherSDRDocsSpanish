# Establecer la frecuencia de corte bajo del audio de TX

Use el control Low Cut en el applet Phone para elevar el borde inferior de la banda de paso del audio de TX, reduciendo los ruidos retumbantes, el ruido de respiración o las interferencias de baja frecuencia de su señal transmitida.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Applet Panel esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **Low Cut** en el área del filtro de TX en la parte inferior del applet.
3. Haga clic en **<** para disminuir la frecuencia de corte bajo o en **>** para aumentarla. También puede girar la rueda del ratón sobre la visualización del valor para ajustarlo en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los dos botones. El valor predeterminado es **50 Hz**.

## Cómo funcionan los botones de paso

Cada clic en **<** o **>** ajusta la frecuencia de corte bajo al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el valor actual es 87 Hz, al hacer clic en **>** se establece en 100 Hz y al hacer clic en **<** se establece en 50 Hz. Si el valor ya es un múltiplo exacto de 50 Hz, los botones lo mueven al siguiente múltiplo en la dirección elegida.

Esto significa que un solo clic siempre cae en un límite limpio de 50 Hz, independientemente del valor inicial.

## Qué hace cada control

| Control                  | Valor predeterminado | Rango válido                            |
|--------------------------|-----------------------|-----------------------------------------|
| **Low Cut** **<**        | —                     | Ajusta al múltiplo de 50 Hz inferior    |
| **Low Cut** **>**        | —                     | Ajusta al múltiplo de 50 Hz superior    |
| Pantalla de valor Low Cut | 50 Hz                 | 0 Hz a (corte alto − 50 Hz), paso 50 Hz |

## Consejos

- El valor de corte bajo no puede establecerse más alto que la frecuencia de corte alto actual menos 50 Hz. Si está cerca de ese límite, reduzca primero el corte alto o auméntelo para crear espacio.
- Para voz en SSB, un corte bajo típico de 100–200 Hz reduce el ruido de baja frecuencia sin afectar notablemente la inteligibilidad de la voz.
- Debido a que los botones ajustan a múltiplos de 50 Hz, un solo clic desde cualquier valor fuera del límite puede mover la frecuencia menos de 50 Hz. Este comportamiento es normal.

## Solución de problemas

- **Los botones Low Cut no hacen nada** — Confirme que la radio está conectada. Los controles del filtro de TX requieren una conexión de radio activa para enviar los cambios de filtro a la FLEX-8600.

## Relacionados

- [Set the TX audio high-cut frequency](set-the-tx-audio-high-cut-frequency.md)
- [Phone overview](overview.md)
- [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md)

---

# Establecer la frecuencia de corte alto del audio de TX

Use el control High Cut en el applet Phone para reducir el borde superior de la banda de paso del audio de TX, disminuyendo la sibilancia, el silbido o el ruido de alta frecuencia de su señal transmitida.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Applet Panel esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **High Cut** en el área del filtro de TX en la parte inferior del applet.
3. Haga clic en **<** para disminuir la frecuencia de corte alto o en **>** para aumentarla. También puede girar la rueda del ratón sobre la visualización del valor para ajustarlo en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los dos botones. El valor predeterminado es **3300 Hz**.

## Cómo funcionan los botones de paso

Cada clic en **<** o **>** ajusta la frecuencia de corte alto al múltiplo de 50 Hz más cercano en la dirección elegida. Por ejemplo, si el valor actual es 1234 Hz, al hacer clic en **>** se establece en 1250 Hz y al hacer clic en **<** se establece en 1200 Hz. Si el valor ya es un múltiplo exacto de 50 Hz, los botones lo mueven al siguiente múltiplo en la dirección elegida.

Esto significa que un solo clic siempre cae en un límite limpio de 50 Hz, independientemente del valor inicial.

## Qué hace cada control

| Control                   | Valor predeterminado | Rango válido                               |
|---------------------------|-----------------------|--------------------------------------------|
| **High Cut** **<**        | —                     | Ajusta al múltiplo de 50 Hz inferior       |
| **High Cut** **>**        | —                     | Ajusta al múltiplo de 50 Hz superior       |
| Pantalla de valor High Cut | 3300 Hz               | (corte bajo + 50 Hz) a 10000 Hz, paso 50 Hz |

## Consejos

- El valor de corte alto no puede establecerse más bajo que la frecuencia de corte bajo actual más 50 Hz. Si está cerca de ese límite, eleve primero el corte bajo o redúzcalo para crear espacio.
- Para voz en SSB, un corte alto típico de 2700–3000 Hz reduce el silbido mientras mantiene una buena inteligibilidad. Para AM o FM, pueden ser apropiados ajustes más altos.
- Debido a que los botones ajustan a múltiplos de 50 Hz, un solo clic desde cualquier valor fuera del límite puede mover la frecuencia menos de 50 Hz. Este comportamiento es normal.

## Solución de problemas

- **Los botones High Cut no hacen nada** — Confirme que la radio está conectada. Los controles del filtro de TX requieren una conexión de radio activa para enviar los cambios de filtro a la FLEX-8600.

## Relacionados

- [Set the TX audio low-cut frequency](set-the-tx-audio-low-cut-frequency.md)
- [Phone overview](overview.md)
- [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md)

---

# Resumen de Phone

El applet Phone proporciona controles de transmisión (TX) de voz para la radio FLEX-8600. Acceda a él haciendo clic en el botón de la bandeja **PHNE** en la barra lateral derecha.

## Controles

| Control                | Tipo           | Descripción                                                                    |
|------------------------|----------------|--------------------------------------------------------------------------------|
| **AM Carrier**         | Deslizador     | Establece el nivel de potencia de la portadora AM de 0 a 100 por ciento. Arrastre mientras mantiene presionado para ver una etiqueta de porcentaje (ej. "48%"). |
| **VOX**                | Botón de alternancia | Activa o desactiva la transmisión activada por voz.                            |
| **VOX level**          | Deslizador     | Establece el umbral de activación de VOX de 0 a 100 por ciento. Arrastre mientras mantiene presionado para ver una etiqueta de porcentaje. |
| **Delay**              | Deslizador     | Establece el tiempo de retención de VOX de 0 a 100 (unidades arbitrarias) antes de volver a recepción. |
| **DEXP**               | Botón de alternancia | Activa o desactiva el expansor descendente (puerta de ruido). No funcional en firmware v1.4.0.0 — la radio devuelve error 0x5000002D. |
| **DEXP threshold**     | Deslizador     | Establece el umbral de la puerta DEXP de 0 a 100 por ciento. Arrastre mientras mantiene presionado para ver una etiqueta de porcentaje. Misma limitación de firmware que la alternancia DEXP. |
| **Low Cut < / >**      | Cuadro de giro | Ajusta la frecuencia de corte bajo del filtro de TX en pasos de 50 Hz. Predeterminado 50 Hz. Rango: 0 Hz a (corte alto − 50 Hz). |
| **High Cut < / >**     | Cuadro de giro | Ajusta la frecuencia de corte alto del filtro de TX en pasos de 50 Hz. Predeterminado 3300 Hz. Rango: (corte bajo + 50 Hz) a 10000 Hz. |

## Notas

- El deslizador AM Carrier y el deslizador VOX level ahora muestran una etiqueta de porcentaje cuando se arrastran (ej. "48%"). Esto proporciona una retroalimentación visual más clara del valor actual.
- Los controles DEXP están presentes pero no son funcionales en versiones de firmware de la FLEX-8600 anteriores a la 4.2. Intentar usarlos resultará en un error.
- Todos los deslizadores en el applet Phone usan la clase `GuardedSlider`, que proporciona un comportamiento de arrastre suave y retroalimentación visual.

## Relacionados

- [Set the TX audio low-cut frequency](set-the-tx-audio-low-cut-frequency.md)
- [Set the TX audio high-cut frequency](set-the-tx-audio-high-cut-frequency.md)
- [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md)

---

# Habilitar VOX y establecer el umbral de activación

Use los controles VOX en el applet Phone para habilitar la transmisión activada por voz y ajustar la sensibilidad y el tiempo de retención.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Applet Panel esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Haga clic en el botón de alternancia **VOX** para habilitar la transmisión activada por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el deslizador **VOX level** para establecer el umbral de activación:
   - Arrastre el deslizador a la derecha (valor más alto) para requerir audio más fuerte que active la transmisión.
   - Arrastre el deslizador a la izquierda (valor más bajo) para permitir que un audio más silencioso active la transmisión.
   - Mientras arrastra, aparece una etiqueta de porcentaje (ej. "45%") que muestra el nivel actual.
4. Ajuste el deslizador **Delay** para establecer cuánto tiempo continúa la transmisión después de que deje de hablar:
   - Arrastre el deslizador a la derecha para un tiempo de retención más largo.
   - Arrastre el deslizador a la izquierda para un tiempo de retención más corto.

## Qué hace cada control

| Control         | Valor predeterminado | Rango    | Descripción                                      |
|-----------------|-----------------------|----------|--------------------------------------------------|
| **VOX**         | Desactivado           | —        | Activa o desactiva la transmisión activada por voz |
| **VOX level**   | —                     | 0–100%   | Umbral de activación para VOX                    |
| **Delay**       | —                     | 0–100    | Tiempo de retención antes de volver a recepción (unidades arbitrarias) |

## Consejos

- Comience con un nivel de VOX alrededor del 30–50% y ajústelo según su micrófono y volumen de habla.
- Un retardo más largo evita que el transmisor se desconecte entre palabras o pausas cortas, pero un retardo demasiado largo puede hacer que el canal parezca ocupado.
- La etiqueta de porcentaje en el deslizador VOX level proporciona una retroalimentación precisa al ajustar el umbral.

## Solución de problemas

- **El botón VOX no se enciende** — Confirme que la radio está conectada. VOX requiere una conexión de radio activa para funcionar.
- **VOX se activa demasiado fácil o no se activa** — Ajuste el deslizador VOX level. Auméntelo para requerir audio más fuerte, redúzcalo para permitir audio más silencioso.
- **VOX se desconecta entre palabras** — Aumente el deslizador Delay para extender el tiempo de retención.

## Relacionados

- [Phone overview](overview.md)
- [Set the TX audio low-cut frequency](set-the-tx-audio-low-cut-frequency.md)
- [Set the TX audio high-cut frequency](set-the-tx-audio-high-cut-frequency.md)

---

# Establecer el nivel de portadora AM

Use el deslizador AM Carrier en el applet Phone para establecer el nivel de potencia de la portadora AM para la operación en modo AM.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Applet Panel esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice el deslizador **AM Carrier** en la parte superior del applet.
3. Arrastre el deslizador al nivel deseado. El rango válido es de 0 a 100 por ciento.
4. Mientras arrastra, aparece una etiqueta de porcentaje (ej. "48%") que muestra el nivel de portadora actual.

## Consejos

- El nivel de portadora AM debe configurarse para que coincida con las capacidades de su transmisor y la profundidad de modulación que desea lograr.
- Los niveles típicos de portadora AM van del 20% al 80% dependiendo de su radio y sistema de antena.
- La etiqueta de porcentaje proporciona una retroalimentación precisa al ajustar el nivel de portadora.

## Solución de problemas

- **El deslizador AM Carrier no tiene efecto** — Confirme que la radio está en modo AM. El deslizador solo controla el nivel de portadora AM.
- **No aparece ninguna etiqueta de porcentaje al arrastrar** — Esto indica una versión anterior del software. Actualice a la v26.5.3 o posterior para ver la etiqueta.

## Relacionados

- [Phone overview](overview.md)
- [Set the TX audio low-cut frequency](set-the-tx-audio-low-cut-frequency.md)
- [Set the TX audio high-cut frequency](set-the-tx-audio-high-cut-frequency.md)
