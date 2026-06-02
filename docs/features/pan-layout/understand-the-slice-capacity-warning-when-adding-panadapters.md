# Comprender la advertencia de capacidad de slices al agregar panadaptadores

Cuando solicita una disposición que necesita más panadaptadores de los que su radio puede admitir, AetherSDR bloquea el cambio y explica el motivo. Esta página describe qué significa la advertencia y cómo trabajar dentro del límite de slices de su radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El cuadro de diálogo **Panadapter Layout** requiere una conexión activa a la radio.
- Sepa cuántos slices admite su radio. El mensaje de advertencia incluye tanto el nombre del modelo como la cantidad de slices.

## Pasos

1. Haga clic derecho en el área del panadaptador para abrir el cuadro de diálogo **Panadapter Layout**.
2. Inspeccione la cuadrícula de disposiciones. Cualquier disposición cuya cantidad de panadaptadores supere el límite de slices de la radio se muestra con un cursor de prohibición y no se puede hacer clic en ella.
3. Si hace clic en un botón de disposición que está dentro del límite pero los slices de la radio ya están todos en uso, AetherSDR cancela el cambio y muestra un mensaje en la barra de estado:

   ```
   Slice capacity is full; cannot add another panadapter (<model> supports <N> slices)
   ```

   donde `<model>` es el modelo de su radio y `<N>` es su límite de slices.
4. Para continuar, primero reduzca la cantidad de slices activos en la radio, luego regrese al cuadro de diálogo **Panadapter Layout** y seleccione la disposición deseada.
5. Para cerrar el cuadro de diálogo sin realizar ningún cambio, haga clic en **Cancel**.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de disposición | Haga clic en una miniatura de vista previa para seleccionar una disposición. El cuadro de diálogo se cierra y la disposición se aplica. | Las miniaturas que requieren más panadaptadores que el límite de slices de la radio muestran un cursor de prohibición y están deshabilitadas. Si los slices ya están al máximo de capacidad cuando se aplica una disposición de apariencia válida, el cambio se cancela y aparece la advertencia en la barra de estado. Se guarda como `PanLayout`. |
| **Cancel** | Cierra el cuadro de diálogo sin cambiar la disposición actual. | No se modifican ajustes. |

## Consejos

- Las miniaturas de disposición deshabilitadas le indican de un vistazo qué disposiciones están fuera del alcance de su radio. No necesita probarlas para descubrirlo.
- La advertencia en la barra de estado puede aparecer incluso para disposiciones cuya miniatura no estaba visualmente deshabilitada, si otro software u otro cliente ha consumido slices desde que se abrió el cuadro de diálogo.
- La disposición actualmente activa se resalta con un borde distintivo en la cuadrícula, para que pueda ver siempre qué disposición está en efecto.

## Solución de problemas

- **Una miniatura de disposición aparece deshabilitada aunque la radio debería admitir suficientes slices** — El cuadro de diálogo calcula la cantidad máxima de panadaptadores a partir del límite de slices informado por la radio en el momento en que se abre. Si la conexión se interrumpió o el límite aún no se informó, es posible que algunas miniaturas aparezcan deshabilitadas incorrectamente. Cierre el cuadro de diálogo, verifique que la conexión de la radio esté activa y vuelva a abrirlo.
- **Apareció la advertencia en la barra de estado, pero esperaba que esa disposición estuviera permitida** — Otro cliente o un slice existente en la radio puede estar consumiendo la capacidad restante. Verifique si hay slices activos en otros clientes SDR conectados a la misma radio, cierre los que no sean necesarios y vuelva a intentarlo.

## Relacionados

- [Panadapter Layout overview](overview.md)
- [Preview and pick among the 10 layout variants](preview-and-pick-among-the-10-layout-variants.md)
- [Switch to a single full-width panadapter](switch-to-a-single-full-width-panadapter.md)
