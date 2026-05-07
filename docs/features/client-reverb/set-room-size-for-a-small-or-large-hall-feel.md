# Ajustar el tamaño de la sala para una sensación de cabina o gran salón

El control Size modifica las dimensiones de la sala modelada en la reverberación Aetherial FreeVerb TX. Girarlo hacia arriba cambia la sensación desde una cabina ajustada hasta un gran salón.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. Si el subcontenedor "Aetherial FreeVerb" no está visible en el panel Aetherial Audio (TXDSP), primero active la etapa VERB.
- No se requiere conexión de radio para ajustar los parámetros de reverberación.

## Pasos

1. Abra los controles de reverberación usando uno de estos dos métodos:
   - En el panel Aetherial Audio (TXDSP), localice el subcontenedor "Aetherial FreeVerb" y ajuste el control Size directamente en la fila compacta.
   - Haga doble clic en la etapa VERB del widget CHAIN para abrir el editor flotante "Aetherial FreeVerb — TX".
2. Gire el control Size hacia la izquierda para una sensación de sala más pequeña y ajustada; gírelo hacia la derecha para una sensación de salón más grande y espaciosa.
3. La etiqueta del control se actualiza en tiempo real y muestra el valor actual como porcentaje (por ejemplo, `50 %`).

## Visualización en vivo

El editor "Aetherial FreeVerb — TX" incluye una visualización compacta de forma de onda (90 px de alto) que se actualiza en tiempo real a medida que ajusta cualquiera de los cinco controles. Muestra tres capas de señal superpuestas:

- **Cian** — el paquete de senoidal seco. Su amplitud disminuye a medida que se aumenta Mix.
- **Amarillo** — reflexiones de primer orden. El espaciado y la cantidad reflejan los ajustes de Size y Damp.
- **Magenta** — la cola reverberante. La longitud sigue a Decay; la atenuación de altas frecuencias sigue a Damp; la posición de inicio sigue a Pre-delay.

La visualización usa un fondo oscuro con una rejilla sutil. No requiere interacción; se actualiza automáticamente cada vez que cambia el valor de un control.

## Función de cada control

| Etiqueta | Predeterminado | Rango | Clave de configuración | Comportamiento |
|----------|----------------|-------|------------------------|----------------|
| Size | 50 % | 0 % a 100 % | `ClientReverbTxSize` | Define el tamaño de sala modelado. Mapeo lineal. |
| Decay | 1.20 s | 0.3 a 5.0 s | `ClientReverbTxDecayS` | Define la longitud de la cola de reverberación. Mapeo exponencial. |
| Damp | 50 % | 0 % a 100 % | `ClientReverbTxDamping` | Valores altos atenúan más rápido las frecuencias altas en la cola. Mapeo lineal. |
| Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Retardo previo entre la señal seca y las primeras reflexiones. Mapeo lineal. |
| Mix | 15 % | 0 % a 100 % | `ClientReverbTxMix` | Balance seco/húmedo. Mapeo lineal. |

## Consejos

- Size y Decay interactúan estrechamente. Un Size grande con un Decay corto suena antinatural; si aumenta Size significativamente, considere aumentar Decay para que coincida.
- La visualización en vivo en el editor flotante ofrece retroalimentación inmediata sobre cómo interactúan Size, Decay, Damp, Pre-delay y Mix antes de transmitir.
- Tanto el control compacto del applet como el editor flotante "Aetherial FreeVerb — TX" manejan los mismos parámetros subyacentes y se mantienen sincronizados automáticamente.
- Haga doble clic en un control para restaurar su valor predeterminado.

## Relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste la caída según su gusto sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Seleccione un Mix sutil: 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omita la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
