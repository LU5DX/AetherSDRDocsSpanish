# Ajustar el tamaño de sala para un sonido íntimo o de gran auditorio

El control Size regula las dimensiones de la sala modelada en el reverb Aetherial FreeVerb TX. Al girarlo hacia la derecha, el carácter pasa de una cabina estrecha a un gran auditorio.

## Antes de comenzar

- La etapa de reverb debe estar habilitada en el widget CHAIN. Si el sub-contenedor "Aetherial FreeVerb" no es visible en el panel Aetherial Audio (TXDSP), habilite primero la etapa VERB.
- No se requiere conexión a una radio para ajustar los parámetros de reverb.

## Pasos

1. Abra los controles de reverb mediante uno de estos dos métodos:
   - En el panel Aetherial Audio (TXDSP), localice el sub-contenedor "Aetherial FreeVerb" y ajuste el control Size directamente en la fila compacta.
   - Haga doble clic en la etapa VERB del widget CHAIN para abrir el editor flotante "Aetherial FreeVerb — TX".
2. Gire el control Size hacia la izquierda para un carácter de sala más pequeño y ajustado; gírelo hacia la derecha para una sensación de auditorio más grande y espacioso.
3. La etiqueta del control se actualiza en tiempo real y muestra el valor actual como porcentaje (por ejemplo, `50 %`).

## Qué hace cada control

| Etiqueta | Valor por defecto | Rango | Clave de configuración | Comportamiento |
|----------|-------------------|-------|------------------------|----------------|
| Size | 50 % | 0 % a 100 % | `ClientReverbTxSize` | Define el tamaño de sala modelado. Mapeo lineal. |
| Decay | 1.20 s | 0.3 a 5.0 s | `ClientReverbTxDecayS` | Define la duración de la cola de reverb. Mapeo exponencial. |
| Damp | 50 % | 0 % a 100 % | `ClientReverbTxDamping` | Valores más altos atenúan las frecuencias agudas más rápidamente en la cola. Mapeo lineal. |
| Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Prerretardo entre la señal directa y las primeras reflexiones. Mapeo lineal. |
| Mix | 15 % | 0 % a 100 % | `ClientReverbTxMix` | Balance señal seca/húmeda. Mapeo lineal. |

## Consejos

- Size y Decay interactúan estrechamente. Un Size grande con un Decay corto suena poco natural; si aumenta Size de forma significativa, considere aumentar también Decay para compensar.
- Tanto el control del applet compacto como el editor flotante "Aetherial FreeVerb — TX" actúan sobre los mismos parámetros subyacentes y se sincronizan automáticamente.
- Hacer doble clic en un control lo restablece a su valor por defecto.

## Temas relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajustar el Decay sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Configurar un Mix sutil — entre 10 y 15 % es lo habitual para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Desactivar el reverb desde la cadena](bypass-reverb-from-the-chain.md)
