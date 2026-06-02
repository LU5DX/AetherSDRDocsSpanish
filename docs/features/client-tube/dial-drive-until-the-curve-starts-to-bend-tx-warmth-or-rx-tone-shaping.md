# Control de Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)

Utilice el mando Drive para inyectar señal en la etapa de válvula y producir saturación armónica. Observar cómo se deforma la curva de transferencia a medida que aumenta Drive le indica exactamente cuándo y cuánta saturación se está produciendo.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea modelar (TX o RX). Actívela a través del widget CHAIN o abriendo el editor flotante de ese lado.
- El subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) debe estar visible dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.

## Pasos

1. Localice el subcontenedor correcto en el panel de applets: "Aetherial Mic-PreAmp" para el modelado de señal TX, o "Aetherial Dynamic Tube" para el modelado de tono RX.
2. Observe la visualización de la curva de transferencia en la parte superior del applet. Con Drive en 0.0 dB la curva es una línea diagonal recta: no hay saturación.
3. Gire el mando Drive en el sentido de las agujas del reloj. Observe la curva de transferencia: los hombros comienzan a comprimirse y curvarse a medida que aumenta Drive. La bola de entrada en vivo se mueve a lo largo de la curva y muestra qué parte de la curva está alcanzando su nivel de señal actual.
4. Deje de aumentar Drive cuando la curva muestre la cantidad de curvatura que desea. Una ligera calidez aparece con una curvatura leve; una saturación más intensa proviene de empujar Drive más hacia 24.0 dB.
5. Si la salida saturada es notablemente más fuerte o más silenciosa que la señal seca, ajuste el mando Output para compensarlo. El medidor OUT del editor flotante (columna de la derecha) muestra el nivel de pico posterior a la saturación y le ayuda a juzgar el ajuste.

## Qué hace cada control

| Control   | Por defecto | Rango válido | Notas |
|-----------|-------------|--------------|-------|
| Drive     | 0.00 dB     | 0.0 – 24.0 dB | Etiqueta 'X.XX dB'. Columna izquierda del editor. |
| Tone      | 0.00        | −1.0 – 1.0   | Etiqueta 'X.XX'. Fila central del editor, a la izquierda del selector Model. |
| Bias      | 0 %         | 0 – 100 %    | Etiqueta mostrada como porcentaje. Fila central del editor, a la derecha del selector Model. Clave de ajuste `ClientTubeTxBias` / `ClientTubeRxBias`. |
| Output    | 0.00 dB     | −24.0 – 12.0 dB | Etiqueta 'X.XX dB'. Columna izquierda del editor. Clave de ajuste `ClientTubeTxOutputDb` / `ClientTubeRxOutputDb`. |
| Dry/Wet   | 100 %       | 0 – 100 %    | Etiqueta mostrada como porcentaje. Columna izquierda del editor (mando superior). |
| Envelope  | 0 %         | −100 – 100 % | Etiqueta mostrada como porcentaje (con signo). Columna derecha del editor. Clave de ajuste `ClientTubeTxEnvelope` / `ClientTubeRxEnvelope`. |
| Attack    | 5.00 ms     | 0.1 – 30.0 ms | Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima. Columna derecha del editor. Mapeo exponencial (0.1 × 300^n). |
| Release   | 35.00 ms    | 10.0 – 500.0 ms | Etiqueta 'X.XX ms' por debajo de 100 ms, 'X.X ms' por encima. Columna derecha del editor. Mapeo exponencial (10 × 50^n). |
| RN2       | desmarcado | Alternancia solo TX (oculto en modo RX) | Activa el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al gate/compresor/saturador. Se encuentra en el panel flotante StripTubePanel debajo del medidor de nivel de salida, solo en el lado TX. Solo modos de voz: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se conserva mediante AudioEngine. |

**Curva de transferencia** — Indicador. Widget ClientTubeCurveWidget en modo compacto. Dibuja la curva de transferencia de la válvula actualmente configurada con una bola en vivo en la entrada. La forma cambia a medida que ajusta Drive, Bias y la selección del modelo. La bola de entrada en vivo recorre la curva al nivel de señal actual, mostrando el régimen de saturación activo. No tiene clave persistente.

**Drive** — Mapeo lineal. Introduce más señal en la etapa de válvula. Los valores más altos hacen que la curva de transferencia se curve más pronunciadamente, produciendo un contenido armónico más fuerte. Etiqueta 'X.XX dB'. Columna izquierda del editor.

**Tone** — Mapeo lineal. Los valores negativos oscurecen la señal saturada; los valores positivos la brillan. Etiqueta 'X.XX'. Fila central del editor, a la izquierda del selector Model.

**Model A / B / C** — Botones de alternancia. Selecciona el modelo de carácter de la válvula. Selección exclusiva: solo un modelo activo a la vez. Por defecto es Model A (marcado). Ámbar cuando está marcado. El valor de respaldo se almacena como entero 0/1/2 en `ClientTubeTxModel` / `ClientTubeRxModel`.

**Bias** — Mapeo lineal. Desplaza el punto de operación en la curva de transferencia, cambiando el equilibrio de armónicos pares e impares. Etiqueta mostrada como porcentaje. Fila central del editor, a la derecha del selector Model. Clave de ajuste `ClientTubeTxBias` (no `ClientTubeTxBiasAmount`) / `ClientTubeRxBias`.

**Output** — Mapeo lineal. Ganancia de maquillaje o ajuste posterior a la válvula. Úselo para igualar el nivel saturado al nivel seco. Etiqueta 'X.XX dB'. Columna izquierda del editor. Clave de ajuste `ClientTubeTxOutputDb` (no `ClientTubeTxOutputGainDb`) / `ClientTubeRxOutputDb`.

**Dry/Wet** — Mapeo lineal. Mezcla seco/húmedo. Al 100 % solo pasa la señal saturada. Reducir Dry/Wet mezcla la señal seca original para una saturación en paralelo. Etiqueta mostrada como porcentaje. Columna izquierda del editor (mando superior).

**Envelope** — Mapeo lineal (−1.0 a +1.0). Modulación dinámica del seguidor de envolvente. Los valores positivos aumentan Drive en los transitorios (la válvula se calienta más en los picos fuertes); los valores negativos lo reducen, comprimiendo los armónicos dinámicamente. Etiqueta mostrada como porcentaje (con signo). Columna derecha del editor. Clave de ajuste `ClientTubeTxEnvelope` / `ClientTubeRxEnvelope`.

**Attack** — Mapeo exponencial (0.1 × 300^n). Establece la rapidez con la que el seguidor de envolvente responde a niveles ascendentes cuando Envelope ≠ 0. La etiqueta muestra 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima. Columna derecha del editor.

**Release** — Mapeo exponencial (10 × 50^n). Establece la rapidez con la que el seguidor de envolvente se recupera después de que los niveles bajan cuando Envelope ≠ 0. La etiqueta muestra 'X.XX ms' por debajo de 100 ms, 'X.X ms' por encima. Columna derecha del editor.

**Medidor de nivel de salida** — Indicador. Widget ClientLevelMeter (extremo derecho del editor) que muestra el nivel de pico posterior a la saturación con balística de ataque rápido / liberación lenta. Etiquetado 'OUT'. Solo visible en el editor flotante ("Aetherial Tube — TX" o "— RX"), no en el mosaico del applet acoplado. Zonas de color: verde (−60 a −12 dB), lima (−12 a −6 dB), ámbar (−6 a −3 dB), rojo (por encima de −3 dB). No tiene clave persistente.

**Modo de edición de valor** — Haga clic en el valor mostrado de cualquier mando para entrar en el modo de edición. El texto del valor se transforma en un campo de texto en línea con un fondo oscuro sutil y un borde cian. Escriba un valor numérico (admite formatos locales como "12,5" y entrada sin unidad como "3.5 ms" o "−6 dB") y presione Enter o haga clic en otro lugar para confirmar. El valor se limita al rango válido del mando. Presione Escape o salga del campo con una entrada no válida para revertir silenciosamente.

## Consejos

- Comience con Drive en 0.0 dB y aumente lentamente. La curva de transferencia es la guía visual más directa de cuánta saturación está agregando.
- Los lados TX y RX son completamente independientes. Los ajustes en la válvula TX no afectan a la válvula RX y viceversa.
- El editor flotante (abierto haciendo doble clic en la etapa TUBE en el widget CHAIN) y los mandos del applet acoplado se mantienen sincronizados: los cambios en uno se reflejan en el otro en aproximadamente 30 ms.
- Si desea escuchar el efecto sin comprometerse con él, reduzca Dry/Wet hacia el 0 % para mezclar de nuevo a seco mientras mantiene su configuración de Drive.
- Use el medidor OUT en el editor flotante para confirmar que el nivel posterior a la saturación está donde espera antes de cerrar el editor.
- Para marcar un valor exacto, haga clic en el valor mostrado del mando para entrar en el modo de edición en línea en lugar de arrastrar el mando.
- El mosaico del applet y el editor flotante usan anulaciones de color de contenedor por applet definidas en el espacio de nombres `color.knob.*` del tema (fondo, primer plano, asa) y `color.text.*` para el texto de etiqueta/valor. La personalización del tema afecta la apariencia del mando en este applet independientemente de otros tipos de applet.

## Solución de problemas

- **La curva de transferencia no se curva cuando se aumenta Drive** — Es posible que la etapa Tube no esté habilitada para ese lado. Actívela a través del widget CHAIN. El applet está oculto hasta que la etapa esté activa.
- **Los mandos en el applet no coinciden con el editor flotante** — El applet se sincroniza desde el motor mediante un temporizador de sondeo. Espere un momento; deberían alinearse en aproximadamente 30 ms. Si permanecen desincronizados, es posible que el motor de audio no esté conectado; verifique que la conexión del equipo esté activa.
- **El medidor OUT no es visible** — El medidor de nivel de salida solo aparece en el editor flotante, no en el mosaico del applet acoplado. Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN.
- **El mosaico del applet acoplado se ve desvaído o atenuado** — Cuando la etapa Tube está en bypass, todo el mosaico acoplado se renderiza con opacidad reducida. Este comportamiento es esperado y coincide con el efecto de atenuación aplicado a la curva EQ cuando esa etapa está en bypass. Vuelva a habilitar la etapa Tube a través del widget CHAIN para restaurar la opacidad completa.
- **La edición de valor en línea muestra un valor incorrecto después de aplicarlo** — Si el valor se escribió con caracteres no admitidos, el mando vuelve a su último ajuste válido. Asegúrese de ingresar solo números y, opcionalmente, un separador decimal.

## Relacionados

- [Visión general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste Bias para modificar el equilibrio de armónicos pares/impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Aclare u oscurezca la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcle saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- Use Envelope para una respuesta dinámica de la válvula
- [Ponga en bypass la válvula desde cualquier cadena](bypass-the-tube-from-either-chain.md)
