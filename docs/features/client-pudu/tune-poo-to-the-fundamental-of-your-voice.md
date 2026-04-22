# Ajuste Poo / Tune a la frecuencia fundamental de su voz

El control **Poo / Tune** centra la banda de procesamiento de baja frecuencia en la frecuencia que usted elija. Ajustarlo a la fundamental de su voz enfoca el saturador o compresor Poo donde su voz realmente tiene energía, en lugar de por encima o por debajo de ella.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena PooDoo Audio. Si el subcontenedor PUDU no es visible, habilite la etapa mediante el widget CHAIN o haga doble clic en la etapa PUDU (Enh) en el widget CHAIN para abrir el editor flotante.
- Necesita una idea aproximada de la frecuencia fundamental de su voz. La mayoría de las voces masculinas se sitúan entre 85 y 180 Hz; la mayoría de las voces femeninas, entre 165 y 255 Hz. Un punto de partida de 100 Hz (el valor predeterminado) funciona bien para muchas voces de barítono y bajo.

## Pasos

1. Abra el subcontenedor PUDU dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. Localice el grupo **Poo** — los tres controles bajo el corchete etiquetado **Poo**.
3. Gire el control **Poo / Tune** para que coincida con la fundamental de su voz. El control muestra su valor como número entero en Hz (por ejemplo, `100 Hz`).
4. Active la transmisión y escuche el audio de monitoreo o observe el pulso del logotipo de PooDoo. Aumente o disminuya **Poo / Tune** hasta que el engrosamiento de los graves se centre en su voz en lugar de sonar turbio (demasiado bajo) o delgado (demasiado alto).
5. Ajuste fino de **Poo / Drive** y **Poo / Mix** al gusto una vez que la frecuencia esté establecida.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Poo / Tune | 100 Hz | 50 a 160 Hz | `ClientPuduTxPooTuneHz` | Mapeo lineal. Centra la banda de enfoque de baja frecuencia. |
| Poo / Drive | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxPooDriveDb` | Empuja con más fuerza el saturador o compresor de baja frecuencia. |
| Poo / Mix | 30 % | 0 a 100 % | `ClientPuduTxPooMix` | Mezcla la banda de graves mejorada con la señal seca. |

## Consejos

- El rango de **Poo / Tune** es de 50 a 160 Hz. Si la fundamental de su voz supera los 160 Hz, ajuste **Poo / Tune** a su valor máximo y apóyese más en el grupo **Doo** para obtener presencia.
- En el modo **Even**, la sección Poo utiliza saturación de baja frecuencia estilo Big Bottom; en el modo **Odd**, utiliza un compresor de bajos de alimentación directa (feed-forward). La misma frecuencia de **Poo / Tune** se aplica en ambos modos, pero el carácter difiere — revise el ajuste si cambia de modo.
- El logotipo de PooDoo se ilumina con el RMS de la señal procesada. Si el logotipo apenas pulsa al transmitir, es posible que **Poo / Mix** esté muy bajo o que la etapa esté omitida (bypassed).

## Solución de problemas

- **El control Poo / Tune no produce efecto audible** — Confirme que la etapa PUDU no esté omitida en el widget CHAIN. Verifique también que **Poo / Mix** esté por encima de 0 %; con 0 % la banda de graves procesada se elimina completamente de la salida.
- **Los graves suenan turbios independientemente de la posición de Tune** — Es posible que **Poo / Drive** esté demasiado alto. Redúzcalo y vuelva a evaluar la frecuencia.
- **El control Poo / Tune no es visible** — El subcontenedor PUDU permanece oculto hasta que la etapa PUDU esté habilitada. Habilítela mediante el widget CHAIN.

## Temas relacionados

- [Descripción general del excitador PUDU](overview.md)
- [Ajuste Poo Drive para grosor de bajos](dial-poo-drive-for-lf-thickness.md)
- [Mezcle la mejora Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Elija el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
