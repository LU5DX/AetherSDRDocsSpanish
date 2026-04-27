# Ajustar el volumen del tono lateral local independientemente del monitor del radio

El tono lateral local en AetherSDR es generado en el lado del cliente por AudioEngine, con una latencia de aproximadamente 10 ms, lo que lo hace independiente del monitor alimentado por DAX del radio. Esta página explica cómo ajustar su volumen sin afectar el tono lateral ni el nivel de monitor del radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al subpanel de CW cuando se selecciona un modo CW.
- El tono lateral local debe estar habilitado. Haga clic en el botón de bandeja `P/CW` en la barra lateral derecha para abrir el applet Phone/CW y, a continuación, habilite Local STn. Consulte [Habilitar el tono lateral CW local de baja latencia (Local STn) para trabajo con paleta, manipulador directo o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md) si aún no lo ha hecho.

## Pasos

1. Haga clic en el botón de bandeja `P/CW` en la barra lateral derecha para abrir el applet Phone/CW.
2. Confirme que el subpanel de CW es visible. Si el slice activo está en un modo CW, el panel cambia a los controles de CW automáticamente.
3. Localice el botón de alternancia Local STn. Confirme que está activo (habilitado).
4. Arrastre el control deslizante de volumen del tono lateral local hacia la izquierda o la derecha para establecer el nivel deseado. El rango es 0–100, con un valor predeterminado de 50.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de ajuste persistente |
|---|---|---|---|
| Local STn | Off | On / Off | `CwLocalSidetoneEnabled` |
| Volumen del tono lateral local | 50 | 0–100 | `CwLocalSidetoneVolume` |
| Follow (tono local) | On | On / Off | `CwLocalSidetonePitchFollow` |
| Tono del tono lateral local | 600 | 100–2000 Hz | `CwLocalSidetonePitchHz` |

**Local STn** — Habilita o deshabilita el generador de tono lateral de baja latencia en el lado del cliente. Cuando está desactivado, no se produce audio local independientemente de la posición del control deslizante de volumen.

**Volumen del tono lateral local** — Establece el volumen únicamente del tono lateral local. No tiene efecto sobre el control deslizante de volumen Sidetone del radio ni sobre el nivel de monitor MON.

**Follow (tono local)** — Cuando está activado, el tono del tono lateral local sigue el ajuste de tono CW del radio. Cuando está desactivado, el control deslizante Local sidetone pitch se activa para el control manual.

**Tono del tono lateral local** — Establece la frecuencia del tono lateral local en Hz. Solo es ajustable cuando Follow está desactivado.

## Consejos

- El control deslizante de volumen del tono lateral local y el control deslizante de volumen Sidetone son completamente independientes. Ajuste cada uno por separado para equilibrar el audio local (~10 ms de latencia) y el del monitor del radio.
- Local STn funciona para paleta, manipulador directo y transmisiones generadas por CWX.

## Relacionados

- [Habilitar el tono lateral CW local de baja latencia (Local STn) para trabajo con paleta, manipulador directo o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Hacer que el tono del tono lateral local siga el tono CW del radio, o ajustarlo manualmente con el control deslizante](make-the-local-sidetone-pitch-follow-the-radio-s-cw-pitch-or-set-it-manually-with-the-slider.md)
- [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)
- [Cambiar el tono CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
