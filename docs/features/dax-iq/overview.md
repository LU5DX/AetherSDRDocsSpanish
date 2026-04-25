# Descripción general de DAX IQ

El applet DAX IQ le permite habilitar y supervisar hasta cuatro flujos de datos IQ independientes desde el FLEX-8600. Use estos flujos para enviar muestras IQ en bruto a software SDR externo a la tasa de muestreo que elija.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX IQ se deshabilita cuando no hay conexión con ninguna radio.
- El panel del applet debe estar visible. Si no lo está, seleccione `View > Applet Panel` para mostrarlo.

## Cómo funciona

El FLEX-8600 admite cuatro canales DAX IQ simultáneos. Cada canal es un flujo independiente de muestras complejas (I y Q) que el software externo puede consumir a través de la interfaz DAX. Los flujos son por sesión: la radio no los conserva entre desconexiones. Cuando AetherSDR se reconecta, espera a que la sesión se estabilice y luego reactiva los canales que usted tenía habilitados anteriormente.

Para abrir el applet DAX IQ, haga clic en el botón de bandeja **IQ** en la barra lateral derecha. El applet está oculto de forma predeterminada.

Cada uno de los cuatro canales — denominados **IQ 1** a **IQ 4** — tiene tres controles en una sola fila:

- Un selector de tasa para establecer la tasa de muestreo de ese canal.
- Un medidor de nivel que muestra la salida RMS actual del flujo.
- Un botón de activación para habilitar o deshabilitar el flujo.

El selector de tasa se sincroniza con la tasa reportada por la radio cuando un flujo está activo, por lo que el valor mostrado siempre refleja lo que la radio está utilizando realmente.

Cuando AetherSDR se desconecta de la radio, todos los botones de activación se restablecen a **Off** y todos los medidores se restablecen a 0.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|---|
| Tasa IQ 1–4 | Establece la tasa de muestreo del canal. | `48k` | `24k` (24000), `48k` (48000), `96k` (96000), `192k` (192000) | `DaxIqRate1` – `DaxIqRate4` |
| Medidor IQ 1–4 | Muestra el nivel RMS del flujo, escalado de 0 a 100. Se restablece a 0 al desconectarse o cuando el flujo se deshabilita. | 0 | 0–100 | — |
| IQ 1–4 Off/On | Activa o desactiva el flujo IQ. Muestra **Off** cuando está inactivo y **On** cuando está activo. | Off | Off / On | `DaxIqEnabled1` – `DaxIqEnabled4` |

## Consejos

- La tasa y el estado de habilitación de cada canal se guardan localmente. Al reconectarse, AetherSDR restaura automáticamente los canales habilitados anteriormente tras una breve espera para permitir que la sesión de radio termine de configurarse.
- Desplazarse por el panel del applet no cambiará accidentalmente los selectores de tasa ni otros controles; los controles del panel se bloquean mientras se desplaza.

## Temas relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Supervisar el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
