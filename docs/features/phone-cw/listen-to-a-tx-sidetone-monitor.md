# Escuchar un monitor de sidetone de transmisión

AetherSDR proporciona un monitor del lado de la radio (disponible en modos Phone y CW) y un sidetone CW de baja latencia del lado del cliente (aproximadamente 10 ms de latencia) que se controla en sincronía con el sidetone de la radio a través de un solo botón Sidetone y un regulador de volumen Sidetone. Esta página cubre ambas rutas para que pueda escuchar su propio audio transmitido mientras opera.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone/CW requiere una conexión de radio activa.
- Abra el Applet Panel. Si no es visible, haga clic en View > Applet Panel.

## Pasos

### Modo Phone: habilitar el monitor de banda lateral

1. Haga clic en el botón de bandeja P/CW en la barra lateral derecha para abrir el applet Phone/CW.
2. Confirme que el applet muestra el panel Phone (el slice activo debe estar en un modo de voz como SSB o AM).
3. Haga clic en MON para habilitar el monitor de banda lateral TX. El botón se resalta cuando está activo.
4. Ajuste el regulador Monitor volume para establecer el nivel de reproducción (0–100).

### Modo CW: habilitar el monitor de sidetone

1. Cambie el slice activo a un modo CW. El applet muestra automáticamente el panel CW.
2. Haga clic en Sidetone para habilitar el monitor CW. El botón se resalta cuando está activo.
   - Este único botón controla tanto el monitor alimentado por DAX de la radio como el generador de sidetone de baja latencia del lado del cliente en sincronía.
3. Ajuste el regulador Sidetone volume para establecer el nivel (0–100).
   - Este único regulador establece el volumen tanto para el monitor del lado de la radio (`mon_gain_cw`) como para el generador de sidetone local simultáneamente.
4. El tono y la panoramización estéreo se configuran automáticamente a partir de los ajustes `cw_pitch` y `mon_pan_cw` de la radio. Para ajustar la panoramización manualmente, use el regulador L / R pan (CW) (doble clic para recentrar).

## Qué hace cada control

| Control         | Qué hace                                                                                                                                                      | Predeterminado |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| MON             | Habilita el monitor de banda lateral TX (panel Phone).                                                                                                                    | —       |
| Monitor volume  | Establece el nivel de reproducción del monitor de banda lateral.                                                                                                                                             | —       |
| Sidetone        | Activa/desactiva el monitor de sidetone CW. También habilita/deshabilita el CwSidetoneGenerator de baja latencia del lado del cliente en sincronía. Tanto el monitor alimentado por DAX de la radio como el sidetone PortAudio local se controlan mediante este único botón. El tono y la panoramización siempre siguen automáticamente los parámetros `cw_pitch` y `mon_pan_cw` de la radio. v0.9.3: la secuencia de sidetone ahora se inicia inmediatamente al conectar en Windows (#2105 — corrección del orden de init de AudioEngine). | —       |
| Sidetone volume | Establece el nivel de reproducción del monitor CW tanto para el monitor del lado de la radio como para el generador de sidetone local simultáneamente.                                               | —       |
| L / R pan (CW)  | Establece la panoramización estéreo del monitor CW; se aplica tanto al monitor de radio como al generador de sidetone local. Doble clic para recentrar.                                         | 50      |

## Consejos

- El botón Sidetone y el regulador Sidetone volume controlan ambas rutas de audio (monitor DAX de radio y generador del lado del cliente) juntos. No hay un control separado para habilitar o ajustar el sidetone local de forma independiente.
- El tono siempre sigue automáticamente el ajuste de tono CW de la radio. Use el spinbox Pitch < / > para cambiar el tono CW de la radio, y tanto el tono de decodificación como el tono de sidetone se actualizarán en consecuencia.
- El botón MON y el botón Sidetone son controles separados en paneles separados. MON se aplica a modos de voz; Sidetone se aplica a modo CW.
- Cuando la fuente de micrófono se establece en PC, el medidor Level aparece inmediatamente al conectar. En otros modos de fuente de micrófono, el medidor se suprime cuando `met_in_rx` está desactivado y la radio no está transmitiendo.

## Solución de problemas

- **El botón MON o Sidetone no tiene efecto** — Confirme que la radio está conectada y el modo del slice activo coincide con el panel que se muestra (Phone vs. CW). El applet cambia de panel automáticamente según el modo del slice activo.
- **Sidetone no produce audio** — Verifique que la salida de audio del sistema esté configurada correctamente. El sidetone del lado del cliente se genera localmente por AetherSDR; confirme que el botón Sidetone está activo. En Windows, la secuencia de sidetone ahora se inicia inmediatamente al conectar (v0.9.3, #2105).
- **El tono del sidetone es incorrecto** — El tono se deriva automáticamente del ajuste `cw_pitch` de la radio. Ajuste el tono usando el spinbox Pitch < / > en el panel CW.
- **El medidor Level no aparece al conectar** — Si la fuente de micrófono se establece en PC, el medidor Level debe aparecer inmediatamente al conectar (v0.9.3, #2086). Para otras fuentes de micrófono, el medidor se suprime hasta que `met_in_rx` esté habilitado o la radio comience a transmitir.

## Relacionado

- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
