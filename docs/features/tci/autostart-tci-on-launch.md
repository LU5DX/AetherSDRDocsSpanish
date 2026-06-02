# Inicio automático de TCI al iniciar

Configure AetherSDR para que inicie el servidor WebSocket TCI automáticamente cada vez que se inicie la aplicación, de modo que software de terceros como Log4OM o herramientas SunSDR se conecten sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón de la bandeja TCI no aparece, esta compilación no incluye TCI.
- La radio debe estar conectada antes de que el servidor TCI pueda atender clientes, aunque la configuración de inicio automático puede ajustarse mientras está desconectada.
- Decida qué puerto debe usar el servidor. El valor predeterminado es `50001`. Consulte [Cambiar el puerto TCI](change-the-tci-port.md) si necesita un puerto diferente antes de habilitar el inicio automático.

## Pasos

1. Haga clic en `Settings > Autostart TCI with AetherSDR`.
2. Confirme que el elemento esté marcado. AetherSDR iniciará el servidor TCI en cada inicio posterior.
3. Para verificar que la configuración haya surtido efecto de inmediato, haga clic en el botón de la bandeja TCI en la barra lateral derecha para abrir el applet del servidor TCI. El estado del servidor debe mostrar `:<puerto> (0 clients)` en lugar de `(stopped)`.

Para deshabilitar el inicio automático, haga clic en `Settings > Autostart TCI with AetherSDR` nuevamente para desmarcarlo.

## Qué hace cada control

| Control                                                         | Valor predeterminado                                                                                                                     | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|-----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Settings > Autostart TCI with AetherSDR` (elemento de menú marcable) | Desactivado                                                                                                                         | Activado / Desactivado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Puerto                                                            | `50001`                                                                                                                     | 1024–65535                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Habilitar (botón de alternancia en el applet del servidor TCI)                     | Desactivado                                                                                                                         | Activado / Desactivado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Ganancia+medidor RX1–RX4                                              | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor TX                                                   | Los arrastres establecen la ganancia TX de TCI y emiten tciTxGainChanged. Al hacer clic derecho se abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure). | TciServer::setTxGain conserva internamente TciTxGain; la interfaz de usuario refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú contextual permite a los usuarios elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes en modo digital: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo cero NaN/Inf), o Measure (paso directo verdadero con conteo de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Modo de desbordamiento TX (clic derecho)                                  | Clip                                                                                                                        | 0 (Clip), 1 (NaNGuard), 2 (Measure)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Etiquetas de asignación de segmentos RX/TX                                  | — (guión largo)                                                                                                                 | — o letra de segmento                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Indicador de estado del servidor                                         | (stopped)                                                                                                                   | `(stopped)`, `:<puerto> (N clients)`, `(puerto en uso)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

## Etiquetas de asignación de segmentos RX/TX

Las etiquetas de estado RX1–RX4 y TX muestran qué segmento impulsa cada canal actualmente. La letra del segmento ahora se muestra como texto enriquecido (HTML) para que los identificadores de segmento con estilo de `SliceLabel::richText` se muestren correctamente. Las etiquetas se actualizan automáticamente cuando cambian las asignaciones de segmentos.

## Modo de desbordamiento TX

Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir un menú contextual con tres modos de manejo de desbordamiento:

| Modo | Valor | Descripción |
|------|-------|-------------|
| Clip (saturación ±1.0) | 0 | Recorta forzosamente los picos a ±1.0. Valor defensivo predeterminado; introduce armónicos en los picos pero protege la conversión int16 posterior. |
| NaN guard (solo cero NaN/Inf) | 1 | Pasa las muestras sin cambios bit a bit; solo pone a cero los valores NaN/Inf patológicos. Conserva la fidelidad del tono en modo digital; los flotantes fuera de rango llegan a la radio. |
| Measure only (paso directo verdadero) | 2 | Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión int16 posterior aún recorta en la ruta DAX nativa de la radio. |

El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). La configuración se conserva en `TciTxOverflowMode` (0/1/2).

## Consejos

- Habilitar el inicio automático también establece `AutoStartTCI` en `True`. Alternar Habilitar en el applet del servidor TCI escribe la misma clave, por lo que ambos controles se mantienen sincronizados.
- Si el puerto ya está en uso al iniciar, el servidor no se iniciará: la alternancia de Habilitar vuelve a desactivarse y el estado muestra `(puerto en uso)`. Cambie el puerto y reinicie AetherSDR, o elimine el proceso en conflicto.
- Los valores de puerto fuera de rango vuelven automáticamente a `50001`.

## Solución de problemas

- **`Settings > Autostart TCI with AetherSDR` no aparece en el menú** — Esta compilación de AetherSDR no incluye soporte WebSocket. TCI no está disponible.
- **El estado del servidor muestra `(puerto en uso)` después del inicio** — Otro proceso ya está vinculado al puerto configurado. Cambie el puerto en el campo Puerto del applet del servidor TCI, guarde y reinicie AetherSDR. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El estado permanece en `(stopped)` a pesar de que el inicio automático está habilitado** — La radio aún no está conectada. El servidor TCI requiere una conexión de radio. Conéctese a la radio; el servidor se iniciará una vez que se establezca la conexión.
- **Las etiquetas de segmento aparecen como HTML sin procesar** — Esto indica una compilación anterior sin la corrección de texto enriquecido. Actualice a v26.5.2.1 o posterior para asegurarse de que las letras de segmento renderizadas en HTML se muestren correctamente (#2606).
- **El texto del estado del servidor aparece en un color incorrecto** — Esto indica un problema de compatibilidad de temas. Actualice a v26.6.1 o posterior para obtener soporte de temas adecuado (#3065). La etiqueta de estado del servidor ahora usa el color del tema `color.background.3` en lugar de un color fijo.

## Relacionado

- [Resumen del servidor TCI](overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
