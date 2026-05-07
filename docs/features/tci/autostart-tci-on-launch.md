# Inicio automático de TCI al iniciar

Configure AetherSDR para que inicie automáticamente el servidor WebSocket de TCI cada vez que se abra la aplicación, de modo que software de terceros como Log4OM o herramientas SunSDR se conecten sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón de TCI en la bandeja está ausente, esta compilación no incluye TCI.
- La radio debe estar conectada antes de que el servidor TCI pueda atender clientes, aunque la configuración de inicio automático se puede ajustar sin conexión.
- Decida qué puerto usará el servidor. El valor predeterminado es `50001`. Consulte [Change the TCI port](change-the-tci-port.md) si necesita un puerto diferente antes de habilitar el inicio automático.

## Pasos

1. Haga clic en `Settings > Autostart TCI with AetherSDR`.
2. Confirme que el elemento esté marcado. AetherSDR iniciará el servidor TCI en cada apertura posterior.
3. Para verificar que el cambio surta efecto de inmediato, haga clic en el botón de TCI en la bandeja de la barra lateral derecha para abrir el applet del Servidor TCI. El estado del servidor debería mostrar `:<puerto> (0 clients)` en lugar de `(stopped)`.

Para deshabilitar el inicio automático, haga clic nuevamente en `Settings > Autostart TCI with AetherSDR` para desmarcarlo.

## Función de cada control

| Control                                                        | Valor predeterminado | Rango válido                                                                                                                                                                                                                         |
|----------------------------------------------------------------|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Settings > Autostart TCI with AetherSDR` (elemento de menú marcable) | Apagado              | Encendido / Apagado                                                                                                                                                                                                                  |
| Puerto                                                         | `50001`              | 1024–65535                                                                                                                                                                                                                           |
| Habilitar (botón de activación en el applet Servidor TCI)       | Apagado              | Encendido / Apagado                                                                                                                                                                                                                  |
| RX1–RX4 ganancia+medidor                                       | 0.5                  | 0.0–1.0                                                                                                                                                                                                                             |
| TX ganancia+medidor                                            | Los deslizadores ajustan la ganancia TX de TCI y emiten tciTxGainChanged. | TciServer::setTxGain conserva TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). |

## Consejos

- Al habilitar el inicio automático también se establece `AutoStartTCI` en `True`. Al alternar Habilitar en el applet Servidor TCI se escribe la misma clave, por lo que ambos controles se mantienen sincronizados.
- Si el puerto ya está en uso al iniciar, el servidor no se iniciará: el botón Habilitar vuelve a Apagado y el estado muestra `(port in use)`. Cambie el puerto y reinicie AetherSDR, o cierre el proceso conflictivo.
- Los valores de puerto fuera de rango se restablecen automáticamente a `50001`.

## Solución de problemas

- **`Settings > Autostart TCI with AetherSDR` no aparece en el menú** — Esta compilación de AetherSDR no incluye soporte WebSocket. TCI no está disponible.
- **El estado del servidor muestra `(port in use)` después del inicio** — Otro proceso ya está vinculado al puerto configurado. Cambie el puerto en el campo Puerto del applet Servidor TCI, guarde y reinicie AetherSDR. Consulte [Change the TCI port](change-the-tci-port.md).
- **El estado permanece `(stopped)` a pesar de tener el inicio automático habilitado** — La radio aún no está conectada. El servidor TCI requiere una conexión de radio. Conéctese a la radio; el servidor se iniciará una vez que se establezca la conexión.

## Relacionados

- [TCI Server overview](overview.md)
- [Enable the TCI server for Log4OM / SunSDR clients](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Change the TCI port](change-the-tci-port.md)
- [Adjust TCI RX gain per channel](adjust-tci-rx-gain-per-channel.md)
- [Adjust TCI TX gain](adjust-tci-tx-gain.md)
