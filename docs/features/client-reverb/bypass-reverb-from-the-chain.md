# Omitir el reverb de la cadena

Deshabilitar la etapa de reverb elimina el procesamiento de Aetherial FreeVerb de la cadena de audio TX sin modificar ninguno de los valores de los controles. Use esta opción cuando desee una transmisión seca pero tenga intención de volver a habilitar el reverb más adelante con los mismos ajustes intactos.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe ser visible en el panel de applets.
- La etapa VERB ya debe aparecer en el widget CHAIN. Si la etapa de reverb nunca se ha habilitado, aún no estará presente en la cadena.

## Pasos

1. Localice el widget CHAIN dentro del contenedor Aetherial Audio (TXDSP) en el panel de applets.
2. Haga clic una vez en la etapa VERB del widget CHAIN para desactivarla.

El indicador de la etapa VERB cambia para mostrar que está inactiva. El subcontenedor "Aetherial FreeVerb" se oculta y la ruta de audio TX pasa sin procesamiento de reverb. Los cinco valores de los controles (`ClientReverbTxSize`, `ClientReverbTxDecayS`, `ClientReverbTxDamping`, `ClientReverbTxPreDelayMs`, `ClientReverbTxMix`) se conservan.

Para volver a habilitar el reverb, haga clic una vez más en la etapa VERB. El subcontenedor reaparece y el procesamiento se reanuda con los ajustes guardados anteriormente.

## Consejos

- Omitir la etapa mediante el widget CHAIN es no destructivo. Los valores de Size, Decay, Damp, Pre y Mix no se restablecen al deshabilitar la etapa.
- Para inspeccionar o ajustar los valores de los controles mientras el reverb está omitido, haga doble clic en la etapa VERB para abrir el editor flotante "Aetherial FreeVerb — TX". Los cambios realizados allí surten efecto la próxima vez que se habilite la etapa.

## Relacionado

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste un Mix sutil — del 10 al 15 % es habitual para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Ajuste el decay a su gusto sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
