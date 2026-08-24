# Buscar dentro de un tema de ayuda sin conexión con Buscar

Use el campo Buscar para buscar texto dentro de cualquier tema de ayuda sin conexión de AetherSDR, sin necesidad de una conexión a internet.

## Antes de comenzar

- Abra cualquier tema de ayuda desde el menú **Help** (por ejemplo, **Getting Started…**, **AetherSDR Help…**).

## Pasos

1. Presione **Ctrl+F** para enfocar el campo Buscar. El campo tiene el texto de marcador de posición "Subject or term".
2. Escriba su término de búsqueda. Los botones **Next** y **Previous** se habilitan cuando el campo no está vacío.
3. Para saltar a la siguiente coincidencia, presione **Enter** o haga clic en **Next**.
4. Para saltar a la coincidencia anterior, presione **Shift+Enter** o haga clic en **Previous**.

La búsqueda se ajusta automáticamente: cuando llega al final del documento, presionar **Next** continúa desde el principio, y viceversa con **Previous**. Un mensaje de estado (por ejemplo, "Wrapped to top" o "No matches") aparece junto a los botones.

## Qué hace cada control

| Control | Etiqueta / Propósito | Comportamiento |
|---------|----------------------|----------------|
| Campo Buscar | "Find:" con marcador de posición "Subject or term" | Escriba su término de búsqueda. Incluye un botón de borrado (X) para restablecer. |
| Botón Next | "Next" | Salta a la siguiente coincidencia (se ajusta del final al principio). Deshabilitado cuando el campo está vacío. |
| Botón Previous | "Previous" | Salta a la coincidencia anterior (se ajusta del principio al final). Deshabilitado cuando el campo está vacío. |
| Estado de Buscar | (indicador) | Muestra "No matches" (con borde rojo en el campo) o "Wrapped to top/bottom". |

## Consejos

- **Ctrl+F** activa el campo Buscar y selecciona cualquier texto existente, de modo que puede escribir de inmediato un nuevo término.
- ¿La búsqueda distingue entre mayúsculas y minúsculas? No: el `find()` de Qt por defecto no distingue mayúsculas de minúsculas y coincide con cualquier aparición sin importar la capitalización.
- Para borrar la búsqueda y ocultar el resaltado de coincidencias, haga clic en el botón X del campo Buscar o elimine el texto y presione Escape.

## Solución de problemas

- **Aparece "No matches" aunque la palabra sea visible** — La coincidencia puede estar dentro de un bloque de código o un encabezado con un estilo diferente. Pruebe con un término más amplio. La búsqueda busca subcadenas, por lo que "noise" coincidirá con "noise cancellation".
- **El campo Buscar desaparece al cerrar el diálogo** — Cada tema de ayuda se abre en su propio diálogo y el estado de búsqueda no se conserva. Vuelva a abrir el tema y busque nuevamente.

## Relacionados

- [Abrir la guía de inicio incluida](open-bundled-getting-started-guide.md)
- [Leer el documento de ayuda completo de AetherSDR](read-the-full-aethersdr-help-document.md)
