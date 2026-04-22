# Cambiar entre la vista de EQ de RX y TX

El applet ClientEqApplet muestra la curva de EQ y el analizador en vivo para una ruta de audio a la vez. Use las pestañas RX y TX para elegir qué ruta —recepción o transmisión— se muestra en el área de curva.

## Antes de comenzar

- El applet ClientEqApplet (etiquetado "CEQ") debe ser visible en el panel de applets. Permanece oculto hasta que la etapa de EQ se habilite mediante el widget CHAIN o el editor flotante.

## Pasos

1. Localice el subcontenedor "CEQ" dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. Haga clic en **RX** para mostrar la curva de EQ y el analizador de la ruta de recepción. Esta pestaña está seleccionada de forma predeterminada.
3. Haga clic en **TX** para mostrar la curva de EQ y el analizador de la ruta de transmisión.

El área de curva se actualiza de inmediato para mostrar la respuesta de EQ combinada y la superposición de FFT en vivo para la ruta seleccionada. Solo una pestaña puede estar activa a la vez.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| **RX** | Pestaña | Seleccionada | Selecciona la ruta de recepción; vincula el área de curva a la instancia de EQ de RX. | — |
| **TX** | Pestaña | No seleccionada | Selecciona la ruta de transmisión; vincula el área de curva a la instancia de EQ de TX. | — |
| Analizador / área de curva | Indicador (solo visualización) | — | 110 px de alto. Muestra una cuadrícula de frecuencia, la respuesta de EQ combinada para la ruta seleccionada y una superposición de analizador FFT en vivo. La edición se realiza en el editor flotante, no aquí. | — |

Configuraciones persistidas que almacenan el estado de cada ruta: `ClientEqRxEnabled`, `ClientEqTxEnabled`, `ClientEqRxBands`, `ClientEqTxBands`.

## Consejos

- Cambiar de pestaña no afecta si el EQ de alguna ruta está habilitado o puenteado (bypass) — solo cambia qué ruta se muestra.
- Para editar las bandas de la ruta mostrada actualmente, abra el editor flotante. Consulte [Abrir el editor flotante para agregar, eliminar o ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md).

## Relacionado

- [Descripción general del EQ paramétrico (cliente)](overview.md)
- [Abrir el editor flotante para agregar, eliminar o ajustar bandas](open-the-floating-editor-to-add-remove-tune-bands.md)
- [Ver el espectro en vivo de la ruta seleccionada](see-the-live-spectrum-of-the-selected-path.md)
- [Puentear la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
