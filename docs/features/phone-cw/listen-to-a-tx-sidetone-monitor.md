# Escuchar el monitor de tono lateral de TX

El monitor de tono lateral de TX le permite escuchar su propio audio transmitido en los auriculares mientras opera en modos de voz. Úselo para confirmar que su audio es limpio y está al nivel correcto sin depender de un receptor separado.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en un modo de voz (SSB, AM, FM). El applet Phone/CW muestra los controles de voz únicamente cuando hay un modo de voz activo; al cambiar a CW se muestra el panel CW en su lugar.
- Abra el applet Phone/CW en el panel de applets. Si no está visible, haga clic en el botón de bandeja **P/CW** en la barra lateral derecha.

## Pasos

1. En el applet Phone/CW, localice el botón de alternancia **MON**.
2. Haga clic en **MON** para activar el monitor de tono lateral. El botón se ilumina cuando está activo.
3. Ajuste el control deslizante **Monitor volume** (0–100) para establecer el nivel del monitor en sus auriculares.
4. Para desactivar el monitor, haga clic en **MON** nuevamente.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| MON | Activa o desactiva el monitor de tono lateral de TX. | Off | On / Off | — |
| Monitor volume | Establece el volumen de reproducción del monitor de banda lateral. | — | 0–100 | — |

## Consejos

- El monitor reproduce lo que el radio está transmitiendo realmente, por lo que refleja cualquier procesamiento de voz o compresión aplicado por el control **PROC**.
- Si utiliza **PC** como fuente de micrófono, el valor de ganancia del micrófono se almacena en el lado del cliente como `PcMicGain` (valor predeterminado 50, rango 0–100) en lugar de ser reportado por el radio.

## Relacionados

- [Descripción general de Phone/CW](overview.md)
- [Ajustar la ganancia del micrófono y activar la mezcla del accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Activar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
