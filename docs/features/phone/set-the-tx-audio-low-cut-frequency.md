# Descripción general de Phone

El applet Phone proporciona controles de transmisión (TX) de voz para la radio FLEX-8600. Acceda a él haciendo clic en el botón de bandeja **PHNE** en la barra lateral derecha.

## Controles

| Control            | Tipo          | Descripción                                                                                                   |
|--------------------|---------------|---------------------------------------------------------------------------------------------------------------|
| **AM Carrier**     | Deslizador    | Establece el nivel de potencia de la portadora AM de 0 a 100 por ciento. Arrastre mientras mantiene presionado para ver una etiqueta de porcentaje (p. ej., "48%"). |
| **VOX**            | Botón de alternancia | Activa o desactiva la transmisión operada por voz.                                                                  |
| **VOX level**      | Deslizador    | Establece el umbral de activación de VOX de 0 a 100 por ciento. Arrastre mientras mantiene presionado para ver una etiqueta de porcentaje.        |
| **Delay**          | Deslizador    | Establece el tiempo de retención de VOX de 0 a 100 (unidades arbitrarias) antes de volver a recepción.                               |
| **DEXP**           | Botón de alternancia | Alterna el expansor descendente (puerta de ruido).                                                                   |
| **DEXP threshold** | Deslizador    | Establece el umbral de puerta de DEXP de 0 a 100 por ciento. Arrastre mientras mantiene presionado para ver una etiqueta de porcentaje.             |
| **Low Cut < / >**  | Campo de texto    | Ajusta la frecuencia de corte bajo del filtro de TX en pasos de 50 Hz. Valor predeterminado: 50 Hz. Rango: 0 Hz a (corte alto − 50 Hz). Haga doble clic para escribir un valor exacto en Hz. |
| **High Cut < / >** | Campo de texto    | Ajusta la frecuencia de corte alto del filtro de TX en pasos de 50 Hz. Valor predeterminado: 3300 Hz. Rango: (corte bajo + 50 Hz) a 10000 Hz. Haga doble clic para escribir un valor exacto en Hz. |

## Notas

- El deslizador de AM Carrier y el deslizador de nivel de VOX muestran una etiqueta de porcentaje al arrastrarlos (p. ej., "48%"). Esto proporciona una retroalimentación visual más clara del valor actual.
- Los controles de DEXP son funcionales en la versión 4.2 del firmware de la FLEX-8600. Los ajustes de DEXP se comunican directamente a la radio y ya no se guardan como preferencias de la aplicación.
- Todos los deslizadores del applet Phone utilizan la clase `GuardedSlider`, que proporciona un comportamiento de arrastre suave y retroalimentación visual.
- El applet Phone admite la personalización de temas. Todos los colores se adaptan al tema activo.
- Los controles de Low Cut y High Cut aceptan entrada numérica directa: haga doble clic en la pantalla de valores, escriba un valor exacto en Hz y presione Enter. En las radios que lo admiten, el valor escrito se aplica exactamente; en otras, la solicitud se cumple en la medida que la radio lo permite, mientras se conserva la lectura propia de la radio.
- Los valores escritos se validan contra el rango de filtro actual. Las entradas fuera de rango se rechazan y se restaura el valor anterior. Los botones de paso aún se ajustan a los límites de la radio.

## Relacionados

- [Establecer la frecuencia de corte bajo del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte alto del audio de TX](set-the-tx-audio-high-cut-frequency.md)
- [Activar VOX y establecer el umbral de disparo](enable-vox-and-set-trigger-threshold.md)

---

# Establecer la frecuencia de corte bajo del audio de TX

Use el control de Low Cut en el applet Phone para elevar el borde inferior de la banda de paso del audio de TX, eliminando retumbos, ruido de respiración o interferencia de baja frecuencia de su señal transmitida.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Applet Panel esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **Low Cut** en el área de filtro de TX en la parte inferior del applet.
3. Haga clic en **<** para disminuir la frecuencia de corte bajo o en **>** para aumentarla. También puede desplazar la rueda del ratón sobre la pantalla de valores para cambiar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los dos botones. El valor predeterminado es **50 Hz**.

## Establecer un valor exacto

Puede escribir un valor exacto en Hz en lugar de cambiar en pasos de 50 Hz:

1. Haga doble clic en la pantalla de valores de corte bajo. Se abre un campo de entrada de texto.
2. Escriba la frecuencia deseada en Hz.
3. Presione **Enter** para confirmar, o **Esc** para cancelar y restaurar el valor anterior.

Cuando escribe un valor, se trata como una solicitud de esa frecuencia exacta. Si la radio admite el valor, se aplica exactamente como se escribió. Si no, la solicitud se rechaza y se restaura el valor anterior. Los botones de paso aún se ajustan a la cuadrícula de pasos de 50 Hz de la radio.

## Cómo funcionan los botones de paso

Cada clic en **<** o **>** ajusta la frecuencia de corte bajo al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el valor actual es 87 Hz, al hacer clic en **>** se establece en 100 Hz y al hacer clic en **<** se establece en 50 Hz. Si el valor ya es un múltiplo exacto de 50 Hz, los botones lo mueven al siguiente múltiplo en la dirección elegida.

Esto significa que un solo clic siempre aterriza en un límite limpio de 50 Hz, independientemente del valor inicial.

## Qué hace cada control

| Control               | Valor predeterminado | Rango válido                             |
|-----------------------|---------|-----------------------------------------|
| **Low Cut** **<**     | —       | Ajusta hacia abajo al múltiplo de 50 Hz inferior siguiente |
| **Low Cut** **>**     | —       | Ajusta hacia arriba al múltiplo de 50 Hz superior siguiente  |
| Pantalla de valores de Low Cut | 50 Hz   | 0 Hz a (corte alto − 50 Hz), paso de 50 Hz  |

## Consejos

- El valor de corte bajo no puede establecerse más alto que la frecuencia de corte alto actual menos 50 Hz. Si está cerca de ese límite, primero baje el corte alto o súbalo para crear espacio.
- Para voz SSB, un corte bajo típico de 100–200 Hz reduce el ruido de baja frecuencia sin afectar notablemente la inteligibilidad de la voz.
- Debido a que los botones se ajustan a múltiplos de 50 Hz, un solo clic desde cualquier valor fuera del límite puede mover la frecuencia menos de 50 Hz. Esto es un comportamiento esperado.

## Solución de problemas

- **Los botones de Low Cut no hacen nada** — Confirme que la radio esté conectada. Los controles de filtro de TX requieren una conexión de radio activa para enviar los cambios de filtro a la FLEX-8600.
- **El valor escrito se rechaza** — El valor está fuera del rango válido (0 Hz a corte alto − 50 Hz) o no está en la cuadrícula de pasos admitida por la radio. Verifique el ajuste actual de corte alto e intente un valor dentro del rango.

## Relacionados

- [Establecer la frecuencia de corte alto del audio de TX](set-the-tx-audio-high-cut-frequency.md)
- [Descripción general de Phone](overview.md)
- [Activar VOX y establecer el umbral de disparo](enable-vox-and-set-trigger-threshold.md)

---

# Establecer la frecuencia de corte alto del audio de TX

Use el control de High Cut en el applet Phone para bajar el borde superior de la banda de paso del audio de TX, reduciendo siseos, silbidos o ruido de alta frecuencia de su señal transmitida.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Applet Panel esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **High Cut** en el área de filtro de TX en la parte inferior del applet.
3. Haga clic en **<** para disminuir la frecuencia de corte alto o en **>** para aumentarla. También puede desplazar la rueda del ratón sobre la pantalla de valores para cambiar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los dos botones. El valor predeterminado es **3300 Hz**.

## Establecer un valor exacto

Puede escribir un valor exacto en Hz en lugar de cambiar en pasos de 50 Hz:

1. Haga doble clic en la pantalla de valores de corte alto. Se abre un campo de entrada de texto.
2. Escriba la frecuencia deseada en Hz.
3. Presione **Enter** para confirmar, o **Esc** para cancelar y restaurar el valor anterior.

Cuando escribe un valor, se trata como una solicitud de esa frecuencia exacta. Si la radio admite el valor, se aplica exactamente como se escribió. Si no, la solicitud se rechaza y se restaura el valor anterior. Los botones de paso aún se ajustan a la cuadrícula de pasos de 50 Hz de la radio.

## Cómo funcionan los botones de paso

Cada clic en **<** o **>** ajusta la frecuencia de corte alto al múltiplo de 50 Hz más cercano en la dirección elegida. Por ejemplo, si el valor actual es 1234 Hz, al hacer clic en **>** se establece en 1250 Hz y al hacer clic en **<** se establece en 1200 Hz. Si el valor ya es un múltiplo exacto de 50 Hz, los botones lo mueven al siguiente múltiplo en la dirección elegida.

Esto significa que un solo clic siempre aterriza en un límite limpio de 50 Hz, independientemente del valor inicial.

## Qué hace cada control

| Control                | Valor predeterminado | Rango válido                                |
|------------------------|---------|--------------------------------------------|
| **High Cut** **<**     | —       | Ajusta hacia abajo al múltiplo de 50 Hz inferior siguiente    |
| **High Cut** **>**     | —       | Ajusta hacia arriba al múltiplo de 50 Hz superior siguiente     |
| Pantalla de valores de High Cut | 3300 Hz | (corte bajo + 50 Hz) a 10000 Hz, paso de 50 Hz  |

## Consejos

- El valor de corte alto no puede establecerse más bajo que la frecuencia de corte bajo actual más 50 Hz. Si está cerca de ese límite, primero suba el corte bajo o bájelo para crear espacio.
- Para voz SSB, un corte alto típico de 2700–3000 Hz reduce el silbido manteniendo una buena inteligibilidad. Para AM o FM, pueden ser apropiados ajustes más altos.
- Debido a que los botones se ajustan a múltiplos de 50 Hz, un solo clic desde cualquier valor fuera del límite puede mover la frecuencia menos de 50 Hz. Esto es un comportamiento esperado.

## Solución de problemas

- **Los botones de High Cut no hacen nada** — Confirme que la radio esté conectada. Los controles de filtro de TX requieren una conexión de radio activa para enviar los cambios de filtro a la FLEX-8600.
- **El valor escrito se rechaza** — El valor está fuera del rango válido (corte bajo + 50 Hz a 10000 Hz) o no está en la cuadrícula de pasos admitida por la radio. Verifique el ajuste actual de corte bajo e intente un valor dentro del rango.

## Relacionados

- [Establecer la frecuencia de corte bajo del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Descripción general de Phone](overview.md)
- [Activar VOX y establecer el umbral de disparo](enable-vox-and-set-trigger-threshold.md)

---

# Activar VOX y establecer el umbral de disparo

Use los controles de VOX en el applet Phone para activar la transmisión operada por voz y ajustar la sensibilidad y el tiempo de retención.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Applet Panel esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Haga clic en el botón de alternancia **VOX** para activar la transmisión operada por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el deslizador de **VOX level** para establecer el umbral de activación:
   - Arrastre el deslizador hacia la derecha (valor más alto) para requerir audio más fuerte que active la transmisión.
   - Arrastre el deslizador hacia la izquierda (valor más bajo) para permitir que audio más silencioso active la transmisión.
   - Mientras arrastra, aparece una etiqueta de porcentaje (p. ej., "45%") que muestra el nivel actual.
4. Ajuste el deslizador de **Delay** para establecer cuánto tiempo continúa la transmisión después de dejar de hablar:
   - Arrastre el deslizador hacia la derecha para un tiempo de retención más largo.
   - Arrastre el deslizador hacia la izquierda para un tiempo de retención más corto.

## Qué hace cada control

| Control         | Valor predeterminado    | Rango    | Descripción                                      |
|-----------------|------------|----------|--------------------------------------------------|
| **VOX**         | Desactivado   | —        | Activa/desactiva la transmisión operada por voz           |
| **VOX level**   | —          | 0–100%   | Umbral de activación para VOX                     |
| **Delay**       | —          | 0–100    | Tiempo de retención antes de volver a recepción (unidades arbitrarias) |

## Consejos

- Comience con un nivel de VOX alrededor de 30–50% y ajústelo según su micrófono y volumen de habla.
- Un retraso más largo evita que el transmisor se corte entre palabras o pausas cortas, pero un retraso demasiado largo puede hacer que el canal parezca ocupado.
- La etiqueta de porcentaje en el deslizador de nivel de VOX proporciona una retroalimentación precisa al ajustar el umbral.

## Solución de problemas

- **El botón de VOX no se activa** — Confirme que la radio esté conectada. VOX requiere una conexión de radio activa para funcionar.
- **VOX se activa con demasiada facilidad o no se activa en absoluto** — Ajuste el deslizador de nivel de VOX. Auméntelo para requerir audio más fuerte, o disminúyalo para permitir audio más silencioso.
- **VOX se corta entre palabras** — Aumente el deslizador de Delay para extender el tiempo de retención.

## Relacionados

- [Descripción general de Phone](overview.md)
- [Establecer la frecuencia de corte bajo del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte alto del audio de TX](set-the-tx-audio-high-cut-frequency.md)

---

# Establecer el nivel de portadora AM

Use el deslizador de AM Carrier en el applet Phone para establecer el nivel de potencia de la portadora AM para la operación en modo AM.

## Antes de comenzar
