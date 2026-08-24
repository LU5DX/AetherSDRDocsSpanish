# Applet de audio DAX

El applet de audio DAX muestra medidores RX por canal y deslizadores de ganancia para DAX 1-8, además de un medidor de TX único, con un interruptor maestro de habilitación que se guarda como `AutoStartDAX`. También muestra indicadores de asignación de slice para que pueda confirmar de un vistazo qué slice está enrutado a dónde sin salir de la ventana principal.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los indicadores de asignación de slice requieren una conexión activa con la radio.
- Al menos un slice debe tener un canal DAX asignado. Si no hay slices asignados, todos los indicadores muestran `—`.
- AetherSDR v26.5.2.1 o posterior muestra las letras de slice con formato de texto enriquecido para mejorar la visibilidad.
- Las filas que superan la capacidad de slices de la radio conectada se ocultan. Una 6300/6400 (2 slices) muestra 2 filas RX DAX; una 6600/8600 (4 slices) muestra 4; una radio con capacidad de 8 slices muestra las 8.
- Los niveles de los medidores RX se suavizan exponencialmente (ataque rápido, caída lenta).

## Comportamiento específico por plataforma

### Windows
En Windows, AetherSDR no incluye un puente de audio DAX integrado. El botón de habilitación DAX, los medidores por canal, los deslizadores de ganancia y los indicadores de asignación de slice no son funcionales porque el controlador de audio en modo kernel necesario solo se incluye en macOS y Linux. En su lugar, el applet muestra únicamente el aviso:

> No hay controlador DAX integrado en Windows. Use TCI o SmartSDR DAX.

Para configurar DAX en Windows, use los controladores SmartSDR DAX de FlexRadio. Para obtener orientación, consulte **Help > Configuring Data Modes**.

### macOS y Linux
En macOS y Linux, el applet de audio DAX completo está disponible. En la v0.9.7 (Linux), la latencia RX de DAX se reduce de aproximadamente 400 ms a aproximadamente 200 ms mediante una ruta de fuente nativa `pw_stream` de PipeWire, que reemplaza al cliente de PulseAudio anterior.

## Pasos

1. Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para abrir el applet de audio DAX.
2. En macOS o Linux, para habilitar el enrutamiento de audio DAX:
   - Haga clic en **DAX Enable**. El texto del botón cambia de "Disabled" a "Enabled".
   - AetherSDR guarda la configuración como `AutoStartDAX` en los ajustes de la aplicación. El puente de audio DAX se inicia y emite `daxToggled`.
3. Observe la etiqueta de estado a la derecha de cada etiqueta de canal (**DAX 1:**, **DAX 2:**, **DAX 3:**, **DAX 4:**, **DAX 5:**, **DAX 6:**, **DAX 7:**, **DAX 8:**).
4. Lea el indicador de cada canal. Este muestra `—` (sin slice asignado) o `Slice A` a `Slice H` (la letra del slice actualmente enrutado a ese canal). En la v26.5.2.1, la letra del slice puede mostrarse con formato de texto enriquecido para una mejor legibilidad.
5. Para ver qué slice impulsa el flujo TX de DAX, lea la etiqueta de estado en la fila **TX:**. Sigue el mismo formato: `—` o `Slice A` a `Slice H`.
6. Para ajustar la ganancia RX en un canal DAX, arrastre el medidor/deslizador de ese canal. El valor de ganancia se guarda en los ajustes de la aplicación (`DaxRxGain1` a `DaxRxGain8`).
7. Para ajustar la ganancia TX en el flujo TX de DAX, arrastre el deslizador **TX gain+meter**. El valor de ganancia se guarda como `DaxTxGain`.
8. Para deshabilitar el enrutamiento de audio DAX, haga clic en **DAX Enable** nuevamente. El texto del botón cambia de "Enabled" de vuelta a "Disabled".

## Qué hace cada control

| Control                               | Tipo                                                                                                                     | Predeterminado                                                                                                                           |
|---------------------------------------|--------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| **DAX Enable**                        | Botón de alternancia                                                                                                     | Apagado                                                                                                                              |
| **DAX 1 gain+meter**                  | Medidor/deslizador                                                                                                       | 0.5                                                                                                                                  |
| **DAX 2 gain+meter**                  | Medidor/deslizador                                                                                                       | 0.5                                                                                                                                  |
| **DAX 3 gain+meter**                  | Medidor/deslizador                                                                                                       | 0.5                                                                                                                                  |
| **DAX 4 gain+meter**                  | Medidor/deslizador                                                                                                       | 0.5                                                                                                                                  |
| **DAX 5 gain+meter**                  | Medidor/deslizador                                                                                                       | 0.5                                                                                                                                  |
| **DAX 6 gain+meter**                  | Medidor/deslizador                                                                                                       | 0.5                                                                                                                                  |
| **DAX 7 gain+meter**                  | Medidor/deslizador                                                                                                       | 0.5                                                                                                                                  |
| **DAX 8 gain+meter**                  | Medidor/deslizador                                                                                                       | 0.5                                                                                                                                  |
| **TX gain+meter**                     | Medidor/deslizador                                                                                                       | 0.5                                                                                                                                  |
| Indicador                             | Ubicación                                                                                                                | Valores posibles                                                                                                                      |
| ---                                   | ---                                                                                                                      | ---                                                                                                                                  |
| Estado de asignación de slice (por canal) | Muestra qué slice está actualmente enrutado a cada canal DAX.                                                               | Las letras de slice se muestran como identificadores de texto enriquecido.                                                                                       |
| Estado de asignación TX              | A la derecha de la etiqueta **TX:**                                                                                                   | `—` o `Slice A`–`Slice H`                                                                                                           |
| DAX 5 gain+meter                      | Medidor/deslizador combinado; arrastre para establecer la ganancia RX en el canal DAX 5.                                                             | Visible solo cuando la radio conectada admite al menos 5 slices.                                                                    |
| DAX 6 gain+meter                      | Medidor/deslizador combinado; arrastre para establecer la ganancia RX en el canal DAX 6.                                                             | Visible solo cuando la radio conectada admite al menos 6 slices.                                                                    |
| DAX 7 gain+meter                      | Medidor/deslizador combinado; arrastre para establecer la ganancia RX en el canal DAX 7.                                                             | Visible solo cuando la radio conectada admite al menos 7 slices.                                                                    |
| DAX 8 gain+meter                      | Medidor/deslizador combinado; arrastre para establecer la ganancia RX en el canal DAX 8.                                                             | Visible solo en una radio con capacidad de 8 slices.                                                                                            |
| Nota de Windows                       | En las compilaciones de Windows, el applet muestra únicamente la nota 'No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX.' (#4112). | Windows no tiene puente DAX integrado (sin controlador de audio en modo kernel); todos los demás controles se omiten y sus definidores están protegidos contra valores nulos. |

Estos indicadores son de solo lectura. Se actualizan automáticamente cuando cambia la asignación de canal DAX de un slice. La asignación de slice a canal se configura en el propio slice, no en este applet.

## Consejos

- Los indicadores se actualizan en tiempo real. Si cambia la asignación de canal DAX de un slice en la radio o en otra parte de la interfaz, el applet refleja el cambio inmediatamente sin necesidad de actualización manual.
- Un canal que muestra `—` significa que ningún slice está asignado actualmente a él; el audio no fluirá por ese canal.
- A partir de la v26.5.2.1, las letras de slice en los indicadores de estado pueden usar formato de texto enriquecido. Este es un cambio interno; no es necesario ajustar ninguna configuración para ver los indicadores correctamente.
- El applet de audio DAX utiliza el estilo del tema (clase `applet/dax`). Si personaliza el tema de la aplicación, la apariencia del applet puede variar para coincidir con el resto de la interfaz.
- Se han añadido etiquetas de accesibilidad: el botón **DAX Enable** está etiquetado como "DAX enable" con la descripción "Enable or disable DAX digital audio routing", y los deslizadores de ganancia RX están etiquetados como "DAX RX 1 gain" a "DAX RX 4 gain" y el deslizador de ganancia TX como "DAX TX gain" para mejorar la compatibilidad con software de lectura de pantalla.

## Relacionados

- [Descripción general del audio DAX](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Identificar qué slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Establecer la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
