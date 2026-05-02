# Tono lateral CW: tono de audio, volumen y activación en v0.9.2.1

En v0.9.2.1 se han eliminado los controles independientes **Local STn**, **Local sidetone volume**, **Follow (local pitch)** y **Local sidetone pitch**. El tono lateral CW de baja latencia en el lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) ahora está controlado íntegramente por el mismo botón **Sidetone** y el deslizador **Sidetone volume** que controlan el monitor alimentado por DAX del radio. El tono de audio y el paneo se toman siempre de forma automática desde los ajustes `cw_pitch` y `mon_pan_cw` del radio; no existe anulación manual.

Si anteriormente usaba los controles de tono lateral local independientes, consulte [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md) para conocer el flujo de trabajo actual.

## Antes de comenzar

- La slice activa debe estar en un modo CW para que el subpanel CW sea visible en el applet Phone/CW.

## Pasos

### Para activar el tono lateral CW (monitor del radio y generador local)

1. Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha.
2. Haga clic en **Sidetone** para activarlo. El monitor alimentado por DAX del radio y el CwSidetoneGenerator del lado del cliente se inician simultáneamente.

### Para desactivar el tono lateral CW

1. Haga clic en **Sidetone** nuevamente. Tanto el monitor del radio como el generador local se detienen.

### Para ajustar el volumen del tono lateral

1. Arrastre el deslizador **Sidetone volume** (0–100). El mismo valor se aplica simultáneamente al ajuste `mon_gain_cw` del radio y al volumen del generador de tono lateral local.

### Para ajustar el tono de audio del tono lateral

1. Use el selector **Pitch < / >** para modificar el tono en incrementos de 10 Hz (100–6000 Hz). El generador de tono lateral local sigue este valor automáticamente; no existe un control de tono local independiente.

### Para ajustar el paneo estéreo del tono lateral

1. Arrastre el deslizador **L / R pan (CW)** (0–100, valor predeterminado 50 = centro). El mismo valor de paneo se envía al radio (`mon_pan_cw`) y se aplica como paneo de potencia constante al generador de tono lateral local.
2. Haga doble clic en el deslizador para restablecerlo al centro (50).

## Qué hace cada control

| Control             | Valor predeterminado | Rango válido          |
|---------------------|----------------------|-----------------------|
| **Sidetone**        | —                    | On / Off              |
| **Sidetone volume** | —                    | 0–100                 |
| **Pitch < / >**     | 600 Hz               | 100–6000 Hz (paso 10) |
| **L / R pan (CW)**  | 50                   | 0–100                 |

## Consejos

- Dado que el tono de audio y el paneo se derivan siempre de los ajustes `cw_pitch` y `mon_pan_cw` del radio, el tono lateral local y el monitor del radio están siempre sincronizados; no se requiere sincronización manual.
- El CwSidetoneGenerator local tiene aproximadamente 10 ms de latencia, lo que lo hace adecuado para trabajo con paleta a alta velocidad donde la latencia de ida y vuelta del DAX del radio es perceptible.
- Ya no existen los ajustes `CwLocalSidetoneEnabled`, `CwLocalSidetoneVolume`, `CwLocalSidetonePitchFollow` ni `CwLocalSidetonePitchHz`. Si tiene scripts o archivos de configuración que hagan referencia a estas claves, pueden eliminarse.

## Solución de problemas

- **No se escucha tono lateral aunque Sidetone esté activado** — Verifique que el dispositivo de salida de audio esté seleccionado correctamente en los ajustes de audio de AetherSDR. Confirme también que **Sidetone volume** sea mayor que 0.
- **El tono lateral no se inicia en Windows hasta que se activa el radio** — Este era un problema conocido en v0.9.2 y versiones anteriores. En v0.9.3 la transmisión del tono lateral comienza inmediatamente al conectarse (#2105). Si está usando una versión anterior, actualice a v0.9.3 o posterior.
- **El indicador de nivel de micrófono no aparece al conectarse cuando se usa la PC como fuente de micrófono** — Este era un problema conocido en v0.9.2 y versiones anteriores. En v0.9.3 el indicador aparece inmediatamente al conectarse cuando la fuente de micrófono está configurada como PC (#2086). Si está usando una versión anterior, actualice a v0.9.3 o posterior.
- **El tono de audio del tono lateral no coincide con lo esperado** — El tono está controlado únicamente por el selector **Pitch < / >**. Ajústelo allí; el generador local lo seguirá de inmediato.
- **El paneo no tiene efecto** — Confirme que la salida de audio esté configurada en estéreo. Los dispositivos de salida mono no reflejarán los cambios de paneo.
- **El panel Phone no se actualiza inmediatamente cuando VOX se activa mediante un atajo de teclado** — Este era un problema conocido en v0.9.2 y versiones anteriores. En v0.9.3 el panel Phone se actualiza instantáneamente cuando VOX se activa mediante un atajo de teclado (#2084). Si está usando una versión anterior, actualice a v0.9.3 o posterior.

## Relacionados

- [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)
- [Cambiar el tono CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
- [Configurar la velocidad CW y el retardo de break-in](set-cw-speed-and-break-in-delay.md)
