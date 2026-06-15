# Inicio automático de TCI al arrancar

Configure AetherSDR para que inicie el servidor WebSocket de TCI automáticamente cada vez que la aplicación se ejecute, para que software de terceros como Log4OM o herramientas SunSDR se conecten sin intervención manual.

## Antes de empezar

- AetherSDR debe estar compilado con soporte para WebSocket (`HAVE_WEBSOCKETS`). Si el botón de la bandeja de TCI está ausente, esta compilación no incluye TCI.
- La radio debe estar conectada antes de que el servidor TCI pueda atender clientes, aunque la configuración de inicio automático puede ajustarse mientras está desconectado.
- Decida qué puerto debe usar el servidor. El valor predeterminado es `50001`. Consulte [Cambiar el puerto TCI](change-the-tci-port.md) si necesita un puerto diferente antes de habilitar el inicio automático.

## Pasos

1. Haga clic en `Settings > Autostart TCI with AetherSDR`.
2. Confirme que el elemento esté marcado. AetherSDR iniciará ahora el servidor TCI en cada ejecución posterior.
3. Para verificar que la configuración surta efecto de inmediato, haga clic en el botón de la bandeja de TCI en la barra lateral derecha para abrir el applet del Servidor TCI. El estado del servidor debería mostrar `:<puerto> (0 clientes)` en lugar de `(detenido)`.

Para deshabilitar el inicio automático, haga clic nuevamente en `Settings > Autostart TCI with AetherSDR` para desmarcarlo.

## Qué hace cada control

| Control                                                         | Valor predeterminado                                                                                                        | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|-----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Settings > Autostart TCI with AetherSDR` (elemento de menú marcable) | Desactivado                                                                                                                     | Activado / Desactivado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Puerto                                                            | `50001`                                                                                                                     | 1024–65535                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Habilitar (botón de alternancia en el applet del Servidor TCI)                     | Desactivado                                                                                                                         | Activado / Desactivado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Ganancia+medidor RX1–RX4                                              | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor TX                                                   | Los arrastres establecen la ganancia TX de TCI y emiten tciTxGainChanged. El clic derecho abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure). | TciServer::setTxGain persiste TciTxGain internamente; la IU refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú contextual permite a los usuarios elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes en modo digital: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo pone a cero NaN/Inf), o Measure (paso directo verdadero con conteo de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Modo de desbordamiento TX (clic derecho)                                  | Clip                                                                                                                        | 0 (Clip), 1 (NaNGuard), 2 (Measure)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Etiquetas de asignación de slice RX/TX                                              | — (guión largo)                                                                                                                 | — o letra del slice                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Indicador de estado del servidor                                         | (detenido)                                                                                                                   | `(detenido)`, `:<puerto> (N clientes)`, `(puerto en uso)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

## Nombres de accesibilidad para los deslizadores de ganancia

Cada deslizador de ganancia de TCI ahora tiene un nombre de accesibilidad para admitir lectores de pantalla y tecnologías de asistencia:

- **Deslizadores de ganancia RX1–RX4**: Nombrados "TCI RX 1 gain" hasta "TCI RX 4 gain" respectivamente.
- **Deslizador de ganancia TX**: Nombrado "TCI TX gain".

Estos nombres se establecen automáticamente y no requieren configuración por parte del usuario.

## Etiquetas de asignación de slice RX/TX

Las etiquetas de estado RX1–RX4 y TX muestran qué slice impulsa actualmente cada canal. La letra del slice ahora se renderiza como texto enriquecido (HTML) para que los identificadores de slice estilizados de `SliceLabel::richText` se muestren correctamente. Las etiquetas se actualizan automáticamente cuando cambian las asignaciones de slice.

## Modo de desbordamiento TX

Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual con tres modos de manejo de desbordamiento:

| Modo | Valor | Descripción |
|------|-------|-------------|
| Clip (saturación ±1.0) | 0 | Recorte forzado de excesos a ±1.0. Valor predeterminado defensivo; introduce armónicos en excesos pero protege la conversión posterior a int16. |
| NaN guard (solo poner a cero NaN/Inf) | 1 | Pasa las muestras exactamente como son; solo pone a cero valores patológicos NaN/Inf. Preserva la fidelidad del tono en modo digital; los flotantes fuera de rango llegan a la radio. |
| Measure only (paso directo verdadero) | 2 | Nunca modifica las muestras. Cuenta los excesos para telemetría; la conversión posterior a int16 aún recorta en la ruta DAX nativa de la radio. |

El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). La configuración se persiste en `TciTxOverflowMode` (0/1/2).

## Consejos

- Habilitar el inicio automático también establece `AutoStartTCI` en `True`. Alternar Habilitar en el applet del Servidor TCI escribe la misma clave, por lo que ambos controles permanecen sincronizados.
- Si el puerto ya está en uso al iniciar, el servidor no se iniciará: el botón de alternancia Habilitar vuelve a la posición desactivada y el estado muestra `(puerto en uso)`. Cambie el puerto y reinicie AetherSDR, o detenga el proceso conflictivo.
- Los valores de puerto fuera de rango vuelven automáticamente a `50001`.

## Solución de problemas

- **`Settings > Autostart TCI with AetherSDR` no aparece en el menú** — Esta compilación de AetherSDR no incluye soporte para WebSocket. TCI no está disponible.
- **El estado del servidor muestra `(puerto en uso)` después del inicio** — Otro proceso ya está vinculado al puerto configurado. Cambie el puerto en el campo Puerto del applet del Servidor TCI, guarde y reinicie AetherSDR. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El estado permanece `(detenido)` a pesar de tener el inicio automático habilitado** — La radio aún no está conectada. El servidor TCI requiere una conexión de radio. Conéctese a la radio; el servidor se iniciará una vez que se establezca la conexión.
- **Las etiquetas de slice aparecen como HTML sin procesar** — Esto indica una compilación anterior sin la corrección de texto enriquecido. Actualice a v26.5.2.1 o posterior para asegurarse de que las letras de slice renderizadas en HTML se muestren correctamente (#2606).
- **El texto del estado del servidor aparece en el color incorrecto** — Esto indica un problema de compatibilidad con el tema. Actualice a v26.6.1 o posterior para obtener soporte de tema adecuado (#3065). La etiqueta de estado del servidor ahora usa el color del tema `color.background.3` en lugar de un color codificado.

## Relacionado

- [Descripción general del Servidor TCI](overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
