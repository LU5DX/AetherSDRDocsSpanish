# Haga clic en el espectro para activar un panadapter (modo multi-slice)

En un diseño con múltiples panadapters, solo un panadapter está activo a la vez. Al hacer clic en el área del espectro de un panadapter inactivo, este adquiere el foco para que sus controles, slices y sintonización se apliquen a él.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Deben estar abiertos al menos dos panadapters. En modo de un solo panadapter, los botones de la barra de título (⬈, □, ×) están ocultos y no hay nada entre lo que alternar.

## Pasos

1. Localice el panadapter que desea activar. Su barra de título muestra el slice al que está vinculado (por ejemplo, "Slice B").
2. Haga clic en cualquier lugar del área del espectro / waterfall de ese panadapter.
3. El panadapter ahora está activo. La sintonización, el zoom con desplazamiento y todos los controles del slice se aplican a él.

## Qué hace cada control

| Control              | Tipo                                                                                                 | Valor predeterminado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|----------------------|------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Título del slice     | Indicador                                                                                            | Slice A                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Espectro / waterfall | Área de clic / arrastre                                                                              | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ⬈ / ↩ (emergente/acoplar) | Saca el panadapter a una ventana flotante o lo acopla de nuevo; emite popOutClicked o dockClicked. | Oculto en modo mono-pan. La ventana flotante no tiene marco (v0.9.0, #1922) — arrastre mediante la barra de título interna de la aplicación, redimensione mediante el control de tamaño en la esquina inferior derecha; consulte 00-navigation.json para conocer el marco compartido sin bordes. En macOS, cada ciclo de flotación/acoplamiento llama ahora a resetGpuResources() y re-vincula la superficie QRhi/Metal a la nueva ventana para que el espectro permanezca vivo (v0.9.5.1, #2280). El estado guardado de la ventana flotante ya no se restaura cuando se añaden panadaptadores posteriores, evitando que aparezca una ventana flotante en blanco. rebuildDockedSplitter() recupera cualquier ranura vacía del splitter cuando un pan se acopla de nuevo. |
| □ (maximizar)        | Botón pulsador                                                                                       | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| × (cerrar)           | Botón pulsador                                                                                       | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Sens                 | Deslizador                                                                                           | 30                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| 🔒P (Bloquear tono)   | Botón de alternancia                                                                                 | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| 🔒S (Bloquear velocidad) | Botón de alternancia                                                                                 | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Lo (tono mínimo)     | Deslizador                                                                                           | 500 Hz                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Hi (tono máximo)     | Deslizador                                                                                           | 700 Hz                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| CPY ALL              | Botón pulsador                                                                                       | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| CPY VIS              | Botón pulsador                                                                                       | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| CLR                  | Botón pulsador                                                                                       | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ✕ (cerrar CW)        | Botón pulsador                                                                                       | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Texto decodificado CW | Campo de texto de solo lectura                                                                       | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Start Sweep          | Botón pulsador                                                                                       | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Clear Sweep          | Botón pulsador                                                                                       | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| PWR (potencia de barrido) | Deslizador                                                                                           | 1 W                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

Los botones ⬈ / ↩, □ y × están ocultos en el modo de un solo panadapter. Aparecen solo cuando hay más de un panadapter abierto.

## Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro cuando está habilitado. Requiere enrutamiento de audio de PC para funcionar; se muestra un recordatorio "(requires PC Audio)" cuando el audio aún no está enrutado.

El texto decodificado se colorea según el nivel de confianza:

| Color | Umbral de costo |
|---|---|
| Verde | por debajo de 0.15 |
| Amarillo | 0.15 – por debajo de 0.35 |
| Naranja | 0.35 – por debajo de 0.60 |
| Rojo | 0.60 y superior |

El deslizador **Sens** asigna el rango 0 – 100 a un umbral de costo de 1.0 – 0.1. Los valores más altos filtran las decodificaciones de menor confianza.

Los deslizadores **Lo** y **Hi** establecen el rango de búsqueda de tono. Lo está limitado para que no sea mayor que Hi, y Hi está limitado para que no sea menor que Lo.

Haga clic en **CPY ALL** para copiar todo el búfer de texto decodificado al portapapeles. Haga clic en **CPY VIS** para copiar solo el texto actualmente visible en el área de desplazamiento. Haga clic en **CLR** para borrar el búfer de decodificación. Haga clic en **✕ (cerrar CW)** para ocultar el panel.

### Menú contextual en el área de texto de decodificación CW

Al hacer clic con el botón derecho dentro del área de texto de decodificación CW se abre un menú contextual. Además de las acciones de texto estándar (Seleccionar todo, Copiar, etc.), el menú incluye un elemento **Clear**. Seleccionar **Clear** tiene el mismo efecto que hacer clic en el botón **CLR**: borra el búfer de decodificación.

## Controles de barrido SWR del panel ANT

El panel ANT incluye controles para ejecutar un barrido SWR de baja potencia a través de la banda TX actual y mostrar el resultado en el panadapter.

- **Start Sweep** — ejecuta un barrido de sintonización de baja potencia a través de la banda TX actual y traza la SWR en el panadapter. El barrido utiliza el slice asociado al panel actual y el nivel de potencia establecido por el deslizador PWR. Cuando se utiliza un sintonizador de antena TGXL, el barrido omite automáticamente el sintonizador antes de barrer y restaura el estado original del sintonizador cuando finaliza o se aborta.
- **Clear Sweep** — elimina la traza del barrido SWR mostrada en el panadapter.
- **Deslizador PWR** — establece la potencia de portadora utilizada durante el barrido. El rango es de 1 W a 10 W. El valor actual se muestra como una etiqueta de solo lectura a la derecha del deslizador. El deslizador también se puede establecer mediante programación a través de `setSwrSweepPowerWatts`; la etiqueta se actualiza automáticamente.

### Fases del barrido SWR

El barrido progresa a través de las siguientes fases internas. Estas no son directamente visibles en la interfaz de usuario, pero determinan lo que la radio está haciendo en cada punto durante el barrido:

| Fase | Descripción |
|---|---|
| Idle | No hay ningún barrido en curso. |
| WaitingForTgxlBypass | Esperando a que el sintonizador TGXL confirme el modo de bypass antes de que comience la RF. |
| TgxlBypassSettle | Permitir un período de estabilización después de que se confirme el bypass del TGXL. |
| Sweeping | Recorriendo las frecuencias de barrido y recopilando muestras de SWR. |
| StoppingTune | Esperando a que la radio detenga la portadora de sintonización después de que el barrido se complete o sea abortado. |
| RestoringTgxl | Restaurando el sintonizador TGXL a su estado original de operación/bypass. |

Las lecturas de SWR pueden provenir de los medidores de potencia directa/reflejada de la propia radio o del medidor del sintonizador TGXL, dependiendo de cuál esté disponible para el puerto de antena conectado.

## Visibilidad de la fila DSP (DSP extendido, #2177)

La fila de reducción de ruido NRL (fila DSP 4) está disponible tanto en el firmware de la serie 6000 como en la serie 8000 y siempre es visible, independientemente de si el DSP extendido está habilitado. Las filas NRS (fila 5), RNN (fila 6) y NRF (fila 8) permanecen ocultas a menos que la radio conectada informe compatibilidad con DSP extendido.

## Consejos

- Arrastre en el área del Espectro / waterfall para sintonizar la frecuencia del slice. Desplácese para hacer zoom en el span.
- Para darle a un panadapter más espacio en pantalla sin cerrar otros, haga clic en □ (maximizar) en su barra de título. Consulte [Maximizar un panadapter para que ocupe el área principal](maximize-one-panadapter-to-fill-the-main-area.md).
- Para mover un panadapter a una ventana separada, haga clic en ⬈ (emergente). Consulte [Sacar un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md).

## Relacionados

- [Maximizar un panadapter para que ocupe el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Sacar un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Comprensión de slices y VFO](../../getting-started/concepts/understanding-slices.md)
<!-- docmesh:llm version=v0.9.4 date=2026-05-01 -->
