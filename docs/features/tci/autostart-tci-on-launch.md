# Inicio automático de TCI al iniciar

Configure AetherSDR para que inicie el servidor WebSocket TCI automáticamente cada vez que se abra la aplicación, de modo que software de terceros como Log4OM o clientes SunSDR se conecten sin intervención manual.

## Antes de comenzar

- AetherSDR debe compilarse con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón de la bandeja TCI no está presente, esta compilación no incluye TCI.
- La radio debe estar conectada antes de que el servidor TCI pueda atender clientes, aunque la configuración de inicio automático puede ajustarse mientras está desconectada.
- Decida qué puerto usará el servidor. El valor predeterminado es `50001`. Consulte [Cambiar el puerto TCI](change-the-tci-port.md) si necesita un puerto diferente antes de habilitar el inicio automático.

## Pasos

1. Haga clic en `Settings > Autostart TCI with AetherSDR`.
2. Confirme que el elemento esté marcado. AetherSDR iniciará el servidor TCI en cada apertura posterior.
3. Para verificar que el ajuste surta efecto de inmediato, haga clic en el botón de la bandeja TCI en la barra lateral derecha para abrir el applet del Servidor TCI. El estado del servidor debe mostrar `:<puerto> (0 clientes)` en lugar de `(detenido)`.

Para deshabilitar el inicio automático, haga clic nuevamente en `Settings > Autostart TCI with AetherSDR` para desmarcarlo.

## Qué hace cada control

| Control                                                                        | Predeterminado                                                                                                              | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Settings > Autostart TCI with AetherSDR` (elemento de menú marcable)          | Desactivado                                                                                                                 | Activado / Desactivado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Puerto                                                                         | `50001`                                                                                                                     | 1024–65535                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Habilitar (botón de conmutación en el applet del Servidor TCI)                 | Desactivado                                                                                                                 | Activado / Desactivado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX1–RX4                                                       | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Ganancia+medidor TX                                                            | Los deslizadores establecen la ganancia TX de TCI y emiten tciTxGainChanged. El clic derecho abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure). | TciServer::setTxGain persiste TciTxGain internamente; la IU refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú contextual permite al usuario elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes de modo digital: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (pasante, solo pone a cero NaN/Inf), o Measure (bypass verdadero con conteo de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Modo de desbordamiento TX (clic derecho)                                       | Clip                                                                                                                        | 0 (Clip), 1 (NaNGuard), 2 (Measure)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Etiquetas de asignación de slivers RX/TX                                       | — (guión largo)                                                                                                             | — o letra de sliver                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Indicador de estado del servidor                                               | (detenido)                                                                                                                  | `(detenido)`, `:<puerto> (N clientes)`, `(puerto en uso)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

## Nombres de accesibilidad para deslizadores de ganancia

Cada deslizador de ganancia TCI ahora tiene un nombre de accesibilidad para soportar lectores de pantalla y tecnologías de asistencia:

- **Deslizadores de ganancia RX1–RX4**: Nombrados "TCI RX 1 gain" hasta "TCI RX 4 gain" respectivamente.
- **Deslizador de ganancia TX**: Nombrado "TCI TX gain".

Estos nombres se establecen automáticamente y no requieren configuración del usuario.

## Etiquetas de asignación de slivers RX/TX

Las etiquetas de estado RX1–RX4 y TX muestran qué sliver impulsa cada canal actualmente. La letra del sliver ahora se muestra como texto enriquecido (HTML) para que los identificadores de sliver con estilo de `SliceLabel::richText` se muestren correctamente. Las etiquetas se actualizan automáticamente cuando cambian las asignaciones de slivers.

## Modo de desbordamiento TX

Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual con tres modos de manejo de desbordamiento:

| Modo | Valor | Descripción |
|------|-------|-------------|
| Clip (saturación ±1.0) | 0 | Recorte forzado de sobreexcursiones a ±1.0. Predeterminado defensivo; introduce armónicos en sobreexcursiones pero protege la conversión posterior a int16. |
| NaN guard (solo pone a cero NaN/Inf) | 1 | Pasa las muestras bit exacto; solo pone a cero valores NaN/Inf patológicos. Preserva la fidelidad del tono en modo digital; los flotantes fuera de rango llegan a la radio. |
| Measure only (bypass verdadero) | 2 | Nunca modifica las muestras. Cuenta sobreexcursiones para telemetría; la conversión posterior a int16 aún recorta en la ruta DAX nativa de la radio. |

El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). El ajuste se persiste en `TciTxOverflowMode` (0/1/2).

## Anotaciones de accesibilidad para controles TCI

Los controles del applet del servidor TCI ahora tienen nombres y descripciones de accesibilidad explícitos para soportar lectores de pantalla y tecnologías de asistencia:

- **Campo de puerto TCI**: Nombre accesible "TCI port", descripción "TCP port the TCI server listens on".
- **Botón de habilitación del servidor TCI**: Nombre accesible "TCI server enable", descripción "Start or stop the TCI server".

Estas anotaciones se establecen mediante los métodos `setAccessibleName` y `setAccessibleDescription` y no requieren configuración del usuario. El ancho del botón es de 76 píxeles para acomodar las etiquetas de texto "Enabled" y "Disabled".

## Estado del texto del botón de habilitación

El botón de conmutación Enable muestra "Enabled" cuando el servidor está en ejecución y "Disabled" cuando está detenido. El texto se actualiza dinámicamente al alternar el botón manualmente o cuando el inicio automático activa el servidor al iniciar. Esto hace que el estado del servidor sea visible incluso para usuarios con deficiencias en la visión del color.

## Consejos

- Habilitar el inicio automático también establece `AutoStartTCI` en `True`. Alternar Enable en el applet del Servidor TCI escribe la misma clave, por lo que ambos controles se mantienen sincronizados.
- Si el puerto ya está en uso al iniciar, el servidor no se iniciará: el conmutador Enable vuelve a apagado y el estado muestra `(puerto en uso)`. Cambie el puerto y reinicie AetherSDR, o cierre el proceso en conflicto.
- Los valores de puerto fuera de rango vuelven automáticamente a `50001`.

## Solución de problemas

- **`Settings > Autostart TCI with AetherSDR` no aparece en el menú** — Esta compilación de AetherSDR no incluye soporte WebSocket. TCI no está disponible.
- **El estado del servidor muestra `(puerto en uso)` después de iniciar** — Otro proceso ya está vinculado al puerto configurado. Cambie el puerto en el campo Port del applet del Servidor TCI, guarde y reinicie AetherSDR. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El estado permanece `(detenido)` a pesar de que el inicio automático está habilitado** — La radio aún no está conectada. El servidor TCI requiere una conexión de radio. Conéctese a la radio; el servidor se iniciará una vez que se establezca la conexión.
- **Las etiquetas de sliver aparecen como HTML sin procesar** — Esto indica una compilación anterior sin la corrección de texto enriquecido. Actualice a v26.5.2.1 o posterior para asegurar que las letras de sliver renderizadas en HTML se muestren correctamente (#2606).
- **El texto del estado del servidor aparece en el color incorrecto** — Esto indica un problema de compatibilidad con el tema. Actualice a v26.6.1 o posterior para obtener el soporte de tema adecuado (#3065). La etiqueta de estado del servidor ahora usa el color del tema `color.background.3` en lugar de un color fijo.

## Relacionados

- [Descripción general del Servidor TCI](overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
