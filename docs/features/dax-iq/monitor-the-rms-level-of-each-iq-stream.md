# Supervisar el nivel RMS de cada flujo IQ

El applet DAX IQ muestra un medidor de nivel en tiempo real para cada uno de los cuatro flujos IQ, lo que permite confirmar que un flujo activo está transportando señal y estimar su intensidad de forma aproximada.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Al menos un flujo IQ debe estar habilitado (el botón muestra "On"). El medidor indica 0 cuando un flujo está apagado o la radio está desconectada.

## Pasos

1. Haga clic en el botón "IQ" de la bandeja en la barra lateral derecha para abrir el applet DAX IQ.
2. Localice la fila correspondiente al canal que desea supervisar: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
3. Confirme que el botón de alternancia a la derecha de esa fila muestra "On". Si muestra "Off", el medidor permanecerá en 0.
4. Observe la barra de progreso en el centro de la fila. Se actualiza en tiempo real mientras el flujo transporta señal.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango |
|---|---|---|---|
| Medidor IQ 1–4 | Barra de progreso que muestra el nivel RMS del flujo IQ. Escalado a partir del valor RMS bruto × 200. | 0 | 0–100 |
| IQ 1–4 Off/On | Activa o desactiva el flujo IQ. El medidor se restablece a 0 al cambiar a "Off". | Off | Off / On |
| Tasa IQ 1–4 | Frecuencia de muestreo del flujo IQ. No afecta la escala del medidor. | 48k | 24k, 48k, 96k, 192k |

Ninguno de estos controles tiene claves de configuración persistente que afecten directamente al medidor. El estado del medidor es en vivo y se restablece a 0 al desconectarse o deshabilitarse.

## Consejos

- Una lectura de 0 en un flujo con estado "On" puede indicar ausencia de señal dentro del slice (canal receptor), un receptor mal configurado o un problema de red que descarta paquetes IQ.
- El medidor se restablece a 0 automáticamente cuando la radio se desconecta o cuando el flujo se cambia a "Off". Este es el comportamiento esperado, no un error.
- La escala del medidor es 0–100, derivada de RMS × 200. Una lectura a escala completa (100) corresponde a un valor RMS de 0.5 o superior.

## Solución de problemas

- **El medidor permanece en 0 aunque el flujo está en "On"** — Es posible que la radio todavía esté configurando el flujo. Espere un momento después de habilitarlo; la conexión con la radio requiere un breve período de estabilización antes de que comiencen a fluir los datos. Si el medidor continúa en 0, verifique que su software SDR externo esté conectado al canal IQ correcto y que la radio tenga un slice activo en ese canal.
- **El medidor se restablece a 0 después de reconectarse** — Esto es normal. Los flujos son por sesión y la radio no los conserva entre conexiones. AetherSDR vuelve a habilitar automáticamente los flujos persistentes tras la reconexión.

## Temas relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la frecuencia de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
- [Descripción general de DAX IQ](overview.md)
