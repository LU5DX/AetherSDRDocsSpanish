# Tono, volumen y activación del sidetone CW en v0.9.2.1

En la v0.9.2.1 se han eliminado los controles independientes **Local STn**, **Volumen local del sidetone**, **Seguir (tono local)** y **Tono local del sidetone**. El sidetone CW de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) ahora se controla completamente mediante el mismo interruptor **Sidetone** y el deslizador **Volumen del sidetone** que controlan el monitor alimentado por DAX de la radio. El tono y la panoramización siempre se obtienen automáticamente de los ajustes `cw_pitch` y `mon_pan_cw` de la radio; no existe una anulación manual.

Si anteriormente utilizaba los controles independientes de sidetone local, consulte [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md) para conocer el flujo de trabajo actual.

## Antes de comenzar

- El slice activo debe estar en un modo CW para que el subpanel CW sea visible en el applet Phone/CW.

## Pasos

### Para activar el sidetone CW (tanto el monitor de la radio como el generador local)

1. Abra el applet Phone/CW haciendo clic en el botón de la bandeja **P/CW** en la barra lateral derecha.
2. Haga clic en **Sidetone** para activarlo. Tanto el monitor alimentado por DAX de la radio como el CwSidetoneGenerator del lado del cliente se inician simultáneamente.

### Para desactivar el sidetone CW

1. Haga clic en **Sidetone** nuevamente. Tanto el monitor de la radio como el generador local se detienen.

### Para ajustar el volumen del sidetone

1. Arrastre el deslizador **Volumen del sidetone** (0–100). El mismo valor se aplica simultáneamente al ajuste `mon_gain_cw` de la radio y al volumen del generador de sidetone local.

### Para ajustar el tono del sidetone

1. Use el cuadro de giro **Tono < / >** para incrementar el tono en pasos de 10 Hz (100–6000 Hz). El generador de sidetone local sigue este valor automáticamente; no existe un control de tono local independiente.

### Para ajustar la panoramización estéreo del sidetone

1. Arrastre el deslizador **Pan L / R (CW)** (0–100, valor predeterminado 50 = centro). El mismo valor de panoramización se envía a la radio (`mon_pan_cw`) y se aplica como panoramización de potencia constante al generador de sidetone local.
2. Haga doble clic en el deslizador para devolverlo al centro (50).

## Qué hace cada control

| Control             | Valor predeterminado | Rango válido          |
|---------------------|----------------------|-----------------------|
| **Sidetone**        | —                    | Activado / Desactivado|
| **Volumen del sidetone** | —                | 0–100                 |
| **Tono < / >**      | 600 Hz               | 100–6000 Hz (paso 10) |
| **Pan L / R (CW)**  | 50                   | 0–100                 |

## Consejos

- Debido a que el tono y la panoramización siempre se derivan de los ajustes `cw_pitch` y `mon_pan_cw` de la radio, el sidetone local y el monitor de la radio siempre están sincronizados; no se necesita sincronización manual.
- El CwSidetoneGenerator local tiene aproximadamente 10 ms de latencia, lo que lo hace adecuado para el trabajo con manípulos de alta velocidad donde la latencia de ida y vuelta DAX de la radio es notable.
- Ya no existen los ajustes `CwLocalSidetoneEnabled`, `CwLocalSidetoneVolume`, `CwLocalSidetonePitchFollow` ni `CwLocalSidetonePitchHz`. Si tiene scripts o archivos de configuración que hagan referencia a estas claves, puede eliminarlos.

## Solución de problemas

- **No se escucha sidetone aunque Sidetone esté activado** — Verifique que su dispositivo de salida de audio esté seleccionado correctamente en la configuración de audio de AetherSDR. También confirme que **Volumen del sidetone** esté por encima de 0.
- **El sidetone no se inicia en Windows hasta que pulse la radio** — Este era un problema conocido en v0.9.2 y anteriores. En v0.9.3, el flujo de sidetone se inicia inmediatamente al conectar (#2105). Si está ejecutando una versión anterior, actualice a v0.9.3 o posterior.
- **El indicador de nivel de micrófono no aparece al conectar cuando se usa PC como fuente de micrófono** — Este era un problema conocido en v0.9.2 y anteriores. En v0.9.3, el indicador aparece inmediatamente al conectar cuando la fuente de micrófono está configurada en PC (#2086). Si está ejecutando una versión anterior, actualice a v0.9.3 o posterior.
- **El tono del sidetone no coincide con lo esperado** — El tono se controla únicamente mediante el cuadro de giro **Tono < / >**. Ajústelo allí; el generador local lo seguirá inmediatamente.
- **La panoramización no tiene efecto** — Confirme que su salida de audio esté configurada para estéreo. Los dispositivos de salida mono no reflejarán los cambios de panoramización.
- **El panel Phone no se actualiza inmediatamente cuando se alterna VOX mediante un atajo de teclado** — Este era un problema conocido en v0.9.2 y anteriores. En v0.9.3, el panel Phone se actualiza instantáneamente cuando se alterna VOX mediante un atajo de teclado (#2084). Si está ejecutando una versión anterior, actualice a v0.9.3 o posterior.

## Relacionados

- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
- [Cambiar el tono CW / frecuencia del sidetone](change-cw-pitch-sidetone-frequency.md)
- Configurar la velocidad CW y el retardo de break-in
