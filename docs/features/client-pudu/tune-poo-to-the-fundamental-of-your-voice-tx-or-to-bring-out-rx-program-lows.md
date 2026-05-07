# Sintonice Cuerpo a la frecuencia fundamental de su voz (TX) o para resaltar los bajos del programa de RX

El mando **Body / Tune** establece la frecuencia central de la banda de saturación de baja frecuencia. En TX, apúntelo a la frecuencia fundamental de su voz para añadir cuerpo y calidez en el tono adecuado. En RX, muévalo hacia el contenido de baja frecuencia dominante del audio entrante para resaltar los bajos del programa.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena Aetherial Audio. Si el applet Poodoo no es visible, habilite la etapa PUDU a través del widget CHAIN en el lado TX o RX.
- Decida si está ajustando la cadena TX ("Aetherial TX Poodoo™") o la cadena RX ("Aetherial RX Poodoo™") — tienen parámetros completamente independientes.

## Pasos

1. Abra el editor PUDU para el lado que desea ajustar: haga doble clic en la etapa PUDU en el widget CHAIN. Se abrirá el editor sin marco titulado "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX".
2. Localice el grupo **Poo** — los tres mandos bajo la etiqueta de grupo "Poo" en la mitad izquierda de la fila de mandos.
3. Gire el mando **Poo / Tune** (el mando central del grupo Poo) a la frecuencia deseada.
   - Para TX: comience cerca de la frecuencia fundamental de su voz. Una voz masculina típica tiene un fundamental de 85–180 Hz; una voz femenina típica tiene un fundamental de 165–255 Hz. El valor predeterminado es 100 Hz.
   - Para RX: barra hacia el contenido de baja frecuencia dominante del programa que desee enfatizar.
4. Monitoree el logotipo PooDoo: su brillo pulsa con el RMS de la señal procesada, proporcionando retroalimentación en tiempo real mientras ajusta la frecuencia.
5. Ajuste **Poo / Mix** para mezclar el resultado a su gusto. Los cambios se guardan automáticamente.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Poo / Tune** | 100 Hz | 50 a 160 Hz | `ClientPuduTxPooTuneHz` / `ClientPuduRxPooTuneHz` |
| **Poo / Drive** | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxPooDriveDb` / `ClientPuduRxPooDriveDb` |
| **Poo / Mix** | 30 % | 0 a 100 % | `ClientPuduTxPooMix` / `ClientPuduRxPooMix` |

El mando **Poo / Tune** utiliza un mapeo lineal en su rango de 50–160 Hz. La lectura se muestra en hercios enteros (por ejemplo, "100 Hz").

## Consejos

- La banda Poo es intencionalmente estrecha. Si escucha poco efecto después de la sintonización, primero suba **Poo / Drive** y luego vuelva a barrer **Poo / Tune** hasta que oiga la saturación activarse.
- En modo **Even**, la etapa Poo usa saturación LF Big Bottom; en modo **Odd** usa un compresor de graves feed-forward. La frecuencia de sintonización óptima puede diferir ligeramente entre modos — vuelva a verificarla después de cambiar.
- Mantenga **Poo / Mix** por debajo del 50 % en TX para evitar empañar la señal transmitida. Comience con el valor predeterminado del 30 % y auméntelo solo si la mejora es inaudible.
- Cuando la etapa PUDU está en bypass, todo el applet se atenúa a aproximadamente un 55 % de opacidad. Esto es solo un indicador visual — no se pierde ningún parámetro.

## Solución de problemas

- **Girar Poo / Tune no tiene efecto audible** — confirme que la etapa PUDU está habilitada (el widget CHAIN controla el bypass). Además, verifique que **Poo / Drive** esté por encima de 0.0 dB y **Poo / Mix** esté por encima del 0 %; ambos en sus mínimos silenciarán la banda Poo independientemente del ajuste de Tune.
- **Los mandos del grupo Poo no son visibles** — el applet PUDU está oculto hasta que la etapa PUDU se habilite a través del widget CHAIN o del editor flotante.

## Relacionados

- [Resumen de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
- [Ajuste Poo Drive para grosor de baja frecuencia](dial-poo-drive-for-lf-thickness.md)
- [Mezcle la mejora Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Elija el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
