# Deshabilitar un flujo IQ para liberar ancho de banda

Deshabilitar un flujo DAX IQ activo impide que consuma ancho de banda DSP del radio y rendimiento de red. Haga esto cuando una aplicación SDR externa ya no necesite los datos IQ, o cuando desee recuperar recursos para otras rebanadas (slices).

## Antes de comenzar

- AetherSDR debe estar conectado a un radio Flex. El applet DAX IQ requiere una conexión de radio activa.
- Abra el applet DAX IQ haciendo clic en el botón IQ de la bandeja en la barra lateral derecha. El applet está oculto de forma predeterminada.
- Identifique qué canal (IQ 1–4) desea deshabilitar. El botón de alternancia de ese canal debe mostrar actualmente "On".

## Pasos

1. Haga clic en el botón IQ de la bandeja en la barra lateral derecha para mostrar el applet DAX IQ si aún no está visible.
2. Encuentre la fila del canal que desea detener: IQ 1, IQ 2, IQ 3 o IQ 4.
3. Haga clic en el botón "On" en el extremo derecho de esa fila.
4. La etiqueta del botón cambia a "Off", el estilo del botón cambia a la apariencia inactiva y el medidor de nivel se restablece a 0.

El flujo ahora está deshabilitado. El radio deja de transmitir datos IQ para ese canal.

## Qué hace cada control

| Control | Función | Valor predeterminado | Valores válidos |
|---|---|---|---|
| IQ 1–4 Off/On | Activa o desactiva el flujo IQ para ese canal. Al hacer clic mientras está en "On", deshabilita el flujo y restablece el medidor. | Off | Off, On |
| Tasa IQ 1–4 | Establece la frecuencia de muestreo del canal. No tiene efecto mientras el flujo está deshabilitado, pero conserva su valor. | 48k | 24k, 48k, 96k, 192k |
| Medidor IQ 1–4 | Muestra el nivel RMS en tiempo real del flujo IQ. Se restablece a 0 de inmediato cuando el flujo se deshabilita. | 0 | 0–100 |

## Sugerencias

- Los flujos IQ son por sesión y el radio no los conserva. Si AetherSDR se desconecta y vuelve a conectar, los cuatro canales regresan a "Off" independientemente de su estado anterior.
- Deshabilitar un flujo también restablece su medidor de nivel a 0. Si el medidor continúa mostrando un valor superior a 0 brevemente después de hacer clic en "Off", se estabilizará una vez que el radio confirme que el flujo se ha detenido y el estado del botón se sincronice con el radio.
- Si el software SDR externo aún mantiene el flujo abierto, el botón puede revertirse a "On" cuando el radio le reporte el estado del flujo a AetherSDR. Cierre la aplicación externa primero y luego deshabilite el flujo.

## Solución de problemas

- **El botón revierte a "On" inmediatamente después de hacer clic** — El radio está reportando el flujo como aún activo, probablemente porque un software externo conectado a ese canal IQ lo mantiene abierto. Cierre la aplicación externa e intente de nuevo.
- **El medidor de nivel no se restablece a 0** — El medidor se restablece cuando el radio confirma que el flujo ha desaparecido. Un breve retraso es normal. Si no se restablece en absoluto, es posible que el flujo no se haya deshabilitado correctamente; verifique el estado de la conexión de su radio.

## Relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Seleccionar la frecuencia de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Descripción general de DAX IQ](overview.md)
