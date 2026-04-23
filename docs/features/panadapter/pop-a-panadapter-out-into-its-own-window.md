# Extraer un panadapter a su propia ventana

Mueva un panadapter a una ventana flotante para posicionarlo libremente en un segundo monitor o redimensionarlo de forma independiente del diseño principal de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El botón de extracción solo está disponible cuando hay una conexión de radio activa.
- Debe tener más de un panadapter abierto. En el modo de panel único, los botones de la barra de título (incluido el botón de extracción) están ocultos.

## Pasos

1. Localice el panadapter que desea flotar. Su barra de título se encuentra en el borde superior y muestra una etiqueta de slice (ranura de frecuencia) como "Slice A".
2. Haga clic en el botón **⬈** de la barra de título. El panadapter se desprende en una ventana flotante separada.
3. Arrastre o redimensione la ventana flotante según sea necesario usando los controles de ventana normales de su sistema operativo.
4. Para acoplar el panadapter de vuelta en la ventana principal, haga clic en el botón **↩** que aparece en la barra de título de la ventana flotante.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Notas |
|---|---|---|---|
| **⬈ / ↩ (extraer/acoplar)** | Extrae el panadapter a una ventana flotante; cuando está flotando, cambia a ↩ para acoplarlo de nuevo. | — | Oculto en modo de panel único. |
| **□ (maximizar)** | Maximiza este panadapter para llenar el área principal en un diseño de múltiples paneles. | — | Oculto en modo de panel único. |
| **× (cerrar)** | Cierra este panadapter. | — | Oculto en modo de panel único. |
| **Título del slice** | Indicador que muestra qué slice está vinculado a este panadapter (p. ej., "Slice A"). | Slice A | Solo lectura; va desde Slice A hasta Slice H. |

## Consejos

- El botón **□ (maximizar)** expande el panadapter dentro de la ventana principal sin hacerlo flotar. Use la extracción en su lugar si desea el panadapter en una pantalla separada.
- Puede extraer múltiples panadapters simultáneamente, uno por ventana flotante.

## Relacionado

- [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multislice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Descripción general del panadapter](overview.md)
