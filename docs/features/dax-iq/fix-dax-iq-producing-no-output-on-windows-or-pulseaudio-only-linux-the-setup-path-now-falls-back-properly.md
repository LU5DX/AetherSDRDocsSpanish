# Solucionar el problema de DAX IQ sin salida de audio en Windows o Linux solo con PulseAudio

A partir de AetherSDR v26.5.1, la ruta de configuración de audio DAX IQ se inicializa correctamente en sistemas Windows y Linux que usan únicamente PulseAudio (sin PipeWire). Anteriormente, la configuración del flujo de audio finalizaba silenciosamente sin inicializarse, lo que provocaba que no hubiera salida IQ en esas plataformas.

## Antes de comenzar

- Asegúrese de tener instalado AetherSDR v26.5.1 o posterior.
- Si está ejecutando Linux con **solo PulseAudio** (sin PipeWire), esta corrección se aplica automáticamente.

## Pasos

No es necesaria ninguna acción por parte del usuario. La corrección se aplica del lado de la aplicación:

1. Inicie AetherSDR y conéctese a su radio FLEX-8600.
2. Active un canal DAX IQ usando el botón de la bandeja `IQ` y luego haga clic en el botón de alternancia del canal deseado (IQ 1–4) para ponerlo en **On**.
3. Si anteriormente tenía flujos IQ activados pero no veía salida, simplemente alterne el o los canales afectados a **Off** y luego nuevamente a **On** para activar la ruta de configuración corregida.

## Función de cada control

| Control | Etiqueta | Valor predeterminado | Notas |
|---------|----------|----------------------|-------|
| Botón de alternancia | IQ 1–4 **On**/**Off** | **Off** | Haga clic para activar o desactivar el flujo IQ. Al alternar a **On**, la configuración de audio ahora recurre correctamente a PulseAudio en Windows y Linux sin PipeWire. |

## Consejos

- Si DAX IQ sigue sin producir salida después de la actualización, intente reiniciar AetherSDR por completo y luego vuelva a activar el flujo IQ.
- La corrección solo se aplica al momento de configurar el flujo; los flujos que ya estaban activados antes de la actualización pueden necesitar ser desactivados y activados nuevamente.

## Solución de problemas

- **Sin salida de audio en Windows o Linux solo con PulseAudio después de la actualización** — Alterne el canal IQ afectado a **Off** y luego a **On** nuevamente. Esto activa la ruta de configuración corregida que inicializa correctamente el flujo de audio.
- **Aún sin salida después de alternar** — Verifique que su programa SDR externo (por ejemplo, HDSDR, SDR Console) esté configurado para recibir audio del dispositivo DAX IQ correcto. La corrección aborda la configuración interna de AetherSDR; su receptor aún debe estar apuntado al dispositivo de audio virtual correcto.

## Relacionados

- [Descripción general de DAX IQ](overview.md)
- [Activar un flujo IQ para programas SDR externos](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
