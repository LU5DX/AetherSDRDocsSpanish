# Verificar que la curva sumada coincide con el objetivo previsto

Utilice el área de curva del applet "Aetherial TX EQ" o "Aetherial RX EQ" para confirmar que la respuesta combinada de todas las bandas habilitadas tiene la forma deseada antes de transmitir o escuchar.

## Antes de comenzar

- La etapa de EQ correspondiente debe estar habilitada. Si el applet no es visible, habilite la etapa de EQ mediante el widget CHAIN o abra primero el editor flotante.
- Al menos una banda debe estar configurada para que la curva muestre una respuesta no plana. Una línea plana indica que no hay bandas activas o que todas están en bypass.

## Pasos

1. Localice el sub-contenedor "Aetherial TX EQ" o "Aetherial RX EQ" dentro del contenedor padre Aetherial Audio (TXDSP) en el panel de applets.
2. Observe el área de curva — la pantalla de 110 px que ocupa el tile. La línea blanca (o resaltada) trazada sobre la cuadrícula de frecuencias es la respuesta de EQ sumada: el efecto acumulado de todas las bandas habilitadas para esa ruta.
3. Compare la forma de la respuesta sumada con su objetivo:
   - Un realce en una frecuencia determinada aparece como un pico hacia arriba.
   - Un corte aparece como una caída hacia abajo.
   - El filtrado paso-alto y paso-bajo aparece como una atenuación en los bordes.
4. Si el analizador FFT en tiempo real está activo, una segunda traza muestra el espectro en tiempo real del audio que pasa por esa ruta. Utilícelo para verificar que la curva está afectando al audio donde se espera.
5. Si la forma no coincide con su objetivo, haga doble clic en la etapa de EQ en el widget CHAIN de la misma ruta (TX o RX) para abrir el editor flotante titulado "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX" y ajuste las bandas desde allí. La curva del applet se actualiza conforme realiza cambios.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Área de analizador / curva | Indicador (solo lectura) | Muestra la respuesta de EQ sumada para la ruta de este tile (TX o RX) y una superposición del analizador FFT en tiempo real del audio que pasa por esa ruta. No es editable desde el applet; para editar se requiere el editor flotante. | — |
| Respuesta de EQ sumada | Estado de indicador | Muestra la respuesta en frecuencia acumulada de todas las bandas habilitadas. Aparece plana cuando no hay bandas activas o el modelado es cero; aparece con forma cuando una o más bandas alteran la respuesta. | `ClientEqTxBands` (TX) / `ClientEqRxBands` (RX) |
| Superposición del analizador en tiempo real | Estado de indicador | FFT en tiempo real del audio que pasa por esta ruta. Funciona mientras el applet es visible; permanece inactivo cuando no hay audio fluyendo. | — |

## Consejos

- El applet es de solo lectura. No es posible arrastrar bandas ni cambiar parámetros desde él. Toda edición se realiza en el editor flotante.
- Los tiles de TX y RX son independientes. Revisar uno no proporciona información sobre la otra ruta.
- Si la curva parece correcta en el applet pero el audio no suena bien, confirme que la etapa de EQ no está en bypass. Una etapa en bypass deja pasar el audio sin cambios, independientemente de lo que muestre la curva.

## Solución de problemas

- **El área de curva está plana aunque las bandas estén configuradas** — La etapa de EQ puede estar deshabilitada o en bypass. Revise el widget CHAIN y confirme que `ClientEqTxEnabled` o `ClientEqRxEnabled` está activo para la ruta correspondiente.
- **El applet no es visible** — La etapa de EQ aún no ha sido habilitada. Habilítela mediante el widget CHAIN o abra el editor flotante, lo cual también hace aparecer el tile.
- **La superposición del analizador en tiempo real no se mueve** — No hay audio pasando por esa ruta o la etapa de EQ está deshabilitada. Transmita audio (ruta TX) o reciba una señal (ruta RX) y confirme que la etapa está habilitada.

## Relacionados

- [Descripción general de Aetherial Parametric EQ (TX / RX)](overview.md)
- [Abrir el editor sin marco para agregar, quitar o ajustar bandas en ambas rutas](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Inspeccionar la curva de EQ TX y el espectro en tiempo real](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva de EQ RX y el espectro en tiempo real](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Poner en bypass la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
