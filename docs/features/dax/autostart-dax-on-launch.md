# Inicio automático de DAX al lanzar la aplicación

Configure AetherSDR para iniciar el puente de audio DAX automáticamente cada vez que se inicie la aplicación, de modo que los canales DAX estén listos sin necesidad de habilitarlos manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX requiere una conexión de radio activa.
- La función DAX está disponible en macOS y en sistemas Linux basados en PipeWire.

## Pasos

1. Para configurar DAX para que inicie automáticamente en cada lanzamiento, vaya a `Settings > Autostart DAX with AetherSDR` y haga clic en el elemento del menú para marcarlo. Esto guarda el parámetro `AutoStartDAX` con el valor `True`.
2. Para habilitar DAX de inmediato en la sesión actual sin reiniciar, abra el applet DAX: haga clic en el botón **DAX** de la bandeja en la barra lateral derecha.
3. En el applet DAX, haga clic en **Enable** para iniciar el puente de audio ahora. El botón se ilumina en verde cuando está activo.

Para desactivar el inicio automático, vaya nuevamente a `Settings > Autostart DAX with AetherSDR` y desmarque la opción.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| `Settings > Autostart DAX with AetherSDR` | Elemento de menú con casilla de verificación. Cuando está marcado, DAX inicia automáticamente al lanzar la aplicación. | Off | On / Off | `AutoStartDAX` |
| **Enable** (en el applet DAX) | Interruptor principal del puente de audio DAX. También lee y escribe `AutoStartDAX`. | Off | On / Off | `AutoStartDAX` |
| DAX 1 gain+meter | Medidor y control deslizante de ganancia combinados para el canal RX 1 de DAX. | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| DAX 2 gain+meter | Medidor y control deslizante de ganancia combinados para el canal RX 2 de DAX. | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| DAX 3 gain+meter | Medidor y control deslizante de ganancia combinados para el canal RX 3 de DAX. | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| DAX 4 gain+meter | Medidor y control deslizante de ganancia combinados para el canal RX 4 de DAX. | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| TX gain+meter | Medidor y control deslizante de ganancia combinados para el flujo TX de DAX. | 0.5 | 0.0–1.0 | `DaxTxGain` |

## Consejos

- El botón **Enable** en el applet DAX y `Settings > Autostart DAX with AetherSDR` escriben el mismo parámetro `AutoStartDAX`. Hacer clic en **Enable** en el applet equivale a marcar el elemento del menú para los lanzamientos futuros.
- Los valores de ganancia de todos los canales se guardan de inmediato al cambiarlos. Si ajusta las ganancias en una sesión, se restaurarán en la siguiente.

## Solución de problemas

- **El applet DAX no es visible** — El applet está oculto de forma predeterminada. Haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para mostrarlo.
- **`Settings > Autostart DAX with AetherSDR` no aparece en el menú** — Este elemento solo aparece en plataformas compatibles (macOS y Linux basado en PipeWire). No está disponible en todas las configuraciones.
- **DAX inicia pero no pasa audio** — Verifique que haya un slice asignado a un canal DAX. El indicador de estado de cada canal muestra `—` cuando no hay ningún slice enrutado hacia él, o `Slice A`–`Slice H` cuando hay uno asignado. Consulte [Cómo ver qué slice está usando cada canal DAX en este momento](see-which-slice-is-currently-using-each-dax-channel.md).

## Temas relacionados

- [Descripción general del audio DAX](overview.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando cada canal DAX en este momento](see-which-slice-is-currently-using-each-dax-channel.md)
