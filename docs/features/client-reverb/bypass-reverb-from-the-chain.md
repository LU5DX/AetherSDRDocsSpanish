# Omitir la reverberación de la cadena

Deshabilitar la etapa de reverberación elimina el procesamiento Aetherial FreeVerb de la cadena de audio de TX sin cambiar ninguno de los valores de los mandos. Utilice esto cuando desee una transmisión seca, pero tenga la intención de volver a habilitar la reverberación más tarde con los mismos ajustes intactos.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa VERB ya debe aparecer en el widget CHAIN. Si la etapa de reverberación nunca se ha habilitado, aún no estará presente en la cadena.

## Pasos

1. Localice el widget CHAIN dentro del contenedor Aetherial Audio (TXDSP) en el panel de applets.
2. Haga un solo clic en la etapa VERB en el widget CHAIN para desactivarla.

El indicador de la etapa VERB cambia para mostrar que está inactiva. El subcontenedor "Aetherial FreeVerb" se oculta y la ruta de audio de TX pasa sin procesamiento de reverberación. Los cinco valores de los mandos (`ClientReverbTxSize`, `ClientReverbTxDecayS`, `ClientReverbTxDamping`, `ClientReverbTxPreDelayMs`, `ClientReverbTxMix`) se conservan.

Para volver a habilitar la reverberación, haga un solo clic en la etapa VERB nuevamente. El subcontenedor reaparece y el procesamiento se reanuda con los ajustes guardados previamente.

## Visualización de reverberación en vivo

A partir de la v0.9.7, el applet Aetherial FreeVerb incluye un panel compacto de visualización en vivo (90 px de alto) que se actualiza en tiempo real mientras ajusta los mandos. Se muestra directamente dentro del editor "Aetherial FreeVerb — TX", sobre la fila de mandos, y no requiere configuración.

La visualización muestra tres elementos superpuestos sobre un fondo oscuro:

| Elemento | Color | Qué representa |
|---|---|---|
| Paquete de seno seco | Cian | La señal sin procesar. Se desvanece hacia la derecha a medida que aumenta Mix. |
| Reflexiones de primer orden | Amarillo | Reflexiones tempranas. El espaciado y la cantidad responden a Size; la disminución de la amplitud responde a Damp. |
| Cola reverberante | Magenta | La cola de reverberación completa. La longitud sigue a Decay; la atenuación de alta frecuencia sigue a Damp; la posición de inicio sigue a Pre. |

Los cinco mandos alimentan la visualización directamente. Los cambios en Size, Decay, Damp, Pre o Mix se reflejan de inmediato; no necesita transmitir para ver el efecto.

## Consejos

- Omitir mediante el widget CHAIN no es destructivo. Sus valores de Size, Decay, Damp, Pre y Mix no se restablecen cuando la etapa está deshabilitada.
- Para inspeccionar o ajustar los valores de los mandos mientras la reverberación está omitida, haga doble clic en la etapa VERB para abrir el editor flotante "Aetherial FreeVerb — TX". Los cambios realizados allí surten efecto la próxima vez que se habilite la etapa.
- Utilice la visualización en vivo para ajustar Decay y Mix antes de salir al aire. Un Decay corto (0,3–1,2 s) con un Mix bajo (10–15 %) mantiene la voz inteligible.

## Relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste un Mix sutil: 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Ajuste el Decay al gusto sin que el habla se vuelva turbia](tune-decay-to-taste-without-muddying-speech.md)
