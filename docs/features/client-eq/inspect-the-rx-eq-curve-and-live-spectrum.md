# Inspeccionar la curva del ecualizador RX y el espectro en vivo

El applet "Aetherial RX EQ" ofrece una vista compacta y siempre visible de la respuesta en frecuencia sumada del ecualizador RX, junto con una superposición de analizador FFT en tiempo real del audio que pasa por la cadena RX. Úselo para monitorear el efecto de sus ajustes de ecualización RX de un vistazo, sin necesidad de abrir el editor completo.

## Antes de comenzar

- El subcontenedor "Aetherial RX EQ" permanece oculto hasta que la etapa RX EQ esté habilitada. Habilítela desde el widget CHAIN o desde el editor flotante antes de esperar que aparezca el applet.
- El applet se encuentra dentro del contenedor principal "Aetherial Audio (TXDSP)" en el panel de applets. Asegúrese de que el panel de applets esté visible (`View > Applet Panel`).

## Pasos

1. En el panel de applets, localice el contenedor principal "Aetherial Audio (TXDSP)".
2. Expándalo y encuentre el subcontenedor "Aetherial RX EQ".
3. Observe el área del analizador / curva: la pantalla de 110 px de alto que muestra la cuadrícula de frecuencias.
4. La curva de respuesta EQ sumada muestra la respuesta en frecuencia acumulada de todas las bandas RX habilitadas. Una línea plana indica que no hay modelado neto; una línea con forma refleja los ajustes de banda activos almacenados en `ClientEqRxBands`.
5. La superposición del analizador en vivo, que se extiende sobre la misma área, muestra el FFT en tiempo real del audio que pasa por la cadena RX. Cuando hay audio presente, la superposición está activa; cuando no pasa audio, la superposición permanece inactiva.
6. Para inspeccionar con más detalle o editar bandas, haga doble clic en la etapa RX EQ en el widget CHAIN para abrir el editor flotante "Aetherial Parametric EQ — RX".

## Qué hace cada control

| Control | Comportamiento | Valor por defecto | Clave de ajuste |
|---|---|---|---|
| Área del analizador / curva | Muestra la curva de respuesta EQ sumada y la superposición del analizador FFT en tiempo real para la cadena RX. Solo lectura en este applet. | — | — |
| Respuesta EQ sumada | Muestra la respuesta en frecuencia acumulada de todas las bandas RX habilitadas. | plana | `ClientEqRxBands` |
| Superposición del analizador en vivo | FFT en tiempo real del audio que pasa por la cadena RX. | inactiva | — |
| Estado habilitado del RX EQ | Indica si la etapa RX EQ está activa. Se controla desde el widget CHAIN o el editor flotante, no desde este applet. | — | `ClientEqRxEnabled` |

## Consejos

- El área del analizador / curva es de solo lectura en el applet. Para agregar, eliminar o ajustar bandas, abra el editor flotante haciendo doble clic en la etapa RX EQ en el widget CHAIN.
- Si desea flotar, extraer o ocultar el subcontenedor "Aetherial RX EQ", haga clic derecho en su barra de título para acceder a esas opciones.

## Resolución de problemas

- **El subcontenedor "Aetherial RX EQ" no es visible** — El applet permanece oculto hasta que la etapa RX EQ esté habilitada. Habilite la etapa desde el widget CHAIN o el editor flotante. Verifique que `ClientEqRxEnabled` esté configurado.
- **La superposición del analizador en vivo aparece inactiva incluso durante la recepción** — El audio debe estar pasando por la cadena RX para que el FFT funcione. Confirme que la radio esté conectada y que el enrutamiento de audio esté activo.

## Relacionado

- [Descripción general del Aetherial Parametric EQ (TX / RX)](overview.md)
- [Inspeccionar la curva del ecualizador TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Omitir la etapa de ecualización desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
