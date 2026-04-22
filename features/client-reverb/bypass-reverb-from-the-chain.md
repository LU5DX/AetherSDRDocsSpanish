# Omitir el reverb de la cadena

Esta página explica cómo deshabilitar la etapa de reverb en TX para que deje de procesar el audio transmitido. Úsela cuando desee eliminar el reverb por completo sin modificar ninguno de los valores de los controles.

## Antes de comenzar

- El subcontenedor REVERB es visible dentro del contenedor principal PooDoo Audio (TXDSP) únicamente cuando la etapa de reverb ha sido habilitada mediante el widget CHAIN o el editor flotante de Reverb.
- Si el subcontenedor REVERB no es visible, la etapa ya está omitida.

## Pasos

1. Ubique el widget CHAIN dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. Haga clic una vez en la etapa Reverb en el widget CHAIN para deshabilitarla.

El subcontenedor REVERB se ocultará y la cola de reverb dejará de aplicarse a la señal transmitida. El ajuste persistente `ClientReverbTxEnabled` queda establecido como deshabilitado. Todos los valores de los controles (Size, Decay, Damp, Pre, Mix) se conservan.

## Consejos

- Para volver a habilitar el reverb sin reconfigurarlo, haga clic nuevamente en la etapa Reverb en el widget CHAIN. Los valores anteriores de los controles se restauran.
- Hacer doble clic en la etapa Reverb en el widget CHAIN abre el editor flotante de Reverb en lugar de alternar la omisión.

## Relacionado

- [Descripción general del reverb](overview.md)
- [Ajuste de un Mix sutil — 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
