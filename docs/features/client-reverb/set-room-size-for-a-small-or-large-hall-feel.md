# Aetherial FreeVerb — Reverberación de TX

El Aetherial FreeVerb es un efecto de reverberación en el lado de TX que agrega ambiente de sala o salón a su voz transmitida. Proporciona una fila compacta de 5 perillas — Size, Decay, Damp, Pre-delay, Mix — con una visualización en vivo que muestra la señal seca y la cola de reverberación.

## Antes de comenzar

- La etapa de reverberación debe estar habilitada en el widget CHAIN. Si el subcontenedor "Aetherial FreeVerb" no es visible en el panel Aetherial Audio (TXDSP), habilite primero la etapa VERB.
- No se requiere una conexión de radio para ajustar los parámetros de reverberación.

## Pasos

1. Abra los controles de reverberación usando uno de estos dos métodos:
   - En el panel Aetherial Audio (TXDSP), localice el subcontenedor "Aetherial FreeVerb" y ajuste cualquier perilla directamente en la fila compacta.
   - Haga doble clic en la etapa VERB en el widget CHAIN para abrir el editor flotante "Aetherial FreeVerb — TX".
2. Gire la perilla Size hacia la izquierda para un carácter de sala más pequeño y ajustado; gírela hacia la derecha para una sensación de salón más amplia y espaciosa.
3. Gire la perilla Decay para controlar cuánto dura la cola de reverberación. Los valores más altos producen un sostenido más prolongado.
4. Gire la perilla Damp para controlar la rapidez con que decaen las altas frecuencias. Los valores más altos producen una cola más cálida y menos brillante.
5. Gire la perilla Pre para ajustar el retardo entre la señal seca y las primeras reflexiones.
6. Gire la perilla Mix para ajustar el balance seco/húmedo. Los ajustes típicos para voz son 10-15 % húmedo.
7. La etiqueta de cada perilla se actualiza en tiempo real y muestra el valor actual.
8. Para escribir un valor exacto, haga clic en la etiqueta de valor debajo de la perilla. La etiqueta se transforma en un editor de texto en línea con un fondo oscuro y borde cian. Escriba el número deseado y presione Enter. El valor se limita al rango válido. Hacer clic en otro lugar (pérdida de foco) también confirma la edición.

## Visualización en vivo

El editor "Aetherial FreeVerb — TX" incluye una pantalla de forma de onda compacta (90 px de alto) que se actualiza en tiempo real mientras ajusta cualquiera de las cinco perillas. Muestra tres capas de señal superpuestas sobre un fondo oscuro con una rejilla sutil:

- **Cian** — el paquete de seno seco. Su amplitud disminuye a medida que se aumenta Mix.
- **Amarillo** — reflexiones de primer orden. El espaciado y la cantidad reflejan los ajustes de Size y Damp.
- **Magenta** — la cola reverberante. La longitud sigue a Decay; la amortiguación de altas frecuencias sigue a Damp; la posición de inicio sigue a Pre-delay.

La pantalla se actualiza automáticamente cada vez que cambia un valor de perilla. No se requiere interacción.

## Qué hace cada control

| Etiqueta            | Valor predeterminado | Rango       | Comportamiento | Notas |
|---------------------|----------------------|-------------|----------------|-------|
| Size                | 50 %                 | 0 % a 100 % | Mapeo lineal. Establece el tamaño de la sala modelada. | Etiqueta mostrada como porcentaje. |
| Decay               | 1.20 s               | 0.3 a 5.0 s | Mapeo exponencial (0.3 * (5.0/0.3)^n, ~16.7x). Establece la longitud de la cola de reverberación. | Etiqueta 'X.XX s'. |
| Damp                | 50 %                 | 0 % a 100 % | Mapeo lineal. Los valores más altos amortiguan más rápido las altas frecuencias en la cola. | Etiqueta mostrada como porcentaje. |
| Pre                 | 20 ms                | 0 a 100 ms  | Mapeo lineal. Predelanto entre la señal seca y las primeras reflexiones. | Etiqueta 'X ms'. |
| Mix                 | 15 %                 | 0 % a 100 % | Mapeo lineal. Balance seco / húmedo. | Etiqueta mostrada como porcentaje. |
| Visualización de reverberación | ReverbVizBox — visualización en vivo que muestra el paquete de seno seco (cian), reflexiones de primer orden (amarillo) y cola reverberante (magenta). Los valores de las cinco perillas alimentan la representación, por lo que la pantalla sigue las ediciones de perillas en tiempo real. 90 px de alto. | Siempre visible | Reemplaza el widget de curva usado por otros applets de DSP. El algoritmo de representación coincide con StripReverbPanel::GridBox. | Rejilla de fondo con líneas de mira en el centro como referencia espacial. |

## Indicadores de visualización

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Paquete de seno seco | Visible, cian, degradado | Señal seca visualizada como un paquete de seno. Cian, con un degradado horizontal que se desvanece a transparente hacia la derecha. |
| Reflexiones de primer orden | Visible, pulsos amarillos | Reflexiones tempranas mostradas como ráfagas de seno amarillas que decaen, espaciado y amplitud determinados por los valores de Size y Damping. |
| Cola reverberante | Visible, magenta, decaimiento exponencial | Cola de reverberación dibujada como una onda seno magenta con decaimiento exponencial, longitud determinada por Decay y Damping. |
| Rejilla de fondo | Siempre visible | Fondo de rejilla punteada delgada con líneas de mira en el centro como referencia espacial. |

## Edición de valor en línea

Cada perilla admite entrada numérica directa:

1. Haga clic en la etiqueta de valor debajo de la perilla. La etiqueta se transforma en un editor de texto con fondo oscuro y borde cian.
2. Escriba el valor deseado. El análisis con reconocimiento de configuración regional admite tanto el punto decimal como la coma (por ejemplo, `0.5` o `0,5`). Los caracteres no numéricos adicionales se eliminan automáticamente.
3. Presione Enter para confirmar, o haga clic en otro lugar para aplicar el valor. El valor se limita al rango válido de la perilla.
4. Para cancelar sin cambiar el valor, presione Escape.
5. Mientras el editor tiene el foco, los eventos de la rueda del ratón aún ajustan la perilla normalmente.

## Consejos

- Size y Decay interactúan estrechamente. Un Size grande con un Decay corto suena antinatural; si aumenta Size significativamente, considere aumentar Decay para que coincida.
- La visualización en vivo en el editor flotante proporciona retroalimentación inmediata sobre cómo interactúan Size, Decay, Damp, Pre-delay y Mix antes de transmitir.
- Tanto la fila compacta de perillas del applet como el editor flotante "Aetherial FreeVerb — TX" controlan los mismos parámetros subyacentes y se mantienen sincronizados automáticamente.
- Hacer doble clic en una perilla la restablece a su valor predeterminado.
- Use la edición en línea para valores numéricos precisos en lugar de depender solo de la rotación de la perilla.

## Relacionado

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste el decaimiento al gusto sin enturbiar el habla](tune-decay-to-taste-without-muddying-speech.md)
- [Marque un Mix sutil — 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omita la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
