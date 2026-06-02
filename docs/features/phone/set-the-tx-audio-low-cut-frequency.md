# Descripción general de Phone

El applet Phone proporciona controles de transmisión (TX) de voz para la radio FLEX-8600. Acceda a él haciendo clic en el botón de la bandeja **PHNE** en la barra lateral derecha.

## Controles

| Control                  | Tipo          | Descripción                                                                 |
|--------------------------|---------------|-----------------------------------------------------------------------------|
| **AM Carrier**           | Deslizador    | Ajusta el nivel de potencia de la portadora AM de 0 a 100 por ciento. Arrastre mientras mantiene presionado para ver una etiqueta de porcentaje (por ejemplo, "48%"). |
| **VOX**                  | Botón de alternancia | Activa o desactiva la transmisión por voz.                                |
| **VOX level**            | Deslizador    | Ajusta el umbral de activación de VOX de 0 a 100 por ciento. Arrastre mientras mantiene presionado para ver una etiqueta de porcentaje. |
| **Delay**                | Deslizador    | Ajusta el tiempo de retención de VOX de 0 a 100 (unidades arbitrarias) antes de volver a recepción. |
| **DEXP**                 | Botón de alternancia | Activa o desactiva el expansor descendente (puerta de ruido). No funcional en la versión de firmware v1.4.0.0 — la radio devuelve el error 0x5000002D. |
| **DEXP threshold**       | Deslizador    | Ajusta el umbral de la puerta DEXP de 0 a 100 por ciento. Arrastre mientras mantiene presionado para ver una etiqueta de porcentaje. Misma limitación de firmware que la alternancia DEXP. |
| **Low Cut < / >**        | Cuadro de giro | Ajusta la frecuencia de corte baja del filtro de TX en pasos de 50 Hz. Valor predeterminado 50 Hz. Rango: 0 Hz a (frecuencia de corte alta − 50 Hz). |
| **High Cut < / >**       | Cuadro de giro | Ajusta la frecuencia de corte alta del filtro de TX en pasos de 50 Hz. Valor predeterminado 3300 Hz. Rango: (frecuencia de corte baja + 50 Hz) a 10000 Hz. |

## Notas

- El deslizador AM Carrier y el deslizador VOX level ahora muestran una etiqueta de porcentaje al ser arrastrados (por ejemplo, "48%"). Esto proporciona una retroalimentación visual más clara del valor actual.
- Los controles DEXP están presentes pero no son funcionales en versiones de firmware de la FLEX-8600 anteriores a la 4.2. Intentar usarlos resultará en un error.
- Todos los deslizadores en el applet Phone utilizan la clase `GuardedSlider`, que proporciona un comportamiento de arrastre suave y retroalimentación visual.
- El applet Phone ahora admite la personalización de temas. Todos los colores se adaptan al tema activo.

## Relacionado

- [Ajustar la frecuencia de corte baja del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Ajustar la frecuencia de corte alta del audio de TX](set-the-tx-audio-high-cut-frequency.md)
- [Activar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)

---

# Ajustar la frecuencia de corte baja del audio de TX

Use el control Low Cut en el applet Phone para elevar el borde inferior de la banda de paso del audio de TX, reduciendo el retumbo, el ruido de respiración o la interferencia de baja frecuencia de su señal transmitida.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Applet Panel esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **Low Cut** en el área del filtro de TX en la parte inferior del applet.
3. Haga clic en **<** para disminuir la frecuencia de corte baja o en **>** para aumentarla. También puede desplazar la rueda del ratón sobre la pantalla de valor para avanzar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los dos botones. El valor predeterminado es **50 Hz**.

## Cómo funcionan los botones de paso

Cada clic en **<** o **>** ajusta la frecuencia de corte baja al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el valor actual es 87 Hz, al hacer clic en **>** se establece en 100 Hz y al hacer clic en **<** se establece en 50 Hz. Si el valor ya es un múltiplo exacto de 50 Hz, los botones lo mueven al siguiente múltiplo en la dirección elegida.

Esto significa que un solo clic siempre aterriza en un límite limpio de 50 Hz, independientemente del valor inicial.

## Qué hace cada control

| Control                | Valor predeterminado | Rango válido                                  |
|------------------------|----------------------|------------------------------------------------|
| **Low Cut** **<**      | —                    | Ajusta al siguiente múltiplo inferior de 50 Hz |
| **Low Cut** **>**      | —                    | Ajusta al siguiente múltiplo superior de 50 Hz |
| Pantalla de valor Low Cut | 50 Hz            | 0 Hz a (frecuencia de corte alta − 50 Hz), paso 50 Hz |

## Consejos

- El valor de corte baja no puede establecerse más alto que la frecuencia de corte alta actual menos 50 Hz. Si se acerca a ese límite, primero reduzca la frecuencia de corte alta o auméntela para crear espacio.
- Para voz SSB, un corte bajo típico de 100–200 Hz reduce el ruido de baja frecuencia sin afectar notablemente la inteligibilidad de la voz.
- Debido a que los botones se ajustan a múltiplos de 50 Hz, hacer clic una vez desde cualquier valor fuera del límite puede mover la frecuencia menos de 50 Hz. Este comportamiento es esperado.

## Solución de problemas

- **Los botones Low Cut no hacen nada** — Confirme que la radio esté conectada. Los controles del filtro de TX requieren una conexión de radio activa para enviar cambios de filtro a la FLEX-8600.

## Relacionado

- [Ajustar la frecuencia de corte alta del audio de TX](set-the-tx-audio-high-cut-frequency.md)
- [Descripción general de Phone](overview.md)
- [Activar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)

---

# Ajustar la frecuencia de corte alta del audio de TX

Use el control High Cut en el applet Phone para reducir el borde superior de la banda de paso del audio de TX, disminuyendo la sibilancia, el silbido o el ruido de alta frecuencia de su señal transmitida.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Applet Panel esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **High Cut** en el área del filtro de TX en la parte inferior del applet.
3. Haga clic en **<** para disminuir la frecuencia de corte alta o en **>** para aumentarla. También puede desplazar la rueda del ratón sobre la pantalla de valor para avanzar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los dos botones. El valor predeterminado es **3300 Hz**.

## Cómo funcionan los botones de paso

Cada clic en **<** o **>** ajusta la frecuencia de corte alta al múltiplo de 50 Hz más cercano en la dirección elegida. Por ejemplo, si el valor actual es 1234 Hz, al hacer clic en **>** se establece en 1250 Hz y al hacer clic en **<** se establece en 1200 Hz. Si el valor ya es un múltiplo exacto de 50 Hz, los botones lo mueven al siguiente múltiplo en la dirección elegida.

Esto significa que un solo clic siempre aterriza en un límite limpio de 50 Hz, independientemente del valor inicial.

## Qué hace cada control

| Control                 | Valor predeterminado | Rango válido                                      |
|-------------------------|----------------------|---------------------------------------------------|
| **High Cut** **<**      | —                    | Ajusta al siguiente múltiplo inferior de 50 Hz    |
| **High Cut** **>**      | —                    | Ajusta al siguiente múltiplo superior de 50 Hz    |
| Pantalla de valor High Cut | 3300 Hz          | (frecuencia de corte baja + 50 Hz) a 10000 Hz, paso 50 Hz |

## Consejos

- El valor de corte alta no puede establecerse más bajo que la frecuencia de corte baja actual más 50 Hz. Si se acerca a ese límite, primero aumente la frecuencia de corte baja o redúzcala para crear espacio.
- Para voz SSB, un corte alto típico de 2700–3000 Hz reduce el silbido mientras mantiene una buena inteligibilidad. Para AM o FM, pueden ser apropiados valores más altos.
- Debido a que los botones se ajustan a múltiplos de 50 Hz, hacer clic una vez desde cualquier valor fuera del límite puede mover la frecuencia menos de 50 Hz. Este comportamiento es esperado.

## Solución de problemas

- **Los botones High Cut no hacen nada** — Confirme que la radio esté conectada. Los controles del filtro de TX requieren una conexión de radio activa para enviar cambios de filtro a la FLEX-8600.

## Relacionado

- [Ajustar la frecuencia de corte baja del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Descripción general de Phone](overview.md)
- [Activar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)

---

# Activar VOX y establecer el umbral de activación

Use los controles VOX en el applet Phone para activar la transmisión por voz y ajustar la sensibilidad y el tiempo de retención.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Applet Panel esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Haga clic en el botón de alternancia **VOX** para activar la transmisión por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el deslizador **VOX level** para establecer el umbral de activación:
   - Arrastre el deslizador hacia la derecha (valor más alto) para requerir un audio más fuerte para activar la transmisión.
   - Arrastre el deslizador hacia la izquierda (valor más bajo) para permitir que un audio más silencioso active la transmisión.
   - Mientras arrastra, aparece una etiqueta de porcentaje (por ejemplo, "45%") que muestra el nivel actual.
4. Ajuste el deslizador **Delay** para establecer cuánto tiempo continúa la transmisión después de que usted deje de hablar:
   - Arrastre el deslizador hacia la derecha para un tiempo de retención más largo.
   - Arrastre el deslizador hacia la izquierda para un tiempo de retención más corto.

## Qué hace cada control

| Control           | Valor predeterminado | Rango    | Descripción                                       |
|-------------------|----------------------|----------|---------------------------------------------------|
| **VOX**           | Desactivado          | —        | Activa o desactiva la transmisión por voz         |
| **VOX level**     | —                    | 0–100%   | Umbral de activación para VOX                     |
| **Delay**         | —                    | 0–100    | Tiempo de retención antes de volver a recepción (unidades arbitrarias) |

## Consejos

- Comience con un nivel de VOX alrededor del 30–50% y ajústelo según su micrófono y volumen al hablar.
- Un retardo más largo evita que el transmisor se desconecte entre palabras o pausas cortas, pero un retardo demasiado largo puede hacer que el canal parezca ocupado.
- La etiqueta de porcentaje en el deslizador VOX level proporciona una retroalimentación precisa al ajustar el umbral.

## Solución de problemas

- **El botón VOX no se enciende** — Confirme que la radio esté conectada. VOX requiere una conexión de radio activa para funcionar.
- **VOX se activa demasiado fácilmente o no se activa en absoluto** — Ajuste el deslizador VOX level. Auméntelo para requerir un audio más fuerte, disminúyalo para permitir un audio más silencioso.
- **VOX se desconecta entre palabras** — Aumente el deslizador Delay para extender el tiempo de retención.

## Relacionado

- [Descripción general de Phone](overview.md)
- [Ajustar la frecuencia de corte baja del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Ajustar la frecuencia de corte alta del audio de TX](set-the-tx-audio-high-cut-frequency.md)

---

# Ajustar el nivel de portadora AM

Use el deslizador AM Carrier en el applet Phone para establecer el nivel de potencia de la portadora AM para la operación en modo AM.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Applet Panel esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice el deslizador **AM Carrier** en la parte superior del applet.
3. Arrastre el deslizador al nivel deseado. El rango válido es de 0 a 100 por ciento.
4. Mientras arrastra, aparece una etiqueta de porcentaje (por ejemplo, "48%") que muestra el nivel de portadora actual.

## Consejos

- El nivel de portadora AM debe configurarse para que coincida con las capacidades de su transmisor y la profundidad de modulación que desea lograr.
- Los niveles típicos de portadora AM varían del 20% al 80% dependiendo de su radio y sistema de antena.
- La etiqueta de porcentaje proporciona una retroalimentación precisa al ajustar el nivel de portadora.

## Solución de problemas

- **El deslizador AM Carrier no tiene efecto** — Confirme que la radio esté en modo AM. El deslizador solo controla el nivel de portadora AM.
- **No aparece ninguna etiqueta de porcentaje al arrastrar** — Esto indica una versión anterior del software. Actualice a v26.5.3 o posterior para ver la etiqueta.

## Relacionado

- [Descripción general de Phone](overview.md)
- [Ajustar la frecuencia de corte baja del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Ajustar la frecuencia de corte alta del audio de TX](set-the-tx-audio-high-cut-frequency.md)
