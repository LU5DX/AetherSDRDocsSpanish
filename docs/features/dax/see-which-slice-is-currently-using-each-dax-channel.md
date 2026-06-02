# Ver qué receptor virtual utiliza cada canal DAX

El applet de audio DAX muestra un indicador de asignación de receptor virtual junto a cada canal DAX para que pueda confirmar de un vistazo qué receptor está enrutado a dónde, sin salir de la ventana principal.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo de radio. Los indicadores de asignación de receptor virtual requieren una conexión activa con el equipo.
- Al menos un receptor virtual debe tener asignado un canal DAX. Si no hay ningún receptor asignado, todos los indicadores mostrarán `—`.
- A partir de AetherSDR v26.5.2.1, las letras de los receptores virtuales se muestran con formato de texto enriquecido para mejorar la visibilidad.

## Pasos

1. Haga clic en el botón **DAX** de la barra lateral derecha para abrir el applet de audio DAX.
2. Observe la etiqueta de estado a la derecha de cada etiqueta de canal (**DAX 1:**, **DAX 2:**, **DAX 3:**, **DAX 4:**).
3. Lea el indicador de cada canal. Muestra `—` (ningún receptor asignado) o `Slice A` hasta `Slice H` (la letra del receptor enrutado actualmente a ese canal). En v26.5.2.1, la letra del receptor puede mostrarse con formato de texto enriquecido para mejorar la legibilidad.
4. Para ver qué receptor está manejando el flujo de TX de DAX, lea la etiqueta de estado en la fila **TX:**. Sigue el mismo formato: `—` o `Slice A` hasta `Slice H`.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| **DAX Enable** | Botón de alternancia | Off | — | `AutoStartDAX` | Inicia el puente de audio DAX; emite `daxToggled`. |
| **DAX 1 gain+meter** | Medidor/deslizador | 0.5 | 0.0–1.0 | `DaxRxGain1` | Arrastre para ajustar la ganancia de RX en el canal DAX 1. |
| **DAX 2 gain+meter** | Medidor/deslizador | 0.5 | 0.0–1.0 | `DaxRxGain2` | Arrastre para ajustar la ganancia de RX en el canal DAX 2. |
| **DAX 3 gain+meter** | Medidor/deslizador | 0.5 | 0.0–1.0 | `DaxRxGain3` | Arrastre para ajustar la ganancia de RX en el canal DAX 3. |
| **DAX 4 gain+meter** | Medidor/deslizador | 0.5 | 0.0–1.0 | `DaxRxGain4` | Arrastre para ajustar la ganancia de RX en el canal DAX 4. |
| **TX gain+meter** | Medidor/deslizador | 0.5 | 0.0–1.0 | `DaxTxGain` | Arrastre para ajustar la ganancia de TX en el flujo de TX de DAX. |

| Indicador | Ubicación | Valores posibles | Configuración persistente |
|---|---|---|---|
| Estado de asignación de receptor (por canal) | A la derecha de las etiquetas **DAX 1:** – **DAX 4:** | `—` o `Slice A` – `Slice H` | Ninguna |
| Estado de asignación de TX | A la derecha de la etiqueta **TX:** | `—` o `Slice A` – `Slice H` | Ninguna |

Estos indicadores son de solo lectura. Se actualizan automáticamente cuando cambia la asignación del canal DAX de un receptor virtual. La asignación de receptor a canal se configura en el propio receptor, no en este applet.

## Consejos

- Los indicadores se actualizan en tiempo real. Si cambia la asignación del canal DAX de un receptor en el equipo de radio o en otra parte de la interfaz, el applet refleja el cambio inmediatamente, sin necesidad de actualización manual.
- Un canal que muestra `—` significa que ningún receptor está asignado actualmente a él; el audio no fluirá por ese canal.
- A partir de v26.5.2.1, las letras de los receptores virtuales en los indicadores de estado pueden usar formato de texto enriquecido. Esto es un cambio interno; no necesita ajustar ninguna configuración para ver los indicadores correctamente.
- El applet de audio DAX utiliza el estilo del tema (clase `applet/dax`). Si personaliza su tema de aplicación, la apariencia del applet puede variar para coincidir con el resto de la interfaz.

## Relacionados

- [Información general del audio DAX](overview.md)
- [Habilitar DAX para enrutar audio de receptor virtual a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identificar qué receptor virtual es el de TX](identify-which-slice-is-the-tx-slice.md)
- [Configurar la ganancia de RX de DAX por canal](set-dax-rx-gain-per-channel.md)
