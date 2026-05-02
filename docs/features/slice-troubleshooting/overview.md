# Solución de problemas de slice

El diálogo Slice Troubleshooting captura una instantánea de cada slice (receptor virtual), panadapter (vista panorámica), transverter, canal DAX, dispositivo de audio, estado DSP del cliente y enlaces de dispositivos de control (MIDI) en la radio conectada, y verifica posibles problemas de configuración. Úselo para diagnosticar problemas de audio, silenciamiento, antena, transverter y enrutamiento de audio remoto, o para recopilar datos de diagnóstico antes de contactar al soporte.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo no está disponible sin una conexión de radio activa.

## Cómo funciona

Abra el diálogo con `Help > Slice Troubleshooting...`. Al abrirse, AetherSDR lee el estado actual de la radio en una instantánea. La instantánea abarca slices, panadapters, transverters, canales DAX, dispositivos de audio, estado DSP del cliente, enlaces de dispositivos de control (MIDI) y configuraciones de banda TX. El diálogo verifica esa instantánea en busca de un conjunto de patrones de problemas conocidos — audio faltante, silenciamiento bloqueado, antena faltante, problemas de validez del transverter, problemas de enrutamiento de audio, anomalías en el estado DSP y conflictos de propiedad entre múltiples clientes — y presenta los resultados en dos pestañas.

La pestaña **Issue Summary** muestra una lista con viñetas en lenguaje sencillo de los problemas detectados. Si no hay ningún problema, la lista está vacía. Esta es la forma más rápida de verificar si AetherSDR ha identificado un problema de configuración.

El Issue Summary ahora incluye diagnósticos de RX de audio remoto. Para la sección de audio a nivel de radio, el resumen reporta el ID de flujo de audio RX remoto, si se espera un flujo, si la creación está pendiente, si se ha recibido un mensaje de estado, si el flujo es propiedad del cliente actual, la configuración de compresión en uso y cualquier nota de enrutamiento. Para la sección de enrutamiento de audio por slice, el resumen reporta el ID de flujo de audio RX remoto junto con los indicadores de esperado, creación pendiente, eliminación solicitada, estado recibido y de nuestra propiedad.

La pestaña **JSON** muestra la instantánea completa como JSON estructurado (versión de esquema 3). Esta vista contiene todos los campos recopilados por AetherSDR: estado del slice, parámetros del panadapter, frecuencias RF/IF del transverter, desplazamientos, indicadores de validez, asignaciones de canales DAX, dispositivos de audio, estado DSP del cliente, enlaces de dispositivos de control, configuraciones de banda TX y estado de RX de audio remoto. El personal de soporte y los usuarios avanzados pueden inspeccionar aquí los valores de campos individuales.

La instantánea refleja el estado de la radio en el momento en que fue tomada. Si cambia la configuración del slice mientras el diálogo está abierto, haga clic en **Refresh Snapshot** para volver a leer el estado actual antes de sacar conclusiones o compartir datos.

## Qué hace cada control

| Control          | Tipo      | Comportamiento                                                                                        |
|------------------|-----------|-------------------------------------------------------------------------------------------------|
| Issue Summary    | Pestaña   | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI) y propiedad entre múltiples clientes. |
| JSON             | Pestaña   | Muestra la instantánea JSON completa (versión de esquema 3) de slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, configuraciones de banda TX y estado de RX de audio remoto. |
| Refresh Snapshot | Botón     | Vuelve a leer el estado del slice en la instantánea. Úselo después de cambiar la configuración de la radio. |
| Copy Summary     | Botón     | Copia el texto del resumen de problemas al portapapeles.                                        |
| Copy JSON        | Botón     | Copia la instantánea JSON completa al portapapeles.                                             |
| Export JSON...   | Botón     | Abre un diálogo de archivo para guardar la instantánea JSON en un archivo.                      |
| Close            | Botón     | Cierra el diálogo.                                                                              |
| Status label     | Indicador | Muestra el resultado de la acción de copia o exportación más reciente (por ejemplo, "Copied to clipboard"). |

## Consejos

- Tome una nueva instantánea con **Refresh Snapshot** después de cada cambio de configuración. El diálogo no se actualiza automáticamente mientras está abierto.
- Use **Copy Summary** para pegar una lista concisa de problemas en una publicación de foro de soporte o en un correo electrónico. Use **Copy JSON** o **Export JSON...** cuando adjunte datos de diagnóstico completos a un informe de error.
- Si está solucionando problemas de audio remoto, verifique tanto la sección de RX de audio remoto a nivel de radio como la sección de ruta de flujo de radio por slice en el Issue Summary. Ambas secciones deben mostrar IDs de flujo e indicadores de propiedad consistentes para que el audio se enrute correctamente.

## Relacionados

- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje sencillo de problemas de slice sospechosos](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspeccionar las frecuencias RF/IF, el desplazamiento y los indicadores de validez de cada transverter para diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
