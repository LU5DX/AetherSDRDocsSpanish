# Observe la reducción de ganancia en vivo mientras habla o escucha

El ClientCompApplet muestra un medidor de reducción de ganancia en vivo y una curva de transferencia animada mientras el audio pasa a través del compresor. Utilice estos indicadores para ver qué tan duro está trabajando el compresor en tiempo real — mientras transmite (lado TX) o mientras recibe audio (lado RX) — sin abrir el editor flotante.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa del compresor que desea monitorear (TX o RX) debe estar habilitada; el mosaico se renderiza con opacidad reducida cuando la etapa está desactivada. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el mosaico aparece atenuado.

## Pasos

1. Ubique el subcontenedor "Aetherial Compressor" (lado TX) o "Aetherial AGC-C" (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Hable por su micrófono (TX) o deje que el audio recibido se reproduzca (RX).
3. Observe la **Barra de reducción de ganancia** — la franja horizontal ámbar debajo de la curva de transferencia. La franja se llena desde la derecha a medida que aumenta la reducción de ganancia, hasta un máximo de 20 dB.
4. Observe la **Curva de transferencia** — la bola de envolvente en vivo se mueve a lo largo de la curva estática para mostrar el nivel de entrada actual en relación con los ajustes de umbral y relación.
5. Utilice la marca de -6 dB en la **Barra de reducción de ganancia** como referencia. Un llenado que alcanza o supera ligeramente esa marca de forma consistente es una cantidad de compresión de trabajo típica.

## Función de cada control

| Control | Tipo | Qué ve | Notas |
|---|---|---|---|
| Curva de transferencia | Indicador | Curva estática de entrada/salida con una bola en vivo al nivel de envolvente actual. | Solo vista en el applet; editable en el editor flotante. |
| Barra de reducción de ganancia | Medidor | Franja horizontal ámbar, llenado desde la derecha. Escala de 0 a 20 dB de reducción de ganancia. Una marca indica el punto de -6 dB. | Se actualiza a aproximadamente 30 Hz con balística suavizada. |
| Thresh | Perilla | Umbral actual. Valor predeterminado -18.0 dB; rango -60.0 a 0.0 dB. | TX: `ClientCompTxThresholdDb`. RX: `ClientCompRxThresholdDb`. |
| Ratio | Perilla | Relación actual. Valor predeterminado 3.0; rango 1.0 a 20.0. Se muestra como X.XX:1. | TX: `ClientCompTxRatio`. RX: `ClientCompRxRatio`. |
| Attack | Perilla | Tiempo de ataque actual. Valor predeterminado 20.0 ms; rango 0.1 a 300.0 ms. | TX: `ClientCompTxAttackMs`. RX: `ClientCompRxAttackMs`. |
| Release | Perilla | Tiempo de liberación actual. Valor predeterminado 200 ms; rango 5 a 2000 ms. | TX: `ClientCompTxReleaseMs`. RX: `ClientCompRxReleaseMs`. |
| Makeup | Perilla | Ganancia de compensación actual. Valor predeterminado 0.0 dB; rango -12.0 a 24.0 dB. | TX: `ClientCompTxMakeupDb`. RX: `ClientCompRxMakeupDb`. |

## Consejos

- Si la **Barra de reducción de ganancia** nunca se mueve, el nivel de entrada no está superando el umbral. Baje la perilla Thresh o aumente la ganancia de su micrófono.
- Si la **Barra de reducción de ganancia** está fijada en 20 dB o cerca de forma continua, la relación o el umbral están configurados de forma muy agresiva. Aumente el valor de Thresh o baje la perilla Ratio para suavizar la compresión.
- La bola de envolvente en la **Curva de transferencia** descansa en la línea de umbral cuando no hay audio presente. Durante el audio, viaja a lo largo de la curva; una bola situada en la porción curva de la curva confirma compresión activa.
- Los mosaicos TX y RX se actualizan de forma independiente. Puede monitorear ambos simultáneamente si ambos subcontenedores están expandidos.

## Solución de problemas

- **El mosaico aparece atenuado** — La etapa del compresor está desactivada. El mosaico ahora se renderiza con aproximadamente un 55 % de opacidad cuando la etapa está deshabilitada, coincidiendo con el efecto de atenuación utilizado en la curva de EQ. Active la etapa desde el widget CHAIN (un solo clic en la etapa COMP) o consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md).
- **La Barra de reducción de ganancia no muestra movimiento durante el audio** — El nivel de entrada no está alcanzando el umbral. Reduzca el valor de la perilla Thresh o verifique que el dispositivo de audio correcto esté activo y produciendo señal.
- **La bola de envolvente no se mueve** — El applet no está conectado a un motor de audio activo. Verifique que la radio esté conectada y que el audio fluya a través de la cadena de procesamiento TX o RX correspondiente.

## Relacionados

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
