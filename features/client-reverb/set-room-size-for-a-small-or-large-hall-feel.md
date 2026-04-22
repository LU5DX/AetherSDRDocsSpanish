# Ajustar el tamaño de sala para una sensación de cabina pequeña o sala grande

El control Size regula el tamaño de sala modelado en el reverb de TX, permitiéndole configurar desde una cabina pequeña hasta una sala grande. Use esta página para localizar el control y ajustarlo a su gusto.

## Antes de comenzar

- El subcontenedor REVERB debe estar visible en el contenedor principal PooDoo Audio (TXDSP). Permanece oculto hasta que la etapa Reverb se habilita mediante el widget CHAIN o el editor flotante de Reverb.
- No se requiere conexión con la radio para ajustar la configuración del reverb.

## Pasos

1. Localice el subcontenedor **REVERB** dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. Si el subcontenedor no está visible, habilite la etapa Reverb haciendo clic en ella en el widget CHAIN, o haga doble clic en la etapa Reverb en el widget CHAIN para abrir el editor flotante de Reverb y habilitarla desde allí.
3. Localice el control **Size** — el primero a la izquierda de los cinco controles en la fila compacta.
4. Arrastre el control **Size** hacia arriba para una sala más grande o hacia abajo para una sala más pequeña. La etiqueta muestra el valor actual como porcentaje (por ejemplo, `50 %`).
   - Para una sensación de sala pequeña, configure **Size** hacia `0 %`.
   - Para una sensación de sala grande, configure **Size** hacia `100 %`.
5. Ajuste los controles restantes para complementar el tamaño de sala (consulte la sección Relacionados a continuación).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Size | 50 % | 0 % a 100 % | `ClientReverbTxSize` | Establece el tamaño de sala modelado. Mapeo lineal. |
| Decay | 1.20 s | 0.3 a 5.0 s | `ClientReverbTxDecayS` | Establece la longitud de la cola del reverb. Mapeo exponencial. |
| Damp | 50 % | 0 % a 100 % | `ClientReverbTxDamping` | Los valores más altos atenúan las frecuencias altas más rápidamente en la cola. Mapeo lineal. |
| Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Predelay entre la señal seca y las primeras reflexiones. Mapeo lineal. |
| Mix | 15 % | 0 % a 100 % | `ClientReverbTxMix` | Balance seco/húmedo. Mapeo lineal. |

## Consejos

- Cuando aumente Size considerablemente, considere aumentar también Decay: una sala modelada más grande sostiene las reflexiones durante más tiempo de forma natural.
- Mantenga presionada la tecla `Shift` mientras arrastra cualquier control para un ajuste más fino (un cuarto de la sensibilidad de arrastre normal).
- Haga doble clic en la etapa Reverb en el widget CHAIN para abrir el editor flotante de Reverb, que ofrece los mismos controles en un formato más grande y fácil de manipular.
- Haga clic derecho en la barra de título del subcontenedor **REVERB** para flotarlo, extraerlo u ocultarlo.

## Relacionados

- [Descripción general del reverb](overview.md)
- [Ajustar Decay a gusto sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Reducir el brillo en las frecuencias altas de la cola con Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Desplazar las reflexiones respecto a la señal seca con Pre](offset-reflections-from-the-dry-signal-with-pre.md)
- [Configurar un Mix sutil — entre 10 y 15 % es habitual para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omitir el reverb desde la cadena](bypass-reverb-from-the-chain.md)
