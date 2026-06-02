# Solución: DAX IQ no produce salida en Windows o Linux solo con PulseAudio

A partir de AetherSDR v26.5.1, la ruta de configuración de audio DAX IQ se inicializa correctamente en sistemas Windows y Linux que usan solo PulseAudio (sin PipeWire). Anteriormente, la configuración de flujo fallaba silenciosamente sin inicializar, lo que resultaba en una salida IQ nula en esas plataformas.

## Antes de comenzar

- Asegúrese de tener instalado AetherSDR v26.5.1 o posterior.
- Si utiliza Linux con **solo PulseAudio** (sin PipeWire), esta solución se aplica automáticamente.

## Pasos

No se requiere ninguna acción del usuario. La corrección se aplica del lado de la aplicación:

1. Inicie AetherSDR y conéctese a su radio FLEX-8600.
2. Active un canal DAX IQ usando el botón de la bandeja `IQ`, luego haga clic en el botón de alternancia para el canal deseado (IQ 1–4) y ajústelo a **On**.
3. Si anteriormente tenía flujos IQ activados pero no veía salida, simplemente alterne el(los) canal(es) afectado(s) a **Off** y luego nuevamente a **On** para activar la ruta de configuración corregida.

## Función de cada control

| Control | Etiqueta | Predeterminado | Notas |
|---------|----------|----------------|-------|
| Botón de alternancia | IQ 1–4 **On**/**Off** | **Off** | Haga clic para activar o desactivar el flujo IQ. Al alternar a **On**, la configuración de audio ahora recurre correctamente a PulseAudio en Windows y Linux sin PipeWire. |
| Cuadro combinado | IQ 1–4 rate | **48k** | Elija una frecuencia de muestreo de 24k, 48k, 96k o 192k. Al cambiar la frecuencia, se emite `iqRateChanged(channel, rate)`. Se sincroniza con la frecuencia informada por la radio cuando hay un flujo activo. |
| Medidor | IQ 1–4 meter | 0 | Muestra el nivel RMS del flujo IQ, escalado de 0 a 100 (RMS × 200). Se restablece a 0 al desconectar o desactivar. |

## Cambios visuales en v26.6.1

El applet DAX IQ ahora usa estilo adaptado al tema. En lugar de colores fijos, los fondos y segmentos de la barra de progreso del medidor se adaptan al tema actual. Esto garantiza una apariencia uniforme en temas claro y oscuro.

## Consejos

- Si DAX IQ aún no produce salida después de la actualización, intente reiniciar AetherSDR por completo y luego vuelva a activar el flujo IQ.
- La corrección solo se aplica al configurar el flujo: los flujos que ya estaban activados antes de la actualización pueden necesitar alternarse a Off y On nuevamente.

## Solución de problemas

- **Sin salida de audio en Windows o Linux solo con PulseAudio después de la actualización** — Alterne el canal IQ afectado a **Off** y luego nuevamente a **On**. Esto activa la ruta de configuración corregida que inicializa correctamente el flujo de audio.
- **Aún sin salida después de alternar** — Verifique que su software SDR externo (por ejemplo, HDSDR, SDR Console) esté configurado para recibir audio del dispositivo DAX IQ correcto. La corrección aborda la configuración interna de AetherSDR; su receptor aún debe estar apuntado al dispositivo de audio virtual correcto.
- **El medidor no muestra actividad** — Asegúrese de que el flujo esté en **On** y que la frecuencia de muestreo seleccionada coincida con lo que espera su software SDR externo.

## Relacionado

- [Descripción general de DAX IQ](overview.md)
- [Activar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la frecuencia de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
