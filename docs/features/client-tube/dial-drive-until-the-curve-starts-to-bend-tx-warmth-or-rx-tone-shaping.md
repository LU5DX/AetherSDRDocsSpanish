# Ajuste de Drive hasta que la curva comience a doblarse (calidez en TX o modelado de tono en RX)

Use el mando Drive para inyectar más señal en la etapa de válvula y producir saturación armónica. Observar cómo se dobla la curva de transferencia a medida que aumenta Drive le indica exactamente cuándo y cuánta saturación se está generando.

## Antes de comenzar

- La etapa de válvula debe estar habilitada en el lado que desea modelar (TX o RX). Actívela a través del widget CHAIN o abriendo el editor flotante para ese lado.
- El subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) debe estar visible dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.

## Pasos

1. Localice el subcontenedor correcto en el panel de applets: "Aetherial Mic-PreAmp" para modelado de señal en TX, o "Aetherial Dynamic Tube" para modelado de tono en RX.
2. Observe la visualización de la curva de transferencia en la parte superior del applet. Con Drive en 0.0 dB, la curva es una línea diagonal recta: no hay saturación.
3. Gire el mando Drive en sentido horario. Observe la curva de transferencia: los extremos comienzan a comprimirse y doblarse a medida que Drive aumenta. La bola de entrada en vivo se mueve a lo largo de la curva y muestra qué parte de la curva está siendo alcanzada por su nivel de señal actual.
4. Deje de aumentar Drive cuando la curva muestre la cantidad de curvatura deseada. La calidez sutil aparece con una ligera curvatura; la saturación más intensa proviene de aumentar Drive más hacia 24.0 dB.
5. Si la salida saturada es notablemente más fuerte o más débil que la señal seca, ajuste el mando Output para compensarlo. El medidor OUT del editor flotante (columna del extremo derecho) muestra el nivel pico posterior a la saturación y le ayuda a juzgar el ajuste.

## Función de cada control

| Control   | Valor predeterminado | Rango válido                     |
|-----------|---------------------|----------------------------------|
| Drive     | 0.00 dB             | 0.0 – 24.0 dB                    |
| Tone      | 0.00                | −1.0 – 1.0                       |
| Bias      | 0 %                 | 0 – 100 %                        |
| Output    | 0.00 dB             | −24.0 – 12.0 dB                  |
| Dry/Wet   | 100 %               | 0 – 100 %                        |
| Envelope  | 0 %                 | −100 – 100 %                     |
| Attack    | 5.00 ms             | 0.1 – 30.0 ms                    |
| Release   | 35.00 ms            | 10.0 – 500.0 ms                  |
| RN2       | desmarcado          | Alternancia solo TX (oculto en modo RX) |

**Curva de transferencia** — Indicador. ClientTubeCurveWidget en modo compacto. Dibuja la curva de transferencia de válvula configurada actualmente con una bola en vivo en la entrada. La forma cambia al ajustar Drive, Bias y la selección de modelo. La bola de entrada en vivo recorre la curva al nivel de señal actual, mostrando el régimen de saturación activo. Sin clave persistida.

**Drive** — Mapeo lineal. Inyecta más señal en la etapa de válvula. Los valores más altos hacen que la curva de transferencia se doble más pronunciadamente, generando un contenido armónico más fuerte. Etiqueta 'X.XX dB'. Columna izquierda del editor.

**Tone** — Mapeo lineal. Los valores negativos oscurecen la señal saturada; los positivos la aclaran. Etiqueta 'X.XX'. Fila central del editor, a la izquierda del selector de modelo.

**Modelo A / B / C** — Botones de alternancia. Selecciona el modelo de carácter de válvula. Selección exclusiva: solo un modelo activo a la vez. El valor predeterminado es Modelo A (marcado). Color ámbar cuando está marcado. El valor de respaldo se almacena como entero 0/1/2 en `ClientTubeTxModel` / `ClientTubeRxModel`.

**Bias** — Mapeo lineal. Desplaza el punto de operación en la curva de transferencia, cambiando el equilibrio entre armónicos pares e impares. Etiqueta mostrada como porcentaje. Fila central del editor, a la derecha del selector de modelo. Clave de configuración `ClientTubeTxBias` (no `ClientTubeTxBiasAmount`) / `ClientTubeRxBias`.

**Output** — Mapeo lineal. Ganancia de compensación o ajuste posterior a la válvula. Úselo para igualar el nivel saturado al nivel seco. Etiqueta 'X.XX dB'. Columna izquierda del editor. Clave de configuración `ClientTubeTxOutputDb` (no `ClientTubeTxOutputGainDb`) / `ClientTubeRxOutputDb`.

**Dry/Wet** — Mapeo lineal. Mezcla seco/húmedo. Al 100 %, solo pasa la señal saturada. Reducir Dry/Wet mezcla la señal seca original para obtener saturación en paralelo. Etiqueta mostrada como porcentaje. Columna izquierda del editor (mando superior).

**Envelope** — Mapeo lineal (−1.0 a +1.0). Modulación dinámica con seguidor de envolvente. Los valores positivos aumentan la unidad en los transitorios (la válvula se calienta más en los picos fuertes); los valores negativos la reducen, comprimiendo los armónicos de forma dinámica. Etiqueta mostrada como porcentaje (con signo). Columna derecha del editor. Clave de configuración `ClientTubeTxEnvelope` / `ClientTubeRxEnvelope`.

**Attack** — Mapeo exponencial (0.1 × 300^n). Establece la rapidez con la que el seguidor de envolvente responde a niveles crecientes cuando Envelope ≠ 0. La etiqueta muestra 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima. Columna derecha del editor.

**Release** — Mapeo exponencial (10 × 50^n). Establece la rapidez con la que el seguidor de envolvente se recupera después de que los niveles disminuyen cuando Envelope ≠ 0. La etiqueta muestra 'X.XX ms' por debajo de 100 ms, 'X.X ms' por encima. Columna derecha del editor.

**Medidor de nivel de salida** — Indicador. Widget ClientLevelMeter (extremo derecho del editor) que muestra el nivel pico posterior a la saturación con balística de ataque rápido / liberación lenta. Etiquetado como 'OUT'. Solo visible en el editor flotante ("Aetherial Tube — TX" o "— RX"), no en el mosaico del applet acoplado. Zonas de color: verde (−60 a −12 dB), lima (−12 a −6 dB), ámbar (−6 a −3 dB), rojo (por encima de −3 dB). Sin clave persistida.

**Modo de edición de valor** — Haga clic en el valor mostrado de cualquier mando para entrar en modo de edición. El texto del valor se transforma en un campo de texto en línea con un fondo oscuro sutil y un borde cian. Escriba un valor numérico (admite formatos adaptados a la configuración regional como "12,5" y entrada sin unidad como "3.5 ms" o "−6 dB") y presione Enter o haga clic en otro lugar para confirmar. El valor se ajusta al rango válido del mando. Presione Escape o abandone el campo con una entrada no válida para revertir silenciosamente.

## Consejos

- Comience con Drive en 0.0 dB y auméntelo lentamente. La curva de transferencia es la guía visual más directa de cuánta saturación está agregando.
- Los lados TX y RX son completamente independientes. Los ajustes en la válvula de TX no afectan la válvula de RX y viceversa.
- El editor flotante (abierto al hacer doble clic en la etapa TUBE en el widget CHAIN) y los mandos del applet acoplado permanecen sincronizados: los cambios en uno se reflejan en el otro en aproximadamente 30 ms.
- Si desea escuchar el efecto sin comprometerse, reduzca Dry/Wet hacia el 0 % para mezclar la señal seca mientras mantiene su configuración de Drive.
- Use el medidor OUT en el editor flotante para confirmar que el nivel posterior a la saturación es el esperado antes de cerrar el editor.
- Para ajustar un valor exacto, haga clic en el valor mostrado del mando para entrar en el modo de edición en línea en lugar de arrastrar el mando.
- El mosaico del applet y el editor flotante utilizan anulaciones de color del contenedor por applet definidas en el espacio de nombres `color.knob.*` del tema (fondo, primer plano, mango) y `color.text.*` para el texto de etiquetas/valores. La personalización del tema afecta la apariencia de los mandos en este applet de forma independiente de otros tipos de applet.

## Solución de problemas

- **La curva de transferencia no se dobla al aumentar Drive** — Es posible que la etapa de válvula no esté habilitada para ese lado. Actívela a través del widget CHAIN. El applet está oculto hasta que la etapa esté activa.
- **Los mandos del applet no coinciden con el editor flotante** — El applet se sincroniza con el motor mediante un temporizador de sondeo. Espere un momento; deberían alinearse en unos 30 ms. Si permanecen desincronizados, es posible que el motor de audio no esté conectado; verifique que la conexión de radio esté activa.
- **El medidor OUT no es visible** — El medidor de nivel de salida solo aparece en el editor flotante, no en el mosaico del applet acoplado. Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN.
- **El mosaico del applet acoplado se ve apagado o atenuado** — Cuando la etapa de válvula está en bypass, todo el mosaico acoplado se renderiza con opacidad reducida. Este comportamiento es esperado y coincide con el efecto de atenuación aplicado a la curva EQ cuando esa etapa está en bypass. Vuelva a habilitar la etapa de válvula a través del widget CHAIN para restaurar la opacidad completa.
- **La edición de valor en línea muestra un valor incorrecto después de aplicar** — Si el valor se escribió con caracteres no admitidos, el mando vuelve a su última configuración válida. Asegúrese de ingresar solo números y, opcionalmente, un separador decimal.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste de Bias para modificar el equilibrio de armónicos pares/impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Aclare u oscurezca la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcla en paralelo de saturación con Mix](parallel-blend-saturation-with-mix.md)
- Use Envelope para una respuesta de válvula dinámica
- [Bypasse la válvula desde cualquier cadena](bypass-the-tube-from-either-chain.md)
