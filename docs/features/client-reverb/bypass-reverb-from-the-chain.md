# Omitir la reverberación de la cadena

Deshabilitar la etapa de reverberación elimina el procesamiento Aetherial FreeVerb de la cadena de audio de TX sin cambiar ninguno de los valores de los mandos. Utilice esto cuando desee una transmisión seca pero tenga la intención de volver a habilitar la reverberación más tarde con la misma configuración intacta.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe ser visible en el panel de applets.
- La etapa VERB ya debe aparecer en el widget CHAIN. Si la etapa de reverberación nunca se ha habilitado, aún no estará presente en la cadena.

## Pasos

1. Localice el widget CHAIN dentro del contenedor Aetherial Audio (TXDSP) en el panel de applets.
2. Haga un solo clic en la etapa VERB en el widget CHAIN para desactivarla.

El indicador de la etapa VERB cambia para mostrar que está inactiva. El editor "Aetherial FreeVerb — TX" se oculta y la ruta de audio de TX pasa sin procesamiento de reverberación. Los cinco valores de los mandos (`ClientReverbTxSize`, `ClientReverbTxDecayS`, `ClientReverbTxDamping`, `ClientReverbTxPreDelayMs`, `ClientReverbTxMix`) se conservan.

Para volver a habilitar la reverberación, haga un solo clic en la etapa VERB nuevamente. El editor reaparece y el procesamiento se reanuda con la configuración guardada previamente.

## Visualización en vivo de la reverberación

El applet Aetherial FreeVerb incluye un panel de visualización en vivo compacto (90 px de alto) que se actualiza en tiempo real mientras ajusta los mandos. Se muestra directamente dentro del editor "Aetherial FreeVerb — TX" sobre la fila de mandos y no requiere configuración.

La visualización muestra tres elementos superpuestos sobre un fondo de cuadrícula punteada fina con líneas de mira en el centro como referencia espacial:

| Elemento | Color | Qué representa |
|---------|-------|----------------|
| Paquete de seno seco | Cian, con degradado de desvanecimiento a transparente hacia la derecha | La señal sin procesar. |
| Reflexiones de primer orden | Amarillo, ráfagas de seno en decadencia | Reflexiones tempranas. El espaciado y la amplitud responden a Size y Damp. |
| Cola reverberante | Magenta, con decaimiento exponencial | La cola de reverberación completa. La longitud sigue a Decay; la atenuación de altas frecuencias sigue a Damp; la posición de inicio sigue a Pre. |

Los cinco mandos alimentan la visualización directamente. Los cambios en Size, Decay, Damp, Pre o Mix se reflejan de inmediato; no necesita transmitir para ver el efecto.

## Edición de valor en línea

Cada mando admite la edición de valor en línea. En lugar de arrastrar el mando, puede hacer clic en la etiqueta de valor debajo de cualquier mando y escribir un valor numérico directamente.

### Pasos

1. Localice el editor "Aetherial FreeVerb — TX" haciendo doble clic en la etapa VERB en el widget CHAIN.
2. Haga clic en el texto del valor debajo de cualquier mando (Size, Decay, Damp, Pre o Mix).
3. Escriba el valor numérico deseado.
4. Presione Enter o haga clic fuera del editor para confirmar.

El mando se actualiza al valor ingresado, limitado al rango válido. Si escribe un valor no válido, el mando vuelve a su configuración anterior.

**Notas:**
- El editor de valores admite separadores decimales según la configuración regional (por ejemplo, "12,5" en configuraciones regionales con coma decimal).
- Mientras edita, aparece un fondo oscuro con un borde cian para indicar el modo de edición.
- Presione Escape o haga clic fuera del editor para cancelar sin aplicar cambios.
- Los eventos de la rueda del ratón aún funcionan mientras el editor está enfocado.

## Controles de los mandos

Aetherial FreeVerb contiene cinco mandos dispuestos en una sola fila. Cada mando controla un parámetro de reverberación. Los colores de los mandos (fondo del anillo, arco del anillo, puntero, etiqueta, valor) están determinados por la configuración actual de `color.knob.*` y `color.text.*` del tema. Cuando el applet se coloca dentro de un contenedor con su propia anulación de color (por ejemplo, un applet/comp con un primer plano de mando ámbar), esas anulaciones se aplican automáticamente.

| Control | Etiqueta | Valor predeterminado | Rango válido | Clave de ajuste | Comportamiento | Notas |
|---------|----------|----------------------|--------------|-----------------|----------------|-------|
| Mando | Size | 50 % | 0.0 a 1.0 | `ClientReverbTxSize` | Mapeo lineal. Establece el tamaño de la sala modelada. | Etiqueta mostrada como porcentaje. |
| Mando | Decay | 1.20 s | 0.3 a 5.0 s | `ClientReverbTxDecayS` | Mapeo exponencial (0.3 * (5.0/0.3)^n, ~16.7x). Establece la longitud de la cola de reverberación. | Etiqueta 'X.XX s'. |
| Mando | Damp | 50 % | 0.0 a 1.0 | `ClientReverbTxDamping` | Mapeo lineal. Los valores más altos atenúan las altas frecuencias más rápido en la cola. | Etiqueta mostrada como porcentaje. |
| Mando | Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Mapeo lineal. Predelay entre la señal seca y las primeras reflexiones. | Etiqueta 'X ms'. |
| Mando | Mix | 15 % | 0.0 a 1.0 | `ClientReverbTxMix` | Mapeo lineal. Balance seco/húmedo. | Etiqueta mostrada como porcentaje. |

## Consejos

- Omitir a través del widget CHAIN no es destructivo. Sus valores de Size, Decay, Damp, Pre y Mix no se restablecen cuando la etapa está deshabilitada.
- Para inspeccionar o ajustar los valores de los mandos mientras la reverberación está omitida, haga doble clic en la etapa VERB para abrir el editor flotante "Aetherial FreeVerb — TX". Los cambios realizados allí surten efecto la próxima vez que se habilite la etapa.
- Utilice la visualización en vivo para ajustar Decay y Mix antes de salir al aire. Un Decay corto (0.3–1.2 s) con un Mix bajo (10–15 %) mantiene la voz inteligible.
- Utilice la edición de valor en línea para una entrada numérica precisa en lugar de arrastrar el mando.

## Relacionado

- [Aetherial FreeVerb overview](overview.md)
- [Dial in a subtle Mix — 10-15 % is typical for voice](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Tune decay to taste without muddying speech](tune-decay-to-taste-without-muddying-speech.md)
