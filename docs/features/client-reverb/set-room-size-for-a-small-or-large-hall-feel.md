# Ajuste el tamaño de sala para una sensación de cabina pequeña o gran salón

El control Size regula las dimensiones de sala modeladas en el reverb Aetherial FreeVerb TX. Al girarlo hacia la derecha, el carácter pasa de una cabina compacta a un gran salón.

## Antes de comenzar

- La etapa de reverb debe estar habilitada en el widget CHAIN. Si el sub-contenedor "Aetherial FreeVerb" no es visible en el panel Aetherial Audio (TXDSP), habilite primero la etapa VERB.
- No se requiere conexión con la radio para ajustar los parámetros de reverb.

## Pasos

1. Abra los controles de reverb mediante uno de estos dos métodos:
   - En el panel Aetherial Audio (TXDSP), localice el sub-contenedor "Aetherial FreeVerb" y ajuste el control Size directamente en la fila compacta.
   - Haga doble clic en la etapa VERB del widget CHAIN para abrir el editor flotante "Aetherial FreeVerb — TX".
2. Gire el control Size hacia la izquierda para un carácter de sala más pequeño y ajustado; gírelo hacia la derecha para una sensación de salón más amplio y espacioso.
3. La etiqueta del control se actualiza en tiempo real y muestra el valor actual como porcentaje (por ejemplo, `50 %`).

## Qué hace cada control

| Etiqueta | Valor predeterminado | Rango | Clave de ajuste | Comportamiento |
|----------|----------------------|-------|-----------------|----------------|
| Size | 50 % | 0 % a 100 % | `ClientReverbTxSize` | Establece el tamaño de sala modelado. Mapeo lineal. |
| Decay | 1.20 s | 0.3 a 5.0 s | `ClientReverbTxDecayS` | Establece la duración de la cola de reverb. Mapeo exponencial. |
| Damp | 50 % | 0 % a 100 % | `ClientReverbTxDamping` | Valores más altos atenúan las frecuencias altas más rápido en la cola. Mapeo lineal. |
| Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Pre-retardo entre la señal seca y las primeras reflexiones. Mapeo lineal. |
| Mix | 15 % | 0 % a 100 % | `ClientReverbTxMix` | Balance seco/húmedo. Mapeo lineal. |

## Consejos

- Size y Decay interactúan estrechamente. Un Size grande con un Decay corto suena poco natural; si aumenta Size de forma significativa, considere incrementar Decay en consecuencia.
- Tanto el control del applet compacto como el editor flotante "Aetherial FreeVerb — TX" controlan los mismos parámetros subyacentes y permanecen sincronizados automáticamente.
- Hacer doble clic en un control restablece su valor predeterminado.

## Temas relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste el Decay a su gusto sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Configure un Mix sutil: entre 10 y 15 % es habitual para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Bypass del reverb desde la cadena](bypass-reverb-from-the-chain.md)
