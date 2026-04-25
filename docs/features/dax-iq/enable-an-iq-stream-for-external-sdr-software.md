# Habilitar un flujo IQ para software SDR externo

El applet DAX IQ permite activar uno o más de los cuatro flujos IQ disponibles en el FLEX-8600, poniendo datos IQ en bruto a disposición del software SDR externo en su sistema. Debe habilitar un flujo antes de que las aplicaciones externas puedan recibir datos de él.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los controles DAX IQ no están disponibles sin una conexión de radio activa.
- El panel del applet debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de bandeja **IQ** en la barra lateral derecha para abrir el applet DAX IQ.
2. Localice la fila del canal que desea: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
3. Si es necesario, establezca la tasa de muestreo usando el cuadro combinado de tasa para ese canal (valor predeterminado: **48k**). Consulte [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md) para más detalles.
4. Haga clic en el botón **Off** en la fila de ese canal. La etiqueta del botón cambia a **On** y su estilo cambia para indicar que el flujo está activo.
5. Configure su software SDR externo para recibir el flujo IQ en el número de canal DAX IQ correspondiente.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Valores válidos |
|---|---|---|---|
| Cuadro combinado de tasa (IQ 1–4) | Establece la tasa de muestreo del flujo IQ. El cuadro combinado se sincroniza con la tasa reportada por la radio cuando un flujo está activo. La tasa seleccionada se guarda por canal. | 48k | 24k, 48k, 96k, 192k |
| Botón alternante Off/On (IQ 1–4) | Habilita o deshabilita el flujo IQ para ese canal. Muestra **Off** cuando está inactivo, **On** cuando está activo. | Off | Off, On |
| Medidor de nivel (IQ 1–4) | Muestra el nivel RMS del flujo IQ activo en una escala de 0 a 100. Se restablece a 0 cuando el flujo se deshabilita o la radio se desconecta. | 0 | 0–100 |

## Consejos

- Los flujos IQ son por sesión en la radio. AetherSDR guarda los canales que tenía habilitados y la tasa de muestreo seleccionada. Al reconectarse, AetherSDR espera brevemente a que la sesión de radio se estabilice antes de volver a habilitar los flujos previamente activos — los botones mostrarán brevemente **Off** después de conectarse antes de restaurarse.
- Puede habilitar hasta cuatro flujos IQ simultáneamente, uno por canal.
- Si su software externo no recibe datos, confirme que el botón **On** esté encendido para el canal correcto y que la aplicación externa esté configurada para el número de canal correspondiente.

## Solución de problemas

- **El botón vuelve a Off poco después de hacer clic en On** — La radio rechazó la solicitud del flujo, probablemente porque la sesión aún no estaba completamente establecida. Espere unos segundos después de conectarse e intente de nuevo.
- **El medidor de nivel permanece en 0 a pesar de que el flujo está en On** — Es posible que la aplicación externa no esté consumiendo el flujo, o que la radio no esté enviando audio en ese slice (canal de recepción). Verifique que su software externo esté conectado al canal DAX IQ correcto.

## Relacionados

- [Descripción general de DAX IQ](overview.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
