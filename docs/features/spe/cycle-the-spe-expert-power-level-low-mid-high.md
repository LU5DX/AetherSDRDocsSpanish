# Ciclar el nivel de potencia del SPE Expert (Low, Mid, High)

Esta página le muestra cómo ciclar el nivel de potencia de salida del amplificador SPE Expert entre Low, Mid y High, igual que la tecla POWER del panel frontal del amplificador.

## Antes de comenzar

- Conecte y configure su amplificador SPE Expert en el applet SPE. Consulte [Descripción general del amplificador SPE Expert](overview.md).
- Asegúrese de que el amplificador esté encendido y responda: el botón POWER está deshabilitado mientras el amplificador esté en silencio.

## Pasos

1. Abra el applet SPE: **Applet panel > SPE tile**.
2. Localice el botón **PWR** en la primera fila de botones. La etiqueta muestra el nivel de potencia actual (LOW, MID o HIGH) una vez que el applet lo conoce.
3. Haga clic en **PWR** para pasar al siguiente nivel. La etiqueta del botón se actualiza para mostrar el nuevo nivel.

## Qué hace cada control

- **PWR** — Muestra el nivel de potencia de salida actual (LOW, MID o HIGH) y pasa al siguiente nivel al hacer clic. Refleja la tecla POWER del panel frontal del amplificador. La etiqueta del botón muestra el nivel actual; al hacer clic se avanza al siguiente.

## Consejos

- El botón se llama **PWR**, no "POWER": esto es para que los cinco botones de la fila no se recorten en el ancho predeterminado del applet.
- Si el botón no muestra ningún nivel de texto, el applet aún no ha recibido el nivel actual del amplificador. Al hacer clic, igualmente ciclará el nivel.

## Solución de problemas

- **El botón PWR está atenuado** — El amplificador no responde o está en estado de silencio. Verifique la conexión serial o ser2net y que el amplificador esté encendido. Use **ON** para encenderlo si es necesario.

## Relacionado

- [Descripción general del amplificador SPE Expert](overview.md)
- [Monitorear la potencia directa y la ROE en el amplificador SPE Expert](monitor-forward-power-and-swr-on-the-spe-expert-amplifier.md)
- [Poner el amplificador SPE Expert en Operate o Standby](put-the-spe-expert-amplifier-in-operate-or-standby.md)
- [Sintonizar el amplificador SPE Expert](tune-the-spe-expert-amplifier.md)
