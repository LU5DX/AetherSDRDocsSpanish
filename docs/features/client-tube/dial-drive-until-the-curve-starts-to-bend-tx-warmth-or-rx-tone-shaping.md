# Gire Drive hasta que la curva comience a doblarse (calidez en TX o modelado de tono en RX)

Use el mando Drive para empujar la señal hacia la etapa de tubo y producir saturación armónica. Observar cómo se dobla la curva de transferencia al aumentar Drive le indica exactamente cuándo y en qué medida se produce la saturación.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea moldear (TX o RX). Habilítela a través del widget CHAIN o abriendo el editor flotante para ese lado.
- El subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) debe ser visible dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.

## Pasos

1. Localice el subcontenedor correcto en el panel de applets: "Aetherial Mic-PreAmp" para el modelado de la señal TX, o "Aetherial Dynamic Tube" para el modelado de tono RX.
2. Observe la pantalla de curva de transferencia en la parte superior del applet. Con Drive en 0.0 dB, la curva es una línea diagonal recta — sin saturación.
3. Gire el mando Drive en sentido horario. Observe la curva de transferencia: los hombros comienzan a comprimirse y doblarse a medida que aumenta Drive. La bola de entrada en tiempo real se desplaza a lo largo de la curva e indica qué parte de la curva alcanza el nivel de señal actual.
4. Deje de aumentar Drive cuando la curva muestre la cantidad de doblez deseada. Una calidez sutil aparece con un doblez leve; una saturación más pronunciada se obtiene llevando Drive más cerca de 24.0 dB.
5. Si la salida saturada es notablemente más fuerte o más suave que la señal seca, ajuste el mando Output para compensar. El medidor OUT del editor flotante (columna del extremo derecho) muestra el nivel de pico post-saturación y ayuda a determinar el ajuste necesario.

## Qué hace cada control

| Control | Valor por defecto | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| Drive | 0.0 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` / `ClientTubeRxDriveDb` |
| Tone | 0.00 | −1.0 – 1.0 | `ClientTubeTxTone` / `ClientTubeRxTone` |
| Bias | 0 % | 0 – 100 % | `ClientTubeTxBias` / `ClientTubeRxBias` |
| Output | 0.0 dB | −24.0 – 12.0 dB | `ClientTubeTxOutputDb` / `ClientTubeRxOutputDb` |
| Dry/Wet | 100 % | 0 – 100 % | `ClientTubeTxDryWet` / `ClientTubeRxDryWet` |

**Curva de transferencia** — Indicador. Dibuja la curva de transferencia del tubo en tiempo real. La forma cambia al ajustar Drive, Bias y la selección de modelo. La bola de entrada en tiempo real recorre la curva al nivel de señal actual, mostrando el régimen de saturación activo. Sin clave persistida.

**Drive** — Empuja más señal hacia la etapa de tubo. Los valores más altos hacen que la curva de transferencia se doble con mayor intensidad, produciendo mayor contenido armónico.

**Tone** — Los valores negativos oscurecen la señal saturada; los valores positivos la aclaran.

**Bias** — Desplaza el punto de operación en la curva de transferencia, cambiando el equilibrio entre armónicos pares e impares.

**Output** — Ganancia de compensación o recorte post-tubo. Utilícelo para igualar el nivel saturado con el nivel seco.

**Dry/Wet** — Mezcla seca/húmeda. Al 100 % solo pasa la señal saturada. Reducir Dry/Wet mezcla la señal seca original para obtener saturación en paralelo.

**Medidor de nivel de salida** — Indicador. Visible únicamente en el editor flotante ("Aetherial Tube — TX" o "— RX"), en la columna del extremo derecho etiquetada OUT. Muestra el nivel de pico post-saturación con balística de ataque rápido / liberación lenta. Zonas de color: verde (−60 a −12 dB), lima (−12 a −6 dB), ámbar (−6 a −3 dB), rojo (por encima de −3 dB). Sin clave persistida.

## Consejos

- Comience con Drive en 0.0 dB y auméntelo lentamente. La curva de transferencia es la guía visual más directa para saber cuánta saturación está añadiendo.
- Los lados TX y RX son completamente independientes. Los ajustes en el tubo TX no afectan al tubo RX y viceversa.
- El editor flotante (abierto haciendo doble clic en la etapa TUBE en el widget CHAIN) y los mandos del applet acoplado permanecen sincronizados — los cambios en uno se reflejan en el otro en aproximadamente 30 ms.
- Si desea escuchar el efecto sin comprometerse con él, reduzca Dry/Wet hacia 0 % para volver a la señal seca manteniendo el ajuste de Drive en su lugar.
- Use el medidor OUT en el editor flotante para confirmar que el nivel post-saturación es el esperado antes de cerrar el editor.

## Solución de problemas

- **La curva de transferencia no se dobla al aumentar Drive** — Es posible que la etapa Tube no esté habilitada para ese lado. Habilítela a través del widget CHAIN. El applet permanece oculto hasta que la etapa esté activa.
- **Los mandos del applet no coinciden con el editor flotante** — El applet se sincroniza desde el motor mediante un temporizador de sondeo. Espere un momento; deberían alinearse en aproximadamente 30 ms. Si continúan desincronizados, es posible que el motor de audio no esté conectado — verifique que la conexión con la radio esté activa.
- **El medidor OUT no es visible** — El medidor de nivel de salida solo aparece en el editor flotante, no en el panel del applet acoplado. Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Desplace Bias para ajustar el equilibrio de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Aclare u oscurezca la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcla de saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Omita el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
