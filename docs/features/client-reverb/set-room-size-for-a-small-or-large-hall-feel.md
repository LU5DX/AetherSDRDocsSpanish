# Ajuste del tamaño de la sala para una sensación de espacio pequeño o salón grande

El mando Size controla las dimensiones modeladas de la sala en la reverberación Aetherial FreeVerb TX. Al girarlo, el carácter cambia de una cabina cerrada a un salón grande.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. Si el subcontenedor "Aetherial FreeVerb" no es visible en el panel Aetherial Audio (TXDSP), habilite primero la etapa VERB.
- No se requiere una conexión de radio para ajustar los parámetros de reverberación.

## Pasos

1. Abra los controles de reverberación usando uno de estos dos métodos:
   - En el panel Aetherial Audio (TXDSP), localice el subcontenedor "Aetherial FreeVerb" y ajuste el mando Size directamente en la fila compacta.
   - Haga doble clic en la etapa VERB en el widget CHAIN para abrir el editor flotante "Aetherial FreeVerb — TX".
2. Gire el mando Size hacia la izquierda para un carácter de sala más pequeño y cerrado; gírelo hacia la derecha para una sensación de salón más grande y espacioso.
3. La etiqueta del mando se actualiza en tiempo real y muestra el valor actual como porcentaje (por ejemplo, `50 %`).
4. Para escribir un valor exacto, haga clic en la etiqueta del valor debajo del mando. La etiqueta se transforma en un editor de texto en línea con un borde cian. Escriba el número deseado y presione Enter. El valor se limita al rango válido. Hacer clic en otro lugar (pérdida de foco) también confirma la edición.

## Visualización en vivo

El editor "Aetherial FreeVerb — TX" incluye una pantalla de forma de onda compacta (90 px de alto) que se actualiza en tiempo real mientras ajusta cualquiera de los cinco mandos. Muestra tres capas de señal superpuestas:

- **Cian** — el paquete de seno seco. Su amplitud disminuye a medida que se aumenta Mix.
- **Amarillo** — reflexiones de primer orden. El espaciado y la cantidad reflejan los ajustes de Size y Damp.
- **Magenta** — la cola reverberante. La longitud sigue a Decay; la atenuación de altas frecuencias sigue a Damp; la posición de inicio sigue a Pre-delay.

La pantalla usa un fondo oscuro con una cuadrícula sutil. No se requiere interacción; se actualiza automáticamente cada vez que cambia un valor de mando.

## Qué hace cada control

| Etiqueta             | Valor predeterminado | Rango   | Comportamiento | Notas |
|----------------------|----------------------|---------|----------------|-------|
| Size                 | 50 %                 | 0 % a 100 % | Mapeo lineal. Establece el tamaño modelado de la sala. | Etiqueta mostrada como porcentaje. |
| Decay                | 1.20 s               | 0.3 a 5.0 s | Mapeo exponencial (0.3 * (5.0/0.3)^n, ~16.7x). Establece la longitud de la cola de reverberación. | Etiqueta 'X.XX s'. |
| Damp                 | 50 %                 | 0 % a 100 % | Mapeo lineal. Valores más altos atenúan las frecuencias altas más rápido en la cola. | Etiqueta mostrada como porcentaje. |
| Pre                  | 20 ms                | 0 a 100 ms | Mapeo lineal. Predelay entre la señal seca y las primeras reflexiones. | Etiqueta 'X ms'. |
| Mix                  | 15 %                 | 0 % a 100 % | Mapeo lineal. Balance seco/húmedo. | Etiqueta mostrada como porcentaje. |
| Visualización de reverberación | ReverbVizBox — visualización en vivo que muestra el paquete de seno seco (cian), reflexiones de primer orden (amarillo) y cola reverberante (magenta). Los cinco valores de mandos alimentan la representación para que la pantalla siga las ediciones de los mandos en tiempo real. 90 px de alto. | Siempre visible | Reemplaza el widget de curva usado por otros applets DSP. El algoritmo de representación coincide con StripReverbPanel::GridBox. | Cuadrícula de fondo con retículas en el centro como referencia espacial. |

## Indicadores de visualización

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Paquete de seno seco | Visible, cian, degradado | Señal seca visualizada como un paquete de seno. Cian, con un degradado horizontal que se desvanece hacia la derecha. |
| Reflexiones de primer orden | Visible, pulsos amarillos | Reflexiones tempranas mostradas como ráfagas de seno amarillas que se desvanecen, espaciado y amplitud impulsados por los valores de Size y Damping. |
| Cola reverberante | Visible, magenta, con decaimiento exponencial | Cola de reverberación dibujada como una onda seno magenta con decaimiento exponencial, longitud determinada por Decay y Damping. |
| Cuadrícula de fondo | Siempre visible | Fondo con cuadrícula de guiones finos y retículas en el centro como referencia espacial. |

## Edición de valor en línea

Cada mando admite entrada numérica directa:

1. Haga clic en la etiqueta del valor debajo del mando. La etiqueta se transforma en un editor de texto con fondo oscuro y borde cian.
2. Escriba el valor deseado. El análisis con reconocimiento de configuración regional admite tanto el punto decimal como la coma (por ejemplo, `0.5` o `0,5`). Los caracteres no numéricos adicionales se eliminan automáticamente.
3. Presione Enter para confirmar, o haga clic en otro lugar para aplicar el valor. El valor se limita al rango válido del mando.
4. Para cancelar sin cambiar el valor, presione Escape.
5. Mientras el editor tiene el foco, los eventos de la rueda del ratón aún ajustan el mando normalmente.

## Consejos

- Size y Decay interactúan estrechamente. Un Size grande con un Decay corto suena antinatural; si aumenta Size significativamente, considere aumentar Decay para igualar.
- La visualización en vivo en el editor flotante proporciona retroalimentación inmediata sobre cómo interactúan Size, Decay, Damp, Pre-delay y Mix antes de transmitir.
- Tanto el mando del applet compacto como el editor flotante "Aetherial FreeVerb — TX" controlan los mismos parámetros subyacentes y se mantienen sincronizados automáticamente.
- Haga doble clic en un mando para restablecerlo a su valor predeterminado.
- Use la edición en línea para valores numéricos precisos en lugar de depender únicamente de la rotación del mando.

## Relacionados

- [Resumen de Aetherial FreeVerb](overview.md)
- [Ajuste el decaimiento al gusto sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Marque un Mix sutil: 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Desvíe la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
