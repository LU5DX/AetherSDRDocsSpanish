# Haga clic en el espectro para activar un panadapter (modo multi-slice)

En un diseño de multi-panadapter, solo un panadapter está activo a la vez. Al hacer clic en el área de espectro de un panadapter inactivo, este entra en foco para que sus controles, slices y sintonización se apliquen a él.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Deben estar abiertos al menos dos panadapters. En modo de panadapter único, los botones de la barra de título (⬈, □, ×) están ocultos y no hay nada para cambiar.

## Pasos

1. Ubique el panadapter que desea activar. Su barra de título muestra el slice al que está vinculado (por ejemplo, "Slice B").
2. Haga clic en cualquier lugar del área Spectrum / waterfall de ese panadapter.
3. El panadapter está ahora activo. La sintonización, el zoom por desplazamiento y todos los controles del slice se aplican a él.

## Qué hace cada control

| Control              | Tipo                                                                                                 | Por defecto                                                                                                                                                                                                                                                                                                                                     |
|----------------------|------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Slice title          | Indicador                                                                                            | Slice A                                                                                                                                                                                                                                                                                                                                         |
| Spectrum / waterfall | Área de clic / arrastre                                                                             | —                                                                                                                                                                                                                                                                                                                                               |
| ⬈ / ↩ (pop-out/dock) | Saca el panadapter a una ventana flotante o lo acopla nuevamente; emite popOutClicked o dockClicked. | Oculto en modo single-pan. La ventana flotante no tiene marco (v0.9.0, #1922) — arrastre mediante la tira de título dentro de la aplicación, redimensione mediante el control de tamaño en la esquina inferior derecha; consulte 00-navigation.json para el marco sin marco compartido. v0.9.3: la ventana flotante hereda el tema oscuro al crearse (#2096); la geometría se guarda antes del cierre para corregir la carrera de restauración de posición (#2154). |
| □ (maximize)         | Botón de acción                                                                                      | —                                                                                                                                                                                                                                                                                                                                               |
| × (close)            | Botón de acción                                                                                      | —                                                                                                                                                                                                                                                                                                                                               |
| Sens                 | Control deslizante                                                                                   | 30                                                                                                                                                                                                                                                                                                                                              |
| 🔒P (Lock Pitch)      | Botón de alternancia                                                                                 | —                                                                                                                                                                                                                                                                                                                                               |
| 🔒S (Lock Speed)      | Botón de alternancia                                                                                 | —                                                                                                                                                                                                                                                                                                                                               |
| Lo (pitch min)       | Control deslizante                                                                                   | 500 Hz                                                                                                                                                                                                                                                                                                                                          |
| Hi (pitch max)       | Control deslizante                                                                                   | 700 Hz                                                                                                                                                                                                                                                                                                                                          |
| CPY ALL              | Botón de acción                                                                                      | —                                                                                                                                                                                                                                                                                                                                               |
| CPY VIS              | Botón de acción                                                                                      | —                                                                                                                                                                                                                                                                                                                                               |
| CLR                  | Botón de acción                                                                                      | —                                                                                                                                                                                                                                                                                                                                               |
| ✕ (close CW)         | Botón de acción                                                                                      | —                                                                                                                                                                                                                                                                                                                                               |
| CW decode text       | Campo de texto de solo lectura                                                                       | —                                                                                                                                                                                                                                                                                                                                               |

Los botones ⬈ / ↩, □ y × están ocultos en modo de panadapter único. Aparecen solo cuando está abierto más de un panadapter.

## Panel de decodificación CW

El panel de decodificación CW aparece debajo del espectro cuando está habilitado. Requiere enrutamiento de audio de PC para funcionar — se muestra un recordatorio "(requires PC Audio)" cuando el audio aún no está enrutado.

El texto decodificado se colorea por nivel de confianza:

| Color  | Umbral de costo |
|---|---|
| Verde | por debajo de 0.15 |
| Amarillo | 0.15 – por debajo de 0.35 |
| Naranja | 0.35 – por debajo de 0.60 |
| Rojo | 0.60 y superior |

El control deslizante **Sens** mapea el rango 0 – 100 a un umbral de costo de 1.0 – 0.1. Los valores más altos filtran las decodificaciones de menor confianza.

Los controles deslizantes **Lo** e **Hi** establecen el rango de búsqueda de tono. Lo se limita a no ser mayor que Hi, e Hi se limita a no ser menor que Lo.

Haga clic en **CPY ALL** para copiar todo el búfer de texto decodificado al portapapeles. Haga clic en **CPY VIS** para copiar solo el texto actualmente visible en el área de desplazamiento. Haga clic en **CLR** para borrar el búfer de decodificación. Haga clic en **✕ (close CW)** para ocultar el panel.

### Menú de clic derecho en el área de texto de decodificación CW

Al hacer clic derecho dentro del área de texto de decodificación CW se abre un menú contextual. Además de las acciones de texto estándar (Select All, Copy, etc.), el menú incluye un elemento **Clear**. Seleccionar **Clear** tiene el mismo efecto que hacer clic en el botón **CLR** — borra el búfer de decodificación.

## Consejos

- Arrastre en el área Spectrum / waterfall para sintonizar la frecuencia del slice. Desplace para ampliar el span.
- Para dar más espacio en pantalla a un panadapter sin cerrar los otros, haga clic en □ (maximize) en su barra de título. Consulte [Maximize one panadapter to fill the main area](maximize-one-panadapter-to-fill-the-main-area.md).
- Para mover un panadapter a una ventana separada, haga clic en ⬈ (pop-out). Consulte [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md).

## Relacionado

- [Maximize one panadapter to fill the main area](maximize-one-panadapter-to-fill-the-main-area.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)
- [Close an extra panadapter](close-an-extra-panadapter.md)
- [Understanding slices and VFOs](../../getting-started/concepts/understanding-slices.md)
