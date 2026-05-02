# Establecer un borde de filtro personalizado desde el panel VFO

Los botones de presets de filtro del panel VFO permiten guardar y recuperar anchos de filtro rápidamente. Al hacer clic derecho en un botón de preset, se abre un diálogo donde puede establecer valores exactos de borde inferior y superior para ese slot. Use esta función cuando los anchos de preset integrados no se ajusten a sus necesidades operativas.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO debe estar abierto. Si no es visible, haga clic en la bandera marcadora VFO en la pantalla del espectro correspondiente al slice que desea ajustar.
- El panel VFO no debe estar contraído. Si muestra únicamente una franja de frecuencia, haga clic en cualquier parte de él para expandirlo.
- Abra la pestaña **Mode** dentro del panel VFO para que los botones de preset de filtro sean visibles.

## Pasos

1. Haga clic en la bandera marcadora VFO en la pantalla del espectro para abrir el panel VFO del slice de destino.
2. En el panel VFO, haga clic en la pestaña **Mode** para mostrar el selector de modo y los botones de preset de filtro.
3. Haga clic derecho en el botón de preset de filtro cuyos bordes desea personalizar. Aparece un menú contextual o diálogo.
4. Ingrese los valores deseados de borde inferior y borde superior en los campos proporcionados.
5. Confirme la entrada para guardar los bordes personalizados en ese slot de preset.

El botón de preset aplica ahora sus bordes de filtro personalizados al hacer clic en él. Los valores se conservan en `FilterPresets`.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Botones de preset de filtro (pestaña Mode) | Aplica un preset de ancho de filtro guardado al hacer clic. Haga clic derecho para guardar el ancho de filtro actual o establecer bordes inferior/superior personalizados para ese slot. | — | `FilterPresets` |
| Etiqueta de ancho de filtro | Muestra el ancho de banda de filtro actual. Haga clic para recorrer los botones de preset de filtro en la pestaña Mode. | — | — |
| Botón de bordes de filtro | Activa o desactiva las líneas de borde del filtro en la pantalla de pasabanda del espectro. | visible | `Slice{N}_FilterEdgesHidden` |

## Consejos

- Para verificar los bordes de filtro activos en el espectro, confirme que el botón de bordes de filtro se encuentre en su estado predeterminado de visible. Si las líneas de borde están ocultas, presione el botón de bordes de filtro para hacerlas visibles nuevamente.
- Hacer clic derecho en un botón de preset guarda el ancho de filtro *actual* en ese slot como alternativa a ingresar los valores de borde manualmente. Use esto para capturar rápidamente un filtro que ya haya ajustado.

## Relacionados

- [Aplicar un preset de ancho de filtro desde el panel VFO](apply-a-filter-width-preset-from-the-vfo-panel.md)
- [Ocultar o mostrar las líneas de borde de filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Cambiar el modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
