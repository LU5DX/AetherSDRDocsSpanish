# Comprender la advertencia de capacidad de slices al agregar panadaptadores

Cuando solicita una disposición que necesita más panadaptadores de los que su radio puede soportar, AetherSDR bloquea el cambio y explica el motivo. Esta página describe qué significa la advertencia y cómo trabajar dentro del límite de slices de su radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El cuadro de diálogo Panadapter Layout requiere una conexión activa con la radio.
- Sepa cuántos slices soporta su radio. El mensaje de advertencia incluye tanto el nombre del modelo como la cantidad de slices.

## Pasos

1. Haga clic derecho en el área del panadaptador para abrir el cuadro de diálogo **Panadapter Layout**.
2. Inspeccione la cuadrícula de disposiciones. Cualquier disposición cuyo número de panadaptadores exceda el límite de slices de la radio se muestra con un cursor prohibido y no se puede hacer clic en ella.
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
| Botones de disposición | Haga clic en un mosaico de vista previa para seleccionar una disposición. El cuadro de diálogo se cierra y la disposición se aplica. | Los mosaicos que requieren más panadaptadores que el límite de slices de la radio muestran un cursor prohibido y están deshabilitados. Si los slices ya están al máximo de capacidad cuando se aplica una disposición de apariencia válida, el cambio se cancela y aparece la advertencia en la barra de estado. Se persiste como `PanLayout`. |
| **Cancel** | Cierra el cuadro de diálogo sin cambiar la disposición actual. | No se modifican ajustes. |

## Consejos

- Los mosaicos de disposición deshabilitados le indican de un vistazo qué disposiciones están fuera del alcance de su radio. No necesita probarlas para averiguarlo.
- La advertencia de la barra de estado puede aparecer incluso para disposiciones cuyo mosaico no estaba deshabilitado visualmente, si otro software u otro cliente ha consumido slices desde que se abrió el cuadro de diálogo.
- La disposición actualmente activa se resalta con un borde distintivo en la cuadrícula, para que siempre pueda ver qué disposición está en efecto.

## Solución de problemas

- **Un mosaico de disposición aparece deshabilitado aunque la radio debería soportar suficientes slices** — El cuadro de diálogo calcula el número máximo de panadaptadores a partir del límite de slices informado por la radio en el momento en que se abre. Si la conexión se interrumpió o el límite aún no se informó, algunos mosaicos pueden aparecer deshabilitados incorrectamente. Cierre el cuadro de diálogo, verifique que la conexión con la radio esté activa y vuelva a abrirlo.
- **Apareció la advertencia de la barra de estado, pero esperaba que esa disposición estuviera permitida** — Otro cliente o un slice existente en la radio puede estar consumiendo la capacidad restante. Verifique si hay slices activos en otros clientes SDR conectados a la misma radio, cierre los que no sean necesarios e intente de nuevo.

## Relacionado

- [Panadapter Layout overview](overview.md)
- [Preview and pick among the 10 layout variants](preview-and-pick-among-the-10-layout-variants.md)
- [Switch to a single full-width panadapter](switch-to-a-single-full-width-panadapter.md)
