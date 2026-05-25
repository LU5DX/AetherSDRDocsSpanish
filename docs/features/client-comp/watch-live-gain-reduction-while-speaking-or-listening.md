# Observe la reducción de ganancia en vivo mientras habla o escucha

El ClientCompApplet muestra un medidor de reducción de ganancia en vivo y una curva de transferencia animada mientras el audio pasa por el compresor. Use estos indicadores para ver en tiempo real qué tan duro está trabajando el compresor — mientras transmite (lado TX) o mientras recibe audio (lado RX) — sin abrir el editor flotante.

Cada perilla del compresor admite edición inline de valores: haga clic en el texto del valor para ingresar un valor numérico preciso directamente, luego presione Enter o haga clic en otra parte para confirmarlo.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa del compresor que desea monitorear (TX o RX) debe estar habilitada; el mosaico se renderiza con opacidad reducida cuando la etapa está puenteada. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el mosaico aparece atenuado.

## Pasos

1. Localice el subcontenedor "Aetherial Compressor" (lado TX) o "Aetherial AGC-C" (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Hable en su micrófono (TX) o reproduzca audio recibido (RX).
3. Observe la **barra de reducción de ganancia** — la franja horizontal ámbar debajo de la curva de transferencia. La franja se llena desde la derecha a medida que aumenta la reducción de ganancia, hasta un máximo de 20 dB.
4. Observe la **curva de transferencia** — la bola de envolvente en vivo se mueve a lo largo de la curva estática para mostrar el nivel de entrada actual en relación con los ajustes de umbral y relación.
5. Use la marca de -6 dB en la **barra de reducción de ganancia** como referencia. Un llenado que alcanza o supera ligeramente esa marca es una cantidad de compresión de trabajo típica.

## Ingreso de valores precisos directamente

Haga clic en cualquier texto de valor mostrado de una perilla para abrir un editor inline. Escriba un número y presione Enter, o haga clic en otra parte para aplicar el valor. El editor se cierra automáticamente y la perilla se actualiza.

- El editor acepta formatos decimales según la configuración regional (por ejemplo, "12,5" en regiones con coma decimal).
- Ingrese números simples sin unidades (por ejemplo, escriba "5" o "5.0" para 5.0 ms de Ataque).
- Presione Escape para cancelar la edición y restaurar el valor anterior.
- El editor aparece como una superposición transparente que coincide con la apariencia normal de la etiqueta. Cuando está enfocado, un fondo oscuro sutil y un borde cian indican el modo de edición.

## Función de cada control

| Control           | Tipo                                                                                                                                                                                                                                             | Lo que se ve                                                                                                                                                                 |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva transfer.   | Indicador                                                                                                                                                                                                                                        | Curva estática de entrada/salida con una bola en vivo al nivel de envolvente actual.                                                                                         |
| Barra red. gan.   | Medidor                                                                                                                                                                                                                                          | Franja horizontal ámbar, llenado desde la derecha. Escala de 0 a 20 dB de reducción de ganancia. Una marca indica el punto de -6 dB.                                        |
| Thresh            | Perilla                                                                                                                                                                                                                                          | Umbral actual. Valor predeterminado -18.0 dB; rango -60.0 a 0.0 dB. Haga clic en el valor para escribir un umbral preciso.                                                  |
| Ratio             | Perilla                                                                                                                                                                                                                                          | Relación actual. Valor predeterminado 3.0; rango 1.0 a 20.0. Se muestra como X.XX:1. Haga clic en el valor para escribir una relación precisa.                               |
| Attack            | Perilla                                                                                                                                                                                                                                          | Tiempo de ataque actual. Valor predeterminado 20.0 ms; rango 0.1 a 300.0 ms. Haga clic en el valor para escribir un tiempo de ataque preciso.                                |
| Release           | Perilla                                                                                                                                                                                                                                          | Tiempo de liberación actual. Valor predeterminado 200 ms; rango 5 a 2000 ms. Haga clic en el valor para escribir un tiempo de liberación preciso.                           |
| Makeup            | Perilla                                                                                                                                                                                                                                          | Ganancia de compensación actual. Valor predeterminado 0.0 dB; rango -12.0 a 24.0 dB. Haga clic en el valor para escribir una ganancia de compensación precisa.               |
| Drive             | Aumento de ganancia previo a la compresión. Empuja más señal por encima del umbral para que el compresor actúe con más fuerza, aumentando la potencia promedio. Combínelo con Phase para mantener los picos limpios.                           | Se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta muestra '+X.X dB'. Tooltip explica la combinación #2887 de reducción de PAPR.            |
| Phase             | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/oct de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcional). Simetriza los picos asimétricos de la voz antes de la compresión para reducir el PAPR. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. Tooltip: 'Rotador de fase pre-comp (#2887). 0=off, 4=valor predeterminado broadcast.' |

## Consejos

- Si la **barra de reducción de ganancia** nunca se mueve, el nivel de entrada no está cruzando el umbral. Baje la perilla Thresh o aumente la ganancia de su micrófono.
- Si la **barra de reducción de ganancia** está fija en o cerca de 20 dB continuamente, la relación o el umbral están ajustados de forma muy agresiva. Aumente el valor de Thresh o baje la perilla Ratio para suavizar la compresión.
- La bola de envolvente en la **curva de transferencia** descansa en la línea de umbral cuando no hay audio presente. Durante el audio, viaja a lo largo de la curva; una bola situada en la porción curvada de la curva confirma que hay compresión activa.
- Los mosaicos TX y RX se actualizan de forma independiente. Puede monitorear ambos simultáneamente si ambos subcontenedores están expandidos.
- Las etiquetas de los ejes de la curva de transferencia utilizan texto estático en caché para mejorar el rendimiento de renderizado. La caché se reconstruye automáticamente al cambiar entre los modos de visualización compacto y completo.
- Para ingresar un valor preciso, haga clic en el texto del valor mostrado. El editor inline acepta entrada numérica con separadores decimales según la configuración regional. Use signos negativos cuando corresponda (por ejemplo, "-24.0" para el umbral).

## Solución de problemas

- **El mosaico aparece atenuado** — La etapa del compresor está puenteada. El mosaico ahora se renderiza con aproximadamente 55 % de opacidad cuando la etapa está deshabilitada, coincidiendo con el efecto de atenuación utilizado en la curva EQ. Habilite la etapa desde el widget CHAIN (un solo clic en la etapa COMP) o consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md).
- **La barra de reducción de ganancia no muestra movimiento durante el audio** — El nivel de entrada no está alcanzando el umbral. Reduzca el valor de la perilla Thresh o verifique que el dispositivo de audio correcto esté activo y produciendo señal.
- **La bola de envolvente no se mueve** — El applet no está conectado a un motor de audio activo. Verifique que la radio esté conectada y que el audio fluya a través de la cadena de procesamiento TX o RX correspondiente.
- **El editor inline no aparece** — Haga clic directamente en el texto del valor numérico debajo de cada perilla. El editor solo aparece al hacer clic en el valor, no en el cuerpo de la perilla en sí.

## Relacionado

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
