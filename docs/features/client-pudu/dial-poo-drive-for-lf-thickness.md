# Dial Poo Drive para el grosor de bajas frecuencias

El control Poo / Drive determina con qué intensidad se impulsa el saturador de bajas frecuencias o el compresor de graves. Al aumentarlo, se añade grosor y peso al extremo inferior del audio transmitido.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena PooDoo Audio. El applet PUDU permanece oculto hasta que la etapa esté activa.
- Abra el applet PUDU navegando al subcontenedor "PUDU" dentro del contenedor principal PooDoo Audio (TXDSP), o haga doble clic en la etapa PUDU (Enh) en el widget CHAIN para abrir el editor flotante de PUDU.

## Pasos

1. Localice el grupo "Poo" en el applet PUDU. Los tres controles giratorios bajo la etiqueta del grupo "Poo" son Drive, Tune y Mix.
2. Gire el primer control, etiquetado "Drive", en sentido horario para aumentar el drive o en sentido antihorario para reducirlo.
3. Lea el valor actual en la pantalla central del control, mostrado como `X.X dB`.
4. Suelte el control. La configuración se guarda inmediatamente en `ClientPuduTxPooDriveDb`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Poo / Drive | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxPooDriveDb` | Impulsa con mayor intensidad el saturador de bajas frecuencias (modo Even) o el compresor de graves (modo Odd). Mapeo lineal. |
| Poo / Tune | 100 Hz | 50 a 160 Hz | `ClientPuduTxPooTuneHz` | Centra la banda de enfoque de bajas frecuencias. |
| Poo / Mix | 30 % | 0 a 100 % | `ClientPuduTxPooMix` | Mezcla la banda de graves procesada con la señal sin procesar. |

## Consejos

- El carácter del control Drive depende del modo seleccionado. En el modo "Even", impulsa un saturador asimétrico de linaje Aphex con saturación de graves Big Bottom. En el modo "Odd", impulsa un compresor de graves feed-forward de linaje Behringer. Establezca el modo antes de ajustar el Drive.
- El logotipo de PooDoo pulsa con el nivel RMS de la señal procesada. Obsérvelo mientras aumenta el Drive: un pulso más rápido y brillante indica que se está añadiendo más energía en las bajas frecuencias.
- Use Poo / Mix para controlar cuánto de la señal procesada llega a la salida. Un Drive alto con un Mix bajo puede añadir calidez sutil sin saturar la señal original.

## Relacionados

- [Seleccionar el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Poo al fundamental de su voz](tune-poo-to-the-fundamental-of-your-voice.md)
- [Mezclar el realce de Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Descripción general del excitador PUDU](overview.md)
