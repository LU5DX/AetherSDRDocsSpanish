# Gire Drive hasta que la curva empiece a doblarse (calidez en TX o modelado de tono en RX)

Use el control Drive para impulsar la señal hacia la etapa de tubo y producir saturación armónica. Observar cómo la curva de transferencia se dobla al aumentar Drive le indica exactamente cuándo y en qué medida ocurre la saturación.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea procesar (TX o RX). Habilítela a través del widget CHAIN o abriendo el editor flotante para ese lado.
- El subcontenedor "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) debe estar visible dentro del contenedor padre Aetherial Audio (TXDSP) en el panel de applets.

## Pasos

1. Ubique el subcontenedor correcto en el panel de applets: "Aetherial Mic-PreAmp" para el modelado de señal TX, o "Aetherial Dynamic Tube" para el modelado de tono RX.
2. Observe la curva de transferencia en la parte superior del applet. Con Drive en 0.0 dB, la curva es una línea diagonal recta — sin saturación.
3. Gire el control Drive en sentido horario. Observe la curva de transferencia: los hombros comienzan a comprimirse y doblarse a medida que aumenta Drive. La bola de entrada en tiempo real se desplaza a lo largo de la curva y muestra qué parte de la curva está alcanzando el nivel de señal actual.
4. Deje de aumentar Drive cuando la curva muestre la cantidad de curvatura deseada. Una calidez sutil aparece con una ligera curvatura; una saturación más intensa se obtiene empujando Drive hasta 24.0 dB.
5. Si la salida saturada es notablemente más alta o más baja que la señal sin procesar, ajuste el control Output para compensar. El medidor OUT del editor flotante (columna más a la derecha) muestra el nivel de pico post-saturación y ayuda a calibrar el ajuste.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistente (TX / RX) |
|---|---|---|---|
| Drive | 0.0 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` / `ClientTubeRxDriveDb` |
| Tone | 0.00 | −1.0 – 1.0 | `ClientTubeTxTone` / `ClientTubeRxTone` |
| Bias | 0 % | 0 – 100 % | `ClientTubeTxBias` / `ClientTubeRxBias` |
| Output | 0.0 dB | −24.0 – 12.0 dB | `ClientTubeTxOutputDb` / `ClientTubeRxOutputDb` |
| Dry/Wet | 100 % | 0 – 100 % | `ClientTubeTxDryWet` / `ClientTubeRxDryWet` |

**Curva de transferencia** — Indicador. Dibuja la curva de transferencia del tubo en tiempo real. La forma cambia al ajustar Drive, Bias y la selección de modelo. La bola de entrada en tiempo real recorre la curva al nivel de señal actual, mostrando el régimen de saturación activo. Sin clave persistente.

**Drive** — Impulsa más señal hacia la etapa de tubo. Los valores más altos hacen que la curva de transferencia se doble con mayor intensidad, produciendo un contenido armónico más fuerte.

**Tone** — Los valores negativos oscurecen la señal saturada; los valores positivos la aclaran.

**Bias** — Desplaza el punto de operación en la curva de transferencia, modificando el equilibrio entre armónicos pares e impares.

**Output** — Ganancia de compensación o recorte posterior al tubo. Úsela para igualar el nivel saturado con el nivel sin procesar.

**Dry/Wet** — Mezcla seca/húmeda. Al 100 % solo pasa la señal saturada. Reducir Dry/Wet mezcla la señal seca original para obtener saturación en paralelo.

**Medidor de nivel de salida** — Indicador. Visible únicamente en el editor flotante ("Aetherial Tube — TX" o "— RX"), en la columna más a la derecha etiquetada como OUT. Muestra el nivel de pico post-saturación con balística de ataque rápido y liberación lenta. Zonas de color: verde (−60 a −12 dB), verde lima (−12 a −6 dB), ámbar (−6 a −3 dB), rojo (por encima de −3 dB). Sin clave persistente.

## Consejos

- Comience con Drive en 0.0 dB y auméntelo lentamente. La curva de transferencia es la guía visual más directa para conocer la cantidad de saturación que está añadiendo.
- Los lados TX y RX son completamente independientes. Los ajustes en el tubo TX no afectan al tubo RX ni viceversa.
- El editor flotante (que se abre haciendo doble clic en la etapa TUBE en el widget CHAIN) y los controles del applet anclado permanecen sincronizados — los cambios en uno se reflejan en el otro en aproximadamente 30 ms.
- Si desea escuchar el efecto sin confirmarlo, reduzca Dry/Wet hacia 0 % para volver a la señal seca conservando el ajuste de Drive en su lugar.
- Use el medidor OUT en el editor flotante para confirmar que el nivel post-saturación es el esperado antes de cerrar el editor.

## Solución de problemas

- **La curva de transferencia no se dobla al aumentar Drive** — Es posible que la etapa Tube no esté habilitada para ese lado. Habilítela a través del widget CHAIN. El applet permanece oculto hasta que la etapa esté activa.
- **Los controles del applet no coinciden con los del editor flotante** — El applet se sincroniza desde el motor mediante un temporizador de sondeo. Espere un momento; deberían alinearse en unos 30 ms. Si continúan desincronizados, es posible que el motor de audio no esté conectado — verifique que la conexión de radio esté activa.
- **El medidor OUT no es visible** — El medidor de nivel de salida solo aparece en el editor flotante, no en el mosaico del applet anclado. Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Desplace Bias para ajustar el equilibrio entre armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Aclare u oscurezca la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compense cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcla de saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Omita el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
