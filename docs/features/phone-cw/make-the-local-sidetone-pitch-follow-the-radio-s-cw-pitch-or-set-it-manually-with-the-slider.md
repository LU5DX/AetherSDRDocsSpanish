# Tono lateral CW, volumen y activación en v0.9.2.1

En v0.9.2.1 se han eliminado los controles separados **Local STn**, **Volumen de tono lateral local**, **Seguir (tono local)** y **Tono lateral local**. El tono lateral CW de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) ahora está controlado completamente por el mismo interruptor **Sidetone** y el deslizador **Sidetone volume** que controlan el monitor alimentado por DAX de la radio. El tono y el paneo siempre se toman automáticamente de la configuración `cw_pitch` y `mon_pan_cw` de la radio; no hay anulación manual.

Si anteriormente usaba los controles de tono lateral local separados, consulte [Listen to a TX sidetone monitor](listen-to-a-tx-sidetone-monitor.md) para el flujo de trabajo actual.

## Antes de comenzar

- El slice activo debe estar en un modo CW para que el subpanel CW sea visible en la ventana Phone/CW applet.

## Pasos

### Para activar el tono lateral CW (tanto el monitor de radio como el generador local)

1. Abra la ventana Phone/CW applet haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha.
2. Haga clic en **Sidetone** para activarlo. Tanto el monitor alimentado por DAX de la radio como el CwSidetoneGenerator del lado del cliente se inician simultáneamente.

### Para desactivar el tono lateral CW

1. Haga clic en **Sidetone** de nuevo. Tanto el monitor de radio como el generador local se detienen.

### Para ajustar el volumen del tono lateral

1. Arrastre el deslizador **Sidetone volume** (0–100). El mismo valor se aplica a la configuración `mon_gain_cw` de la radio y al volumen del generador de tono lateral local simultáneamente.

### Para ajustar el tono del tono lateral

1. Use el cuadro giratorio **Pitch < / >** para aumentar el tono en incrementos de 10 Hz (100–6000 Hz). El generador de tono lateral local sigue este valor automáticamente; no hay control de tono local separado.

### Para ajustar el paneo estéreo del tono lateral

1. Arrastre el deslizador **L / R pan (CW)** (0–100, predeterminado 50 = centro). El mismo valor de paneo se envía a la radio (`mon_pan_cw`) y se aplica como paneo de potencia constante al generador de tono lateral local.
2. Haga doble clic en el deslizador para devolverlo al centro (50).

## Qué hace cada control

| Control             | Predeterminado | Rango válido          |
|---------------------|---------|-----------------------|
| **Sidetone**        | —       | Activado / Desactivado|
| **Sidetone volume** | —       | 0–100                 |
| **Pitch < / >**     | 600 Hz  | 100–6000 Hz (paso 10) |
| **L / R pan (CW)**  | 50      | 0–100                 |

## Consejos

- Debido a que el tono y el paneo siempre se derivan de la configuración `cw_pitch` y `mon_pan_cw` de la radio, el tono lateral local y el monitor de radio siempre están de acuerdo — no se necesita sincronización manual.
- El CwSidetoneGenerator local tiene aproximadamente 10 ms de latencia, lo que lo hace adecuado para trabajo de paleta de alta velocidad donde la latencia DAX de ida y vuelta de la radio es notoria.
- Ya no existen configuraciones `CwLocalSidetoneEnabled`, `CwLocalSidetoneVolume`, `CwLocalSidetonePitchFollow` o `CwLocalSidetonePitchHz`. Si tiene scripts o archivos de configuración que hagan referencia a estas claves, pueden eliminarse.

## Resolución de problemas

- **No se escucha tono lateral aunque Sidetone esté activado** — Verifique que su dispositivo de salida de audio esté seleccionado correctamente en la configuración de audio de AetherSDR. También confirme que **Sidetone volume** está por encima de 0.
- **El tono lateral no comienza en Windows hasta que activa la radio** — Este era un problema conocido en v0.9.2 y anteriores. En v0.9.3 el flujo de tono lateral comienza inmediatamente al conectarse (#2105). Si ejecuta una versión anterior, actualice a v0.9.3 o posterior.
- **El indicador de nivel de micrófono no aparece al conectarse cuando se usa PC como fuente de micrófono** — Este era un problema conocido en v0.9.2 y anteriores. En v0.9.3 el indicador aparece inmediatamente al conectarse cuando la fuente de micrófono se establece en PC (#2086). Si ejecuta una versión anterior, actualice a v0.9.3 o posterior.
- **El tono del tono lateral no coincide con lo que espera** — El tono está controlado únicamente por el cuadro giratorio **Pitch < / >**. Ajústelo allí; el generador local seguirá inmediatamente.
- **El paneo no tiene efecto** — Confirme que su salida de audio está configurada para estéreo. Los dispositivos de salida mono no reflejarán cambios de paneo.
- **El panel Phone no se actualiza inmediatamente cuando VOX se alterna mediante el atajo de teclado** — Este era un problema conocido en v0.9.2 y anteriores. En v0.9.3 el panel Phone se actualiza instantáneamente cuando VOX se alterna mediante el atajo de teclado (#2084). Si ejecuta una versión anterior, actualice a v0.9.3 o posterior.

## Relacionado

- [Listen to a TX sidetone monitor](listen-to-a-tx-sidetone-monitor.md)
- [Change CW pitch / sidetone frequency](change-cw-pitch-sidetone-frequency.md)
- [Set CW speed and break-in delay](set-cw-speed-and-break-in-delay.md)
