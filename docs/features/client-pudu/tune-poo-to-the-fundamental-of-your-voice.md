# Ajuste Poo / Tune a la fundamental de su voz

El control **Poo / Tune** establece la frecuencia central de la banda de procesamiento de baja frecuencia del excitador PUDU. Ajustarlo a la fundamental de su voz garantiza que la etapa Poo trabaje donde realmente se sitúan su micrófono y su carácter vocal, en lugar de por encima o por debajo.

## Antes de comenzar

- El excitador PUDU debe estar habilitado y visible. Aparece en el subcontenedor "PUDU" dentro del contenedor principal PooDoo Audio (TXDSP). Si está oculto, habilite la etapa PUDU mediante el widget CHAIN o haga doble clic en la etapa PUDU (Enh) en el widget CHAIN para abrir el editor PUDU flotante.
- Conozca la frecuencia fundamental aproximada de su voz. Para la mayoría de las voces masculinas, esto es aproximadamente de 85 a 180 Hz; para la mayoría de las voces femeninas, aproximadamente de 165 a 255 Hz. El rango de **Poo / Tune** cubre de 50 a 160 Hz, por lo que es más útil para fundamentales más graves o para apuntar al cuerpo de baja frecuencia de la voz en lugar del tono fundamental en sí.

## Pasos

1. Abra el subcontenedor PUDU dentro del contenedor principal PooDoo Audio (TXDSP).
2. Localice el grupo **Poo**: los tres controles debajo de la etiqueta del soporte "Poo".
3. Transmita en su modo de operación normal y hable al micrófono a su nivel de operación típico.
4. Gire el control **Poo / Tune** mientras escucha la señal procesada. Gírelo hacia valores más bajos para enfocar la banda en una fundamental más grave; gírelo hacia valores más altos para elevarla.
5. Deje de ajustar cuando el realce de graves suene centrado en su voz, sin sonar turbio ni delgado.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Poo / Tune | 100 Hz | 50 a 160 Hz | `ClientPuduTxPooTuneHz` |
| Poo / Drive | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxPooDriveDb` |
| Poo / Mix | 30 % | 0 a 100 % | `ClientPuduTxPooMix` |

**Poo / Tune** centra la banda de enfoque de baja frecuencia utilizando un mapeo lineal en el rango de 50 a 160 Hz. La etiqueta del control muestra el valor actual como "X Hz".

**Poo / Drive** y **Poo / Mix** son controles complementarios. Drive determina la intensidad con la que se excita el saturator o compresor en la frecuencia sintonizada; Mix mezcla la banda baja procesada con la señal seca. Consulte [Dial Poo Drive for LF thickness](dial-poo-drive-for-lf-thickness.md) y [Blend the Poo enhancement with Mix](blend-the-poo-enhancement-with-mix.md).

## Consejos

- El logotipo de PooDoo pulsa con mayor brillo a medida que aumenta el RMS de la señal húmeda. Úselo como un indicador visual aproximado de que la etapa Poo está funcionando; si el logotipo apenas reacciona durante el habla, es probable que **Poo / Drive** esté configurado demasiado bajo o **Poo / Mix** cercano a cero.
- Si el audio procesado suena retumbante o indistinto, es probable que la frecuencia de sintonía esté por debajo de la fundamental real de su voz. Aumente **Poo / Tune** en pequeños pasos hasta que el realce siga su voz.
- El modo **Even** utiliza saturación de baja frecuencia estilo Big Bottom; el modo **Odd** utiliza un compresor de graves feed-forward. El carácter de la banda Poo difiere entre modos, por lo que debe verificar nuevamente el ajuste Tune después de cambiar. Consulte [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md).
- El límite superior de **Poo / Tune** es 160 Hz. Si la fundamental de su voz se encuentra por encima de ese rango, enfoque la sección Poo en el cuerpo sub-fundamental de su voz y use la sección **Doo** para la presencia. Consulte [Centre Doo on the presence band for your mic](centre-doo-on-the-presence-band-for-your-mic.md).

## Relacionados

- [Dial Poo Drive for LF thickness](dial-poo-drive-for-lf-thickness.md)
- [Blend the Poo enhancement with Mix](blend-the-poo-enhancement-with-mix.md)
- [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md)
- [Centre Doo on the presence band for your mic](centre-doo-on-the-presence-band-for-your-mic.md)
