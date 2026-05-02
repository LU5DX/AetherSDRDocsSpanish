# Ocultar o mostrar las líneas de borde del filtro en el espectro

El panel VFO ofrece un interruptor por slice para ocultar o mostrar las líneas verticales que marcan los bordes de la banda pasante del filtro de recepción en la pantalla del espectro. Ocultarlas reduce el desorden visual cuando se desea una vista del panadapter más limpia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice que desea ajustar debe tener un marcador VFO visible en la pantalla del espectro.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro correspondiente al slice deseado. El panel VFO se abre anclado al marcador.
2. Localice el botón **Filter edges button** en el panel VFO.
3. Haga clic en **Filter edges button** para desactivar las líneas de borde del filtro. Haga clic de nuevo para restaurarlas.

El estado se guarda de inmediato. Cuando vuelva a abrir AetherSDR, la configuración se restaura al estado en que la dejó para ese slice.

## Qué hace cada control

| Control | Valor predeterminado | Configuración persistente |
|---|---|---|
| **Filter edges button** | Mostradas (bordes visibles) | `Slice{N}_FilterEdgesHidden` |

`{N}` es el número del slice. Cada slice almacena su propio valor de forma independiente.

## Consejos

- La configuración es por slice. Ocultar los bordes del filtro en el slice 0 no afecta al slice 1 ni a ningún otro slice.
- Si el panel VFO está contraído en la vista de solo frecuencia, expándalo primero haciendo clic en la barra contraída para acceder al **Filter edges button**.

## Relacionados

- [Cambiar el grosor de la línea del marcador VFO](change-the-vfo-marker-line-thickness.md)
- [Contraer el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Descripción general del panel VFO](overview.md)
