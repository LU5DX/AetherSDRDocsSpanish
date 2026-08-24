# Comprender el momento de restauración de la asignación de canales DAX a slices tras la conexión o un cambio de banda en un band stack

Esta página explica cuándo AetherSDR restaura sus asignaciones de canal DAX a slice después de conectarse a una radio o de cambiar de banda dentro de un band stack, para que sepa qué esperar y pueda verificar que el enrutamiento sea correcto.

## Antes de comenzar

- DAX debe estar habilitado (el botón Enable en el applet DAX Audio muestra "Enabled")
- Usted está conectado a una radio FLEX-8600

## Pasos

1. Abra el applet DAX Audio haciendo clic en el botón de bandeja **DAX** en la barra lateral derecha.
2. Conéctese a su radio o cambie a una entrada diferente del band stack.
3. Observe las etiquetas de estado por canal (DAX 1 hasta DAX 8) y la etiqueta de estado TX.
4. Inmediatamente después de la conexión o el cambio de banda, estas etiquetas pueden mostrar "—" por un breve momento antes de poblarse con letras de slice como "Slice A" o "Slice B".
5. Espere a que las etiquetas se estabilicen. La restauración ocurre a medida que la radio propaga el estado de los slices a AetherSDR; no es instantánea.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de ajuste persistente |
|---|---|---|---|
| Botón **DAX Enable** | desactivado | activado/desactivado | `AutoStartDAX` |
| **Ganancia+medidor DAX 1–8** | 0.5 | 0.0–1.0 | `DaxRxGain1` … `DaxRxGain8` |
| **Ganancia+medidor TX** | 0.5 | 0.0–1.0 | `DaxTxGain` |
| **Estado de asignación DAX 1–8** | "—" | "—" o "Slice A"…"Slice H" | `DaxChannel_Slice{letter}` |
| **Estado de asignación TX** | "—" | "—" o "Slice A"…"Slice H" | (reportado por la radio) |

## Consejos

- Las etiquetas de estado por canal se actualizan cada vez que cambia el canal DAX de un slice. Tras un cambio de banda en el band stack, los slices pueden recrearse, por lo que las asignaciones se vuelven a propagar y las etiquetas se restablecen brevemente a "—" antes de repoblarse.
- Si tiene muchos slices, déle a la radio uno o dos segundos para que envíe todo el estado de los slices antes de confiar en las asignaciones mostradas para enrutar audio a software digital.

## Solución de problemas

- **Las etiquetas de estado de canal DAX permanecen en "—" después de la conexión** — Es posible que DAX aún no esté habilitado. Haga clic en **Enable** en el applet DAX Audio; las asignaciones solo se muestran mientras el puente DAX esté en funcionamiento.
- **Las asignaciones aparecen pero el audio está en el canal equivocado** — Verifique que esté mirando la letra de slice correcta en la etiqueta de estado y confirme que el enrutamiento del canal DAX en su software digital coincida con lo que muestra AetherSDR.

## Relacionado

- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](../../features/dax/enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ver qué slice está usando actualmente cada canal DAX](../../features/dax/see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar qué slice es el slice TX](../../features/dax/identify-which-slice-is-the-tx-slice.md)
