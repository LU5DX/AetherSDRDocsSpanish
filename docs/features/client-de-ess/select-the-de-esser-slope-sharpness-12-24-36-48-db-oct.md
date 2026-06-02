# Seleccionar la pendiente de atenuación del de-esser (12/24/36/48 dB/oct)

Elija qué tan agresivamente el filtro de la cadena lateral del de-esser atenúa las frecuencias fuera de la banda sibilante. Los valores de pendiente más altos producen un corte más pronunciado, reduciendo la atenuación colateral en las frecuencias medias.

## Antes de comenzar

- El de-esser debe estar habilitado en la cadena de audio (un solo clic en DESS en el widget CHAIN).
- Abra el editor De-Ess haciendo doble clic en DESS en el widget CHAIN, o abra Aetherial Audio Channel Strip y haga doble clic en DESS en la cadena de RX para el editor De-Ess de RX.

## Pasos

1. En el editor De-Ess (con el título "Aetherial De-Esser — TX" o "Aetherial De-Esser — RX"), localice el botón pulsador **Slope** en la columna izquierda, área inferior.
2. Haga clic en el botón pulsador **Slope**. Cada clic avanza al siguiente valor: 12 dB/oct → 24 dB/oct → 36 dB/oct → 48 dB/oct, luego vuelve al inicio.
3. La etiqueta del botón se actualiza para mostrar la pendiente actual, por ejemplo "24 dB/oct".
4. Pronuncie una frase sibilante (p. ej., "Sally sells sea shells") y escuche el sonido más natural con la mínima atenuación en las partes no sibilantes de su voz.

## Qué hace cada control

| Control | Etiqueta              | Descripción                                                                                                       |
|---------|-----------------------|-------------------------------------------------------------------------------------------------------------------|
| Slope   | Botón pulsador **Slope** | Recorre la cantidad de etapas del filtro paso banda de la cadena lateral. Cada etapa añade 12 dB/oct de atenuación fuera de la banda sibilante. |

## Consejos

- Comience con **24 dB/oct** (2 etapas) — esto proporciona un buen equilibrio entre un corte preciso y un sonido suave.
- Para sibilancias intensas que se activan en muchas palabras, pruebe con **12 dB/oct** — la pendiente más suave preserva un timbre más natural.
- Para sonidos "S" extremos en una voz por lo demás clara, **48 dB/oct** puede apuntar solo a la banda sibilante más áspera con un impacto mínimo en las frecuencias medias.

## Tematización de colores (v26.6.1)

A partir de v26.6.1, el editor De-Ess y sus widgets internos (la curva de respuesta de la cadena lateral, las perillas y el medidor de reducción de ganancia) leen los colores del motor de temas. El contenedor del editor se registra bajo la clave de contenedor `applet/deess`, por lo que los autores de temas pueden asignar colores distintos al panel del editor De-Ess. Los colores de la curva (etiquetas de ejes, líneas de cuadrícula, curva del paso banda, línea de umbral y bola de frecuencia central) usan el mismo espacio de nombres de temas que otros applets de Aetherial. Los componentes de las perillas (arco, anillo de fondo, puntero y etiquetas) leen de `color.knob.*`.

## Relacionado

- [Descripción general de Aetherial De-Esser](overview.md)
- [Angostar o ensanchar la banda de la cadena lateral con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
