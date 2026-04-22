# Monitorear el nivel RMS de cada flujo IQ

El applet DAX IQ muestra un medidor de nivel en tiempo real para cada uno de los cuatro flujos IQ. Úselo para confirmar que un flujo activo está transportando señal antes de enrutarlo a software externo.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet DAX IQ requiere una conexión de radio activa.
- Al menos un flujo IQ debe estar habilitado (activado en "On"). El medidor muestra 0 cuando un flujo está desactivado o el radio está desconectado.

## Pasos

1. Haga clic en el botón de bandeja **IQ** en la barra lateral derecha para abrir el applet DAX IQ.
2. Ubique la fila del canal que desea monitorear: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
3. Confirme que el botón de alternancia en esa fila muestre **On**. Si muestra **Off**, habilite el flujo primero — consulte [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md).
4. Observe el medidor de nivel en el centro de la fila. Se actualiza en tiempo real a medida que el flujo transporta señal.

## Qué hace cada control

| Control | Qué muestra | Rango | Valor predeterminado |
|---|---|---|---|
| Medidor IQ 1–4 | Nivel RMS del flujo IQ, escalado a partir del valor RMS bruto (RMS × 200) | 0–100 | 0 |
| IQ 1–4 Off/On | Si el flujo está activo en el radio | Off / On | Off |

El medidor se restablece a 0 cuando el flujo se cambia a **Off** o el radio se desconecta.

## Consejos

- Un medidor que permanece en 0 con un flujo en **On** indica que no están llegando datos IQ. Verifique que la tasa de muestreo esté configurada y que el radio tenga un slice (receptor de segmento) activo en ese canal.
- La escala del medidor es 0–100, obtenida multiplicando el valor RMS bruto por 200. Los valores de amplitud IQ típicamente se encuentran en el rango 0.0–0.5, por lo que una lectura de 100 representa la escala completa.
- El medidor no persiste entre sesiones. Los flujos IQ son por sesión y no son guardados por el radio.

## Solución de problemas

- **El medidor muestra 0 aunque el flujo está en On** — Es posible que el radio aún no esté enviando datos en ese canal. Verifique que un receptor slice esté asignado al canal IQ en la configuración de su radio. Confirme también que la aplicación externa haya abierto el flujo.
- **El medidor se restablece a 0 después de reconectar** — Comportamiento esperado. Los flujos IQ son por sesión. Vuelva a cambiar el flujo a **On** después de cada conexión.

## Temas relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
- [Descripción general de DAX IQ](overview.md)
