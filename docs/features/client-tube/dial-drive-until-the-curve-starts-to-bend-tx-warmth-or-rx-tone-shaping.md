# Ajuste de Drive hasta que la curva comience a doblarse (calentamiento en TX o modelado de tono en RX)

Use el mando Drive para introducir señal en la etapa de válvula y producir saturación armónica. Observar cómo se dobla la curva de transferencia al aumentar Drive le indica exactamente cuándo y cuánta saturación está ocurriendo.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea modelar (TX o RX). Hábítela a través del widget CHAIN o abriendo el editor flotante para ese lado.
- El subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) debe estar visible dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.

## Pasos

1. Localice el subcontenedor correcto en el panel de applets: "Aetherial Mic-PreAmp" para el modelado de señal TX, o "Aetherial Dynamic Tube" para el modelado de tono RX.
2. Observe la visualización de la curva de transferencia en la parte superior del applet. Con Drive en 0.0 dB la curva es una línea recta diagonal — sin saturación.
3. Gire el mando Drive en el sentido de las agujas del reloj. Observe la curva de transferencia: los hombros comienzan a comprimirse y doblarse a medida que aumenta Drive. La bola de entrada en vivo se mueve a lo largo de la curva y muestra qué parte de la curva está siendo alcanzada por su nivel de señal actual.
4. Deje de aumentar Drive cuando la curva muestre la cantidad de curvatura que desea. Un calentamiento sutil aparece con una ligera curvatura; una saturación más fuerte proviene de empujar Drive más hacia 24.0 dB.
5. Si la salida saturada es notablemente más fuerte o más silenciosa que la señal seca, ajuste el mando Output para compensar. El medidor OUT del editor flotante (columna del extremo derecho) muestra el nivel pico post-saturación y le ayuda a juzgar el ajuste.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| Drive | 0.0 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` / `ClientTubeRxDriveDb` |
| Tone | 0.00 | −1.0 – 1.0 | `ClientTubeTxTone` / `ClientTubeRxTone` |
| Bias | 0 % | 0 – 100 % | `ClientTubeTxBias` / `ClientTubeRxBias` |
| Output | 0.0 dB | −24.0 – 12.0 dB | `ClientTubeTxOutputDb` / `ClientTubeRxOutputDb` |
| Dry/Wet | 100 % | 0 – 100 % | `ClientTubeTxDryWet` / `ClientTubeRxDryWet` |

**Curva de transferencia** — Indicador. Dibuja la curva de transferencia de la válvula en tiempo real. La forma cambia a medida que ajusta Drive, Bias y la selección del modelo. La bola de entrada en vivo recorre la curva al nivel de señal actual, mostrando el régimen de saturación activo. Sin clave persistida.

**Drive** — Introduce más señal en la etapa de válvula. Los valores más altos hacen que la curva de transferencia se doble más bruscamente, produciendo un contenido armónico más fuerte.

**Tone** — Los valores negativos oscurecen la señal saturada; los valores positivos la iluminan.

**Bias** — Desplaza el punto de operación en la curva de transferencia, cambiando el equilibrio de armónicos pares e impares.

**Output** — Ganancia de maquillaje o recorte post-válvula. Úselo para igualar el nivel saturado con el nivel seco.

**Dry/Wet** — Mezcla de señal seca/saturada. Al 100 % solo pasa la señal saturada. Reducir Dry/Wet mezcla la señal seca original para una saturación en paralelo.

**Medidor de nivel de salida** — Indicador. Visible solo en el editor flotante ("Aetherial Tube — TX" o "— RX"), en la columna del extremo derecho etiquetada OUT. Muestra el nivel pico post-saturación con balística de ataque rápido / liberación lenta. Zonas de color: verde (−60 a −12 dB), lima (−12 a −6 dB), ámbar (−6 a −3 dB), rojo (por encima de −3 dB). Sin clave persistida.

## Consejos

- Comience con Drive en 0.0 dB y aumente lentamente. La curva de transferencia es la guía visual más directa de cuánta saturación está agregando.
- Los lados TX y RX son completamente independientes. Los ajustes en la válvula TX no afectan la válvula RX y viceversa.
- El editor flotante (se abre haciendo doble clic en la etapa TUBE en el widget CHAIN) y las perillas del applet acoplado permanecen sincronizados: los cambios en uno se reflejan en el otro en aproximadamente 30 ms.
- Si desea escuchar el efecto sin comprometerse, reduzca Dry/Wet hacia 0 % para volver a la señal seca mientras mantiene su ajuste de Drive.
- Use el medidor OUT en el editor flotante para confirmar que el nivel post-saturación está donde espera antes de cerrar el editor.

## Solución de problemas

- **La curva de transferencia no se dobla cuando se aumenta Drive** — Es posible que la etapa Tube no esté habilitada para ese lado. Hábítela a través del widget CHAIN. El applet está oculto hasta que la etapa esté activa.
- **Las perillas del applet no coinciden con el editor flotante** — El applet se sincroniza desde el motor mediante un temporizador de sondeo. Espere un momento; deberían alinearse en aproximadamente 30 ms. Si permanecen desincronizados, es posible que el motor de audio no esté conectado; verifique que la conexión de radio esté activa.
- **El medidor OUT no es visible** — El medidor de nivel de salida solo aparece en el editor flotante, no en el mosaico del applet acoplado. Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN.
- **El mosaico del applet acoplado se ve atenuado o tenue** — Cuando la etapa Tube está en bypass, todo el mosaico acoplado se renderiza con opacidad reducida. Este es un comportamiento esperado y coincide con el efecto de atenuación aplicado a la curva EQ cuando esa etapa está en bypass. Vuelva a habilitar la etapa Tube a través del widget CHAIN para restaurar la opacidad completa.

## Relacionados

- [Resumen de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste de Bias para modificar el equilibrio de armónicos pares/impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Ilumine u oscurezca la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcla de saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Bypass de la válvula desde cualquier cadena](bypass-the-tube-from-either-chain.md)
