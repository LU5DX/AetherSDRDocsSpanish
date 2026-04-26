# Dial Poo Drive para el grosor de bajas frecuencias

El control **Poo / Drive** determina con qué intensidad se conduce el saturador de bajas frecuencias o el compresor de graves. Al aumentarlo, se añade cuerpo y peso a los tonos graves del audio transmitido.

## Antes de comenzar

- El bloque PUDU debe estar habilitado en la cadena PooDoo Audio (TXDSP). El applet PUDU permanece oculto hasta que ese bloque esté activo.
- Abra el applet PUDU navegando al subcontenedor **PUDU** dentro del contenedor principal PooDoo Audio (TXDSP), o haga doble clic en el bloque PUDU (Enh) en el widget CHAIN para abrir el editor flotante de PUDU.

## Pasos

1. Localice el grupo **Poo** en el applet PUDU. Los tres controles bajo la etiqueta del grupo **Poo** son **Drive**, **Tune** y **Mix**.
2. Gire el control **Drive** hasta el valor deseado. El control muestra su valor actual como `X.X dB`.
3. Suelte el control. El ajuste se guarda automáticamente en `ClientPuduTxPooDriveDb`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Drive** | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxPooDriveDb` | Conduce con mayor intensidad el saturador de bajas frecuencias (modo Even) o el compresor de graves (modo Odd). Los valores más altos añaden mayor cuerpo en los graves. |

## Consejos

- En el modo **Even**, Drive alimenta el saturador LF de linaje Aphex Big Bottom. En el modo **Odd**, alimenta el compresor de graves de alimentación anticipada (feed-forward) de linaje Behringer. El carácter del efecto con ajustes altos de Drive difiere entre ambos modos.
- Utilice el control **Poo / Mix** para ajustar cuánto de la señal de graves procesada se mezcla con la señal seca. Un Drive alto con un Mix bajo puede añadir calidez sutil sin opacar el tono original.
- El logotipo de PooDoo pulsa con el nivel RMS de la señal procesada, proporcionando una indicación visual de que el bloque Poo está funcionando.

## Relacionados

- [Descripción general del excitador PUDU](overview.md)
- [Elegir el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Poo a la frecuencia fundamental de su voz](tune-poo-to-the-fundamental-of-your-voice.md)
- [Mezclar el realce Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Desactivar PUDU desde la cadena](bypass-pudu-from-the-chain.md)
