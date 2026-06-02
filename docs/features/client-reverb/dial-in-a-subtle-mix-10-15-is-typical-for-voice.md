# Ajuste sutil de la Mezcla — 10-15 % es lo normal para voz

El control Mezcla regula el balance seco/húmedo de la reverberación Aetherial FreeVerb en su audio transmitido. Mantener la Mezcla en el rango 10-15 % añade una ligera sensación de espacio sin que su voz suene procesada o distante.

## Antes de comenzar

- La etapa de Reverberación debe estar habilitada en el widget CHAIN. El subcontenedor "Aetherial FreeVerb" permanece oculto hasta que la etapa esté activa.
- Puede ajustar la Mezcla desde la fila compacta de applets dentro del contenedor Aetherial Audio (TXDSP) o desde el editor flotante "Aetherial FreeVerb — TX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa VERB del widget CHAIN. Aparecerá el editor titulado "Aetherial FreeVerb — TX".
2. Localice el control Mezcla: es el quinto control, el que está más a la derecha en la fila del editor.
3. Gire Mezcla hasta el valor deseado. La etiqueta del control se actualiza en tiempo real, mostrada como porcentaje (por ejemplo, `15 %`). También puede hacer clic en el texto del valor y escribir un número directamente: presione Enter o haga clic en otro lugar para confirmar.
4. Para voz, ajuste Mezcla entre el 10 % y el 15 %. Los valores más bajos mezclan menos cola de reverberación; los valores más altos hacen que el efecto sea más notorio.
5. Cierre el editor o déjelo abierto. El valor se guarda inmediatamente.

## Función de cada control

| Etiqueta                | Valor predeterminado | Rango válido | Notas |
|-------------------------|----------------------|--------------|-------|
| Mix (Mezcla)            | 15 % | 0–100 % (0.0 a 1.0) | Mapeo lineal. Balance seco/húmedo. |
| Size (Tamaño)           | 50 % | 0–100 % (0.0 a 1.0) | Mapeo lineal. Define el tamaño de la sala modelada. |
| Decay (Decaimiento)     | 1.20 s | 0.3 a 5.0 s | Mapeo exponencial (0.3 * (5.0/0.3)^n, ~16.7x). Define la longitud de la cola de reverberación. |
| Damp (Atenuación)       | 50 % | 0–100 % (0.0 a 1.0) | Mapeo lineal. Valores más altos atendan las frecuencias altas más rápido en la cola. |
| Pre (Pre-demora)        | 20 ms | 0 a 100 ms | Mapeo lineal. Pre-demora entre la señal seca y las primeras reflexiones. |
| Visualización de reverberación | ReverbVizBox — visualización en vivo que muestra el paquete de onda senoidal seca (cian), reflexiones de primer orden (amarillo) y cola reverberante (magenta). Los cinco valores de control alimentan la representación, por lo que la pantalla sigue las ediciones de los controles en tiempo real. 90 píxeles de alto. | Reemplaza el widget de curva usado por otros applets de DSP. El algoritmo de representación coincide con StripReverbPanel::GridBox. |

## Edición de valor en línea

La versión v26.5.2.1 añade edición de valor en línea a todos los controles del editor "Aetherial FreeVerb — TX". Haga clic en el valor numérico mostrado debajo de un control para abrir un campo de entrada de texto. Escriba un nuevo valor y presione Enter, o haga clic en cualquier lugar fuera del editor, para confirmar el cambio. El valor se ajusta automáticamente al rango válido del control.

Para cancelar una edición, presione la tecla Escape antes de confirmar. El control vuelve a su valor anterior.

## Visualización en vivo

La versión v0.9.7 añade una pequeña visualización de reverberación dentro del editor "Aetherial FreeVerb — TX". Aparece como una pantalla de forma de onda de 90 píxeles de alto sobre la fila de controles y se actualiza en tiempo real a medida que gira cualquier control.

La pantalla usa tres capas codificadas por colores:

| Color | Qué representa |
|-------|----------------|
| Cian | Señal seca: un paquete de onda senoidal que se desvanece hacia la derecha a medida que aumenta la Mezcla. |
| Amarillo | Reflexiones de primer orden: ráfagas cortas cuyo espaciado se amplía con Tamaño y cuya amplitud disminuye con Atenuación. |
| Magenta | Cola reverberante: una oscilación de decaimiento exponencial cuya longitud sigue a Decaimiento y cuya posición de inicio sigue a Pre-demora. |

La visualización es de solo lectura. No añade ni elimina ningún procesamiento; solo refleja los valores actuales de los controles. El algoritmo de diseño coincide con el panel de reverberación del lado de la tira, por lo que ambas vistas se leen de forma coherente cuando ambas están abiertas al mismo tiempo.

## Tematización de color de los controles

La versión v26.6.1 introduce tematización de color por applet para el applet de reverberación. El contenedor de reverberación se registra como `applet/reverb` en el motor de temas, lo que permite que un archivo de tema asigne colores distintos a los controles de reverberación, independientemente de los controles de otros applets.

Los colores de los controles se toman del espacio de nombres `color.knob.*` en el tema:
- `color.knob.background` — el anillo detrás del arco de valor.
- `color.knob.foreground` — el arco relleno que muestra el valor actual.
- `color.knob.handle` — la línea señaladora dibujada desde el centro del anillo hasta el extremo del arco.
- `color.text.primary` — el texto del valor debajo del control.
- `color.text.secondary` — la etiqueta del control sobre el anillo.

Los cinco controles del editor "Aetherial FreeVerb — TX" usan los mismos colores temáticos. Para aplicar un esquema de color personalizado, consulte [Temas personalizados](custom-themes.md).

## Consejos

- El valor predeterminado de Mezcla es 15 %, que ya está dentro del rango típico para voz. Si restablece el control a su valor predeterminado, vuelve al 15 %.
- Tanto el control compacto del applet como el control del editor flotante se mantienen sincronizados. Los cambios realizados en uno se reflejan en el otro en aproximadamente 33 ms.
- Con Mezcla al 0 %, solo pasa la señal seca; la etapa de reverberación sigue activa pero es inaudible. Para eliminarla por completo de la cadena de procesamiento, consulte [Evitar la reverberación desde la cadena](bypass-reverb-from-the-chain.md).
- Use la visualización en vivo para obtener una lectura rápida de cómo interactúan Decaimiento y Atenuación: una cola larga y brillante en la pantalla corresponde a una reverberación larga y rica en altas frecuencias en el audio transmitido.
- La edición en línea admite formatos de número tanto con punto decimal como con coma decimal. Por ejemplo, ingresar `1,5` y `1.5` producen el mismo valor en sistemas configurados para notación decimal europea.

## Relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Evitar la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
- [Ajustar el decaimiento al gusto sin empañar el habla](tune-decay-to-taste-without-muddying-speech.md)
- [Reducir el brillo agudo de la cola con Atenuación](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Desplazar las reflexiones de la señal seca con Pre-demora](offset-reflections-from-the-dry-signal-with-pre.md)
- [Temas personalizados](custom-themes.md)
