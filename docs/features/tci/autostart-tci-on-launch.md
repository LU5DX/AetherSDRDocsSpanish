# Inicio automático de TCI al arrancar

Configure AetherSDR para que inicie el servidor WebSocket de TCI automáticamente cada vez que la aplicación se lance, de modo que software de terceros como Log4OM o herramientas SunSDR se conecten sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón de bandeja de TCI no está presente, esta compilación no incluye TCI.
- La radio debe estar conectada antes de que el servidor TCI pueda atender clientes, aunque la configuración de inicio automático puede ajustarse estando desconectado.
- Decida qué puerto debe usar el servidor. El valor predeterminado es `50001`. Consulte [Cambiar el puerto TCI](change-the-tci-port.md) si necesita un puerto distinto antes de habilitar el inicio automático.

## Pasos

1. Haga clic en `Settings > Autostart TCI with AetherSDR`.
2. Confirme que el elemento esté marcado. AetherSDR iniciará el servidor TCI en cada lanzamiento posterior.
3. Para verificar que la configuración surtió efecto de inmediato, haga clic en el botón de bandeja de TCI en la barra lateral derecha para abrir el applet TCI Server. El estado del servidor debería indicar `:<port> (0 clients)` en lugar de `(stopped)`.

Para deshabilitar el inicio automático, haga clic en `Settings > Autostart TCI with AetherSDR` nuevamente para desmarcarlo.

## Qué hace cada control

| Control                                                         | Valor predeterminado                                                                                                     | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|-----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Settings > Autostart TCI with AetherSDR` (elemento de menú marcable) | Desactivado                                                                                                                 | Activado / Desactivado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Puerto                                                            | `50001`                                                                                                                     | 1024–65535                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Habilitar (botón de alternancia en el applet TCI Server)                     | Desactivado                                                                                                                         | Activado / Desactivado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Ganancia+medidor RX1–RX8                                              | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor TX                                                   | Los arrastres establecen la ganancia TX de TCI y emiten tciTxGainChanged. El clic derecho abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure). | TciServer::setTxGain persiste TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o de la disponibilidad de DAX hospedado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú de clic derecho permite a los usuarios elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes en modo digital: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo anula NaN/Inf) o Measure (derivación real con conteo de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Modo de desbordamiento TX (clic derecho)                                  | Clip                                                                                                                        | 0 (Clip), 1 (NaNGuard), 2 (Measure)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Etiquetas de asignación de slice RX/TX                              | — (guion largo)                                                                                                                 | — o letra de slice                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Indicador de estado del servidor                                         | (stopped)                                                                                                                   | `(stopped)`, `:<port> (N clients)`, `(port in use)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

## Filas de canales RX y capacidad de slices de la radio

El applet TCI Server muestra hasta ocho filas de canales RX (RX1–RX8), cada una con un control deslizante de ganancia, medidor de nivel y etiqueta de asignación de slice. El número de filas visibles se limita automáticamente a la capacidad de slices de la radio conectada:

- En radios con menos de ocho slices (por ejemplo, una FLEX-6600 con cuatro slices), las filas por encima de la capacidad de slices quedan ocultas.
- Las filas ocultas no se destruyen; simplemente son invisibles. La asignación de canales subyacente permanece y las filas reaparecen automáticamente si la radio informa una mayor capacidad de slices.
- La configuración del control deslizante de ganancia RX de las filas ocultas se conserva y permanece aplicada.

Este comportamiento refleja el del applet DAX y garantiza que la interfaz visible para el operador coincida con lo que la radio puede realmente entregar.

## Etiquetas de asignación de slice RX/TX

Las etiquetas de estado RX1–RX8 y TX muestran qué slice impulsa actualmente cada canal. La letra del slice ahora se representa como texto enriquecido (HTML) para que los identificadores de slice con estilo de `SliceLabel::richText` se muestren correctamente. Las etiquetas se actualizan automáticamente cuando cambian las asignaciones de slices.

Los canales RX 1–8 de TCI transportan los mismos canales DAX que el applet DAX; el índice de receptor TCI es un índice de slice posicional limitado por el número de slices (hasta 8), y el audio del servidor TCI y el control de ganancia ya abarcan los canales 1–8.

## Modo de desbordamiento TX

Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir un menú contextual con tres modos de manejo de desbordamiento:

| Modo | Valor | Descripción |
|------|-------|-------------|
| Clip (saturación ±1.0) | 0 | Limita firmemente los excesos a ±1.0. Predeterminado defensivo; introduce armónicos en el exceso pero protege la conversión posterior a int16. |
| Protección NaN (solo anula NaN/Inf) | 1 | Pasa las muestras de forma bit-exacta; solo anula valores patológicos NaN/Inf. Preserva la fidelidad del tono en modos digitales; los flotantes fuera de rango llegan a la radio. |
| Solo medición (derivación real) | 2 | Nunca modifica las muestras. Cuenta los excesos para telemetría; la conversión posterior a int16 aún limita en la ruta DAX nativa de la radio. |

El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). La configuración se persiste en `TciTxOverflowMode` (0/1/2).

## Nombres de accesibilidad para controles deslizantes de ganancia

Cada control deslizante de ganancia TCI ahora tiene un nombre de accesibilidad para soportar lectores de pantalla y tecnologías de asistencia:

- **Controles deslizantes de ganancia RX1–RX8**: nombrados "TCI RX 1 gain" hasta "TCI RX 8 gain" respectivamente.
- **Control deslizante de ganancia TX**: nombrado "TCI TX gain".

Estos nombres se establecen automáticamente y no requieren configuración del usuario.

## Anotaciones de accesibilidad para controles TCI

Los controles del applet TCI Server ahora tienen nombres y descripciones de accesibilidad explícitos para soportar lectores de pantalla y tecnologías de asistencia:

- **Campo de puerto TCI**: Nombre accesible "TCI port", descripción "TCP port the TCI server listens on".
- **Botón de habilitación del servidor TCI**: Nombre accesible "TCI server enable", descripción "Start or stop the TCI server".

Estas anotaciones se establecen mediante los métodos `setAccessibleName` y `setAccessibleDescription` y no requieren configuración del usuario. El ancho del botón es de 76 píxeles para acomodar las etiquetas de texto "Enabled" y "Disabled".

## Estado del texto del botón de habilitación

El botón de alternancia Enable muestra "Enabled" cuando el servidor está en ejecución y "Disabled" cuando está detenido. El texto se actualiza dinámicamente al alternar el botón manualmente o cuando el inicio automático activa el servidor al lanzar. Esto hace que el estado del servidor sea visible incluso para usuarios con deficiencias en la visión del color.

## Consejos

- Habilitar el inicio automático también establece `AutoStartTCI` en `True`. Alternar Enable en el applet TCI Server escribe la misma clave, por lo que ambos controles permanecen sincronizados.
- Si el puerto ya está en uso al iniciar, el servidor no arrancará: la alternancia Enable vuelve a apagada y el estado muestra `(port in use)`. Cambie el puerto y reinicie AetherSDR, o cierre el proceso en conflicto.
- Los valores de puerto fuera de rango vuelven automáticamente a `50001`.

## Solución de problemas

- **`Settings > Autostart TCI with AetherSDR` no aparece en el menú** — Esta compilación de AetherSDR no incluye soporte WebSocket. TCI no está disponible.
- **El estado del servidor muestra `(port in use)` después del inicio** — Otro proceso ya está vinculado al puerto configurado. Cambie el puerto en el campo Port del applet TCI Server, guarde y reinicie AetherSDR. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El estado permanece en `(stopped)` a pesar de que el inicio automático está habilitado** — La radio aún no está conectada. El servidor TCI requiere una conexión de radio. Conéctese a la radio; el servidor arrancará una vez que se establezca la conexión.
- **Se ven menos de ocho filas RX** — La radio conectada tiene una capacidad de slices inferior a ocho (por ejemplo, una FLEX-6600 tiene cuatro slices). Las filas por encima de la capacidad de slices quedan ocultas para coincidir con las capacidades de la radio. Este es el comportamiento esperado.
- **Las etiquetas de slice aparecen como HTML sin procesar** — Esto indica una compilación anterior sin la corrección de texto enriquecido. Actualice a v26.5.2.1 o posterior para garantizar que las letras de slice renderizadas en HTML se muestren correctamente (#2606).
- **El texto del estado del servidor aparece con el color incorrecto** — Esto indica un problema de compatibilidad de temas. Actualice a v26.6.1 o posterior para obtener soporte de temas adecuado (#3065). La etiqueta de estado del servidor ahora usa el color del tema `color.background.3` en lugar de un color codificado.

## Relacionado

- [Descripción general del servidor TCI](overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
