# Ajuste sutil de la mezcla: entre 10 y 15 % es típico para voz

El control Mix regula el equilibrio seco/húmedo (dry/wet) de la reverberación Aetherial FreeVerb en su audio transmitido. Mantener Mix en el rango 10–15 % añade una ligera sensación de espacio sin que su voz suene procesada o distante.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. El subcontenedor "Aetherial FreeVerb" permanece oculto hasta que la etapa esté activa.
- Puede ajustar Mix desde la fila compacta de applets dentro del contenedor Aetherial Audio (TXDSP) o desde el editor flotante "Aetherial FreeVerb — TX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa VERB del widget CHAIN. Aparecerá el editor titulado "Aetherial FreeVerb — TX".
2. Localice el control Mix: es el quinto control (el más a la derecha) en la fila de perillas del editor.
3. Gire Mix hasta alcanzar el valor deseado. La etiqueta del control se actualiza en tiempo real mostrando un porcentaje (por ejemplo, `15 %`). También puede hacer clic en el texto del valor y escribir un número directamente; presione Enter o haga clic fuera para confirmar.
4. Para voz, ajuste Mix entre un 10 % y un 15 %. Valores más bajos mezclan menos cola de reverberación; valores más altos hacen que el efecto sea más notorio.
5. Cierre el editor o déjelo abierto. El valor se guarda de inmediato.

## Función de cada control

| Etiqueta             | Valor predeterminado | Rango válido | Notas |
|----------------------|----------------------|--------------|-------|
| Mix                  | 15 %                 | 0–100 % (0.0 a 1.0) | Mapeo lineal. Balance seco/húmedo. |
| Size                 | 50 %                 | 0–100 % (0.0 a 1.0) | Mapeo lineal. Define el tamaño de la sala modelada. |
| Decay                | 1.20 s               | 0.3 a 5.0 s         | Mapeo exponencial (0.3 * (5.0/0.3)^n, ~16.7x). Duración de la cola de reverberación. |
| Damp                 | 50 %                 | 0–100 % (0.0 a 1.0) | Mapeo lineal. Valores altos atenúan las frecuencias altas en la cola más rápidamente. |
| Pre                  | 20 ms                | 0 a 100 ms          | Mapeo lineal. Predelay entre la señal seca y las primeras reflexiones. |
| Visualización de reverberación | ReverbVizBox — visualización en vivo que muestra el paquete senoidal seco (cian), reflexiones de primer orden (amarillo) y cola reverberante (magenta). Los cinco valores de los controles alimentan el renderizado, por lo que la visualización sigue las ediciones de los controles en tiempo real. 90 px de altura. | Reemplaza el widget de curva utilizado por otros applets de DSP. El algoritmo de renderizado coincide con StripReverbPanel::GridBox. |

## Edición inline de valores

La versión v26.5.2.1 añade edición inline de valores para todos los controles del editor "Aetherial FreeVerb — TX". Haga clic en el valor numérico que se muestra debajo de un control para abrir un campo de entrada de texto. Escriba un nuevo valor y presione Enter, o haga clic en cualquier lugar fuera del editor, para confirmar el cambio. El valor se ajusta automáticamente al rango válido del control.

Para cancelar una edición, presione la tecla Escape antes de confirmar. El control vuelve a su valor anterior.

## Visualización en vivo

La versión v0.9.7 añade una pequeña visualización de reverberación dentro del editor "Aetherial FreeVerb — TX". Aparece como una representación de forma de onda de 90 px de altura sobre la fila de controles y se actualiza en tiempo real a medida que gira cualquier control.

La visualización utiliza tres capas codificadas por colores:

| Color  | Qué representa |
|--------|----------------|
| Cian   | Señal seca: un paquete senoidal que se desvanece hacia la derecha a medida que Mix aumenta. |
| Amarillo | Reflexiones de primer orden: ráfagas cortas cuyo espaciado se amplía con Size y cuya amplitud disminuye con Damp. |
| Magenta | Cola reverberante: una oscilación de decaimiento exponencial cuya duración sigue a Decay y cuya posición de inicio sigue a Pre. |

La visualización es de solo lectura. No añade ni elimina procesamiento; solo refleja los valores actuales de los controles. El algoritmo de diseño coincide con el panel de reverberación del lado de la tira, por lo que ambas vistas se leen de forma coherente cuando ambas están abiertas al mismo tiempo.

## Consejos

- El valor predeterminado de Mix es 15 %, que ya se encuentra dentro del rango típico para voz. Si restablece el control a su valor predeterminado, volverá a 15 %.
- El control compacto del applet y el control del editor flotante permanecen sincronizados. Los cambios realizados en uno se reflejan en el otro en aproximadamente 33 ms.
- Mix al 0 % solo pasa señal seca; la etapa de reverberación sigue activa pero es inaudible. Para eliminarla por completo de la cadena de procesamiento, consulte [Bypass reverb from the chain](bypass-reverb-from-the-chain.md).
- Use la visualización en vivo para obtener una lectura rápida de cómo interactúan Decay y Damp: una cola larga y brillante en la pantalla corresponde a una reverberación larga y rica en altas frecuencias en el audio transmitido.
- La edición inline admite tanto el formato decimal con punto como con coma. Por ejemplo, ingresar `1,5` y `1.5` produce el mismo valor en sistemas configurados con notación decimal europea.

## Relacionados

- [Aetherial FreeVerb overview](overview.md)
- [Bypass reverb from the chain](bypass-reverb-from-the-chain.md)
- [Tune decay to taste without muddying speech](tune-decay-to-taste-without-muddying-speech.md)
- [Reduce the high-end sparkle of the tail with Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Offset reflections from the dry signal with Pre](offset-reflections-from-the-dry-signal-with-pre.md)
