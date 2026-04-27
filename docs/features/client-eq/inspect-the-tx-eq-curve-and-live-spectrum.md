# Inspeccionar la curva de EQ de TX y el espectro en vivo

El applet "Aetherial TX EQ" muestra la curva de respuesta de EQ sumada y una superposición del analizador FFT en tiempo real para la ruta de audio de TX. Use esta vista para monitorear cómo se está moldeando su señal de transmisión sin necesidad de abrir el editor completo.

## Antes de comenzar

- El sub-contenedor "Aetherial TX EQ" permanece oculto hasta que la etapa TX EQ esté habilitada. Habilítela desde el widget CHAIN o desde el editor flotante ("Aetherial Parametric EQ — TX") antes de esperar que el applet aparezca.
- El applet se encuentra dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets. Si el panel de applets no está visible, verifique `View > Applet Panel`.

## Pasos

1. Localice el contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Encuentre el sub-contenedor "Aetherial TX EQ" dentro de él.
3. Observe el área del analizador / curva — la pantalla de 110 px de altura que muestra la cuadrícula, la curva de respuesta de EQ sumada y la superposición del analizador FFT en tiempo real para la ruta de TX.
4. Observe la línea de respuesta de EQ sumada, que refleja la respuesta en frecuencia acumulada de todas las bandas de TX habilitadas.
5. Observe la superposición del analizador en tiempo real, que muestra el FFT en tiempo real del audio que pasa por la ruta de TX. La superposición está inactiva cuando no hay audio presente y en funcionamiento cuando el audio fluye por la ruta de TX.

## Qué hace cada control

| Control | Descripción | Editable en el applet |
|---|---|---|
| Área del analizador / curva | Muestra la cuadrícula, la curva de respuesta de EQ sumada y la superposición del analizador FFT en tiempo real para la ruta de TX. | No — solo lectura |
| Respuesta de EQ sumada | Muestra la respuesta en frecuencia acumulada de todas las bandas de TX habilitadas. Aparece plana cuando ninguna banda está moldeando la señal. | No |
| Superposición del analizador en vivo | FFT en tiempo real del audio en la ruta de TX. Inactiva cuando no hay audio presente; en funcionamiento cuando el audio fluye. | No |

Para editar bandas se requiere el editor flotante. Consulte [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).

## Consejos

- El applet es solo de visualización. Toda la edición de bandas — agregar, eliminar y ajustar — se realiza en el editor flotante "Aetherial Parametric EQ — TX", que se abre haciendo doble clic en la etapa TX EQ del widget CHAIN.
- Para flotar, extraer u ocultar el sub-contenedor "Aetherial TX EQ", haga clic derecho en su barra de título.

## Solución de problemas

- **El sub-contenedor "Aetherial TX EQ" no está visible** — El applet permanece oculto hasta que la etapa TX EQ esté habilitada. Habilítela desde el widget CHAIN o desde el editor flotante. Consulte [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md).
- **La superposición del analizador en vivo aparece inactiva** — No hay audio pasando por la ruta de TX. Debe haber audio de transmisión presente para que la superposición FFT funcione.

## Relacionados

- [Descripción general de Aetherial Parametric EQ (TX / RX)](overview.md)
- [Inspeccionar la curva de EQ de RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Omitir la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Verificar que la curva sumada coincida con el objetivo deseado](verify-the-summed-curve-matches-your-mental-target.md)
