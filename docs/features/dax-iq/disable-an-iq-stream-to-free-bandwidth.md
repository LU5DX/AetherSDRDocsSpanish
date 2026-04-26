# Deshabilitar un flujo IQ para liberar ancho de banda

Cada flujo DAX IQ activo consume ancho de banda entre AetherSDR y el radio. Deshabilitar un flujo que no está en uso libera esa capacidad para otras tareas.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet DAX IQ requiere una conexión activa con el radio.
- Abra el applet DAX IQ haciendo clic en el botón IQ de la bandeja en la barra lateral derecha. El applet está oculto de forma predeterminada.

## Pasos

1. Localice la fila del canal que desea detener: IQ 1, IQ 2, IQ 3 o IQ 4.
2. Verifique que el botón de alternancia de esa fila muestre "On". Si ya muestra "Off", el flujo ya está inactivo.
3. Haga clic en el botón "On". La etiqueta del botón cambia a "Off", el estilo del botón se atenúa y el medidor de nivel se reinicia a 0.

El radio cierra el flujo de inmediato. El cambio se guarda para que el flujo no se reactive automáticamente en la próxima conexión.

## Qué hace cada control

| Control | Predeterminado | Valores válidos | Clave de ajuste persistido |
|---|---|---|---|
| IQ 1–4 Off/On | Off | Off, On | `DaxIqEnabled1` – `DaxIqEnabled4` |
| IQ 1–4 velocidad | 48k | 24k, 48k, 96k, 192k | `DaxIqRate1` – `DaxIqRate4` |
| IQ 1–4 medidor | 0 | 0–100 (RMS × 200) | — |

## Consejos

- El medidor se reinicia a 0 en cuanto se deshabilita un flujo. Una lectura distinta de cero confirma que el flujo sigue activo antes de deshabilitarlo.
- Los flujos IQ son por sesión en el lado del radio, pero AetherSDR conserva su elección de On/Off. Tras reconectarse, cualquier canal cuya clave de ajuste sea `"True"` se reactivará automáticamente después de un breve retardo una vez que la sesión esté lista. Establecer un canal en "Off" evita ese reinicio automático.
- Si solo necesita reducir la velocidad de datos en lugar de detener el flujo por completo, baje el selector de velocidad a 24k en vez de deshabilitar el flujo.

## Solución de problemas

- **El botón vuelve a "On" poco después de hacer clic en "Off"** — Otra aplicación puede estar solicitando el flujo, o se reconectó al radio mientras el ajuste persistido seguía siendo `"True"`. Haga clic en "Off" nuevamente; el ajuste se guardará como `"False"` y el flujo no se reiniciará en la próxima conexión.
- **El medidor permanece en un valor distinto de cero después de deshabilitar** — Es normal que haya un breve retardo entre la solicitud de deshabilitación y el reconocimiento del radio. El medidor se reinicia a 0 una vez que el radio confirma que el flujo ha sido cerrado.

## Relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la velocidad de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
