# Ajuste de Drive hasta que la curva comience a doblarse (calidez en TX o modelado de tono en RX)

Use la perilla Drive para introducir señal en la etapa de válvula y producir saturación armónica. Observar cómo se dobla la curva de transferencia a medida que aumenta Drive le indica exactamente cuándo y cuánta saturación está ocurriendo.

## Antes de comenzar

- La etapa de válvula debe estar habilitada en el lado que desea modelar (TX o RX). Habilítela a través del widget CHAIN o abriendo el editor flotante de ese lado.
- El subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) debe estar visible dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.

## Pasos

1. Localice el subcontenedor correcto en el panel de applets: "Aetherial Mic-PreAmp" para modelado de señal TX, o "Aetherial Dynamic Tube" para modelado de tono RX.
2. Observe la visualización de la curva de transferencia en la parte superior del applet. Con Drive en 0.0 dB, la curva es una línea diagonal recta — sin saturación.
3. Gire la perilla Drive en el sentido de las agujas del reloj. Observe la curva de transferencia: los hombros comienzan a comprimirse y doblarse a medida que aumenta Drive. La bola de entrada en vivo se mueve a lo largo de la curva y muestra qué parte de la curva está alcanzando su nivel de señal actual.
4. Deje de aumentar Drive cuando la curva muestre la cantidad de curvatura que desea. La calidez sutil aparece con una curvatura ligera; la saturación más intensa proviene de empujar Drive más hacia 24.0 dB.
5. Si la salida saturada es notablemente más fuerte o más silenciosa que la señal seca, ajuste la perilla Output para compensar. El medidor OUT del editor flotante (columna del extremo derecho) muestra el nivel pico posterior a la saturación y le ayuda a juzgar el ajuste.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| Drive | 0.00 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` / `ClientTubeRxDriveDb` |
| Tone | 0.00 | −1.0 – 1.0 | `ClientTubeTxTone` / `ClientTubeRxTone` |
| Bias | 0 % | 0 – 100 % | `ClientTubeTxBias` / `ClientTubeRxBias` |
| Output | 0.00 dB | −24.0 – 12.0 dB | `ClientTubeTxOutputDb` / `ClientTubeRxOutputDb` |
| Dry/Wet | 100 % | 0 – 100 % | `ClientTubeTxDryWet` / `ClientTubeRxDryWet` |
| Envelope | 0 % | −100 – 100 % | `ClientTubeTxEnvelope` / `ClientTubeRxEnvelope` |
| Attack | 5.00 ms | 0.1 – 30.0 ms | `ClientTubeTxAttackMs` / `ClientTubeRxAttackMs` |
| Release | 35.00 ms | 10.0 – 500.0 ms | `ClientTubeTxReleaseMs` / `ClientTubeRxReleaseMs` |

**Transfer curve** — Indicador. Dibuja la curva de transferencia de la válvula en tiempo real. La forma cambia a medida que ajusta Drive, Bias y la selección del modelo. La bola de entrada en vivo recorre la curva al nivel de señal actual, mostrando el régimen de saturación activo. Sin clave persistida.

**Drive** — Introduce más señal en la etapa de válvula. Los valores más altos hacen que la curva de transferencia se doble más bruscamente, produciendo un contenido armónico más fuerte.

**Tone** — Los valores negativos oscurecen la señal saturada; los valores positivos la brillan.

**Model A / B / C** — Botones de alternancia. Selecciona el modelo de carácter de la válvula. Selección exclusiva — solo un modelo activo a la vez. El valor predeterminado es Model A (marcado). El valor de respaldo se almacena como entero 0/1/2 en `ClientTubeTxModel` / `ClientTubeRxModel`.

**Bias** — Desplaza el punto de operación en la curva de transferencia, cambiando el equilibrio de armónicos pares e impares.

**Output** — Ganancia de compensación o maquillaje posterior a la válvula. Úselo para igualar el nivel saturado al nivel seco.

**Dry/Wet** — Mezcla seco/húmedo. Al 100 % solo pasa la señal saturada. Reducir Dry/Wet mezcla la señal seca original para una saturación en paralelo.

**Envelope** — Modulación dinámica de seguidor de envolvente. Los valores positivos aumentan la excitación en los transitorios (la válvula se calienta más en los picos fuertes); los valores negativos la reducen, comprimiendo los armónicos dinámicamente. La etiqueta se muestra como porcentaje (con signo).

**Attack** — Establece la rapidez con la que el seguidor de envolvente responde a los niveles crecientes cuando Envelope ≠ 0. Mapeo exponencial (0.1 × 300^n). La etiqueta muestra 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima.

**Release** — Establece la rapidez con la que el seguidor de envolvente se recupera después de que los niveles bajan cuando Envelope ≠ 0. Mapeo exponencial (10 × 50^n). La etiqueta muestra 'X.XX ms' por debajo de 100 ms, 'X.X ms' por encima.

**Output level meter** — Indicador. Visible solo en el editor flotante ("Aetherial Tube — TX" o "— RX"), en la columna del extremo derecho etiquetada OUT. Muestra el nivel pico posterior a la saturación con balística de ataque rápido / liberación lenta. Zonas de color: verde (−60 a −12 dB), lima (−12 a −6 dB), ámbar (−6 a −3 dB), rojo (por encima de −3 dB). Sin clave persistida.

**Value edit mode** — Haga clic en cualquier valor mostrado de una perilla para ingresar al modo de edición. El texto del valor se transforma en un campo de texto en línea con un fondo oscuro sutil y un borde cian. Escriba un valor numérico (admite formatos adaptados a la configuración regional como "12,5" y entrada sin unidades como "3.5 ms" o "−6 dB") y presione Enter o haga clic en otro lugar para confirmar. El valor se limita al rango válido de la perilla. Presione Escape o abandone el campo con una entrada no válida para revertir silenciosamente.

## Consejos

- Comience con Drive en 0.0 dB y auméntelo lentamente. La curva de transferencia es la guía visual más directa para saber cuánta saturación está agregando.
- Los lados TX y RX son completamente independientes. Los ajustes en la válvula TX no afectan la válvula RX ni viceversa.
- El editor flotante (abierto haciendo doble clic en la etapa TUBE en el widget CHAIN) y las perillas del applet acoplado se mantienen sincronizados; los cambios en uno se reflejan en el otro en aproximadamente 30 ms.
- Si desea escuchar el efecto sin comprometerse, reduzca Dry/Wet hacia 0 % para volver a la señal seca mientras mantiene su configuración de Drive.
- Use el medidor OUT en el editor flotante para confirmar que el nivel posterior a la saturación está donde espera antes de cerrar el editor.
- Para marcar un valor exacto, haga clic en el valor mostrado de la perilla para ingresar al modo de edición en línea en lugar de arrastrar la perilla.

## Solución de problemas

- **La curva de transferencia no se dobla cuando se aumenta Drive** — La etapa de válvula puede no estar habilitada para ese lado. Habilítela a través del widget CHAIN. El applet está oculto hasta que la etapa esté activa.
- **Las perillas del applet no coinciden con las del editor flotante** — El applet se sincroniza con el motor en un temporizador de sondeo. Espere un momento; deberían alinearse en aproximadamente 30 ms. Si permanecen desincronizados, es posible que el motor de audio no esté conectado; verifique que la conexión de radio esté activa.
- **El medidor OUT no es visible** — El medidor de nivel de salida solo aparece en el editor flotante, no en el mosaico del applet acoplado. Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN.
- **El mosaico del applet acoplado se ve descolorido o atenuado** — Cuando la etapa de válvula está en bypass, todo el mosaico acoplado se renderiza con opacidad reducida. Este es un comportamiento esperado y coincide con el efecto de atenuación aplicado a la curva EQ cuando esa etapa está en bypass. Vuelva a habilitar la etapa de válvula a través del widget CHAIN para restaurar la opacidad completa.
- **La edición de valor en línea muestra un valor incorrecto después de aplicar** — Si el valor se escribió con caracteres no admitidos, la perilla vuelve a su última configuración válida. Asegúrese de ingresar solo números y, opcionalmente, un separador decimal.

## Relacionados

- [Resumen de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Desplace Bias para ajustar el equilibrio de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Brille u oscurezca la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcle saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Use Envelope para una respuesta de válvula dinámica](use-envelope-for-dynamic-tube-response.md)
- [Ponga la válvula en bypass desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
