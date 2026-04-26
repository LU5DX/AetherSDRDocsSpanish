# Monitorear la reducción de ganancia en tiempo real al hablar o escuchar

El ClientCompApplet muestra un medidor de reducción de ganancia en tiempo real y una curva de transferencia animada mientras el audio pasa por el compresor. Use estos indicadores para ver qué tan intensamente trabaja el compresor en tiempo real — durante la transmisión (lado TX) o durante la recepción de audio (lado RX) — sin necesidad de abrir el editor flotante.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa del compresor que desea monitorear (TX o RX) debe estar habilitada — el mosaico permanece oculto mientras la etapa está desactivada. Consulte [Desactivar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md) si el mosaico no es visible.

## Pasos

1. Localice el subcontenedor "Aetherial Compressor" (lado TX) o el subcontenedor "Aetherial AGC-C" (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Hable por su micrófono (TX) o deje que el audio recibido se reproduzca (RX).
3. Observe la **barra de reducción de ganancia** — la franja horizontal ámbar debajo de la curva de transferencia. La franja se llena desde la derecha a medida que aumenta la reducción de ganancia, hasta un máximo de 20 dB.
4. Observe la **curva de transferencia** — la bola de envolvente en movimiento se desplaza a lo largo de la curva estática para mostrar el nivel de entrada actual en relación con los ajustes de umbral y relación.
5. Use la marca de -6 dB en la **barra de reducción de ganancia** como referencia. Un llenado que alcanza o supera ligeramente esa marca de forma constante representa una cantidad de compresión de trabajo típica.

## Qué hace cada control

| Control | Tipo | Qué se ve | Notas |
|---|---|---|---|
| Curva de transferencia | Indicador | Curva estática de entrada/salida con una bola en movimiento en el nivel de envolvente actual. | Solo lectura en el applet; editable en el editor flotante. |
| Barra de reducción de ganancia | Medidor | Franja horizontal ámbar, rellena desde la derecha. La escala va de 0 a 20 dB de reducción de ganancia. Una marca señala el punto de -6 dB. | Se actualiza a aproximadamente 30 Hz con balística suavizada. |
| Thresh | Mando | Umbral actual. Valor predeterminado -18.0 dB; rango de -60.0 a 0.0 dB. | TX: `ClientCompTxThresholdDb`. RX: `ClientCompRxThresholdDb`. |
| Ratio | Mando | Relación actual. Valor predeterminado 3.0; rango de 1.0 a 20.0. Se muestra como X.XX:1. | TX: `ClientCompTxRatio`. RX: `ClientCompRxRatio`. |
| Attack | Mando | Tiempo de ataque actual. Valor predeterminado 20.0 ms; rango de 0.1 a 300.0 ms. | TX: `ClientCompTxAttackMs`. RX: `ClientCompRxAttackMs`. |
| Release | Mando | Tiempo de liberación actual. Valor predeterminado 200 ms; rango de 5 a 2000 ms. | TX: `ClientCompTxReleaseMs`. RX: `ClientCompRxReleaseMs`. |
| Makeup | Mando | Ganancia de compensación actual. Valor predeterminado 0.0 dB; rango de -12.0 a 24.0 dB. | TX: `ClientCompTxMakeupDb`. RX: `ClientCompRxMakeupDb`. |

## Consejos

- Si la **barra de reducción de ganancia** no se mueve nunca, el nivel de entrada no supera el umbral. Reduzca el mando Thresh o aumente la ganancia de su micrófono.
- Si la **barra de reducción de ganancia** permanece fija en o cerca de 20 dB de forma continua, la relación o el umbral están configurados de manera muy agresiva. Aumente el valor de Thresh o reduzca el mando Ratio para suavizar la compresión.
- La bola de envolvente en la **curva de transferencia** descansa sobre la línea de umbral cuando no hay audio presente. Durante el audio, se desplaza a lo largo de la curva; una bola situada en la parte curvada de la curva confirma que la compresión está activa.
- Los mosaicos TX y RX se actualizan de forma independiente. Puede monitorear ambos simultáneamente si ambos subcontenedores están expandidos.

## Solución de problemas

- **El mosaico no es visible** — La etapa del compresor está desactivada. Habilite la etapa desde el widget CHAIN (haga clic una vez en la etapa COMP) o consulte [Desactivar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- **La barra de reducción de ganancia no muestra movimiento durante el audio** — El nivel de entrada no alcanza el umbral. Reduzca el valor del mando Thresh o verifique que el dispositivo de audio correcto esté activo y generando señal.
- **La bola de envolvente no se mueve** — El applet no está conectado a un motor de audio activo. Verifique que la radio esté conectada y que el audio fluya a través de la cadena de procesamiento TX o RX correspondiente.

## Relacionados

- [Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Configurar la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Ajustar ataque/liberación para lograr una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Abrir el editor completo del compresor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
