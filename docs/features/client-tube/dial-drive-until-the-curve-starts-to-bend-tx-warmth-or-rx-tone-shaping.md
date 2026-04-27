# Gire Drive hasta que la curva comience a curvarse (calidez en TX o moldeado de tono en RX)

Use el potenciómetro Drive para empujar la señal hacia la etapa de tubo y producir saturación armónica. Observar cómo la curva de transferencia se curva al aumentar Drive le indica exactamente cuándo y cuánta saturación se está produciendo.

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea moldear (TX o RX). Habilítela mediante el widget CHAIN o abriendo el editor flotante para ese lado.
- El subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) debe ser visible dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.

## Pasos

1. Localice el subcontenedor correcto en el panel de applets: "Aetherial Mic-PreAmp" para el moldeado de señal TX, o "Aetherial Dynamic Tube" para el moldeado de tono RX.
2. Observe la pantalla de la curva de transferencia en la parte superior del applet. Con Drive en 0.0 dB, la curva es una línea diagonal recta — sin saturación.
3. Gire el potenciómetro Drive en sentido horario. Observe la curva de transferencia: los hombros comienzan a comprimirse y curvarse a medida que Drive aumenta. La bola de entrada en tiempo real se mueve a lo largo de la curva y muestra qué parte de la curva está alcanzando el nivel de señal actual.
4. Deje de aumentar Drive cuando la curva muestre la cantidad de curvatura deseada. La calidez sutil aparece con una curvatura leve; la saturación más intensa se obtiene llevando Drive más hacia 24.0 dB.
5. Si la salida saturada es notablemente más fuerte o más débil que la señal seca, ajuste el potenciómetro Output para compensar.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistente (TX / RX) |
|---|---|---|---|
| Drive | 0.0 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` / `ClientTubeRxDriveDb` |
| Tone | 0.00 | −1.0 – 1.0 | `ClientTubeTxTone` / `ClientTubeRxTone` |
| Bias | 0 % | 0 – 100 % | `ClientTubeTxBiasAmount` / `ClientTubeRxBiasAmount` |
| Output | 0.0 dB | −24.0 – 12.0 dB | `ClientTubeTxOutputGainDb` / `ClientTubeRxOutputGainDb` |
| Mix | 100 % | 0 – 100 % | `ClientTubeTxDryWet` / `ClientTubeRxDryWet` |

**Curva de transferencia** — Indicador. Dibuja la curva de transferencia del tubo en tiempo real. La forma cambia al ajustar Drive, Bias y la selección de modelo. La bola de entrada en tiempo real recorre la curva al nivel de señal actual, mostrando el régimen de saturación activo. Sin clave persistente.

**Drive** — Empuja más señal hacia la etapa de tubo. Los valores más altos hacen que la curva de transferencia se curve con mayor intensidad, produciendo un contenido armónico más fuerte.

**Tone** — Los valores negativos oscurecen la señal saturada; los valores positivos la aclaran.

**Bias** — Desplaza el punto de operación en la curva de transferencia, cambiando el equilibrio entre armónicos pares e impares.

**Output** — Ganancia de compensación o recorte posterior al tubo. Úselo para igualar el nivel saturado con el nivel seco.

**Mix** — Mezcla seca/húmeda. Al 100 % solo pasa la señal saturada. Reducir Mix mezcla la señal seca original para lograr saturación en paralelo.

## Consejos

- Comience con Drive en 0.0 dB y auméntelo lentamente. La curva de transferencia es la guía visual más directa para saber cuánta saturación está agregando.
- Los lados TX y RX son completamente independientes. Los ajustes al tubo TX no afectan al tubo RX y viceversa.
- El editor flotante (abierto haciendo doble clic en la etapa TUBE en el widget CHAIN) y los potenciómetros del applet acoplado permanecen sincronizados — los cambios en uno se reflejan en el otro en aproximadamente 30 ms.
- Si desea escuchar el efecto sin confirmarlo, reduzca Mix hacia 0 % para volver a la señal seca manteniendo la configuración de Drive en su lugar.

## Solución de problemas

- **La curva de transferencia no se curva al aumentar Drive** — Es posible que la etapa de tubo no esté habilitada para ese lado. Habilítela mediante el widget CHAIN. El applet permanece oculto hasta que la etapa esté activa.
- **Los potenciómetros del applet no coinciden con el editor flotante** — El applet se sincroniza desde el motor mediante un temporizador de sondeo. Espere un momento; deberían alinearse en aproximadamente 30 ms. Si permanecen desincronizados, es posible que el motor de audio no esté conectado — verifique que la conexión con la radio esté activa.

## Relacionado

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Desplace Bias para ajustar el equilibrio de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Aclare u oscurezca la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcle la saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Omita el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
