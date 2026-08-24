# Solución de problemas de slices

El cuadro de diálogo de Solución de problemas de slices captura una instantánea de cada slice, panadapter, transvertidor, canal DAX, dispositivo de audio, estado DSP del cliente y enlaces de dispositivos de control (MIDI) en la radio conectada y verifica si hay problemas de configuración probables. Úselo para diagnosticar problemas de audio, silencio, antena, transvertidor y enrutamiento de audio remoto, o para recopilar datos de diagnóstico antes de contactar al soporte.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El cuadro de diálogo no está disponible sin una conexión activa a la radio.

## Cómo funciona

Abra el cuadro de diálogo con `Help > Slice Troubleshooting...`. Cuando se abre el cuadro de diálogo, AetherSDR lee el estado actual de la radio en una instantánea. La instantánea cubre slices, panadapters, transvertidores, canales DAX, dispositivos de audio, estado DSP del cliente, enlaces de dispositivos de control (MIDI), configuraciones de banda TX y estado de los puntos finales de audio. El cuadro de diálogo verifica esa instantánea para detectar un conjunto de patrones de problemas conocidos: audio faltante, silencio atascado, antena faltante, problemas de validez del transvertidor, problemas de enrutamiento de audio, anomalías en el estado del DSP y conflictos de propiedad entre múltiples clientes, y presenta los resultados en dos pestañas.

**La pestaña Issue Summary** muestra una lista con viñetas en lenguaje sencillo de los problemas detectados. Si no hay ningún problema, la lista está vacía. Esta es la forma más rápida de ver si AetherSDR ha identificado un problema de configuración.

El Issue Summary incluye diagnósticos de RX de audio remoto. Para la sección de audio a nivel de radio, el resumen informa el ID de flujo del RX de audio remoto, si se espera un flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si el flujo es propiedad del cliente actual, la configuración de compresión en uso y cualquier nota de enrutamiento. Para la sección de enrutamiento de audio por slice, el resumen informa el ID de flujo del RX de audio remoto junto con los indicadores de esperado, creación pendiente, eliminación solicitada, estado visto y propiedad nuestra.

El Issue Summary también incluye diagnósticos detallados de los puntos finales de audio que muestran el estado operativo de cada punto final, el estado de ejecución, el backend, el nombre del dispositivo, la frecuencia de muestreo, el número de canales, el formato de muestra, el estado de remuestreo, las métricas del búfer y cualquier error o nota.

Para los puntos finales de audio que informan remuestreo relacionado con la voz, los diagnósticos también incluyen la normalización de entrada de voz a 48 kHz, el remuestreo de salida de voz a 24 kHz y los indicadores de remuestreo RADE a 24 kHz.

El Issue Summary incluye diagnósticos del medidor TX. Cuando los medidores TX no están activos — por ejemplo, cuando la radio no está transmitiendo actualmente — el resumen informa que la potencia directa TX es el último valor recibido en lugar de una lectura actual, y la ROE TX se omite en lugar de mostrarse como desactualizada. Esta advertencia se incluye cuando la antigüedad del medidor TX está disponible, junto con el tiempo transcurrido desde la última muestra, y ayuda a evitar malinterpretar una ROE faltante como un problema de antena.

**La pestaña JSON** muestra la instantánea completa como JSON estructurado (versión de esquema 3). Esta vista contiene todos los campos que AetherSDR recopiló: estado del slice, parámetros del panadapter, frecuencias RF/IF del transvertidor, compensaciones, indicadores de validez, asignaciones de canales DAX, dispositivos de audio, estado DSP del cliente, enlaces de dispositivos de control, configuraciones de banda TX, estado del RX de audio remoto y detalles de los puntos finales de audio. El personal de soporte y los usuarios avanzados pueden inspeccionar los valores de los campos individuales aquí.

La instantánea refleja el estado de la radio en el momento en que se tomó. Si cambia la configuración de los slices mientras el cuadro de diálogo está abierto, haga clic en **Refresh Snapshot** para volver a leer el estado actual antes de sacar conclusiones o compartir datos.

El cuadro de diálogo recuerda la posición y el tamaño de su ventana entre sesiones. Se volverá a abrir en la misma ubicación donde lo cerró por última vez.

## Qué hace cada control

| Control          | Tipo                                                                                           | Comportamiento                                                                                                                                                                                       |
|------------------|------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Issue Summary    | Pestaña                                                                                        | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados, incluidos diagnósticos de enrutamiento de audio, DSP, estado de dispositivos de control (MIDI), propiedad de múltiples clientes y puntos finales de audio. |
| JSON             | Pestaña                                                                                        | Muestra la instantánea JSON completa (versión de esquema 3) de slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, configuraciones de banda TX, estado del RX de audio remoto y puntos finales de audio. |
| Refresh Snapshot | Botón                                                                                          | Vuelve a leer el estado de los slices en la instantánea. Úselo después de cambiar la configuración de la radio.                                                                                     |
| Copy Summary     | Botón                                                                                          | Copia el texto del resumen de problemas al portapapeles.                                                                                                                                            |
| Copy JSON        | Botón                                                                                          | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                  |
| Export JSON...   | Botón                                                                                          | Abre un cuadro de diálogo de archivos para guardar la instantánea JSON en un archivo.                                                                                                                |
| Find:            | Campo de texto                                                                                 | Resalta las coincidencias del término ingresado en la pestaña activa (Issue Summary o JSON). Tiene un botón de borrado y un texto de marcador de posición 'Search snapshot...'. Enter salta a la siguiente coincidencia; el uso compartido de pestañas actualiza los contadores de resaltado. La etiqueta de estado muestra '<N> match(es) in current tab.' |
| Find Next        | Botón                                                                                          | Salta a la siguiente coincidencia del término de búsqueda en la pestaña activa. Se envuelve dentro de la pestaña actual. Un término vacío no produce coincidencias.                                    |
| Close            | Botón                                                                                          | Cierra el cuadro de diálogo.                                                                                                                                                                         |
| Status label     | Indicador                                                                                      | Muestra el resultado de la acción de copiar o exportar más reciente (por ejemplo, "Copied to clipboard") o el recuento de coincidencias de búsqueda.                                                   |

## Consejos

- Tome una nueva instantánea con **Refresh Snapshot** después de cada cambio de configuración. El cuadro de diálogo no se actualiza automáticamente mientras está abierto.
- Use **Copy Summary** para pegar una lista concisa de problemas en una publicación de foro de soporte o correo electrónico. Use **Copy JSON** o **Export JSON...** cuando adjunte datos de diagnóstico completos a un informe de error.
- Si está solucionando problemas de audio remoto, verifique tanto la sección de RX de audio remoto a nivel de radio como la sección de ruta de flujo de radio por slice en el Issue Summary. Ambas secciones deben mostrar ID de flujo e indicadores de propiedad coherentes para que el audio se enrute correctamente.
- Al investigar problemas de audio, revise los diagnósticos de puntos finales de audio en el Issue Summary. Los puntos finales no operativos, los recuentos altos de subejecución o los mensajes de error indican consideraciones del backend de audio.
- Al solucionar problemas de lecturas del medidor TX, tenga en cuenta que la potencia directa TX mantiene su último valor suavizado mientras que la ROE TX muestra n/a cuando los medidores no están activos. El Issue Summary identifica explícitamente cuándo los medidores están desactualizados para que no confunda una lectura de vatios plausible con una actual.

## Relacionados

- [Capture a slice snapshot for support](capture-a-slice-snapshot-for-support.md)
- [Read a plain-language list of suspected slice problems](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Refresh the snapshot after changing slice state](refresh-the-snapshot-after-changing-slice-state.md)
- [Copy the full JSON snapshot to the clipboard](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Export the snapshot to a file to attach to a bug report](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspect each transverter's RF/IF, offset and validity flags for XVTR diagnosis](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
