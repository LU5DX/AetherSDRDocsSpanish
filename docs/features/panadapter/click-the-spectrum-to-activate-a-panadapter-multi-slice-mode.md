# Haga clic en el espectro para activar un panadapter (modo de múltiples slices)

En una disposición de múltiples panadapters, solo un panadapter está activo a la vez. Al hacer clic en el área del espectro de un panadapter inactivo, este se pone en foco para que sus controles, slices y sintonización se apliquen a él.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Deben estar abiertos al menos dos panadapters. En el modo de un solo panadapter, los botones de la barra de título (⬈, □, ×) están ocultos y no hay nada entre lo que cambiar.

## Pasos

1. Localice el panadapter que desea activar. Su barra de título muestra el slice al que está vinculado (por ejemplo, "Slice B").
2. Haga clic en cualquier lugar del área de espectro / waterfall de ese panadapter.
3. El panadapter ya está activo. La sintonización, el zoom con desplazamiento y todos los controles de slice se aplican a él.

## Qué hace cada control

| Control              | Tipo                                 | Predeterminado | Descripción |
|----------------------|--------------------------------------|---------|-------------|
| Título del slice     | Indicador                            | Slice A | Muestra qué slice está vinculado a este panadapter. |
| ⬈ / ↩ (desacoplar/acoplar) | Botón pulsador                      | —       | Desacopla el panadapter en una ventana flotante o lo vuelve a acoplar; emite popOutClicked o dockClicked. Oculto en modo de un solo pan. La ventana flotante no tiene marco (v0.9.0, #1922) — arrastre mediante la barra de título dentro de la aplicación, redimensione mediante el asa de tamaño en la esquina inferior derecha; consulte 00-navigation.json para el marco compartido sin bordes. En macOS, cada ciclo de flotación/acoplamiento ahora llama a resetGpuResources() y re-vincula la superficie QRhi/Metal a la nueva ventana para que el espectro permanezca activo (v0.9.5.1, #2280). El estado guardado de la ventana flotante ya no se restaura cuando se añaden panadapters posteriores, lo que evita que aparezca una ventana flotante vacía. rebuildDockedSplitter() reclama cualquier espacio vacío del divisor cuando un panel se acopla de nuevo. |
| □ (maximizar)        | Botón pulsador                          | —       | Maximiza este panadapter en una disposición de múltiples paneles; emite maximizeRequested. Oculto en modo de un solo pan. |
| × (cerrar)           | Botón pulsador                          | —       | Cierra este panadapter; emite closeRequested. Oculto en modo de un solo pan. |
| Espectro / waterfall | Área de arrastre                       | —       | Haga clic para activar el panadapter; arrastre para sintonizar, desplácese para hacer zoom (SpectrumWidget). |
| Etiqueta de estadísticas CW | Indicador                          | —       | Muestra el tono y la velocidad de CW detectados en el formato `<hz> Hz  <wpm> WPM`. |
| Sens                 | Deslizador                             | 30      | Filtra decodificaciones de baja confianza; cuanto más alto, más estricto. Asigna 0-100 a un umbral de costo de 1.0-0.1. Clave de configuración: `CwDecoderSensitivity`. |
| 🔒P (Bloquear tono)  | Botón de alternancia                   | —       | Bloquea el tono del decodificador CW en la frecuencia sintonizada actual. |
| 🔒S (Bloquear velocidad) | Botón de alternancia               | —       | Bloquea la velocidad del decodificador CW en las PPM actuales. |
| Rango de tono        | Deslizador de doble control            | Bajo: 500 Hz, Alto: 700 Hz | Establece el rango de búsqueda de tono del decodificador (Bajo a Alto). Rango: 300-1200 Hz. La etiqueta muestra "Pitch". |
| Rango de PPM         | Deslizador de doble control            | Bajo: 15 PPM, Alto: 40 PPM | Establece el rango de búsqueda de velocidad del decodificador. Rango: 5-60 PPM. La etiqueta muestra "WPM". |
| A- (reducir tamaño de fuente) | Botón pulsador                  | —       | Disminuye el tamaño de fuente del texto decodificado en un paso. Se conserva entre sesiones mediante `CwDecodeSettings::fontPx()`. Rango: 8–32 px. |
| A+ (aumentar tamaño de fuente) | Botón pulsador                  | —       | Aumenta el tamaño de fuente del texto decodificado en un paso. Se conserva entre sesiones mediante `CwDecodeSettings::fontPx()`. Rango: 8–32 px. |
| CPY ALL (copiar todo) | Botón pulsador                      | —       | Copia todo el texto decodificado al portapapeles. |
| CPY VIS (copiar visible) | Botón pulsador                    | —       | Copia solo el texto actualmente visible en el área de desplazamiento. |
| CLR (limpiar)        | Botón pulsador                          | —       | Limpia el búfer de decodificación CW. |
| ✕ (cerrar CW)        | Botón pulsador                          | —       | Oculta el panel de decodificación CW; emite cwPanelCloseRequested. |
| Texto decodificado CW | Campo de texto de solo lectura        | —       | Visualización continua de CW decodificado coloreado por confianza. El tamaño de fuente es ajustable por el usuario mediante los botones A- y A+. Colores: <0.15 verde, <0.35 amarillo, <0.60 naranja, >=0.60 rojo. |
| Iniciar barrido      | Botón pulsador                          | —       | Ejecuta un barrido de sintonización de baja potencia en la banda TX actual y traza la ROE en el panadapter. |
| Limpiar barrido      | Botón pulsador                          | —       | Elimina el trazo de barrido de ROE mostrado del panadapter. |
| PWR (potencia de barrido) | Deslizador                         | 1 W     | Establece la potencia de portadora utilizada durante el barrido. Rango: 1 W a 10 W. El valor actual se muestra como una etiqueta de solo lectura a la derecha del deslizador. |

Los botones ⬈ / ↩, □ y × están ocultos en el modo de un solo panadapter. Solo aparecen cuando hay más de un panadapter abierto.

## Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro cuando está habilitado. Requiere enrutamiento de audio de PC para funcionar; se muestra un recordatorio "(requires PC Audio)" cuando el audio aún no está enrutado.

El texto decodificado se colorea según el nivel de confianza:

| Color | Umbral de costo |
|---|---|
| Verde | inferior a 0.15 |
| Amarillo | 0.15 – inferior a 0.35 |
| Naranja | 0.35 – inferior a 0.60 |
| Rojo | 0.60 y superior |

El deslizador **Sens** asigna el rango de 0 – 100 a un umbral de costo de 1.0 – 0.1. Los valores más altos filtran las decodificaciones de menor confianza.

El deslizador de doble control **Rango de tono** establece el rango de búsqueda de tono del decodificador. El control inferior establece el tono mínimo (Bajo), el control superior establece el tono máximo (Alto). El rango es de 300-1200 Hz.

El deslizador de doble control **Rango de PPM** establece el rango de búsqueda de velocidad del decodificador. El control inferior establece la velocidad mínima, el control superior establece la velocidad máxima. El rango es de 5-60 PPM. Valores predeterminados: 15-40 PPM.

Haga clic en **A-** para disminuir el tamaño de fuente del texto decodificado, o en **A+** para aumentarlo. El tamaño de fuente se conserva entre sesiones y tiene un rango de 8–32 píxeles. La altura del panel se ajusta proporcionalmente para mostrar más o menos líneas de texto decodificado.

Haga clic en **CPY ALL** para copiar todo el búfer de texto decodificado al portapapeles. Haga clic en **CPY VIS** para copiar solo el texto actualmente visible en el área de desplazamiento. Haga clic en **CLR** para limpiar el búfer de decodificación. Haga clic en **✕ (cerrar CW)** para ocultar el panel.

### Redimensionar el panel de decodificación CW

Un asa de arrastre delgada en el borde superior del panel de decodificación CW permite redimensionar el panel verticalmente. Para redimensionar:

1. Pase el cursor sobre el borde superior del panel de decodificación CW hasta que el cursor cambie a un cursor de redimensionamiento vertical.
2. Haga clic y arrastre hacia arriba o hacia abajo para ajustar la altura del panel.
3. La altura del panel se conserva entre sesiones mediante `CwDecodeSettings::panelHeight()` con un rango de 60–600 píxeles.

### Texto decodificado del lado TX

Cuando la radio está transmitiendo, el decodificador también decodifica la manipulación de su transmisor y la añade al área de texto de CW decodificado en cian (#5fc8ff). Esto permite ver tanto el CW entrante como el saliente en el mismo panel, con códigos de color para distinguir su propio envío de las señales recibidas. Se inserta un espacio entre las transmisiones de recepción y transmisión para mantenerlas visualmente separadas.

El mismo filtro de confianza (deslizador Sens) se aplica al texto del lado TX y al del lado RX.

### Menú contextual en el área de texto de CW decodificado

Al hacer clic con el botón derecho dentro del área de texto de CW decodificado se abre un menú contextual. Además de las acciones de texto estándar (Seleccionar todo, Copiar, etc.), el menú incluye un elemento **Clear**. Seleccionar **Clear** tiene el mismo efecto que hacer clic en el botón **CLR**: limpia el búfer de decodificación.

## Congelación del waterfall durante la transmisión

Cuando la radio comienza a transmitir (basado en el estado de interbloqueo TRANSMITTING de la radio, no en el borde MOX local), la visualización del waterfall se congela automáticamente. Esto evita un artefacto de estela de TX de 10 a 23 segundos que anteriormente aparecía después de dejar de manipular. Cualquier cliente que transmita a la radio activa la congelación. El waterfall se descongela cuando finaliza la transmisión.

Al reconectar la radio, los FPS del panadapter deseados y la duración de la línea del waterfall se reafirman para evitar caer silenciosamente al valor predeterminado de 10 Hz de la radio (#2465). Los panadapters secundarios (Slice B–H) también tienen su rango de dBm preparado en la reconexión para que el ajuste automático del nivel de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que causaba un espectro plano en la reconexión (#3034).

## Controles de barrido de ROE del panel ANT

El panel ANT incluye controles para ejecutar un barrido de ROE de baja potencia en la banda TX actual y mostrar el resultado en el panadapter.

- **Start Sweep** — ejecuta un barrido de sintonización de baja potencia en la banda TX actual y traza la ROE en el panadapter. El barrido utiliza el slice asociado con el panel actual y el nivel de potencia establecido por el deslizador PWR. Cuando se utiliza un sintonizador de antena TGXL, el barrido omite automáticamente el sintonizador antes de barrer y restaura el estado original del sintonizador cuando finaliza o se aborta.
- **Clear Sweep** — elimina el trazo de barrido de ROE mostrado del panadapter.
- **Deslizador PWR** — establece la potencia de portadora utilizada durante el barrido. El rango es de 1 W a 10 W. El valor actual se muestra como una etiqueta de solo lectura a la derecha del deslizador. El deslizador también se puede configurar mediante programación a través de `setSwrSweepPowerWatts`; la etiqueta se actualiza automáticamente.

### Fases del barrido de ROE

El barrido progresa a través de las siguientes fases internas. Estas no son directamente visibles en la interfaz de usuario, pero determinan lo que la radio está haciendo en cada punto durante el barrido:

| Fase | Descripción |
|---|---|
| Idle | No hay ningún barrido en curso. |
| WaitingForTgxlBypass | Esperando a que el sintonizador TGXL confirme el modo de derivación antes de que comience la RF. |
| TgxlBypassSettle | Permitir un período de estabilización después de que se confirme la derivación del TGXL. |
| Sweeping | Recorriendo las frecuencias de barrido y recopilando muestras de ROE. |
| StoppingTune | Esperando a que la radio detenga la portadora de sintonía después de que el barrido se complete o se aborte. |
| RestoringTgxl | Restaurando el sintonizador TGXL a su estado operativo/de derivación original. |

Las lecturas de ROE pueden provenir de los medidores de potencia directa/reflejada de la propia radio o del medidor del sintonizador TGXL, dependiendo de cuál esté disponible para el puerto de antena conectado.

## Visibilidad de la fila DSP (DSP extendido, #2177)

La fila de reducción de ruido NRL (fila DSP 4) está disponible tanto en el firmware de la serie 6000 como en la serie 8000 y siempre es visible, independientemente de si el DSP extendido está habilitado. Las filas NRS (fila 5), RNN (fila 6) y NRF (fila 8) permanecen ocultas a menos que la radio conectada informe soporte de DSP extendido.

## Soporte de temas (v0.9.7)

La barra de título del panadapter y el panel CW ahora utilizan un estilo basado en temas en lugar de colores fijos. El fondo de la barra de título utiliza un degradado con las variables de tema `{{color.text.disabled}}` y `{{color.background.1}}`. El fondo del panel CW utiliza `{{color.background.0}}` con un borde superior en `{{color.background.1}}`. El texto del título CW usa `{{color.accent}}`, el texto de sugerencia usa `{{color.meter.bar.fill}}` y las etiquetas usan `{{color.text.label}}`. El deslizador utiliza el estilo de deslizador principal mediante `applyPrimarySliderStyle()`.

## Consejos

- Arrastre sobre el área de Espectro / waterfall para sintonizar la frecuencia del slice. Desplácese para hacer zoom en el span.
- Para darle a un panadapter más espacio en pantalla sin cerrar otros, haga clic en □ (maximizar) en su barra de título. Consulte [Maximize one panadapter to fill the main area](maximize-one-panadapter-to-fill-the-main-area.md).
- Para mover un panadapter a una ventana separada, haga clic en ⬈ (desacoplar). Consulte [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md).
- Ajuste el tamaño del texto de decodificación CW con los botones A- y A+ según su preferencia. La configuración se conserva entre sesiones.

## Relacionados

- [Maximize one panadapter to fill the main area](maximize-one-panadapter-to-fill-the-main-area.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)
- [Close an extra panadapter](close-an-extra-panadapter.md)
- [Understanding slices and VFOs](../../getting-started/concepts/understanding-slices.md)
