# Inicio automático de TCI al iniciar

Configure AetherSDR para que inicie el servidor WebSocket TCI automáticamente cada vez que se lance la aplicación, de modo que software de terceros como Log4OM o herramientas SunSDR se conecten sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón de la bandeja TCI no está presente, esta compilación no incluye TCI.
- La radio debe estar conectada antes de que el servidor TCI pueda atender clientes, aunque la configuración de inicio automático puede ajustarse mientras está desconectado.
- Decida qué puerto debe usar el servidor. El valor predeterminado es `50001`. Consulte [Cambiar el puerto TCI](change-the-tci-port.md) si necesita un puerto diferente antes de habilitar el inicio automático.

## Pasos

1. Haga clic en `Settings > Autostart TCI with AetherSDR`.
2. Confirme que el elemento esté marcado. AetherSDR iniciará ahora el servidor TCI en cada lanzamiento posterior.
3. Para verificar que la configuración surta efecto de inmediato, haga clic en el botón de la bandeja TCI en la barra lateral derecha para abrir el applet del Servidor TCI. El estado del servidor debería mostrar `:<puerto> (0 clientes)` en lugar de `(detenido)`.

Para deshabilitar el inicio automático, haga clic en `Settings > Autostart TCI with AetherSDR` nuevamente para desmarcarlo.

## Qué hace cada control

| Control                                                         | Predeterminado | Rango válido | Descripción |
|-----------------------------------------------------------------|---------------|--------------|-------------|
| `Settings > Autostart TCI with AetherSDR` (elemento de menú marcable) | Desactivado   | Activado / Desactivado | Inicia el servidor TCI automáticamente en cada lanzamiento. |
| Puerto                                                          | `50001`       | 1024–65535   | El puerto TCP en el que escucha el servidor TCI. Cambiarlo reinicia el servidor si está habilitado. |
| Habilitar (botón de alternancia en el applet Servidor TCI)      | Desactivado   | Activado / Desactivado | Inicia o detiene el servidor TCI. Si falla la vinculación, vuelve a desactivado y el estado muestra `(puerto en uso)`. |
| Ganancia+medidor RX1–RX4                                        | 0.5           | 0.0–1.0      | Medidor/deslizador combinado; arrastre para establecer la ganancia RX TCI para el canal. Un ajuste por canal (`TciRxGain1`–`TciRxGain4`). |
| Ganancia+medidor TX                                             | 0.5           | 0.0–1.0      | Arrastre para establecer la ganancia TX TCI. Haga clic derecho para abrir el selector de modo de desbordamiento TX. |
| Modo de desbordamiento TX (clic derecho)                        | Recortar      | 0 (Recortar), 1 (Proteger NaN), 2 (Medir) | Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual que selecciona cómo se manejan las muestras fuera de rango (>1.0) de clientes de modo digital. Se guarda como `TciTxOverflowMode`. |
| Etiquetas de asignación de segmento RX/TX                       | — (guión)     | — o letra de segmento | Muestra qué segmento controla actualmente cada fila RX/TX. Se actualiza automáticamente. |
| Indicador de estado del servidor                                | (detenido)    | `(detenido)`, `:<puerto> (N clientes)`, `(puerto en uso)` | Indica el estado del servidor y el número de clientes conectados. El color cambia a rojo en caso de error de vinculación. |

## Etiquetas de asignación de segmento RX/TX

Las etiquetas de estado RX1–RX4 y TX muestran qué segmento controla actualmente cada canal. La letra del segmento ahora se representa como texto enriquecido (HTML) para que los identificadores de segmento con estilo de `SliceLabel::richText` se muestren correctamente. Las etiquetas se actualizan automáticamente cuando cambian las asignaciones de segmento.

## Modo de desbordamiento TX

Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual con tres modos de manejo de desbordamiento:

| Modo | Valor | Descripción |
|------|-------|-------------|
| Recortar (saturación ±1.0) | 0 | Limita forzosamente los excesos a ±1.0. Valor predeterminado defensivo; introduce armónicos en excesos pero protege la conversión a int16. |
| Proteger NaN (solo cero para NaN/Inf) | 1 | Pasa las muestras bit a bit exactas; solo pone a cero valores patológicos NaN/Inf. Preserva la fidelidad del tono en modo digital; los flotantes fuera de rango llegan a la radio. |
| Solo medir (bypass real) | 2 | Nunca modifica las muestras. Cuenta los excesos para telemetría; la conversión a int16 aún recorta en la ruta DAX nativa de la radio. |

El valor predeterminado es Recortar para que los usuarios existentes no vean cambios de comportamiento (#3065). La configuración se guarda en `TciTxOverflowMode` (0/1/2).

## Consejos

- Habilitar el inicio automático también establece `AutoStartTCI` en `True`. Alternar Habilitar en el applet Servidor TCI escribe la misma clave, por lo que ambos controles se mantienen sincronizados.
- Si el puerto ya está en uso al iniciar, el servidor no se iniciará: el botón de alternancia Habilitar vuelve a desactivado y el estado muestra `(puerto en uso)`. Cambie el puerto y reinicie AetherSDR, o elimine el proceso conflictivo.
- Los valores de puerto fuera de rango vuelven automáticamente a `50001`.

## Solución de problemas

- **`Settings > Autostart TCI with AetherSDR` no aparece en el menú** — Esta compilación de AetherSDR no incluye soporte WebSocket. TCI no está disponible.
- **El estado del servidor muestra `(puerto en uso)` después del inicio** — Otro proceso ya está vinculado al puerto configurado. Cambie el puerto en el campo Puerto del applet Servidor TCI, guarde y reinicie AetherSDR. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El estado permanece en `(detenido)` a pesar de tener el inicio automático habilitado** — La radio aún no está conectada. El servidor TCI requiere una conexión de radio. Conéctese a la radio; el servidor se iniciará una vez establecida la conexión.
- **Las etiquetas de segmento aparecen como HTML sin procesar** — Esto indica una compilación anterior sin la corrección de texto enriquecido. Actualice a v26.5.2.1 o posterior para garantizar que las letras de segmento renderizadas en HTML se muestren correctamente (#2606).

## Relacionados

- [Descripción general del Servidor TCI](overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX TCI](adjust-tci-tx-gain.md)
