# Confirme la responsabilidad del operador antes de ejecutar el barrido de ROE de antena

Antes de que el barrido de ROE de antena transmita, debe confirmar que comprende su responsabilidad como operador. Esta página le muestra cómo aceptar la exención de responsabilidad o cancelar el barrido.

## Antes de comenzar

- El barrido de ROE de antena debe iniciarse desde el menú contextual del panadapter o desde la acción de barrido de ROE de la ventana principal (MainWindow).
- Debe poseer una licencia de radioaficionado válida que permita las transmisiones que realizará el barrido.

## Pasos

1. Inicie el barrido de ROE de antena desde el menú contextual del panadapter o desde la acción de barrido de ROE de la ventana principal (MainWindow).
2. Lea el texto de la exención de responsabilidad del operador.
3. (Opcional) Marque la casilla **Remember my answer** para omitir este diálogo en futuros barridos.
4. Haga clic en **I am licensed to use this feature** para aceptar la exención de responsabilidad y proceder con el barrido.  
   — O —  
   Haga clic en **Cancel** para rechazar la exención de responsabilidad y abortar el barrido.

## Solución de problemas

- **El diálogo no aparece en barridos posteriores** — La casilla **Remember my answer** se marcó durante una confirmación anterior. El ajuste `SwrSweepLicenseConfirmed` está almacenado como `"True"`. Para volver a mostrar el diálogo, borre el ajuste editando el archivo de configuración en `~/.config/AetherSDR/AetherSDR.settings` y cambiando `SwrSweepLicenseConfirmed` a `"False"`.

## Relacionados

- [Recuerda la confirmación para que el diálogo no se muestre en barridos posteriores](remembers-confirmation-so-the-dialog-does-not-show-on-subsequent-sweeps.md)
