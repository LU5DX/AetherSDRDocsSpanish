# Compensar las reflexiones respecto a la señal seca con Pre

Use el mando Pre para insertar un intervalo entre la señal seca y las primeras reflexiones de reverberación. Al aumentar Pre, la cola de reverberación se percibe más separada de la voz, lo que puede mejorar la claridad en transmisiones de voz sin reducir el efecto de sala general.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN o en el editor flotante Reverb. El subcontenedor REVERB permanece oculto hasta que la etapa esté activa.
- Abra el subcontenedor REVERB dentro del contenedor principal PooDoo Audio (TXDSP), o haga doble clic en la etapa Reverb del widget CHAIN para abrir el editor flotante Reverb.

## Pasos

1. Localice la fila de cinco mandos en el subcontenedor REVERB o en el editor flotante Reverb.
2. Encuentre el mando etiquetado como **Pre**.
3. Haga clic y arrastre el mando Pre hacia arriba para aumentar el pre-delay, o hacia abajo para disminuirlo. Mantenga presionado Shift mientras arrastra para un ajuste más fino.
4. Lea el valor actual en la etiqueta situada debajo del mando, que se muestra como `X ms`.
5. Suelte cuando la etiqueta muestre el pre-delay deseado.

Para restablecer Pre a su valor predeterminado, haga doble clic en el mando.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Configuración persistida | Comportamiento |
|---------|---------------|--------------|--------------------------|----------------|
| Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Mapeo lineal. Establece el retardo entre la señal seca y las primeras reflexiones de reverberación. Los valores más altos desplazan la cola más hacia atrás respecto a la voz. |

## Consejos

- Un valor de Pre de 0 ms hace que las reflexiones comiencen de inmediato, mezclándose estrechamente con la voz seca. Valores de 20–40 ms proporcionan una sensación de sala más natural en voz.
- La rueda de desplazamiento del ratón ajusta Pre en pasos del 1 % del rango total (aproximadamente 1 ms por muesca). El arrastre con Shift reduce el movimiento a un cuarto de la velocidad para una colocación precisa.
- Pre funciona junto con Mix. Si la cola parece estar ahogando la voz, reduzca Mix en lugar de bajar Pre hasta el mínimo.

## Relacionados

- [Descripción general de la reverberación](overview.md)
- [Ajustar un Mix sutil — entre el 10 y el 15 % es lo habitual para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Ajustar el decay al gusto sin enturbiar el habla](tune-decay-to-taste-without-muddying-speech.md)
- [Omitir la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
