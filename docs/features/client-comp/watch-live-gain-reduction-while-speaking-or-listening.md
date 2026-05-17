# Observe la reducción de ganancia en vivo mientras habla o escucha

El ClientCompApplet muestra un medidor de reducción de ganancia en vivo y una curva de transferencia animada mientras el audio pasa por el compresor. Utilice estos indicadores para ver en tiempo real qué tan fuerte está trabajando el compresor — durante la transmisión (lado TX) o al recibir audio (lado RX) — sin tener que abrir el editor flotante.

Cada perilla del compresor admite la edición de valores en línea: haga clic en el texto del valor para ingresar directamente un valor numérico preciso, luego presione Enter o haga clic en otro lugar para confirmarlo.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa del compresor que desea monitorear (TX o RX) debe estar habilitada; el mosaico se renderiza con opacidad reducida cuando la etapa está desactivada. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el mosaico aparece atenuado.

## Pasos

1. Localice el subcontenedor "Aetherial Compressor" (lado TX) o "Aetherial AGC-C" (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Hable en su micrófono (TX) o deje que el audio recibido se reproduzca (RX).
3. Observe la **Barra de reducción de ganancia** — la franja horizontal de color ámbar debajo de la curva de transferencia. La franja se llena desde la derecha a medida que aumenta la reducción de ganancia, hasta un máximo de 20 dB.
4. Observe la **Curva de transferencia** — la bola de envolvente en vivo se mueve a lo largo de la curva estática para mostrar el nivel de entrada actual en relación con los ajustes de umbral y relación.
5. Utilice la marca de -6 dB en la **Barra de reducción de ganancia** como referencia. Un llenado que alcance o supere ligeramente esa marca de forma constante es una cantidad de compresión de trabajo típica.

## Ingreso de valores precisos directamente

Haga clic en el texto del valor mostrado de cualquier perilla para abrir un editor en línea. Escriba un número y presione Enter, o haga clic en otro lugar para aplicar el valor. El editor se cierra automáticamente y la perilla se actualiza.

- El editor acepta formatos decimales según la configuración regional (por ejemplo, "12,5" en regiones de coma decimal).
- Ingrese números simples sin unidades (por ejemplo, escriba "5" o "5.0" para 5.0 ms de Ataque).
- Presione Escape para cancelar la edición y restaurar el valor anterior.
- El editor aparece como una superposición transparente que coincide con la apariencia normal de la etiqueta. Cuando está enfocado, un fondo oscuro sutil y un borde cian indican el modo de edición.

## Función de cada control

| Control | Tipo | Lo que ve | Notas |
|---|---|---|---|
| Curva de transferencia | Indicador | Curva de entrada/salida estática con una bola en vivo en el nivel de envolvente actual. | Solo visualización en el applet; editable en el editor flotante. Las etiquetas de los ejes usan QStaticText con almacenamiento en caché agresivo para un renderizado más suave, especialmente en pantallas HiDPI. |
| Barra de reducción de ganancia | Medidor | Franja horizontal ámbar, llenada desde la derecha. La escala va de 0 a 20 dB de reducción de ganancia. Una marca señala el punto de -6 dB. | Se actualiza a aproximadamente 30 Hz con balística suavizada. |
| Thresh | Perilla | Umbral actual. Predeterminado -18.0 dB; rango -60.0 a 0.0 dB. Haga clic en el valor para escribir un umbral preciso. | TX: `ClientCompTxThresholdDb`. RX: `ClientCompRxThresholdDb`. |
| Ratio | Perilla | Relación actual. Predeterminado 3.0; rango 1.0 a 20.0. Se muestra como X.XX:1. Haga clic en el valor para escribir una relación precisa. | TX: `ClientCompTxRatio`. RX: `ClientCompRxRatio`. |
| Attack | Perilla | Tiempo de ataque actual. Predeterminado 20.0 ms; rango 0.1 a 300.0 ms. Haga clic en el valor para escribir un tiempo de ataque preciso. | TX: `ClientCompTxAttackMs`. RX: `ClientCompRxAttackMs`. |
| Release | Perilla | Tiempo de liberación actual. Predeterminado 200 ms; rango 5 a 2000 ms. Haga clic en el valor para escribir un tiempo de liberación preciso. | TX: `ClientCompTxReleaseMs`. RX: `ClientCompRxReleaseMs`. |
| Makeup | Perilla | Ganancia de compensación actual. Predeterminado 0.0 dB; rango -12.0 a 24.0 dB. Haga clic en el valor para escribir una ganancia de compensación precisa. | TX: `ClientCompTxMakeupDb`. RX: `ClientCompRxMakeupDb`. |

## Consejos

- Si la **Barra de reducción de ganancia** nunca se mueve, el nivel de entrada no está superando el umbral. Baje la perilla Thresh o aumente la ganancia de su micrófono.
- Si la **Barra de reducción de ganancia** está fija en o cerca de 20 dB continuamente, la relación o el umbral están configurados de forma muy agresiva. Aumente el valor de Thresh o baje la perilla Ratio para suavizar la compresión.
- La bola de envolvente en la **Curva de transferencia** descansa en la línea de umbral cuando no hay audio presente. Durante el audio, viaja a lo largo de la curva; una bola situada en la porción curvada de la curva confirma compresión activa.
- Los mosaicos TX y RX se actualizan de forma independiente. Puede monitorear ambos simultáneamente si ambos subcontenedores están expandidos.
- Las etiquetas de los ejes de la curva de transferencia utilizan texto estático en caché para mejorar el rendimiento del renderizado. La caché se reconstruye automáticamente al cambiar entre los modos de visualización compacto y completo.
- Para ingresar un valor preciso, haga clic en el texto del valor mostrado. El editor en línea acepta entrada numérica con separadores decimales según la configuración regional. Use signos negativos cuando sea apropiado (por ejemplo, "-24.0" para el umbral).

## Solución de problemas

- **El mosaico aparece atenuado** — La etapa del compresor está desactivada. El mosaico ahora se renderiza con aproximadamente un 55 % de opacidad cuando la etapa está deshabilitada, coincidiendo con el efecto de atenuación utilizado en la curva del ecualizador. Habilite la etapa desde el widget CHAIN (haga clic una vez en la etapa COMP) o consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md).
- **La Barra de reducción de ganancia no muestra movimiento durante el audio** — El nivel de entrada no está alcanzando el umbral. Reduzca el valor de la perilla Thresh o verifique que el dispositivo de audio correcto esté activo y produciendo señal.
- **La bola de envolvente no se mueve** — El applet no está conectado a un motor de audio activo. Verifique que la radio esté conectada y que el audio fluya a través de la cadena de procesamiento TX o RX correspondiente.
- **El editor en línea no aparece** — Haga clic directamente en el texto del valor numérico debajo de cada perilla. El editor solo aparece al hacer clic en el valor, no en el cuerpo de la perilla.

## Relacionado

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
