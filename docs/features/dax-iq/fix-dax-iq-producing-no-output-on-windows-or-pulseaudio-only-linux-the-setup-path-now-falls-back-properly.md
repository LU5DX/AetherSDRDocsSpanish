# Applet DAX IQ

## Propósito

El applet DAX IQ proporciona controles de flujo DAX IQ por canal: habilitar/deshabilitar cada uno de los cuatro flujos IQ, seleccionar una frecuencia de muestreo y monitorear el nivel en tiempo real. El applet está disponible cuando se conecta a un radio FLEX-8600.

## Acceso al Applet DAX IQ

1. Inicie AetherSDR y conéctese a su radio FLEX-8600.
2. Haga clic en el botón de la bandeja **IQ** para abrir el applet DAX IQ.
3. Use los controles a continuación para gestionar flujos IQ individuales.

## Controles

| Control | Etiqueta | Valor predeterminado | Rango válido | Notas |
|---------|----------|----------------------|--------------|-------|
| Botón de alternancia | IQ 1–4 **On**/**Off** | **Off** | - | Haga clic para habilitar o deshabilitar el flujo IQ. El texto y estilo del botón cambian entre "Off" y "On". Los flujos son por sesión y no son persistidos por el radio. |
| Cuadro combinado | Tasa IQ 1–4 | **48k** | 24k (24000), 48k (48000), 96k (96000), 192k (192000) | Seleccione la frecuencia de muestreo para el flujo IQ. Cambiar la tasa emite `iqRateChanged(channel, rate)`. El cuadro combinado se sincroniza con la tasa reportada por el radio cuando un flujo está activo. |
| Medidor | Medidor IQ 1–4 | 0 | 0–100 (escalado desde RMS × 200) | Muestra el nivel RMS del flujo IQ. Se restablece a 0 al desconectar, deshabilitar o cuando el flujo no está vinculado a un panadapter. |

## Detalles de Comportamiento

### Habilitar/Deshabilitar Flujos IQ

- Haga clic en el botón de alternancia para cambiar un flujo a **On** u **Off**.
- Al habilitar, el applet aplica la frecuencia de muestreo actualmente seleccionada al flujo del radio. Si cambió la tasa mientras el flujo estaba deshabilitado, esa tasa se usa al habilitar.
- Al deshabilitar, el medidor se restablece a 0 y el botón muestra **Off**.

### Selección de Frecuencia de Muestreo

- El cuadro combinado contiene la tasa deseada. Cuando un flujo está activo y no está en proceso de ajuste de tasa, el cuadro combinado se sincroniza con la tasa reportada por el radio.
- Durante el ajuste de tasa (cuando el radio está aplicando una nueva tasa), el cuadro combinado conserva su selección hasta que la tasa del flujo se estabilice.
- Cuando un flujo está deshabilitado, el cuadro combinado retiene la tasa seleccionada, lista para la próxima activación.

### Comportamiento del Medidor

- El medidor muestra el nivel RMS del flujo IQ solo cuando el flujo está activamente vinculado a un panadapter.
- Si el flujo está deshabilitado, o si está habilitado pero no vinculado a un panadapter (dirección pan es `0x0` o vacía), el medidor muestra 0.
- Esto evita que el medidor se congele en el último valor cuando un flujo pierde su vinculación al panadapter.

## Cambios Visuales

El applet DAX IQ utiliza estilos sensibles al tema. Los fondos y segmentos de la barra de progreso del medidor se adaptan al tema actual para una apariencia consistente en temas claros y oscuros.

## Notas Específicas de la Plataforma

- **Windows y Linux (solo PulseAudio, sin PipeWire):** A partir de AetherSDR v26.5.1, la ruta de configuración de audio DAX IQ se inicializa correctamente en estas plataformas. Si previamente tenía flujos IQ habilitados sin salida de audio, alterne el/los canal(es) afectado(s) a **Off** y luego nuevamente a **On**.
- **Linux con PipeWire:** No se requiere ninguna acción especial. El applet DAX IQ funciona de forma nativa.

## Persistencia

El estado de habilitación/deshabilitación del flujo IQ se persiste por sesión en la configuración de la aplicación. Al reconectarse al radio, el applet restaura el estado de los canales previamente habilitados después de un breve retardo (aproximadamente 1,5 segundos) para permitir que se complete la configuración de la sesión y el flujo.

## Solución de Problemas

| Problema | Solución |
|----------|----------|
| **Sin salida de audio en Windows o Linux solo PulseAudio después de la actualización** | Alterne el canal IQ afectado a **Off** y luego nuevamente a **On**. Esto activa la ruta de configuración corregida. |
| **Aún sin salida después de alternar** | Verifique que su software SDR externo (por ejemplo, HDSDR, SDR Console) esté configurado para recibir audio del dispositivo DAX IQ correcto. |
| **El medidor no muestra actividad** | Asegúrese de que el flujo esté en **On**, la frecuencia de muestreo seleccionada coincida con su software externo y el flujo esté vinculado a un panadapter. |
| **El flujo no se restaura después de reconectar** | Asegúrese de que el flujo estuviera habilitado (en **On**) antes de desconectar. El applet solo restaura canales que estaban explícitamente habilitados. |

## Relacionado

- [Descripción general de DAX IQ](overview.md)
- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
