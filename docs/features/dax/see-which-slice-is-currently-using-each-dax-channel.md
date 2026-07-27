# Applet de audio DAX

El applet de audio DAX muestra medidores RX por canal y controles deslizantes de ganancia para DAX 1-4, además de un medidor TX único, con un interruptor maestro de habilitación que persiste como `AutoStartDAX`. También muestra indicadores de asignación de slices para que pueda confirmar de un vistazo qué slice está enrutado a dónde sin salir de la ventana principal.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. Los indicadores de asignación de slices requieren una conexión activa al equipo.
- Al menos un slice debe tener asignado un canal DAX. Si no hay slices asignados, todos los indicadores muestran `—`.
- AetherSDR v26.5.2.1 o posterior muestra las letras de los slices con formato de texto enriquecido para mejorar la visibilidad.

## Comportamiento específico por plataforma

### Windows
En Windows, AetherSDR no incluye un puente de audio DAX integrado. El botón de habilitación DAX, los medidores por canal, los controles deslizantes de ganancia y los indicadores de asignación de slices no son funcionales porque el controlador de audio en modo kernel necesario solo se incluye en macOS y Linux. En su lugar, el applet solo muestra el aviso:

> No hay controlador DAX integrado en Windows. Use TCI o SmartSDR DAX.

Para configurar DAX en Windows, use los controladores SmartSDR DAX de FlexRadio. Para obtener orientación, consulte **Help > Configuring Data Modes**.

### macOS y Linux
En macOS y Linux, el applet de audio DAX completo está disponible. En v0.9.7 (Linux), la latencia RX de DAX se reduce de aproximadamente 400 ms a aproximadamente 200 ms mediante una ruta de origen nativa `pw_stream` de PipeWire, reemplazando el cliente PulseAudio anterior.

## Pasos

1. Haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para abrir el applet de audio DAX.
2. En macOS o Linux, para habilitar el enrutamiento de audio DAX:
   - Haga clic en **DAX Enable**. El texto del botón cambia de "Disabled" a "Enabled".
   - AetherSDR guarda la configuración como `AutoStartDAX` en la configuración de la aplicación. El puente de audio DAX se inicia y emite `daxToggled`.
3. Observe la etiqueta de estado a la derecha de cada etiqueta de canal (**DAX 1:**, **DAX 2:**, **DAX 3:**, **DAX 4:**).
4. Lea el indicador de cada canal. Muestra `—` (sin slice asignado) o `Slice A` a `Slice H` (la letra del slice actualmente enrutado a ese canal). En v26.5.2.1, la letra del slice puede mostrarse con formato de texto enriquecido para una mejor legibilidad.
5. Para ver qué slice está impulsando el flujo TX de DAX, lea la etiqueta de estado en la fila **TX:**. Sigue el mismo formato: `—` o `Slice A` a `Slice H`.
6. Para ajustar la ganancia RX en un canal DAX, arrastre el medidor/control deslizante de ese canal. El valor de ganancia persiste en la configuración de la aplicación (`DaxRxGain1` a `DaxRxGain4`).
7. Para ajustar la ganancia TX en el flujo TX de DAX, arrastre el control deslizante **TX gain+meter**. El valor de ganancia persiste como `DaxTxGain`.
8. Para deshabilitar el enrutamiento de audio DAX, haga clic en **DAX Enable** nuevamente. El texto del botón cambia de "Enabled" de vuelta a "Disabled".

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| **DAX Enable** | Botón de alternancia | Desactivado | — | `AutoStartDAX` | Inicia o detiene el puente de audio DAX. El texto del botón muestra "Enabled" o "Disabled" reflejando el estado actual. No funcional en Windows. |
| **DAX 1 gain+meter** | Medidor/control deslizante | 0.5 | 0.0–1.0 | `DaxRxGain1` | Arrástrelo para ajustar la ganancia RX en el canal DAX 1. |
| **DAX 2 gain+meter** | Medidor/control deslizante | 0.5 | 0.0–1.0 | `DaxRxGain2` | Arrástrelo para ajustar la ganancia RX en el canal DAX 2. |
| **DAX 3 gain+meter** | Medidor/control deslizante | 0.5 | 0.0–1.0 | `DaxRxGain3` | Arrástrelo para ajustar la ganancia RX en el canal DAX 3. |
| **DAX 4 gain+meter** | Medidor/control deslizante | 0.5 | 0.0–1.0 | `DaxRxGain4` | Arrástrelo para ajustar la ganancia RX en el canal DAX 4. |
| **TX gain+meter** | Medidor/control deslizante | 0.5 | 0.0–1.0 | `DaxTxGain` | Arrástrelo para ajustar la ganancia TX en el flujo TX de DAX. |

| Indicador | Ubicación | Valores posibles | Configuración persistente |
|---|---|---|---|
| Estado de asignación de slice (por canal) | A la derecha de las etiquetas **DAX 1:** – **DAX 4:** | `—` o `Slice A`–`Slice H` | Ninguna |
| Estado de asignación TX | A la derecha de la etiqueta **TX:** | `—` o `Slice A`–`Slice H` | Ninguna |

Estos indicadores son de solo lectura. Se actualizan automáticamente cuando cambia la asignación del canal DAX de un slice. La asignación slice a canal se configura en el propio slice, no en este applet.

## Consejos

- Los indicadores se actualizan en tiempo real. Si cambia la asignación del canal DAX de un slice en el equipo o en otra parte de la interfaz, el applet refleja el cambio inmediatamente sin necesidad de actualización manual.
- Un canal que muestra `—` significa que ningún slice está asignado actualmente a él; el audio no fluirá en ese canal.
- A partir de v26.5.2.1, las letras de los slice en los indicadores de estado pueden usar formato de texto enriquecido. Este es un cambio interno; no necesita ajustar ninguna configuración para ver los indicadores correctamente.
- El applet de audio DAX usa el estilo del tema (clase `applet/dax`). Si personaliza el tema de su aplicación, la apariencia del applet puede variar para coincidir con el resto de la interfaz.
- Se han agregado etiquetas de accesibilidad: el botón de habilitación DAX está etiquetado como "DAX enable" con la descripción "Enable or disable DAX digital audio routing", y los controles deslizantes de ganancia RX están etiquetados como "DAX RX 1 gain" a "DAX RX 4 gain" y el control deslizante de ganancia TX como "DAX TX gain" para mejorar la compatibilidad con software de lectura de pantalla.

## Relacionados

- [Descripción general de audio DAX](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identificar qué slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Establecer ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
