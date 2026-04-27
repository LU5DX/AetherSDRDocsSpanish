# Comprender la advertencia de capacidad de slice al agregar panadapters

Cuando solicita una disposición que requiere más panadapters de los que su radio puede admitir, AetherSDR bloquea el cambio y explica el motivo. Esta página describe qué significa la advertencia y cómo trabajar dentro del límite de slices (canales de recepción independientes) de su radio.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El diálogo **Panadapter Layout** requiere una conexión de radio activa.
- Conozca cuántos slices admite su radio. El mensaje de advertencia incluye tanto el nombre del modelo como la cantidad de slices.

## Pasos

1. Haga clic derecho en el área del panadapter para abrir el diálogo **Panadapter Layout**.
2. Inspeccione la cuadrícula de disposiciones. Toda disposición cuyo número de panadapters supere el límite de slices del radio se muestra con un cursor de prohibición y no puede seleccionarse.
3. Si hace clic en un botón de disposición que está dentro del límite, pero todos los slices del radio ya están en uso, AetherSDR cancela el cambio y muestra un mensaje en la barra de estado:

   ```
   Slice capacity is full; cannot add another panadapter (<model> supports <N> slices)
   ```

   donde `<model>` es el modelo de su radio y `<N>` es su límite de slices.
4. Para continuar, primero reduzca el número de slices activos en el radio y, a continuación, regrese al diálogo **Panadapter Layout** y seleccione la disposición deseada.
5. Para cerrar el diálogo sin realizar ningún cambio, haga clic en **Cancel**.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de disposición | Haga clic en una vista previa para seleccionar una disposición. El diálogo se cierra y la disposición se aplica. | Las vistas que requieren más panadapters que el límite de slices del radio muestran un cursor de prohibición y están deshabilitadas. Si los slices ya están al máximo cuando se aplica una disposición de apariencia válida, el cambio se cancela y aparece la advertencia en la barra de estado. Se guarda como `PanLayout`. |
| **Cancel** | Cierra el diálogo sin modificar la disposición actual. | No se modifica ninguna configuración. |

## Consejos

- Las vistas de disposición deshabilitadas le indican de un vistazo qué disposiciones están fuera del alcance de su radio. No es necesario intentarlas para averiguarlo.
- La advertencia en la barra de estado puede aparecer incluso para disposiciones cuya vista no estaba visualmente deshabilitada, si otro software u otro cliente ha consumido slices desde que se abrió el diálogo.
- La disposición actualmente activa aparece resaltada con un borde distintivo en la cuadrícula, de modo que siempre puede ver qué disposición está en uso.

## Solución de problemas

- **Una vista de disposición aparece deshabilitada aunque el radio debería admitir suficientes slices** — El diálogo calcula el número máximo de panadapters a partir del límite de slices reportado por el radio en el momento en que se abre el diálogo. Si la conexión se interrumpió o el límite aún no se había reportado, algunas vistas pueden aparecer deshabilitadas incorrectamente. Cierre el diálogo, verifique que la conexión de radio esté activa y vuelva a abrirlo.
- **Apareció la advertencia en la barra de estado, pero esperaba que esa disposición estuviera permitida** — Otro cliente o un slice existente en el radio puede estar consumiendo la capacidad restante. Compruebe si hay slices activos en otros clientes SDR conectados al mismo radio, cierre los que no sean necesarios y vuelva a intentarlo.

## Temas relacionados

- [Descripción general de Panadapter Layout](overview.md)
- [Vista previa y selección entre las 10 variantes de disposición](preview-and-pick-among-the-10-layout-variants.md)
- [Cambiar a un único panadapter de ancho completo](switch-to-a-single-full-width-panadapter.md)
