# Dial Poo Drive para el grosor de baja frecuencia

El mando **Poo / Drive** controla qué tan fuertemente se impulsa el saturador o compresor de bajas frecuencias. Al aumentarlo se añade más grosor en LF y mayor densidad armónica a la banda baja procesada.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN para el lado TX o RX que desea ajustar. Consulte [Omitir PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md).
- Abra el applet: en el contenedor principal Aetherial Audio (TXDSP), localice el subcontenedor **Aetherial TX Poodoo™** o **Aetherial RX Poodoo™**. Si está oculto, haga doble clic en la etapa PUDU dentro del widget CHAIN para abrir el editor correspondiente ("Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX").

## Pasos

1. Localice el grupo **Poo** — la etiqueta entre corchetes con la lectura "Poo" abarca los tres mandos del lado izquierdo.
2. Encuentre el primer mando bajo ese corchete, etiquetado como **Drive**.
3. Gire **Drive** hasta el valor deseado. El mando muestra el valor actual como `X.X dB`.
4. Suelte el mando. La configuración se guarda automáticamente.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Configuración persistida |
|---|---|---|---|
| **Poo / Drive** (TX) | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxPooDriveDb` |
| **Poo / Drive** (RX) | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduRxPooDriveDb` |

La asignación es lineal. Los valores más altos impulsan con mayor fuerza el saturador de baja frecuencia (modo Even) o el compresor de graves (modo Odd), produciendo mayor efecto LF con el mismo nivel de mezcla **Poo / Mix**.

## Consejos

- El logotipo de PooDoo pulsa con el RMS de la señal húmeda. Obsérvelo mientras gira **Drive** — una pulsación visible en el contenido de graves confirma que la etapa está procesando.
- En modo **Even**, valores altos de Drive activan la saturación LF Big Bottom de manera más agresiva. En modo **Odd**, valores altos de Drive aumentan la compresión de graves con alimentación directa. Elija primero el modo y luego ajuste Drive. Consulte [Seleccionar el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md).
- Drive y **Poo / Mix** interactúan entre sí. Un Drive alto con un Mix bajo puede aplicar un procesado intenso de graves que se mezcla de forma sutil. Consulte [Mezclar la mejora Poo con Mix](blend-the-poo-enhancement-with-mix.md).
- Para enfocar el Drive en una frecuencia específica, ajuste primero **Poo / Tune**. Consulte [Sintonizar Poo a la fundamental de su voz (TX) o para realzar los graves del programa en RX](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md).

## Relacionados

- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
- [Seleccionar el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Sintonizar Poo a la fundamental de su voz (TX) o para realzar los graves del programa en RX](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Mezclar la mejora Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Omitir PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md)
