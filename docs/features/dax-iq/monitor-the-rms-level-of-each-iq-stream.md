# Monitorear el nivel RMS de cada flujo IQ

El applet DAX IQ incluye un medidor de nivel en tiempo real para cada uno de los cuatro flujos IQ. Utilícelo para confirmar que un flujo activo está recibiendo señal y para obtener una noción aproximada del nivel de entrada.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los medidores solo se actualizan cuando un flujo está activo.
- Al menos un flujo IQ debe estar habilitado (el botón muestra "On"). Un flujo deshabilitado mantiene el medidor en 0.

## Pasos

1. Haga clic en el botón **IQ** de la bandeja en la barra lateral derecha para abrir el applet DAX IQ.
2. Localice la fila del canal que desea monitorear: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
3. Si el botón de alternancia de esa fila muestra "Off", haga clic en él para que muestre "On" e iniciar el flujo.
4. Observe el medidor de nivel en esa fila. Se actualiza en tiempo real a medida que llegan datos IQ del radio.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango |
|---|---|---|---|
| Medidor IQ 1–4 | Muestra el nivel RMS del flujo IQ como gráfico de barras. Se reinicia a 0 cuando el flujo se deshabilita o el radio se desconecta. | 0 | 0–100 (escalado desde RMS × 200) |
| IQ 1–4 Off/On | Habilita o deshabilita el flujo IQ para ese canal. El medidor solo se actualiza mientras el botón muestra "On". | Off | Off / On |
| Tasa IQ 1–4 | Establece la tasa de muestreo para el flujo de ese canal. | 48k | 24k, 48k, 96k, 192k |

## Consejos

- Un medidor que permanece en 0 mientras el botón muestra "On" puede indicar que el flujo aún no fue aceptado por el radio. Desconéctese y vuelva a conectarse; AetherSDR rehabilita automáticamente los flujos guardados después de que la sesión se estabilice.
- La escala del medidor va de 0 a 100 internamente, obtenida al multiplicar el valor RMS bruto por 200. Los niveles de señal IQ en operación normal suelen situarse en la parte inferior de la escala.
- El medidor no tiene lectura numérica; es solo una barra. Para obtener un valor RMS preciso, utilice la aplicación receptora conectada al flujo IQ.

## Solución de problemas

- **El medidor permanece en 0 aunque el botón muestra "On"** — Es posible que el flujo no haya sido aceptado por el radio. Desconéctese del radio y vuelva a conectarse. AetherSDR intentará rehabilitar el flujo tras un breve retraso una vez que la sesión esté lista.
- **El medidor se reinicia a 0 después de reconectarse** — Este es el comportamiento esperado. AetherSDR reinicia todos los medidores al desconectarse. Los flujos que estaban habilitados anteriormente se restauran automáticamente al reconectarse.

## Relacionados

- [Habilitar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
- [Elegir la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Descripción general de DAX IQ](overview.md)
