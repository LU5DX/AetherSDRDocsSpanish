# Ajuste Poo a la frecuencia fundamental de su voz

El control **Poo / Tune** establece la frecuencia central de la banda de procesamiento de baja frecuencia del excitador PUDU. Ajustarlo a la fundamental de su voz garantiza que la etapa Poo trabaje donde realmente se encuentran su micrófono y su carácter vocal, sin quedar por encima ni por debajo.

## Antes de comenzar

- El excitador PUDU debe estar habilitado y visible. Aparece en el subcontenedor "PUDU" dentro del contenedor padre PooDoo Audio (TXDSP). Si está oculto, habilite la etapa PUDU mediante el widget CHAIN o haga doble clic en la etapa PUDU (Enh) en el widget CHAIN para abrir el editor flotante de PUDU.
- Conozca la frecuencia fundamental aproximada de su voz. Para la mayoría de las voces masculinas es aproximadamente 85–180 Hz; para la mayoría de las voces femeninas, aproximadamente 165–255 Hz. El rango de **Poo / Tune** cubre de 50 a 160 Hz, por lo que resulta más útil para fundamentales más graves o para apuntar al cuerpo de baja frecuencia de la voz en lugar de la nota fundamental en sí.

## Pasos

1. Abra el subcontenedor PUDU dentro del contenedor padre PooDoo Audio (TXDSP).
2. Localice el grupo **Poo** — los tres controles bajo la etiqueta de corchete "Poo".
3. Transmita en su modo de operación habitual y hable al micrófono a su nivel de operación típico.
4. Gire el control **Poo / Tune** mientras escucha la señal procesada. Gire hacia valores más bajos para centrar la banda en una fundamental más grave; gire hacia valores más altos para elevarla.
5. Deje de ajustar cuando el realce de las bajas frecuencias suene centrado en su voz, sin sonar turbio ni delgado.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Poo / Tune | 100 Hz | 50 a 160 Hz | `ClientPuduTxPooTuneHz` |
| Poo / Drive | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxPooDriveDb` |
| Poo / Mix | 30 % | 0 a 100 % | `ClientPuduTxPooMix` |

**Poo / Tune** centra la banda de enfoque de baja frecuencia mediante un mapeo lineal entre 50–160 Hz. La etiqueta del control muestra el valor actual como "X Hz".

**Poo / Drive** y **Poo / Mix** son controles complementarios. Drive determina con qué intensidad se impulsa el saturador o compresor en la frecuencia sintonizada; Mix mezcla la banda baja procesada con la señal seca. Consulte [Ajuste Poo Drive para grosor en LF](dial-poo-drive-for-lf-thickness.md) y [Mezcle el realce Poo con Mix](blend-the-poo-enhancement-with-mix.md).

## Consejos

- El logotipo de PooDoo pulsa con mayor brillo a medida que sube el RMS de la señal húmeda. Úselo como indicador visual aproximado de que la etapa Poo está funcionando — si el logotipo apenas reacciona durante el habla, es posible que **Poo / Drive** esté demasiado bajo o que **Poo / Mix** esté cerca de cero.
- Si el audio procesado suena retumbante o impreciso, la frecuencia de sintonía probablemente está por debajo de la fundamental real de su voz. Aumente **Poo / Tune** en pasos pequeños hasta que el realce siga su voz.
- El modo **Even** utiliza saturación LF al estilo Big Bottom; el modo **Odd** utiliza un compresor de graves de alimentación hacia adelante. El carácter de la banda Poo difiere entre modos, por lo que compruebe nuevamente la configuración de Tune después de cambiar. Consulte [Elija el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md).
- El límite superior de **Poo / Tune** es 160 Hz. Si la fundamental de su voz está por encima de ese rango, enfoque la sección Poo en el cuerpo subfundamental de su voz y use la sección **Doo** para la presencia. Consulte [Centre Doo en la banda de presencia para su micrófono](centre-doo-on-the-presence-band-for-your-mic.md).

## Relacionados

- [Ajuste Poo Drive para grosor en LF](dial-poo-drive-for-lf-thickness.md)
- [Mezcle el realce Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Elija el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Centre Doo en la banda de presencia para su micrófono](centre-doo-on-the-presence-band-for-your-mic.md)
