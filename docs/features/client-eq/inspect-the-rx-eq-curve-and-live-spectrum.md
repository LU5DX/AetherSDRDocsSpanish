# Inspeccionar la curva de EQ de RX y el espectro en vivo

El applet "Aetherial RX EQ" muestra la respuesta en frecuencia sumada de las bandas de su ecualizador de RX junto con una superposición de analizador FFT en tiempo real. Úselo para verificar que su EQ de RX está dando forma al audio de la manera que desea, sin necesidad de abrir el editor completo.

## Antes de comenzar

- El subcontenedor "Aetherial RX EQ" permanece oculto hasta que la etapa de EQ de RX esté habilitada. Habilítela primero desde el widget CHAIN o desde el editor flotante.
- El applet se encuentra dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets. Asegúrese de que el panel de applets esté visible (`View > Applet Panel`).

## Pasos

1. Localice el contenedor principal "Aetherial Audio (TXDSP)" en el panel de applets.
2. Expándalo para encontrar el subcontenedor "Aetherial RX EQ".
3. Observe el área del analizador/curva — la pantalla de 110 px de altura dentro del mosaico. Muestra dos elementos superpuestos:
   - **Respuesta de EQ sumada** — la respuesta en frecuencia acumulada de todas las bandas de RX habilitadas.
   - **Superposición del analizador en vivo** — un FFT en tiempo real del audio que pasa por la ruta de RX.
4. Es necesario que haya audio pasando por la ruta de RX para que la superposición del analizador en vivo muestre actividad. Reciba una señal o reproduzca audio a través de la cadena para ver el FFT animarse.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Área del analizador/curva | Pantalla de solo lectura que muestra la curva de respuesta de EQ sumada y la superposición del analizador FFT en vivo para la ruta de RX. La edición no está disponible aquí. | — |
| Respuesta de EQ sumada | Muestra la respuesta en frecuencia acumulada de todas las bandas habilitadas. Aparece plana cuando no hay bandas activas o todas están configuradas en 0 dB. | `ClientEqRxBands` |
| Superposición del analizador en vivo | FFT en tiempo real del audio que pasa por la ruta de RX. Inactivo cuando no hay audio presente; se anima cuando fluye audio. | `ClientEqRxEnabled` |

## Consejos

- El área del analizador/curva es de solo lectura en el applet. Para agregar, eliminar o ajustar bandas, abra el editor sin marco haciendo doble clic en la etapa de EQ de RX en el widget CHAIN.
- Haga clic derecho en la barra de título del subcontenedor "Aetherial RX EQ" para flotarlo, extraerlo o ocultarlo si desea posicionarlo de forma independiente.
- La superposición del analizador en vivo funciona únicamente mientras haya audio fluyendo por la ruta de RX. Si la superposición aparece inactiva, confirme que está recibiendo audio y que `ClientEqRxEnabled` está activo.

## Solución de problemas

- **El subcontenedor "Aetherial RX EQ" no es visible** — El applet permanece oculto hasta que la etapa de EQ de RX esté habilitada. Habilítela desde el widget CHAIN o desde el editor flotante. Consulte [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).
- **La superposición del analizador en vivo no muestra actividad** — No hay audio pasando por la ruta de RX. Sintonice una señal o enrute audio por la cadena de RX de alguna otra manera.
- **La respuesta de EQ sumada aparece plana** — No hay bandas configuradas, todas las bandas están omitidas o todas están configuradas en una ganancia de 0 dB. Abra el editor para inspeccionar la configuración de las bandas. Consulte [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).

## Relacionado

- [Descripción general de Aetherial Parametric EQ (TX / RX)](overview.md)
- [Inspeccionar la curva de EQ de TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Verificar que la curva sumada coincide con el objetivo deseado](verify-the-summed-curve-matches-your-mental-target.md)
