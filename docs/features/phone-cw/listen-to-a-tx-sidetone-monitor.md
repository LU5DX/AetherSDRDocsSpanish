# Escuchar el monitor de sidetone de TX

AetherSDR proporciona un monitor del lado del radio (disponible en los modos Phone y CW) y un sidetone CW de baja latencia del lado del cliente (aproximadamente 10 ms de latencia) que se controla de forma sincronizada con el sidetone del radio mediante el único botón Sidetone y el deslizador Sidetone volume. Esta página cubre ambas rutas de audio para que pueda escuchar su propia señal transmitida mientras opera.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone/CW requiere una conexión de radio activa.
- Abra el panel de applets. Si no está visible, haga clic en View > Applet Panel.

## Pasos

### Modo Phone: activar el monitor de banda lateral

1. Haga clic en el botón P/CW del panel lateral derecho para abrir el applet Phone/CW.
2. Confirme que el applet muestra el panel Phone (el slice activo debe estar en un modo de voz como SSB o AM).
3. Haga clic en MON para activar el monitor de banda lateral de TX. El botón se resalta cuando está activo.
4. Ajuste el deslizador Monitor volume para establecer el nivel de reproducción (0–100).

### Modo CW: activar el monitor de sidetone

1. Cambie el slice activo a un modo CW. El applet muestra automáticamente el panel CW.
2. Haga clic en Sidetone para activar el monitor CW. El botón se resalta cuando está activo.
   - Este único botón controla de forma sincronizada tanto el monitor del radio alimentado por DAX como el generador de sidetone de baja latencia del lado del cliente.
3. Ajuste el deslizador Sidetone volume para establecer el nivel (0–100).
   - Este único deslizador establece el volumen tanto para el monitor del lado del radio (`mon_gain_cw`) como para el generador de sidetone local de forma simultánea.
4. El tono (pitch) y el paneo estéreo se configuran automáticamente a partir de los ajustes `cw_pitch` y `mon_pan_cw` del radio. Para ajustar el paneo manualmente, use el deslizador L / R pan (CW) (haga doble clic para centrarlo).

## Qué hace cada control

| Control         | Función                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Valor predeterminado |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| MON             | Activa el monitor de banda lateral de TX (panel Phone).                                                                                                                                                                                                                                                                                                                                                                                                      | —                    |
| Monitor volume  | Establece el nivel de reproducción del monitor de banda lateral.                                                                                                                                                                                                                                                                                                                                                                                             | —                    |
| Sidetone        | Activa o desactiva el monitor de sidetone CW. También habilita o deshabilita de forma sincronizada el CwSidetoneGenerator de baja latencia del lado del cliente. Tanto el monitor del radio alimentado por DAX como el sidetone local de PortAudio son controlados por este único botón. El tono y el paneo siguen automáticamente los valores `cw_pitch` y `mon_pan_cw` del radio. v0.9.3: el flujo de sidetone ahora comienza inmediatamente al conectar en Windows (#2105 — corrección del orden de inicialización de AudioEngine). | —                    |
| Sidetone volume | Establece el nivel de reproducción del monitor CW tanto para el monitor del lado del radio como para el generador de sidetone local de forma simultánea.                                                                                                                                                                                                                                                                                                     | —                    |
| L / R pan (CW)  | Establece el paneo estéreo del monitor CW; se aplica tanto al monitor del radio como al generador de sidetone local. Haga doble clic para centrar.                                                                                                                                                                                                                                                                                                           | 50                   |

## Consejos

- El botón Sidetone y el deslizador Sidetone volume controlan ambas rutas de audio (monitor DAX del radio y generador del lado del cliente) de forma conjunta. No existe un control independiente para activar o ajustar el sidetone local por separado.
- El tono siempre sigue automáticamente el ajuste de tono CW del radio. Use el selector giratorio Pitch < / > para cambiar el tono CW del radio; tanto el tono de decodificación como el tono del sidetone se actualizarán en consecuencia.
- El botón MON y el botón Sidetone son controles independientes en paneles separados. MON se aplica a los modos de voz; Sidetone se aplica al modo CW.
- Cuando la fuente de micrófono está configurada como PC, el indicador Level aparece inmediatamente al conectar. En otros modos de fuente de micrófono, el indicador se suprime cuando `met_in_rx` está desactivado y el radio no está transmitiendo.

## Solución de problemas

- **El botón MON o Sidetone no tiene efecto** — Confirme que el radio está conectado y que el modo del slice activo coincide con el panel que se muestra (Phone vs. CW). El applet cambia de panel automáticamente según el modo del slice activo.
- **El sidetone no produce audio** — Verifique que la salida de audio del sistema esté configurada correctamente. El sidetone del lado del cliente es generado localmente por AetherSDR; confirme que el botón Sidetone está activo. En Windows, el flujo de sidetone ahora comienza inmediatamente al conectar (v0.9.3, #2105).
- **El tono del sidetone es incorrecto** — El tono se deriva automáticamente del ajuste `cw_pitch` del radio. Ajuste el tono usando el selector giratorio Pitch < / > en el panel CW.
- **El indicador Level no aparece al conectar** — Si la fuente de micrófono está configurada como PC, el indicador Level debería aparecer inmediatamente al conectar (v0.9.3, #2086). Para otras fuentes de micrófono, el indicador se suprime hasta que `met_in_rx` esté habilitado o el radio comience a transmitir.

## Relacionado

- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
