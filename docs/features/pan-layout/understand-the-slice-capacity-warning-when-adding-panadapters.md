# Comprender la advertencia de capacidad de slices al agregar panadapters

Cuando solicita un diseño que necesita más panadapters de los que su radio puede admitir, AetherSDR bloquea el cambio y explica el motivo. Esta página describe qué significa la advertencia y cómo trabajar dentro del límite de slices (canales de recepción independientes) de su radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo **Panadapter Layout** requiere una conexión de radio activa.
- Conozca cuántos slices admite su radio. El mensaje de advertencia incluye tanto el nombre del modelo como la cantidad de slices.

## Pasos

1. Haga clic derecho en el área del panadapter para abrir el diálogo **Panadapter Layout**.
2. Examine la cuadrícula de diseños. Cualquier diseño cuya cantidad de panadapters supere el límite de slices de la radio se muestra con un cursor de acceso prohibido y no se puede seleccionar.
3. Si hace clic en un botón de diseño que está dentro del límite, pero los slices de la radio ya están todos en uso, AetherSDR cancela el cambio y muestra un mensaje en la barra de estado:

   ```
   Slice capacity is full; cannot add another panadapter (<model> supports <N> slices)
   ```

   donde `<model>` es el modelo de su radio y `<N>` es su límite de slices.
4. Para continuar, primero reduzca el número de slices activos en la radio y luego regrese al diálogo **Panadapter Layout** para seleccionar el diseño deseado.
5. Para cerrar el diálogo sin realizar ningún cambio, haga clic en **Cancel**.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de diseño | Haga clic en una vista previa para seleccionar una disposición. El diálogo se cierra y el diseño se aplica. | Las vistas que requieren más panadapters que el límite de slices de la radio muestran un cursor de acceso prohibido y están deshabilitadas. Si los slices ya están al límite cuando se aplica un diseño aparentemente válido, el cambio se cancela y aparece la advertencia en la barra de estado. Se guarda como `PanLayout`. |
| **Cancel** | Cierra el diálogo sin cambiar el diseño actual. | No se modifica ninguna configuración. |

## Consejos

- Las vistas de diseño deshabilitadas le indican de un vistazo qué disposiciones están fuera del alcance de su radio. No es necesario intentarlas para averiguarlo.
- La advertencia en la barra de estado puede aparecer incluso para diseños cuya vista no estaba visualmente deshabilitada, si otro software u otro cliente ha consumido slices desde que se abrió el diálogo.
- El diseño activo en ese momento aparece resaltado con un borde distintivo en la cuadrícula, para que siempre pueda ver qué disposición está en efecto.

## Solución de problemas

- **Una vista de diseño aparece deshabilitada aunque la radio debería admitir suficientes slices** — El diálogo calcula la cantidad máxima de panadapters a partir del límite de slices reportado por la radio en el momento en que se abre el diálogo. Si la conexión se interrumpió o el límite aún no se había reportado, algunas vistas pueden aparecer deshabilitadas incorrectamente. Cierre el diálogo, verifique que la conexión de radio esté activa y vuelva a abrirlo.
- **Apareció la advertencia en la barra de estado, pero esperaba que ese diseño fuera válido** — Otro cliente o un slice existente en la radio puede estar consumiendo la capacidad restante. Verifique si hay slices activos en otros clientes SDR conectados a la misma radio, cierre los que no sean necesarios y vuelva a intentarlo.

## Relacionados

- [Descripción general de Panadapter Layout](overview.md)
- [Vista previa y selección entre las 10 variantes de diseño](preview-and-pick-among-the-10-layout-variants.md)
- [Cambiar a un único panadapter de ancho completo](switch-to-a-single-full-width-panadapter.md)
