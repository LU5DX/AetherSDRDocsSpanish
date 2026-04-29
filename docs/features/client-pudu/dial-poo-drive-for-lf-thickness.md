# Dial Poo Drive para el grosor de baja frecuencia

El control **Poo / Drive** regula la intensidad con que se impulsa el saturador o compresor de baja frecuencia. Al aumentarlo se añade más grosor en LF y densidad armónica a la banda baja procesada.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN del lado TX o RX que desea ajustar. Consulte [Omitir PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md).
- Abra el applet: en el contenedor principal Aetherial Audio (TXDSP), localice el subcontenedor **Aetherial TX Poodoo™** o **Aetherial RX Poodoo™**. Si está oculto, haga doble clic en la etapa PUDU del widget CHAIN para abrir el editor correspondiente ("Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX").

## Pasos

1. Localice el grupo **Poo** — la etiqueta de corchete que muestra "Poo" abarca los tres controles del lado izquierdo.
2. Encuentre el primer control bajo ese corchete, etiquetado **Drive**.
3. Gire **Drive** hasta el valor deseado. El control muestra el valor actual como `X.X dB`.
4. Suelte el control. La configuración se guarda automáticamente.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Configuración persistente |
|---|---|---|---|
| **Poo / Drive** (TX) | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxPooDriveDb` |
| **Poo / Drive** (RX) | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduRxPooDriveDb` |

El mapeo es lineal. Los valores más altos impulsan con mayor fuerza el saturador de baja frecuencia (modo Even) o el compresor de bajos (modo Odd), produciendo mayor efecto en LF con el mismo nivel de mezcla en **Poo / Mix**.

## Consejos

- El logotipo de PooDoo pulsa con el nivel RMS de la señal procesada. Obsérvelo mientras gira **Drive** — un pulso visible en el contenido de bajos confirma que la etapa está procesando.
- En el modo **Even**, valores altos de Drive activan la saturación LF Big Bottom de forma más agresiva. En el modo **Odd**, valores altos de Drive incrementan la compresión de bajos por alimentación directa. Elija primero el modo y luego ajuste Drive. Consulte [Elegir el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md).
- Drive y **Poo / Mix** interactúan entre sí. Un Drive alto con un Mix bajo puede aplicar un procesamiento de bajos intenso que se mezcla de forma sutil. Consulte [Mezclar el realce Poo con Mix](blend-the-poo-enhancement-with-mix.md).
- Para enfocar el Drive en una frecuencia específica, ajuste primero **Poo / Tune**. Consulte [Ajustar Poo al fundamental de su voz (TX) o para realzar los graves del programa en RX](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md).

## Relacionados

- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
- [Elegir el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Ajustar Poo al fundamental de su voz (TX) o para realzar los graves del programa en RX](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Mezclar el realce Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Omitir PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md)
