# Omitir la etapa de EQ en la cadena

El EQ paramétrico del lado del cliente puede eliminarse de la cadena de procesamiento de audio sin borrar la configuración de bandas. Omitir la etapa permite comparar el efecto del EQ (A/B) o deshabilitar temporalmente el procesamiento en una ruta sin modificar la otra. El estado de omisión se guarda por ruta en `ClientEqRxEnabled` y `ClientEqTxEnabled`.

## Antes de comenzar

- El subcontenedor CEQ debe estar visible dentro del contenedor padre PooDoo Audio (TXDSP). Permanece oculto hasta que la etapa de EQ se haya habilitado al menos una vez mediante el widget CHAIN o el editor flotante.
- Decida si desea omitir la ruta RX, la ruta TX o ambas, antes de comenzar.

## Pasos

1. Localice el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP).
2. Encuentre el bloque de la etapa EQ en la cadena.
3. Haga clic una vez en el bloque de la etapa EQ para activar o desactivar la omisión en esa ruta. Un solo clic habilita o deshabilita la etapa directamente en la cadena.
4. Para omitir la otra ruta, cambie a ella primero — use la pestaña RX o TX en la parte superior del applet CEQ para confirmar qué ruta está activa — y luego haga clic una vez en el bloque de la etapa EQ nuevamente.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Clave persistente | Comportamiento |
|---|---|---|---|---|
| Etapa EQ (widget CHAIN, un clic) | Alternancia | Habilitado | `ClientEqRxEnabled` / `ClientEqTxEnabled` | Omite o reinserta el EQ del cliente para la ruta seleccionada. No borra los datos de banda almacenados en `ClientEqRxBands` ni en `ClientEqTxBands`. |
| RX | Pestaña | Marcado | — | Selecciona la ruta de recepción para mostrarla en el applet CEQ. |
| TX | Pestaña | Sin marcar | — | Selecciona la ruta de transmisión para mostrarla en el applet CEQ. |

## Sugerencias

- Omitir una ruta deja intacta toda la configuración de bandas. Al volver a habilitarla, la curva completa se restaura de inmediato.
- El área del analizador/curva en el applet CEQ continúa mostrando la forma de respuesta del EQ almacenado incluso mientras la etapa está omitida, de modo que puede inspeccionar su curva sin procesarla.

## Solución de problemas

- **El subcontenedor CEQ no está visible** — La etapa de EQ aún no se ha habilitado. Habilítela una vez mediante el widget CHAIN o el editor flotante para que el subcontenedor CEQ aparezca.
- **Hacer clic una vez en la etapa EQ no tiene efecto** — Confirme que está haciendo clic en el bloque correcto del widget CHAIN. Hacer doble clic abre el editor flotante en lugar de activar la omisión.

## Temas relacionados

- [Descripción general del EQ paramétrico (cliente)](overview.md)
- [Abrir el editor flotante para agregar, eliminar o ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md)
- [Alternar entre la vista del EQ de RX y TX](switch-between-viewing-rx-and-tx-eq.md)
