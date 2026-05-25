# Seleccionar la nitidez de la pendiente del de-esser (12/24/36/48 dB/oct)

Elija con qué agresividad el filtro de la cadena lateral del de-esser atenúa las frecuencias fuera de la banda sibilante. Los valores de pendiente más altos producen un corte más pronunciado, lo que reduce la atenuación colateral en las frecuencias de rango medio.

## Antes de comenzar

- El de-esser debe estar habilitado en la cadena de audio (un solo clic en DESS en el widget CHAIN).
- Abra el editor De-Ess haciendo doble clic en DESS en el widget CHAIN, o abra el Aetherial Audio Channel Strip y haga doble clic en DESS en la cadena RX para el editor De-Ess de RX.

## Pasos

1. En el editor De-Ess (con el título "Aetherial De-Esser — TX" o "Aetherial De-Esser — RX"), localice el botón **Slope** en la columna izquierda, área inferior.
2. Haga clic en el botón **Slope**. Cada clic avanza al siguiente valor: 12 dB/oct → 24 dB/oct → 36 dB/oct → 48 dB/oct, y luego vuelve al inicio.
3. La etiqueta del botón se actualiza para mostrar la pendiente actual, por ejemplo, "24 dB/oct".
4. Pronuncie una frase sibilante (p. ej., "Sally sells sea shells") y escuche el sonido más natural con una atenuación mínima en las partes no sibilantes de su voz.

## Qué hace cada control

| Control | Etiqueta | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---------|----------|-------------|----------------------|--------------|------------------------|
| Pendiente (Slope) | Botón pulsador **Slope** | Recorre el conteo de cascadas del filtro de paso de banda de la cadena lateral. Cada etapa añade 12 dB/oct de rolloff fuera de la banda sibilante. | 24 dB/oct (2 etapas) | 12 / 24 / 36 / 48 dB/oct (1 a 4 etapas) | `ClientDeEssTxSlopeStages` o `ClientDeEssRxSlopeStages` |

## Consejos

- Comience con **24 dB/oct** (2 etapas) — esto proporciona un buen equilibrio entre un corte pronunciado y un sonido suave.
- Para sibilancias intensas que se activan en muchas palabras, pruebe con **12 dB/oct** — la pendiente más suave preserva un timbre más natural.
- Para sonidos "S" extremos en una voz por lo demás clara, **48 dB/oct** puede apuntar solo a la banda sibilante más áspera con un impacto mínimo en el rango medio.

## Relacionados

- [Descripción general del Aetherial De-Esser](overview.md)
- [Reducir o ampliar la banda de la cadena lateral con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Barrer la frecuencia para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
