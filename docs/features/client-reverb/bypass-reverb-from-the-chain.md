# Omitir la reverberación de la cadena

Deshabilitar la etapa de reverberación elimina el procesamiento Aetherial FreeVerb de la cadena de audio de TX sin cambiar los valores de ningún control. Utilice esto cuando desee una transmisión seca, pero piense volver a habilitar la reverberación más tarde con la misma configuración intacta.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa VERB ya debe aparecer en el widget CHAIN. Si la etapa de reverberación nunca se ha habilitado, aún no estará presente en la cadena.

## Pasos

1. Localice el widget CHAIN dentro del contenedor Aetherial Audio (TXDSP) en el panel de applets.
2. Haga clic una vez en la etapa VERB en el widget CHAIN para desactivarla.

El indicador de la etapa VERB cambia para mostrar que está inactiva. El subcontenedor "Aetherial FreeVerb" se oculta y la ruta de audio de TX pasa sin procesamiento de reverberación. Los cinco valores de control (`ClientReverbTxSize`, `ClientReverbTxDecayS`, `ClientReverbTxDamping`, `ClientReverbTxPreDelayMs`, `ClientReverbTxMix`) se conservan.

Para volver a habilitar la reverberación, haga clic una vez en la etapa VERB nuevamente. El subcontenedor reaparece y el procesamiento se reanuda con la configuración guardada anteriormente.

## Visualización de reverberación en vivo

A partir de la v0.9.7, el applet Aetherial FreeVerb incluye un panel compacto de visualización en vivo (90 px de alto) que se actualiza en tiempo real mientras ajusta los controles. Se muestra directamente dentro del editor "Aetherial FreeVerb — TX", encima de la fila de controles, y no requiere configuración.

La visualización muestra tres elementos superpuestos sobre un fondo oscuro:

| Elemento                 | Color | Qué representa |
|-------------------------|--------|----------------|
| Paquete de seno seco    | Cian, con degradado transparente hacia la derecha | La señal no procesada. |
| Reflexiones de primer orden | Amarillo, con ráfagas de seno decadentes | Reflexiones tempranas. El espaciado y la amplitud responden a Size y Damp. |
| Cola reverberante       | Magenta, con decaimiento exponencial | La cola de reverberación completa. La longitud sigue a Decay; la atenuación de altas frecuencias sigue a Damp; la posición de inicio sigue a Pre. |

Los cinco controles alimentan la visualización directamente. Los cambios en Size, Decay, Damp, Pre o Mix se reflejan inmediatamente; no necesita transmitir para ver el efecto.

## Edición de valores en línea

A partir de la v26.5.2.1, cada control admite la edición de valores en línea. En lugar de arrastrar el control, puede hacer clic en la etiqueta de valor debajo de cualquier control y escribir un valor numérico directamente.

### Pasos

1. Localice el editor "Aetherial FreeVerb — TX" haciendo doble clic en la etapa VERB en el widget CHAIN.
2. Haga clic en el texto del valor debajo de cualquier control (Size, Decay, Damp, Pre o Mix).
3. Escriba el valor numérico deseado.
4. Presione Enter o haga clic fuera para confirmar.

El control se actualiza al valor ingresado, limitado al rango válido. Si escribe un valor no válido, el control vuelve a su configuración anterior.

**Notas:**
- El editor de valores admite separadores decimales según la configuración regional (p. ej., "12,5" en configuraciones regionales que usan coma decimal).
- Durante la edición, aparece un fondo oscuro con borde cian para indicar el modo de edición.
- Presione Escape o haga clic fuera del editor para cancelar sin aplicar los cambios.
- Los eventos de la rueda del ratón siguen funcionando mientras el editor está enfocado.

## Controles

El Aetherial FreeVerb contiene cinco controles dispuestos en una sola fila. Cada control ajusta un parámetro de reverberación.

| Control | Etiqueta | Valor predeterminado | Rango válido | Clave de ajuste | Comportamiento | Notas |
|---------|----------|---------------------|--------------|-----------------|----------------|-------|
| Control | Size | 50 % | 0.0 a 1.0 | `ClientReverbTxSize` | Mapeo lineal. Define el tamaño de la sala modelada. | La etiqueta se muestra como porcentaje. |
| Control | Decay | 1.20 s | 0.3 a 5.0 s | `ClientReverbTxDecayS` | Mapeo exponencial (0.3 * (5.0/0.3)^n, ~16.7x). Define la longitud de la cola de reverberación. | Etiqueta 'X.XX s'. |
| Control | Damp | 50 % | 0.0 a 1.0 | `ClientReverbTxDamping` | Mapeo lineal. Los valores más altos amortiguan las frecuencias altas más rápido en la cola. | La etiqueta se muestra como porcentaje. |
| Control | Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Mapeo lineal. Predelay entre la señal seca y las primeras reflexiones. | Etiqueta 'X ms'. |
| Control | Mix | 15 % | 0.0 a 1.0 | `ClientReverbTxMix` | Mapeo lineal. Balance seco/húmedo. | La etiqueta se muestra como porcentaje. |

## Consejos

- Omitir mediante el widget CHAIN no es destructivo. Sus valores de Size, Decay, Damp, Pre y Mix no se restablecen cuando la etapa está deshabilitada.
- Para inspeccionar o ajustar los valores de los controles mientras la reverberación está omitida, haga doble clic en la etapa VERB para abrir el editor flotante "Aetherial FreeVerb — TX". Los cambios realizados allí surtirán efecto la próxima vez que se habilite la etapa.
- Utilice la visualización en vivo para ajustar Decay y Mix antes de salir al aire. Un Decay corto (0.3–1.2 s) con un Mix bajo (10–15 %) mantiene la voz inteligible.
- Utilice la edición de valores en línea para una entrada numérica precisa en lugar de arrastrar el control.

## Relacionado

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste un Mix sutil: 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Ajuste el Decay a su gusto sin enturbiar el habla](tune-decay-to-taste-without-muddying-speech.md)
