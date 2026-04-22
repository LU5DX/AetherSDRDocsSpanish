# Estrechar o ampliar la banda de la cadena lateral con Q

El control Q regula el ancho del filtro de paso de banda de la cadena lateral alrededor de la frecuencia central de sibilancia. Un Q más alto apunta a un segmento más estrecho del espectro; un Q más bajo abarca un rango más amplio. Ajuste Q después de haber localizado el pico de sibilancia con Freq.

## Antes de comenzar

- La etapa De-Ess debe estar habilitada y el applet DESS debe ser visible dentro del contenedor PooDoo Audio (TXDSP). Consulte [Descripción general del De-Esser](overview.md).
- Identifique primero la frecuencia central de su sibilancia. Consulte [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md).

## Pasos

1. Abra el applet DESS dentro del contenedor PooDoo Audio (TXDSP).
2. Localice el control Q en la fila de cuatro controles debajo de la curva de respuesta de la cadena lateral.
3. Gire Q en el sentido de las agujas del reloj para aumentar el valor y estrechar la banda, o en sentido contrario para disminuir el valor y ampliarla.
4. Observe cómo la curva de respuesta de la cadena lateral se actualiza en tiempo real. La forma de la curva muestra el ancho de paso de banda resultante alrededor del punto de frecuencia central.
5. Pronuncie una frase con sibilantes y observe la barra de reducción de ganancia. Confirme que el de-esser se activa únicamente en la sibilancia prevista, no en el audio circundante.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Q | 2.00 | 0.5 a 5.0 | `ClientDeEssTxQ` | Mapeo lineal. Valores más altos estrechan el paso de banda de la cadena lateral; valores más bajos lo amplían. |
| Curva de respuesta de la cadena lateral | — | — | — | Dibuja la forma del filtro de paso de banda con un punto animado en la frecuencia central actual. Se actualiza de inmediato al cambiar Q. |
| Barra de reducción de ganancia | — | 0 a 24 dB GR | — | Muestra la atenuación actual aplicada a la banda de la cadena lateral, refrescada a aproximadamente 30 Hz. |

## Consejos

- Comience con el Q predeterminado de 2.00 y ajuste desde ahí. La mayoría de la sibilancia se resuelve en el rango de 1.5 a 3.5.
- Un Q más estrecho (valor más alto) es más transparente porque deja intactas las frecuencias adyacentes, pero requiere que Freq esté precisamente sobre el pico de sibilancia.
- Un Q más amplio (valor más bajo) tolera mejor una configuración imprecisa de Freq, pero puede afectar consonantes y fricativas más allá de la banda sibilante.
- La curva de respuesta ofrece retroalimentación visual inmediata — úsela junto con la barra de reducción de ganancia en lugar de depender de una sola.

## Solución de problemas

- **La barra de reducción de ganancia muestra poca o ninguna actividad** — Q puede ser demasiado estrecho y el filtro no está alcanzando el pico de sibilancia. Reduzca Q ligeramente, o vuelva a barrer Freq para confirmar que la frecuencia central es correcta.
- **El de-esser se activa en el habla normal, no solo en las sibilantes** — Es probable que Q sea demasiado bajo (la banda es demasiado amplia). Aumente Q para ajustar el filtro alrededor de la frecuencia de sibilancia.

## Relacionados

- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Establecer el umbral justo por debajo de los picos de 'S' más altos](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observar la GR en vivo mientras se lee una frase con sibilantes](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Descripción general del De-Esser](overview.md)
