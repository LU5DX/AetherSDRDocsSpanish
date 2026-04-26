# Ajustar el volumen del tono lateral local independientemente del monitor del radio

El tono lateral local en AetherSDR se genera en el lado del cliente con aproximadamente 10 ms de latencia, de forma independiente al monitor del radio alimentado por DAX. Esta página muestra cómo ajustar su volumen sin afectar la ganancia del tono lateral del radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice (canal de recepción) activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al subpanel de CW cuando el modo CW está activo.
- Local STn debe estar habilitado. Si no lo está, habilítelo primero — consulte [Habilitar el tono lateral CW local de baja latencia (Local STn) para trabajo con paddle, manipulador recto o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md).

## Pasos

1. Abra el applet Phone/CW haciendo clic en el botón **P/CW** de la bandeja en la barra lateral derecha. El subpanel de CW se muestra automáticamente cuando el slice activo está en modo CW.
2. Localice el control deslizante **Local sidetone volume** en el subpanel de CW.
3. Arrastre el control deslizante al nivel deseado. El rango válido es 0–100; el valor predeterminado es 50.

La configuración se guarda inmediatamente como `CwLocalSidetoneVolume` y entra en vigor sin necesidad de reiniciar.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Local STn** | Desactivado | Activado / Desactivado | `CwLocalSidetoneEnabled` | Habilita o deshabilita el tono lateral de baja latencia en el lado del cliente. El volumen no tiene efecto mientras esté desactivado. |
| **Local sidetone volume** | 50 | 0–100 | `CwLocalSidetoneVolume` | Establece el volumen del tono lateral local únicamente. No afecta la ganancia del tono lateral del radio ni el control deslizante **Sidetone volume**. |
| **Sidetone volume** | — | 0–100 | — | Establece el volumen del monitor CW del radio a través de la ruta alimentada por DAX. Se ajusta de forma independiente al volumen del tono lateral local. |

## Consejos

- El control deslizante **Local sidetone volume** y el control deslizante **Sidetone volume** son completamente independientes. Puede silenciar el monitor del radio (establecer **Sidetone volume** en 0 o deshabilitar **Sidetone**) y depender únicamente del tono lateral local para obtener retroalimentación con menor latencia.
- El tono lateral local funciona para transmisiones generadas con paddle, manipulador recto y CWX.

## Relacionados

- [Habilitar el tono lateral CW local de baja latencia (Local STn) para trabajo con paddle, manipulador recto o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Hacer que el tono del tono lateral local siga el tono CW del radio, o establecerlo manualmente con el control deslizante](make-the-local-sidetone-pitch-follow-the-radio-s-cw-pitch-or-set-it-manually-with-the-slider.md)
- [Escuchar un monitor de tono lateral de TX](listen-to-a-tx-sidetone-monitor.md)
- [Cambiar la frecuencia del tono CW / tono lateral](change-cw-pitch-sidetone-frequency.md)
