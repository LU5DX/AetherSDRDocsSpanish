# Solución de problemas del Slice

El diálogo Slice Troubleshooting captura una instantánea de cada slice, panadapter, transverter, canal DAX, dispositivo de audio, estado del DSP del cliente y enlace de dispositivo de control (MIDI) en la radio conectada y busca posibles problemas de configuración. Úselo para diagnosticar problemas de audio, silencio, antena, transverter y enrutamiento de audio remoto, o para recopilar datos de diagnóstico antes de contactar al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo no está disponible sin una conexión activa a la radio.

## Cómo funciona

Abra el diálogo con `Help > Slice Troubleshooting...`. Cuando se abre el diálogo, AetherSDR lee el estado actual de la radio en una instantánea. La instantánea cubre slices, panadapters, transverters, canales DAX, dispositivos de audio, estado del DSP del cliente, enlaces de dispositivos de control (MIDI) y configuración de bandas de TX. El diálogo verifica esa instantánea en busca de un conjunto de patrones de problemas conocidos — audio faltante, silencio atrapado, antena faltante, problemas de validez de transverter, problemas de enrutamiento de audio, anomalías del estado del DSP y conflictos de propiedad multicliente — y presenta los resultados en dos pestañas.

**Pestaña Issue Summary** muestra una lista de puntos en lenguaje común de los problemas detectados. Si nada está mal, la lista está vacía. Esta es la forma más rápida de ver si AetherSDR ha identificado un problema de configuración.

La sección Issue Summary ahora incluye diagnósticos de audio remoto RX. Para la sección de audio a nivel de radio, el resumen informa el ID de flujo de audio remoto RX, si se espera un flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si el flujo es propiedad del cliente actual, la configuración de compresión en uso y cualquier nota de enrutamiento. Para la sección de enrutamiento de audio por slice, el resumen informa el ID de flujo de audio remoto RX junto con los indicadores esperado, creación pendiente, eliminación solicitada, estado visto y propiedad nuestra.

**Pestaña JSON** muestra la instantánea completa como JSON estructurado (versión de esquema 3). Esta vista contiene cada campo que AetherSDR recopiló: estado del slice, parámetros de panadapter, frecuencias RF/IF de transverter, compensaciones, indicadores de validez, asignaciones de canales DAX, dispositivos de audio, estado del DSP del cliente, enlaces de dispositivos de control, configuración de bandas de TX y estado remoto de audio RX. El personal de soporte y los usuarios avanzados pueden inspeccionar los valores de campos individuales aquí.

La instantánea refleja el estado de la radio en el momento en que se tomó. Si cambia la configuración del slice mientras el diálogo está abierto, haga clic en **Refresh Snapshot** para releer el estado actual antes de sacar conclusiones o compartir datos.

## Qué hace cada control

| Control          | Tipo      | Comportamiento                                                                                        |
|------------------|-----------|-------------------------------------------------------------------------------------------------|
| Issue Summary    | Pestaña       | Muestra una lista de puntos en lenguaje común de los problemas detectados, incluido enrutamiento de audio, estado del DSP y dispositivo de control (MIDI), y propiedad multicliente. |
| JSON             | Pestaña       | Muestra la instantánea JSON completa (versión de esquema 3) de slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, configuración de bandas de TX y estado remoto de audio RX. |
| Refresh Snapshot | Botón    | Relees el estado del slice en la instantánea. Úselo después de cambiar la configuración de la radio.            |
| Copy Summary     | Botón    | Copia el texto del resumen de problemas al portapapeles.                                                 |
| Copy JSON        | Botón    | Copia la instantánea JSON completa al portapapeles.                                                |
| Export JSON...   | Botón    | Abre un diálogo de archivo para guardar la instantánea JSON en un archivo.                                        |
| Close            | Botón    | Cierra el diálogo.                                                              |
| Etiqueta de estado     | Indicador | Muestra el resultado de la acción de copia o exportación más reciente (por ejemplo, "Copied to clipboard"). |

## Sugerencias

- Tome una nueva instantánea con **Refresh Snapshot** después de cada cambio de configuración. El diálogo no se actualiza automáticamente mientras está abierto.
- Use **Copy Summary** para pegar una lista concisa de problemas en una publicación de un foro de soporte o correo electrónico. Use **Copy JSON** o **Export JSON...** al adjuntar datos de diagnóstico completos a un informe de errores.
- Si está solucionando problemas de audio remoto, verifique tanto la sección de audio remoto RX a nivel de radio como la sección de ruta de flujo de radio por slice en Issue Summary. Ambas secciones deben mostrar ID de flujo coherentes e indicadores de propiedad para que el audio se enrute correctamente.

## Relacionado

- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje común de posibles problemas de slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de errores](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspeccionar RF/IF, compensación e indicadores de validez de cada transverter para diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
