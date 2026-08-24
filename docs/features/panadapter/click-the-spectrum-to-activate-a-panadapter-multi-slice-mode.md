# Haga clic en el espectro para activar un panadapter (modo multi-slice)

En una disposición de múltiples panadapters, solo un panadapter está activo a la vez. Al hacer clic en el área del espectro de un panadapter inactivo, este se trae al primer plano para que sus controles, slices y sintonización se apliquen a él.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Debe haber al menos dos panadapters abiertos. En el modo de un solo panadapter, los botones de la barra de título (⬈, □, ×) están ocultos y no hay nada entre lo que cambiar.

## Pasos

1. Localice el panadapter que desea activar. Su barra de título muestra el slice al que está vinculado (por ejemplo, "Slice B").
2. Haga clic en cualquier lugar del área de Spectrum / waterfall de ese panadapter.
3. El panadapter ahora está activo. La sintonización, el zoom con desplazamiento y todos los controles de slice se aplican a él.

## Qué hace cada control

| Control              | Tipo                                 | Predeterminado | Descripción |
|----------------------|--------------------------------------|---------|-------------|
| Título del slice     | Indicador                            | Slice A | Muestra qué slice está vinculado a este panadapter. |
| ⬈ / ↩ (pop-out/dock) | Botón pulsador                       | —       | Extrae el panadapter a una ventana flotante o lo vuelve a acoplar; emite popOutClicked o dockClicked. Oculto en el modo de un solo pan. La ventana flotante no tiene marco (v0.9.0, #1922) — arrastre mediante la franja de título dentro de la aplicación, redimensione mediante el control de tamaño en la esquina inferior derecha; consulte 00-navigation.json para el marco compartido sin bordes. En macOS, cada ciclo de flotar/acoplar ahora llama a resetGpuResources() y vuelve a vincular la superficie QRhi/Metal a la nueva ventana para que el espectro permanezca activo (v0.9.5.1, #2280). El estado guardado de la ventana flotante ya no se restaura cuando se añaden panadapters posteriores, lo que evita que aparezca una ventana flotante en blanco. rebuildDockedSplitter() recupera cualquier espacio divisor vacío cuando un pan se vuelve a acoplar. |
| □ (maximizar)        | Botón pulsador                       | —       | Maximiza este panadapter en una disposición multi-pan; emite maximizeRequested. Oculto en el modo de un solo pan. |
| × (cerrar)           | Botón pulsador                       | —       | Cierra este panadapter; emite closeRequested. Oculto en el modo de un solo pan. |
| Spectrum / waterfall | Área de arrastre                     | —       | Al hacer clic se activa el panadapter; arrastre para sintonizar, desplácese para hacer zoom (SpectrumWidget). |
| Etiqueta de estadísticas CW | Indicador                     | —       | Muestra el tono y la velocidad CW detectados en el formato `<hz> Hz  <wpm> WPM`. |
| Sens                 | Deslizador                           | 30      | Filtra decodificaciones de baja confianza; cuanto más alto, más estricto. Asigna 0-100 al umbral de costo 1.0-0.1. Clave de configuración: `CwDecoderSensitivity`. |
| 🔒P (Bloquear tono)   | Botón de alternancia                  | —       | Bloquea el tono del decodificador CW a la frecuencia sintonizada actual. |
| 🔒S (Bloquear velocidad) | Botón de alternancia               | —       | Bloquea la velocidad del decodificador CW a las WPM actuales. |
| Lo (tono mínimo)     | Deslizador                           | 500 Hz  | Tono mínimo que busca el decodificador CW; limitado a ≤ Hi. Rango: 300-1200 Hz. |
| Hi (tono máximo)     | Deslizador                           | 700 Hz  | Tono máximo que busca el decodificador CW; limitado a ≥ Lo. Rango: 300-1200 Hz. |
| CPY ALL              | Botón pulsador                       | —       | Copia todo el texto decodificado al portapapeles. |
| CPY VIS              | Botón pulsador                       | —       | Copia solo el texto actualmente visible en el área de desplazamiento. |
| CLR                  | Botón pulsador                       | —       | Borra el búfer de decodificación CW. |
| ✕ (cerrar CW)        | Botón pulsador                       | —       | Oculta el panel de decodificación CW; emite cwPanelCloseRequested. |
| Texto de decodificación CW | Campo de texto de solo lectura  | —       | Visualización continua del CW decodificado con colores según la confianza. Colores: <0.15 verde, <0.35 amarillo, <0.60 naranja, >=0.60 rojo. |
| Vista FFT 3D         | Botón de alternancia                  | Desactivado | Alterna la vista de espectro FFT 3D. Muestra el historial de señales como una superficie 3D que avanza con sombras de elevación, límites de desplazamiento suave y un nivel de suelo resincronizado después del zoom de ancho de banda. Los indicadores de slice proyectan sombras de elevación en caché. Nuevo en v26.7.x (#4413-#4477). Parte de SpectrumWidget. |
| Iniciar barrido      | Botón pulsador                       | —       | Ejecuta un barrido de sintonización de baja potencia en la banda TX actual y traza la ROE en el panadapter. |
| Borrar barrido       | Botón pulsador                       | —       | Elimina la traza de barrido de ROE mostrada del panadapter. |
| PWR (potencia de barrido) | Deslizador                      | 1 W     | Establece la potencia de portadora utilizada durante el barrido. Rango: 1 W a 10 W. El valor actual se muestra como una etiqueta de solo lectura a la derecha del deslizador. |

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

Los deslizadores **Lo** y **Hi** establecen el rango de búsqueda del tono del decodificador. **Lo** establece el tono mínimo (300 – 1200 Hz), **Hi** establece el tono máximo (300 – 1200 Hz). El valor de **Lo** está limitado a ≤ **Hi**, y el valor de **Hi** está limitado a ≥ **Lo**.

Haga clic en **CPY ALL** para copiar todo el búfer de texto decodificado al portapapeles. Haga clic en **CPY VIS** para copiar solo el texto actualmente visible en el área de desplazamiento. Haga clic en **CLR** para borrar el búfer de decodificación. Haga clic en **✕ (cerrar CW)** para ocultar el panel.

### Redimensionar el panel de decodificación CW

Una fina franja de arrastre en el borde superior del panel de decodificación CW le permite redimensionar el panel verticalmente. Para redimensionar:

1. Pase el cursor sobre el borde superior del panel de decodificación CW hasta que el cursor cambie a un cursor de redimensionamiento vertical.
2. Haga clic y arrastre hacia arriba o hacia abajo para ajustar la altura del panel.
3. La altura del panel se conserva entre sesiones mediante `CwDecodeSettings::panelHeight()` con un rango de 60 a 600 píxeles.

### Texto decodificado del lado TX

Cuando la radio está transmitiendo, el decodificador también decodifica la manipulación (keying) de su transmisor y la añade al área de texto de decodificación CW en cian (#5fc8ff). Esto le permite ver tanto el CW entrante como el saliente en el mismo panel, con códigos de color para que pueda distinguir su propio envío de las señales recibidas. Se inserta un espacio entre las secuencias de recepción y transmisión para mantenerlas visualmente separadas.

El mismo filtro de confianza (deslizador Sens) se aplica al texto del lado TX que al del lado RX.

### Menú contextual en el área de texto de decodificación CW

Al hacer clic con el botón derecho dentro del área de texto de decodificación CW se abre un menú contextual. Además de las acciones de texto estándar (Seleccionar todo, Copiar, etc.), el menú incluye un elemento **Clear**. Seleccionar **Clear** tiene el mismo efecto que hacer clic en el botón **CLR**: borra el búfer de decodificación.

## Congelación del waterfall en transmisión

Cuando la radio comienza a transmitir (según el estado de interbloqueo TRANSMITTING de la radio, no el flanco local de MOX), la visualización del waterfall se congela automáticamente. Esto evita un artefacto de estela de transmisión de 10 a 23 segundos que aparecía anteriormente después de soltar la tecla. Cualquier cliente que transmita a la radio activa la congelación. El waterfall se descongela cuando termina la transmisión.

Al reconectar la radio, los FPS deseados del panadapter y la duración de la línea del waterfall se reafirman para evitar que caigan silenciosamente al valor predeterminado de 10 Hz de la radio (#2465). Los panadapters secundarios (Slices B–H) también tienen su rango de dBm preparado en la reconexión para que el ajuste automático del nivel de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que causaba un espectro plano al reconectar (#3034).

## Vista de espectro FFT 3D

La **vista FFT 3D** alterna la visualización del espectro a una superficie 3D que avanza. En esta vista, el historial de señales se desplaza hacia usted como una superficie con mapeo de elevación, con los indicadores de slice proyectando sombras de elevación en caché. El zoom de ancho de banda resincroniza el nivel del suelo. Desactive esta opción para volver al espectro 2D estándar.

## Controles de barrido de ROE en el panel ANT

El panel ANT incluye controles para ejecutar un barrido de ROE de baja potencia en la banda TX actual y mostrar el resultado en el panadapter.

- **Iniciar barrido** — ejecuta un barrido de sintonización de baja potencia en la banda TX actual y traza la ROE en el panadapter. El barrido utiliza el slice asociado con el panel actual y el nivel de potencia establecido por el deslizador PWR. Cuando se usa un acoplador de antena TGXL, el barrido omite automáticamente el acoplador antes de barrer y restaura el estado original del acoplador cuando termina o se aborta.
- **Borrar barrido** — elimina la traza de barrido de ROE mostrada del panadapter.
- **Deslizador PWR** — establece la potencia de portadora utilizada durante el barrido. El rango es de 1 W a 10 W. El valor actual se muestra como una etiqueta de solo lectura a la derecha del deslizador. El deslizador también se puede establecer mediante programación con `setSwrSweepPowerWatts`; la etiqueta se actualiza automáticamente.

### Fases del barrido de ROE

El barrido avanza a través de las siguientes fases internas. Estas no son directamente visibles en la interfaz, pero determinan lo que la radio está haciendo en cada punto durante el barrido:

| Fase | Descripción |
|---|---|
| Idle | No hay ningún barrido en curso. |
| WaitingForTgxlBypass | Esperando que el acoplador TGXL confirme el modo de derivación (bypass) antes de que comience la RF. |
| TgxlBypassSettle | Permite un período de estabilización después de que se confirme la derivación del TGXL. |
| Sweeping | Recorre las frecuencias de barrido y recopila muestras de ROE. |
| StoppingTune | Esperando que la radio detenga la portadora de sintonía después de que el barrido se complete o se aborte. |
| RestoringTgxl | Restaura el acoplador TGXL a su estado original de operación/derivación. |

Las lecturas de ROE pueden provenir de los medidores de potencia directa/reflejada de la propia radio o del medidor del acoplador TGXL, según cuál esté disponible para el puerto de antena conectado.

## Alojamiento en lienzo (v26.8.4)

Cuando el panadapter está alojado como un elemento en el lienzo del espacio de trabajo, la franja de título transmite un gesto de movimiento en vivo. Un umbral de arrastre de 6 píxeles separa un clic (que activa el panadapter) de un arrastre. Una vez que se supera el umbral, el panadapter sigue el puntero del mouse en el lienzo y emite las señales `canvasDragBegan`, `canvasDragMoved` y `canvasDragEnded`.

Un elemento del lienzo siempre puede extraerse, incluso cuando es el único pan: la ocultación de botones de un solo pan se aplica solo a la disposición apilada. Cuando el panadapter vuelve a la pila, se vuelven a aplicar las reglas normales de visibilidad de botones.

## Visibilidad de la fila DSP (DSP extendido, #2177)

La fila de reducción de ruido NRL (fila DSP 4) está disponible tanto en el firmware de la serie 6000 como en el de la serie 8000 y siempre está visible, independientemente de si el DSP extendido está habilitado. Las filas NRS (fila 5), RNN (fila 6) y NRF (fila 8) permanecen ocultas a menos que la radio conectada informe soporte de DSP extendido.

## Soporte de temas (v0.9.7)

La barra de título del panadapter y el panel CW ahora usan estilos basados en temas en lugar de colores fijos. El fondo de la barra de título usa un degradado con las variables de tema `{{color.text.disabled}}` y `{{color.background.1}}`. El fondo del panel CW usa `{{color.background.0}}` con un borde superior en `{{color.background.1}}`. El texto del título CW usa `{{color.accent}}`, el texto de sugerencia usa `{{color.meter.bar.fill}}` y las etiquetas usan `{{color.text.label}}`. El deslizador usa el estilo de deslizador principal mediante `applyPrimarySliderStyle()`.

## Consejos

- Arrastre sobre el área de Spectrum / waterfall para sintonizar la frecuencia del slice. Desplácese para hacer zoom en el intervalo.
- Para darle a un panadapter más espacio en pantalla sin cerrar otros, haga clic en □ (maximizar) en su barra de título. Consulte [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md).
- Para mover un panadapter a una ventana separada, haga clic en ⬈ (pop-out). Consulte [Extraer un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md).
- Ajuste el tamaño del texto de decodificación CW con los botones A- y A+ según su preferencia. El ajuste se conserva entre sesiones.

## Relacionados

- [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Extraer un panadapter a su propia vent
