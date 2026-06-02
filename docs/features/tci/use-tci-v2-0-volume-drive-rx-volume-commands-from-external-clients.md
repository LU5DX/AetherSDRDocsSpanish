# Uso de los comandos volume/drive/rx_volume de TCI v2.0 desde clientes externos

Los clientes externos (software de registro, software de modos digitales, programas SDR) pueden controlar AetherSDR mediante los comandos `volume`, `drive` y `rx_volume` de TCI v2.0 cuando el servidor TCI está habilitado y la radio está conectada.

## Antes de comenzar

- Habilite el servidor TCI (haga clic en el botón de la bandeja TCI en la barra lateral derecha y luego haga clic en Enable).
- Conéctese a una radio.
- Configure su cliente externo para conectarse al servidor TCI de AetherSDR en el puerto que se muestra en el applet TCI (predeterminado: 50001).

## Pasos

1. En el applet TCI, anote el número de puerto o cámbielo editando el campo de texto y presionando Enter. Rango válido: 1024–65535.
2. Configure su cliente externo para conectarse a la dirección IP de AetherSDR y a ese puerto.
3. Envíe comandos TCI v2.0 desde su cliente:

   - **`volume`** — Establece el volumen RX maestro. AetherSDR asigna esto a la ganancia RX del slice activo actualmente.
   - **`drive`** — Establece el nivel de drive TX. AetherSDR asigna esto a `TciTxGain`.
   - **`rx_volume <canal>`** — Establece la ganancia RX para un canal DAX específico (1–4). AetherSDR asigna esto a `TciRxGain1` a `TciRxGain4`.

4. El servidor TCI recibe estos comandos y actualiza las configuraciones de ganancia correspondientes. Los cambios se reflejan en los controles de medidor/deslizador del applet TCI y se persisten en la configuración.

## Qué hace cada control

| Comando                       | Configuración asignada                                                                                                               | Predeterminado                                                                                                                                                                                                                               |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `volume`                      | Ganancia RX del slice activo                                                                                                         | 0.5                                                                                                                                                                                                                                          |
| `drive`                       | `TciTxGain`                                                                                                                          | 0.5                                                                                                                                                                                                                                          |
| `rx_voice <canal>`            | `TciRxGain1`–`TciRxGain4`                                                                                                            | 0.5                                                                                                                                                                                                                                          |
| Modo de desbordamiento TX (clic derecho) | Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite tciTxOverflowModeChanged. | Nuevo en v26.5.3. Clip limita los picos a ±1.0 con distorsión armónica; NaNGuard preserva los tonos digitales bit a bit solo poniendo a cero NaN/Inf; Measure cuenta los picos para telemetría sin mutación. Persistido como TciTxOverflowMode (0/1/2). |

## Controles del applet TCI

El applet TCI muestra el estado actual y permite ajustar las configuraciones de ganancia:

| Control | Descripción | Clave de configuración |
|---------|-------------|------------------------|
| **Ganancia+medidor RX1** a **Ganancia+medidor RX4** | Medidor/deslizador combinado para cada canal DAX. Arrastre para establecer la ganancia RX de TCI. Emite `tciRxGainChanged`. | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| **Ganancia+medidor TX** | Medidor/deslizador combinado para ganancia TX. Arrastre para establecer la ganancia TX de TCI. Emite `tciTxGainChanged`. Haga clic derecho para abrir el selector de modo de desbordamiento TX. | `TciTxGain` |
| **Puerto** | Campo de texto para el puerto del servidor WebSocket. Cámbielo y presione Enter. Los valores fuera de rango se ajustan a 50001. | `TciPort` |
| **Habilitar** | Botón de alternancia para iniciar o detener el servidor TCI. Si la vinculación falla, vuelve a apagado y el estado muestra "(puerto en uso)". | None |

### Modo de desbordamiento TX (clic derecho)

Haga clic derecho en el control **Ganancia+medidor TX** para abrir un menú contextual que selecciona cómo se manejan las muestras fuera de rango (>1.0) de los clientes TCI antes de llegar a la radio. Emite `tciTxOverflowModeChanged`. El modo seleccionado se persiste como `TciTxOverflowMode` (0/1/2).

| Modo | Valor | Descripción |
|------|-------|-------------|
| Clip (saturación ±1.0) | 0 | Limita los picos a ±1.0. Predeterminado defensivo; introduce armónicos en picos pero protege la conversión posterior a int16. |
| NaN guard (solo pone a cero NaN/Inf) | 1 | Pasa las muestras bit a bit; solo pone a cero valores NaN/Inf patológicos. Preserva la fidelidad de tonos en modos digitales; los flotantes fuera de rango llegan a la radio. |
| Measure only (bypass verdadero) | 2 | Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión posterior a int16 aún limita en la ruta DAX nativa de la radio. |

El valor predeterminado es **Clip** para que los usuarios existentes no vean cambio de comportamiento.

### Etiquetas de asignación de slices RX/TX

| Etiqueta | Descripción | Formato |
|----------|-------------|---------|
| **Estado RX1..RX4** | Muestra qué slice impulsa cada canal DAX de RX. Se muestra como "Slice <letra>" donde la letra puede aparecer como texto HTML enriquecido (ej., con tachado para slices deshabilitados). | `—` o etiqueta de slice HTML enriquecido |
| **Estado TX** | Muestra qué slice es el slice TX activo. Se muestra como "Slice <letra>" con el mismo formato HTML enriquecido que las etiquetas RX. | `—` o etiqueta de slice HTML enriquecido |

### Indicador de estado del servidor

| Estado | Significado |
|--------|-------------|
| `(detenido)` | El servidor no está en ejecución |
| `:<puerto> (N clientes)` | El servidor está en ejecución en el puerto especificado con N clientes conectados |
| `(puerto en uso)` | La vinculación falló — el puerto ya está en uso por otra aplicación |

## Consejos

- El servidor TCI admite sincronización de estado bidireccional: los cambios realizados localmente mediante los deslizadores del applet TCI también se envían a los clientes externos que se suscriben a las actualizaciones de ganancia.
- El comando `rx_volume` acepta un número de canal (1–4). Los números de canal corresponden a los canales DAX mostrados en las filas RX1–RX4 del applet TCI.
- El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (v0.9.5.1, #2276).
- Las etiquetas de asignación de slices ahora usan formato HTML enriquecido (v26.5.2.1, #2606), por lo que los slices deshabilitados o de estado especial pueden mostrarse con formato de texto (ej., tachado).
- Para la fidelidad de tonos bit a bit en modos digitales, use el modo **NaN guard** o **Measure only** para evitar la distorsión armónica del limitador Clip.
- El contenedor del applet TCI ahora usa estilo temático (v26.6.1) — los colores se adaptan al tema activo.

## Relacionado

- [Enable the TCI server for Log4OM / SunSDR clients](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Change the TCI port](change-the-tci-port.md)
- [Adjust TCI RX gain per channel](adjust-tci-rx-gain-per-channel.md)
- [Adjust TCI TX gain](adjust-tci-tx-gain.md)
