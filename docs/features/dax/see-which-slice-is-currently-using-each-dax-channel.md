# Ver qué slice usa cada canal DAX

El applet DAX Audio muestra un indicador de asignación de slice junto a cada canal DAX, para que pueda confirmar de un vistazo qué slice está enrutado a dónde sin salir de la ventana principal.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. Los indicadores de asignación de slice requieren una conexión activa con la radio.
- Al menos un slice debe tener asignado un canal DAX. Si no hay slices asignados, todos los indicadores muestran `—`.
- AetherSDR v26.5.2.1 o posterior muestra las letras de los slices con formato de texto enriquecido para mejorar la visibilidad.

## Pasos

1. Haga clic en el botón **DAX** de la barra lateral derecha para abrir el applet DAX Audio.
2. Observe la etiqueta de estado a la derecha de cada etiqueta de canal (**DAX 1:**, **DAX 2:**, **DAX 3:**, **DAX 4:**).
3. Lea el indicador de cada canal. Muestra `—` (ningún slice asignado) o `Slice A` hasta `Slice H` (la letra del slice enrutado actualmente a ese canal). En v26.5.2.1, la letra del slice puede mostrarse con formato de texto enriquecido para mejorar la legibilidad.
4. Para ver qué slice está manejando el flujo DAX de TX, lea la etiqueta de estado en la fila **TX:**. Sigue el mismo formato: `—` o `Slice A` hasta `Slice H`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| **DAX Enable** | Botón de alternancia | Off | — | `AutoStartDAX` | Inicia el puente de audio DAX; emite `daxToggled`. |
| **DAX 1 gain+meter** | Medidor/deslizador | 0.5 | 0.0–1.0 | `DaxRxGain1` | Arrastre para ajustar la ganancia de RX en el canal DAX 1. |
| **DAX 2 gain+meter** | Medidor/deslizador | 0.5 | 0.0–1.0 | `DaxRxGain2` | Arrastre para ajustar la ganancia de RX en el canal DAX 2. |
| **DAX 3 gain+meter** | Medidor/deslizador | 0.5 | 0.0–1.0 | `DaxRxGain3` | Arrastre para ajustar la ganancia de RX en el canal DAX 3. |
| **DAX 4 gain+meter** | Medidor/deslizador | 0.5 | 0.0–1.0 | `DaxRxGain4` | Arrastre para ajustar la ganancia de RX en el canal DAX 4. |
| **TX gain+meter** | Medidor/deslizador | 0.5 | 0.0–1.0 | `DaxTxGain` | Arrastre para ajustar la ganancia de TX en el flujo DAX de TX. |

| Indicador | Ubicación | Valores posibles | Configuración persistente |
|---|---|---|---|
| Estado de asignación de slice (por canal) | A la derecha de las etiquetas **DAX 1:** – **DAX 4:** | `—` o `Slice A`–`Slice H` | Ninguna |
| Estado de asignación de TX | A la derecha de la etiqueta **TX:** | `—` o `Slice A`–`Slice H` | Ninguna |

Estos indicadores son de solo lectura. Se actualizan automáticamente cuando cambia la asignación del canal DAX de un slice. La asignación de slice a canal se configura en el propio slice, no en este applet.

## Consejos

- Los indicadores se actualizan en tiempo real. Si cambia la asignación del canal DAX de un slice en la radio o en otra parte de la interfaz, el applet refleja el cambio de inmediato sin necesidad de actualización manual.
- Un canal que muestra `—` significa que ningún slice está asignado actualmente a ese canal; el audio no fluirá por ese canal.
- A partir de v26.5.2.1, las letras de los slices en los indicadores de estado pueden usar formato de texto enriquecido. Esto es un cambio interno; no necesita ajustar ninguna configuración para ver los indicadores correctamente.
- El applet DAX Audio utiliza el estilo del tema (clase `applet/dax`). Si personaliza el tema de su aplicación, la apariencia del applet puede variar para coincidir con el resto de la interfaz.
- Se han añadido etiquetas de accesibilidad para los deslizadores de ganancia de RX (como "DAX RX 1 gain", "DAX RX 2 gain", "DAX RX 3 gain", "DAX RX 4 gain") y el deslizador de ganancia de TX (como "DAX TX gain") para mejorar la compatibilidad con lectores de pantalla.

## Relacionado

- [DAX Audio overview](overview.md)
- [Enable DAX to route slice audio to WSJT-X / FLDigi / other digital software](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identify which slice is the TX slice](identify-which-slice-is-the-tx-slice.md)
- [Set DAX RX gain per channel](set-dax-rx-gain-per-channel.md)
