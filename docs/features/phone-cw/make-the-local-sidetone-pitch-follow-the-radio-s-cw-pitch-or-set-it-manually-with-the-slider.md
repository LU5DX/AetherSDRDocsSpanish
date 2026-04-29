# Tono lateral CW: frecuencia, volumen y activación en v0.9.2.1

En v0.9.2.1 se han eliminado los controles independientes **Local STn**, **Local sidetone volume**, **Follow (local pitch)** y **Local sidetone pitch**. El tono lateral CW de baja latencia en el lado del cliente (CwSidetoneGenerator, latencia de ~10 ms) ahora está controlado íntegramente por el mismo botón **Sidetone** y el deslizador **Sidetone volume** que controlan el monitor del radio alimentado por DAX. La frecuencia y el paneo se toman siempre de forma automática desde los parámetros `cw_pitch` y `mon_pan_cw` del radio; no existe ajuste manual.

Si antes utilizaba los controles de tono lateral local independientes, consulte [Cómo escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md) para conocer el flujo de trabajo actual.

## Antes de comenzar

- El slice (canal de recepción) activo debe estar en un modo CW para que el subpanel CW sea visible en el applet Phone/CW.

## Pasos

### Para activar el tono lateral CW (tanto el monitor del radio como el generador local)

1. Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** de la barra lateral derecha.
2. Haga clic en **Sidetone** para activarlo. El monitor del radio alimentado por DAX y el CwSidetoneGenerator del lado del cliente se inician simultáneamente.

### Para desactivar el tono lateral CW

1. Haga clic en **Sidetone** nuevamente. Tanto el monitor del radio como el generador local se detienen.

### Para ajustar el volumen del tono lateral

1. Arrastre el deslizador **Sidetone volume** (0–100). El mismo valor se aplica al parámetro `mon_gain_cw` del radio y al volumen del generador de tono lateral local de forma simultánea.

### Para ajustar la frecuencia del tono lateral

1. Use el control giratorio **Pitch < / >** para cambiar la frecuencia en incrementos de 10 Hz (100–6000 Hz). El generador de tono lateral local sigue este valor automáticamente; no existe un control de frecuencia local independiente.

### Para ajustar el paneo estéreo del tono lateral

1. Arrastre el deslizador **L / R pan (CW)** (0–100, valor predeterminado 50 = centro). El mismo valor de paneo se envía al radio (`mon_pan_cw`) y se aplica como paneo de potencia constante al generador de tono lateral local.
2. Haga doble clic en el deslizador para devolverlo al centro (50).

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Sidetone** | — | On / Off | — | Activa o desactiva de forma sincronizada el monitor CW del radio alimentado por DAX y el CwSidetoneGenerator del lado del cliente. |
| **Sidetone volume** | — | 0–100 | — | Establece `mon_gain_cw` en el radio y el volumen del generador de tono lateral local de forma simultánea. |
| **Pitch < / >** | 600 Hz | 100–6000 Hz (paso 10) | — | Establece la frecuencia del tono lateral/decodificación CW en el radio; el generador local siempre la sigue. |
| **L / R pan (CW)** | 50 | 0–100 | — | Establece `mon_pan_cw` en el radio y aplica paneo de potencia constante al generador local. El doble clic lo recentra en 50. |

## Consejos

- Dado que la frecuencia y el paneo siempre se derivan de los parámetros `cw_pitch` y `mon_pan_cw` del radio, el tono lateral local y el monitor del radio siempre están sincronizados; no es necesaria ninguna sincronización manual.
- El CwSidetoneGenerator local tiene una latencia aproximada de 10 ms, lo que lo hace adecuado para trabajo con paddle a alta velocidad donde la latencia de ida y vuelta del DAX del radio resulta perceptible.
- Ya no existen los parámetros `CwLocalSidetoneEnabled`, `CwLocalSidetoneVolume`, `CwLocalSidetonePitchFollow` ni `CwLocalSidetonePitchHz`. Si tiene scripts o archivos de configuración que hagan referencia a estas claves, pueden eliminarse.

## Resolución de problemas

- **No se escucha tono lateral aunque Sidetone esté activado** — Verifique que el dispositivo de salida de audio esté seleccionado correctamente en la configuración de audio de AetherSDR. Confirme también que **Sidetone volume** sea mayor que 0.
- **La frecuencia del tono lateral no coincide con lo esperado** — La frecuencia está controlada únicamente por el control giratorio **Pitch < / >**. Ajústela allí; el generador local la seguirá de inmediato.
- **El paneo no tiene efecto** — Confirme que la salida de audio esté configurada en estéreo. Los dispositivos de salida mono no reflejarán los cambios de paneo.

## Relacionado

- [Cómo escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)
- [Cambiar la frecuencia del tono lateral CW](change-cw-pitch-sidetone-frequency.md)
- [Ajustar la velocidad CW y el retardo de break-in](set-cw-speed-and-break-in-delay.md)
