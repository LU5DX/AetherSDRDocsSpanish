# Accionamiento hasta que la curva comience a doblarse (calidez en TX o modelado de tono en RX)

Use el mando Drive para introducir la señal en la etapa de válvula y producir saturación armónica. Observar cómo la curva de transferencia se dobla al aumentar Drive le indica exactamente cuándo y cuánta saturación está ocurriendo.

## Antes de comenzar

- La etapa de válvula debe estar habilitada en el lado que desea modelar (TX o RX). Actívela a través del widget CHAIN o abriendo el editor flotante de ese lado.
- El subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) debe estar visible dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.

## Pasos

1. Localice el subcontenedor correcto en el panel de applets: "Aetherial Mic-PreAmp" para el modelado de señal TX, o "Aetherial Dynamic Tube" para el modelado de tono RX.
2. Observe la visualización de la curva de transferencia en la parte superior del applet. Con Drive a 0.0 dB, la curva es una línea diagonal recta — sin saturación.
3. Gire el mando Drive en sentido horario. Observe la curva de transferencia: los hombros comienzan a comprimirse y doblarse a medida que Drive aumenta. La bola de entrada en vivo se mueve a lo largo de la curva y muestra qué parte de la curva está alcanzando su nivel de señal actual.
4. Deje de aumentar Drive cuando la curva muestre la cantidad de curvatura que desea. Una calidez sutil aparece con una curvatura ligera; una saturación más intensa proviene de empujar Drive más hacia 24.0 dB.
5. Si la salida saturada es notablemente más fuerte o más silenciosa que la señal seca, ajuste el mando Output para compensarlo. El medidor OUT del editor flotante (columna de la derecha) muestra el nivel pico posterior a la saturación y le ayuda a juzgar el ajuste.

## Qué hace cada control

| Control   | Por defecto | Rango válido                      |
|-----------|-------------|-----------------------------------|
| Drive     | 0.00 dB     | 0.0 – 24.0 dB                     |
| Tone      | 0.00        | −1.0 – 1.0                        |
| Bias      | 0 %         | 0 – 100 %                         |
| Output    | 0.00 dB     | −24.0 – 12.0 dB                   |
| Dry/Wet   | 100 %       | 0 – 100 %                         |
| Envelope  | 0 %         | −100 – 100 %                      |
| Attack    | 5.00 ms     | 0.1 – 30.0 ms                     |
| Release   | 35.00 ms    | 10.0 – 500.0 ms                   |
| RN2       | desmarcado  | Alternancia solo TX (oculto en modo RX) |

**Curva de transferencia** — Indicador. ClientTubeCurveWidget en modo compacto. Dibuja la curva de transferencia de válvula actualmente configurada con una bola en vivo en la entrada. La forma cambia al ajustar Drive, Bias y la selección del modelo. La bola de entrada en vivo recorre la curva al nivel de señal actual, mostrando el régimen de saturación activo. Sin clave persistida.

**Drive** — Mapeo lineal. Introduce más señal en la etapa de válvula. Los valores más altos hacen que la curva de transferencia se doble más pronunciadamente, produciendo un contenido armónico más fuerte. Etiqueta 'X.XX dB'. Columna izquierda del editor.

**Tone** — Mapeo lineal. Los valores negativos oscurecen la señal saturada; los valores positivos la iluminan. Etiqueta 'X.XX'. Fila central del editor, a la izquierda del selector de modelo.

**Modelo A / B / C** — Botones de alternancia. Selecciona el modelo de carácter de válvula. Selección exclusiva: solo un modelo activo a la vez. Por defecto, Modelo A (marcado). Ámbar cuando está marcado. El valor de respaldo se almacena como entero 0/1/2 en `ClientTubeTxModel` / `ClientTubeRxModel`.

**Bias** — Mapeo lineal. Desplaza el punto de operación en la curva de transferencia, cambiando el equilibrio de armónicos pares e impares. La etiqueta se muestra como porcentaje. Fila central del editor, a la derecha del selector de modelo. Clave de configuración `ClientTubeTxBias` (no `ClientTubeTxBiasAmount`) / `ClientTubeRxBias`.

**Output** — Mapeo lineal. Ganancia de compensación o maquillaje posterior a la válvula. Úselo para igualar el nivel saturado al nivel seco. Etiqueta 'X.XX dB'. Columna izquierda del editor. Clave de configuración `ClientTubeTxOutputDb` (no `ClientTubeTxOutputGainDb`) / `ClientTubeRxOutputDb`.

**Dry/Wet** — Mapeo lineal. Mezcla seco/húmedo. Al 100 %, solo pasa la señal saturada. Reducir Dry/Wet mezcla la señal seca original para una saturación en paralelo. La etiqueta se muestra como porcentaje. Columna izquierda del editor (mando superior).

**Envelope** — Mapeo lineal (−1.0 a +1.0). Modulación dinámica por seguidor de envolvente. Los valores positivos aumentan la excitación en los transitorios (la válvula se calienta más en los picos fuertes); los valores negativos la reducen, comprimiendo los armónicos dinámicamente. La etiqueta se muestra como porcentaje (con signo). Columna derecha del editor. Clave de configuración `ClientTubeTxEnvelope` / `ClientTubeRxEnvelope`.

**Attack** — Mapeo exponencial (0.1 × 300^n). Establece la rapidez con la que el seguidor de envolvente responde a los niveles crecientes cuando Envelope ≠ 0. La etiqueta muestra 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima. Columna derecha del editor.

**Release** — Mapeo exponencial (10 × 50^n). Establece la rapidez con la que el seguidor de envolvente se recupera después de que los niveles bajan cuando Envelope ≠ 0. La etiqueta muestra 'X.XX ms' por debajo de 100 ms, 'X.X ms' por encima. Columna derecha del editor.

**RN2** — Botón de alternancia solo TX (oculto en modo RX). Desmarcado por defecto. Activa el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al gate, compresor o saturador. Ubicado en el StripTubePanel flotante debajo del medidor de nivel de salida, solo en el lado TX. Solo modos de voz: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se conserva a través de AudioEngine.

**Medidor de nivel de salida** — Indicador. Widget ClientLevelMeter (extremo derecho del editor) que muestra el nivel pico posterior a la saturación con balística de ataque rápido / liberación lenta. Etiquetado 'OUT'. Solo visible en el editor flotante ("Aetherial Tube — TX" o "— RX"), no en el mosaico del applet acoplado. Zonas de color: verde (−60 a −12 dB), lima (−12 a −6 dB), ámbar (−6 a −3 dB), rojo (por encima de −3 dB). Sin clave persistida.

**Modo de edición de valores** — Haga clic en el valor mostrado de cualquier mando para entrar en modo de edición. El texto del valor se transforma en un campo de texto en línea con un fondo oscuro sutil y borde cian. Escriba un valor numérico (admite formatos adaptados a la configuración regional como "12,5" y entrada sin unidades como "3.5 ms" o "−6 dB") y presione Enter o haga clic en otro lugar para confirmar. El valor se limita al rango válido del mando. Presione Escape o deje el campo con una entrada no válida para revertir silenciosamente.

## Consejos

- Comience con Drive a 0.0 dB y aumente lentamente. La curva de transferencia es la guía visual más directa de cuánta saturación está agregando.
- Los lados TX y RX son completamente independientes. Los ajustes en la válvula TX no afectan a la válvula RX y viceversa.
- El editor flotante (abierto haciendo doble clic en la etapa TUBE en el widget CHAIN) y los mandos del applet acoplado se mantienen sincronizados: los cambios en uno se reflejan en el otro en aproximadamente 30 ms.
- Si desea escuchar el efecto sin comprometerse, reduzca Dry/Wet hacia el 0 % para volver a la mezcla seca mientras mantiene su configuración de Drive.
- Use el medidor OUT en el editor flotante para confirmar que el nivel posterior a la saturación está donde espera antes de cerrar el editor.
- Para marcar un valor exacto, haga clic en el valor mostrado del mando para entrar en el modo de edición en línea en lugar de arrastrar el mando.
- El mosaico del applet y el editor flotante utilizan anulaciones de color del contenedor por applet definidas en el espacio de nombres `color.knob.*` del tema (fondo, primer plano, asa) y `color.text.*` para el texto de etiquetas/valores. La personalización del tema afecta la apariencia del mando en este applet independientemente de otros tipos de applet.
- Active RN2 en el lado TX en modos de voz (SSB, AM, FM) para suprimir el ruido de fondo antes de la etapa de saturación. La alternancia RN2 se encuentra debajo del medidor de nivel de salida en el editor flotante. Los modos digitales omiten RN2 automáticamente.

## Solución de problemas

- **La curva de transferencia no se dobla cuando se aumenta Drive** — Es posible que la etapa de válvula no esté habilitada para ese lado. Actívela a través del widget CHAIN. El applet está oculto hasta que la etapa esté activa.
- **Los mandos del applet no coinciden con el editor flotante** — El applet se sincroniza con el motor mediante un temporizador de sondeo. Espere un momento; deberían alinearse en unos 30 ms. Si permanecen desincronizados, es posible que el motor de audio no esté conectado; verifique que la conexión de radio esté activa.
- **El medidor OUT no es visible** — El medidor de nivel de salida solo aparece en el editor flotante, no en el mosaico del applet acoplado. Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN.
- **El mosaico del applet acoplado se ve descolorido o atenuado** — Cuando la etapa de válvula está en bypass, todo el mosaico acoplado se renderiza con opacidad reducida. Este comportamiento es esperado y coincide con el efecto de atenuación aplicado a la curva EQ cuando esa etapa está en bypass. Vuelva a habilitar la etapa de válvula a través del widget CHAIN para restaurar la opacidad completa.
- **La edición de valor en línea muestra un valor incorrecto después de aplicar** — Si el valor se escribió con caracteres no admitidos, el mando vuelve a su último valor válido. Asegúrese de ingresar solo números y, opcionalmente, un separador decimal.
- **La alternancia RN2 no es visible** — RN2 es solo TX y solo aparece en el editor flotante para el lado TX ("Aetherial Tube — TX"). Está oculta en el editor flotante RX y en el mosaico del applet acoplado. Si está en un modo digital (RADE, DAX, RTTY, FT8, FDV, CW), RN2 está en bypass y la alternancia puede estar oculta independientemente del lado.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Desplace Bias para ajustar el equilibrio de armónicos pares/impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Ilumine u oscurezca la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcle saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- Use Envelope para una respuesta dinámica de válvula
- [Ponga en bypass la válvula desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
- Active la supresión de ruido RNNoise en TX (RN2)
