# Centre Doo en la banda de presencia de su micrófono

El control **Doo / Tune** establece la frecuencia central de la banda de excitación de alta frecuencia. Ajustarlo para que coincida con el pico de presencia de su micrófono permite que el procesador Doo agregue armónicos y aire exactamente en la parte correcta del espectro.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN. El applet PUDU permanece oculto hasta que la etapa esté activa.
- Abra el applet PUDU dentro del contenedor principal PooDoo Audio (TXDSP), o haga doble clic en la etapa PUDU (Enh) del widget CHAIN para abrir el editor flotante.

## Pasos

1. Ubique el grupo **Doo** — el conjunto de tres controles a la derecha, bajo la etiqueta de corchete "Doo".
2. Encuentre el control **Tune** (el primero debajo del corchete Doo).
3. Gire **Doo / Tune** hasta que el valor mostrado debajo del control coincida con la frecuencia de presencia o aire de su micrófono. El control muestra los valores como `X.X kHz` a partir de 1000 Hz, y como `X Hz` por debajo de 1000 Hz.
4. Transmita hacia una carga dummy o use el audio de monitoreo para verificar el resultado. Ajuste hasta lograr el rango de presencia deseado.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistente |
|---|---|---|---|
| Doo / Tune | 5000 Hz (5.0 kHz) | 1000 a 10000 Hz | `ClientPuduTxDooTuneHz` |

El control utiliza una escala logarítmica: un desplazamiento físico igual cubre proporciones de frecuencia iguales en todo el rango.

## Consejos

- La mayoría de los micrófonos dinámicos tienen un pico de presencia entre 3 kHz y 6 kHz; la mayoría de los micrófonos de condensador, entre 5 kHz y 10 kHz. Comience cerca del pico conocido de su micrófono y barra lentamente mientras monitorea.
- El logotipo de PooDoo pulsa con mayor brillo a medida que sube el nivel de la señal procesada (wet). Esto proporciona una indicación visual aproximada de que el procesador Doo está funcionando, pero use sus oídos para el ajuste final.
- Después de ajustar Doo / Tune, use **Doo / Air** para controlar la cantidad de contenido armónico que se agrega en esa frecuencia; luego utilice **Doo / Mix** para mezclar el efecto con la señal dry.

## Relacionado

- [Agregar aire con Doo Harmonics](add-air-with-doo-harmonics.md)
- [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Ajustar Poo al fundamental de su voz](tune-poo-to-the-fundamental-of-your-voice.md)
- [Descripción general del excitador PUDU](overview.md)
