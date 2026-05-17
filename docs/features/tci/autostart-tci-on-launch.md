# Inicio automático de TCI al arrancar

Configure AetherSDR para que inicie automáticamente el servidor WebSocket TCI cada vez que se lance la aplicación, de modo que programas de terceros como Log4OM o herramientas SunSDR se conecten sin intervención manual.

## Antes de empezar

- AetherSDR debe estar compilado con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón de la bandeja TCI no aparece, esta compilación no incluye TCI.
- La radio debe estar conectada antes de que el servidor TCI pueda atender clientes, aunque la opción de inicio automático se puede configurar estando desconectado.
- Decida qué puerto debe usar el servidor. El valor predeterminado es `50001`. Consulte [Cambiar el puerto TCI](change-the-tci-port.md) si necesita un puerto diferente antes de activar el inicio automático.

## Pasos

1. Haga clic en `Settings > Autostart TCI with AetherSDR`.
2. Confirme que el elemento esté marcado. AetherSDR iniciará ahora el servidor TCI en cada lanzamiento posterior.
3. Para verificar que la configuración surta efecto de inmediato, haga clic en el botón de la bandeja TCI en la barra lateral derecha para abrir el applet del Servidor TCI. El estado del servidor debería mostrar `:<puerto> (0 clientes)` en lugar de `(detenido)`.

Para desactivar el inicio automático, haga clic nuevamente en `Settings > Autostart TCI with AetherSDR` para desmarcarlo.

## Qué hace cada control

| Control                                                         | Valor predeterminado | Rango válido                                                                                                                                                                                                                                                         |
|-----------------------------------------------------------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Settings > Autostart TCI with AetherSDR` (elemento de menú marcable) | Desactivado          | Activado / Desactivado                                                                                                                                                                                                                                               |
| Puerto                                                          | `50001`              | 1024–65535                                                                                                                                                                                                                                                           |
| Habilitar (botón de alternancia en el applet del Servidor TCI)  | Desactivado          | Activado / Desactivado                                                                                                                                                                                                                                               |
| Ganancia+medidor RX1–RX4                                        | 0.5                  | 0.0–1.0                                                                                                                                                                                                                                                              |
| Ganancia+medidor TX                                             | Los controles deslizantes ajustan la ganancia TX de TCI y emiten tciTxGainChanged. | TciServer::setTxGain conserva TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). |
| Etiquetas de asignación de slice RX/TX                          | — (guión largo)      | — o letra del slice                                                                                                                                                                                                                                                  |

### Etiquetas de asignación de slice RX/TX

Las etiquetas de estado RX1–RX4 y TX muestran qué slice controla actualmente cada canal. La letra del slice ahora se muestra como texto enriquecido (HTML) para que los identificadores de slice estilizados de `SliceLabel::richText` se vean correctamente. Las etiquetas se actualizan automáticamente cuando cambian las asignaciones de slice.

## Consejos

- Activar el inicio automático también establece `AutoStartTCI` en `Verdadero`. Al alternar Habilitar en el applet del Servidor TCI se escribe la misma clave, por lo que ambos controles se mantienen sincronizados.
- Si el puerto ya está en uso al iniciar, el servidor no arrancará: el botón de alternancia Habilitar vuelve a la posición de apagado y el estado muestra `(puerto en uso)`. Cambie el puerto y reinicie AetherSDR, o termine el proceso conflictivo.
- Los valores de puerto fuera del rango válido regresan automáticamente a `50001`.

## Solución de problemas

- **`Settings > Autostart TCI with AetherSDR` no aparece en el menú** — Esta compilación de AetherSDR no incluye soporte WebSocket. TCI no está disponible.
- **El estado del servidor muestra `(puerto en uso)` después del inicio** — Otro proceso ya está vinculado al puerto configurado. Cambie el puerto en el campo Puerto del applet del Servidor TCI, guarde y reinicie AetherSDR. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El estado permanece `(detenido)` aunque el inicio automático esté activado** — La radio aún no está conectada. El servidor TCI requiere una conexión de radio. Conéctese a la radio; el servidor se iniciará una vez que se establezca la conexión.
- **Las etiquetas de slice aparecen como HTML sin formato** — Esto indica una compilación anterior sin la corrección de texto enriquecido. Actualice a v26.5.2.1 o posterior para garantizar que las letras de slice renderizadas en HTML se muestren correctamente (#2606).

## Relacionados

- [Visión general del Servidor TCI](overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
