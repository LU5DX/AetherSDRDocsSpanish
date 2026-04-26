# Ajuste Poo / Tune a la fundamental de su voz (TX) o para resaltar los graves en RX

El control **Poo / Tune** establece la frecuencia central de la banda de saturación de baja frecuencia. En TX, apúntelo a la fundamental de su voz para añadir cuerpo y calidez en el tono correcto. En RX, muévalo hacia el contenido de baja frecuencia dominante del audio entrante para resaltar los graves del programa.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena Aetherial Audio. Si el applet Poodoo no es visible, habilite la etapa PUDU mediante el widget CHAIN en el lado TX o RX.
- Decida si está ajustando la cadena TX ("Aetherial TX Poodoo™") o la cadena RX ("Aetherial RX Poodoo™") — ambas tienen configuraciones completamente independientes.

## Pasos

1. Abra el editor PUDU para el lado que desea ajustar: haga doble clic en la etapa PUDU en el widget CHAIN. Se abre el editor sin marco titulado "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX".
2. Localice el grupo **Poo** — los tres controles bajo la etiqueta de corchete "Poo" en la mitad izquierda de la fila de mandos.
3. Gire el control **Tune** (el mando central del grupo Poo) a la frecuencia objetivo.
   - Para TX: comience cerca de la fundamental de su voz. La fundamental típica de una voz masculina es 85–180 Hz; la de una voz femenina típica es 165–255 Hz. El valor predeterminado es 100 Hz.
   - Para RX: desplace el control hacia el contenido de baja frecuencia dominante del programa que desea enfatizar.
4. Observe el logotipo de PooDoo — su brillo pulsa con el RMS de la señal procesada, proporcionando retroalimentación en tiempo real mientras ajusta la frecuencia.
5. Ajuste **Poo / Mix** para mezclar el resultado a su gusto. Los ajustes se guardan automáticamente.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Poo / Tune** | 100 Hz | 50 a 160 Hz | `ClientPuduTxPooTuneHz` / `ClientPuduRxPooTuneHz` |
| **Poo / Drive** | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxPooDriveDb` / `ClientPuduRxPooDriveDb` |
| **Poo / Mix** | 30 % | 0 a 100 % | `ClientPuduTxPooMix` / `ClientPuduRxPooMix` |

El control **Poo / Tune** utiliza un mapeo lineal en su rango de 50–160 Hz. La pantalla muestra valores en hercios enteros (por ejemplo, "100 Hz").

## Consejos

- La banda Poo es intencionalmente estrecha. Si escucha poco efecto después de ajustar la frecuencia, suba primero **Poo / Drive** y luego vuelva a desplazar **Poo / Tune** hasta notar que la saturación actúa.
- En el modo **Even**, la etapa Poo utiliza saturación de graves Big Bottom LF; en el modo **Odd**, utiliza un compresor de graves de alimentación directa. La frecuencia de ajuste óptima puede diferir ligeramente entre modos — verifíquela nuevamente al cambiar de modo.
- Mantenga **Poo / Mix** por debajo de 50 % en TX para evitar ensuciar la señal transmitida. Comience con el valor predeterminado de 30 % y auméntelo solo si la mejora es imperceptible.

## Solución de problemas

- **Girar Poo / Tune no produce ningún efecto audible** — confirme que la etapa PUDU está habilitada (el widget CHAIN controla el bypass). Verifique también que **Poo / Drive** esté por encima de 0.0 dB y que **Poo / Mix** esté por encima de 0 %; ambos en sus valores mínimos silenciarán la banda Poo independientemente del ajuste de Tune.
- **Los controles del grupo Poo no son visibles** — el applet PUDU permanece oculto hasta que la etapa PUDU se habilita mediante el widget CHAIN o el editor flotante.

## Relacionados

- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
- [Ajuste Poo Drive para grosor en bajas frecuencias](dial-poo-drive-for-lf-thickness.md)
- [Mezcle la mejora Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Elija el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
