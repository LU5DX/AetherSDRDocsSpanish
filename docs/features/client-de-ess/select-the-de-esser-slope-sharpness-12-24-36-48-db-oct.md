# Seleccione la pendiente del filtro de-esser (12/24/36/48 dB/oct)

Elija cuán agresivamente el filtro de la cadena lateral del de-esser atenúa las frecuencias fuera de la banda sibilante. Los valores de pendiente más altos producen un corte más pronunciado, reduciendo la atenuación colateral en las frecuencias de rango medio.

## Antes de comenzar

- El de-esser debe estar habilitado en la cadena de audio (un solo clic en DESS en el widget CHAIN).
- Abra el editor De-Ess haciendo doble clic en DESS en el widget CHAIN, o abra el Aetherial Audio Channel Strip y haga doble clic en DESS en la cadena RX para el editor De-Ess de RX.

## Pasos

1. En el editor De-Ess (titulado "Aetherial De-Esser — TX" o "Aetherial De-Esser — RX"), localice el botón pulsador **Slope** en la columna izquierda, área inferior.
2. Haga clic en el botón pulsador **Slope**. Cada clic avanza al siguiente valor: 12 dB/oct → 24 dB/oct → 36 dB/oct → 48 dB/oct, luego vuelve al inicio.
3. La etiqueta del botón se actualiza para mostrar la pendiente actual, por ejemplo "24 dB/oct".
4. Pronuncie una frase sibilante (por ejemplo, "Sally sells sea shells") y escuche el sonido más natural con la mínima atenuación en las partes no sibilantes de su voz.

## Qué hace cada control

| Control | Etiqueta               | Descripción                                                                                             |
|---------|------------------------|---------------------------------------------------------------------------------------------------------|
| Slope   | Botón pulsador **Slope** | Recorre la cantidad de etapas del filtro paso banda de la cadena lateral. Cada etapa añade 12 dB/oct de atenuación fuera de la banda sibilante. |

## Consejos

- Comience con **24 dB/oct** (2 etapas): esto proporciona un buen equilibrio entre un corte pronunciado y un sonido suave.
- Para sibilancias intensas que se activan en muchas palabras, pruebe **12 dB/oct**: la pendiente más suave conserva un timbre más natural.
- Para sonidos "S" extremos en una voz por lo demás clara, **48 dB/oct** puede apuntar solo a la banda sibilante más agresiva con un impacto mínimo en el rango medio.

## Suavizado del medidor de reducción de ganancia (v26.6.3 – v26.7.4)

A partir de la v26.6.3, el medidor de reducción de ganancia utiliza un algoritmo de suavizado mejorado. El temporizador de animación del medidor ahora se detiene cuando el valor de reducción de ganancia se ha estabilizado, reduciendo los repintados innecesarios. El medidor se vuelve a dibujar solo cuando el valor suavizado o una bandera de repintado pendiente indican que se necesita un cambio visual. Esta optimización se aplica tanto al applet acoplado Aetherial De-Esser como a la instancia Aetherial De-Esser — RX accesible a través del Aetherial Audio Channel Strip.

A partir de la v26.7.4, el medidor se repinta en cada tic de animación, independientemente de si el valor se ha estabilizado o de si el indicador suavizado necesita repintarse. Esto garantiza que la curva de respuesta de la cadena lateral y la barra de reducción de ganancia permanezcan visualmente receptivas en todo momento, incluso cuando el valor de reducción de ganancia se ha estabilizado por completo. Se ha eliminado el botón pulsador de estilo de edición utilizado en versiones anteriores; el botón Slope ahora usa el estilo de botón de applet estándar.

## Temas de color (v26.6.1)

A partir de la v26.6.1, el editor De-Ess y sus widgets internos (la curva de respuesta de la cadena lateral, los mandos y el medidor de reducción de ganancia) leen los colores del motor de temas. El contenedor del editor se registra bajo la clave de contenedor `applet/deess`, por lo que los autores de temas pueden asignar colores distintos al panel del editor De-Ess. Los colores de la curva (etiquetas de ejes, líneas de cuadrícula, curva del filtro paso banda, línea de umbral y bola de frecuencia central) utilizan el mismo espacio de nombres de temas que otros applets de Aetherial. Los componentes del mando (arco, anillo de fondo, puntero y etiquetas) leen de `color.knob.*`.

## Relacionados

- [Descripción general del Aetherial De-Esser](overview.md)
- [Estreche o ensanche la banda de la cadena lateral con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Barra Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
