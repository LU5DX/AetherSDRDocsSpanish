# Haga clic en el espectro para activar un panadapter (modo multi-slice)

En una disposición de múltiples panadapters (visualizadores panorámicos de espectro), solo uno está activo a la vez. Al hacer clic en el área de espectro de un panadapter inactivo, este pasa a primer plano y los controles, slices y el sintonizador se aplican a él.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Deben estar abiertos al menos dos panadapters. En el modo de un solo panadapter, los botones de la barra de título (⬈, □, ×) están ocultos y no hay nada entre lo que cambiar.

## Pasos

1. Localice el panadapter que desea activar. Su barra de título muestra el slice al que está vinculado (por ejemplo, "Slice B").
2. Haga clic en cualquier parte del área de Spectrum / waterfall de ese panadapter.
3. El panadapter está ahora activo. El sintonizador, el zoom con la rueda del ratón y todos los controles del slice se aplican a él.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Clave persistente |
|---|---|---|---|---|
| Título del slice | Indicador | Slice A | Slice A – Slice H | — |
| Spectrum / waterfall | Área de clic / arrastre | — | — | — |
| ⬈ / ↩ (pop-out/dock) | Botón de acción | — | — | — |
| □ (maximizar) | Botón de acción | — | — | — |
| × (cerrar) | Botón de acción | — | — | — |
| Sens | Control deslizante | 30 | 0 – 100 | `CwDecoderSensitivity` |
| 🔒P (Lock Pitch) | Botón de alternancia | — | — | — |
| 🔒S (Lock Speed) | Botón de alternancia | — | — | — |
| Lo (pitch mínimo) | Control deslizante | 500 Hz | 300 – 1200 Hz | — |
| Hi (pitch máximo) | Control deslizante | 700 Hz | 300 – 1200 Hz | — |
| CPY ALL | Botón de acción | — | — | — |
| CPY VIS | Botón de acción | — | — | — |
| CLR | Botón de acción | — | — | — |
| ✕ (cerrar CW) | Botón de acción | — | — | — |
| Texto decodificado CW | Campo de texto de solo lectura | — | — | — |

Los botones ⬈ / ↩, □ y × están ocultos en el modo de un solo panadapter. Aparecen únicamente cuando hay más de un panadapter abierto.

## Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro cuando está habilitado. Requiere enrutamiento de audio por PC para funcionar — se muestra un aviso "(requires PC Audio)" cuando el audio aún no está enrutado.

El texto decodificado se colorea según el nivel de confianza:

| Color | Umbral de costo |
|---|---|
| Verde | por debajo de 0.15 |
| Amarillo | 0.15 – por debajo de 0.35 |
| Naranja | 0.35 – por debajo de 0.60 |
| Rojo | 0.60 y superior |

El control deslizante **Sens** mapea el rango 0 – 100 a un umbral de costo de 1.0 – 0.1. Los valores más altos filtran las decodificaciones de menor confianza.

Los controles deslizantes **Lo** y **Hi** establecen el rango de búsqueda de pitch. Lo se limita para que no sea mayor que Hi, y Hi se limita para que no sea menor que Lo.

Haga clic en **CPY ALL** para copiar todo el búfer de texto decodificado al portapapeles. Haga clic en **CPY VIS** para copiar únicamente el texto visible en ese momento en el área de desplazamiento. Haga clic en **CLR** para borrar el búfer de decodificación. Haga clic en **✕ (close CW)** para ocultar el panel.

### Menú contextual del área de texto decodificado CW

Al hacer clic con el botón derecho dentro del área de texto decodificado CW se abre un menú contextual. Además de las acciones de texto estándar (Select All, Copy, etc.), el menú incluye un elemento **Clear**. Seleccionar **Clear** tiene el mismo efecto que hacer clic en el botón **CLR**: borra el búfer de decodificación.

## Consejos

- Arrastre sobre el área de Spectrum / waterfall para sintonizar la frecuencia del slice. Desplace la rueda del ratón para ajustar el span con zoom.
- Para darle a un panadapter más espacio en pantalla sin cerrar los demás, haga clic en □ (maximizar) en su barra de título. Consulte [Maximizar un panadapter para que ocupe el área principal](maximize-one-panadapter-to-fill-the-main-area.md).
- Para mover un panadapter a una ventana independiente, haga clic en ⬈ (pop-out). Consulte [Sacar un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md).

## Relacionado

- [Maximizar un panadapter para que ocupe el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Sacar un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Comprender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
