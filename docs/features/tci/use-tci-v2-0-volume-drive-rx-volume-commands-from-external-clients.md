# Uso de comandos TCI v2.0 de volumen/ganancia de transmisión/volumen de recepción desde clientes externos

Los clientes externos (software de registro, software de modo digital, programas SDR) pueden controlar AetherSDR utilizando los comandos TCI v2.0 `volume`, `drive` y `rx_volume` cuando el servidor TCI está habilitado y la radio está conectada.

## Antes de comenzar

- Habilite el servidor TCI (haga clic en el botón de la bandeja TCI en la barra lateral derecha y luego haga clic en Habilitar).
- Conéctese a una radio.
- Configure su cliente externo para conectarse al servidor TCI de AetherSDR en el puerto que se muestra en el applet TCI (predeterminado: 50001).

## Pasos

1. En el applet TCI, anote el número de Puerto o cámbielo editando el campo de texto y presionando Enter. Rango válido: 1024–65535.
2. Configure su cliente externo para conectarse a la dirección IP de AetherSDR y a ese puerto.
3. Envíe comandos TCI v2.0 desde su cliente:

   - **`volume`** — Establece el volumen de recepción maestro. AetherSDR asigna esto a la ganancia de RX para el slice activo actualmente.
   - **`drive`** — Establece el nivel de ganancia de transmisión. AetherSDR asigna esto a `TciTxGain`.
   - **`rx_volume <canal>`** — Establece la ganancia de RX para un canal DAX específico (1–4). AetherSDR asigna esto a `TciRxGain1` hasta `TciRxGain4`.

4. El servidor TCI recibe estos comandos y actualiza las configuraciones de ganancia correspondientes. Los cambios se reflejan en los controles de medidor/deslizador del applet TCI y se guardan en la configuración.

## Qué hace cada control

| Comando                        | Configuración asignada                                                                                                                | Valor predeterminado                                                                                                                                                                                                                          |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `volume`                       | Ganancia de RX del slice activo                                                                                                       | 0.5                                                                                                                                                                                                                                           |
| `drive`                        | `TciTxGain`                                                                                                                           | 0.5                                                                                                                                                                                                                                           |
| `rx_volume <canal>`            | `TciRxGain1`–`TciRxGain4`                                                                                                            | 0.5                                                                                                                                                                                                                                           |
| Modo de desbordamiento de TX (clic derecho) | Haga clic derecho en el medidor/deslizador de ganancia de TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento de TX. Emite tciTxOverflowModeChanged. | Nuevo en v26.5.3. Clip recorta los picos a ±1.0 con distorsión armónica; NaNGuard preserva los tonos digitales bit exactos solo poniendo a cero NaN/Inf; Measure cuenta los picos para telemetría sin mutación. Se guarda como TciTxOverflowMode (0/1/2). |

## Controles del applet TCI

El applet TCI muestra el estado actual y permite ajustar las configuraciones de ganancia:

| Control | Descripción | Clave de configuración |
|---------|-------------|------------------------|
| **Ganancia+medidor RX1** hasta **Ganancia+medidor RX4** | Medidor/deslizador combinado para cada canal DAX. Arrastre para establecer la ganancia de RX de TCI. Emite `tciRxGainChanged`. Cada control tiene un nombre accesible "TCI RX _N_ gain" para lectores de pantalla. | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| **Ganancia+medidor TX** | Medidor/deslizador combinado para la ganancia de TX. Arrastre para establecer la ganancia de TX de TCI. Emite `tciTxGainChanged`. Haga clic derecho para abrir el selector de modo de desbordamiento de TX. Tiene nombre accesible "TCI TX gain" para lectores de pantalla. | `TciTxGain` |
| **Puerto** | Campo de texto para el puerto del servidor WebSocket. Cámbielo y presione Enter. Los valores fuera de rango se ajustan a 50001. Tiene nombre accesible "TCI port". | `TciPort` |
| **Habilitar** | Botón de alternancia para iniciar o detener el servidor TCI. El texto muestra "Enabled" cuando el servidor está en ejecución o se iniciará automáticamente, y "Disabled" en caso contrario. Si falla la vinculación, vuelve a apagado, el texto cambia a "Disabled" y el estado muestra "(port in use)". | None |

### Modo de desbordamiento de TX (clic derecho)

Haga clic derecho en el control **Ganancia+medidor TX** para abrir un menú contextual para seleccionar cómo se manejan las muestras fuera de rango (>1.0) de los clientes TCI antes de llegar a la radio. Emite `tciTxOverflowModeChanged`. El modo seleccionado se guarda como `TciTxOverflowMode` (0/1/2).

| Modo | Valor | Descripción |
|------|-------|-------------|
| Clip (saturación ±1.0) | 0 | Recorte forzado de picos a ±1.0. Valor defensivo predeterminado; introduce armónicos en caso de pico pero protege la conversión a int16 aguas abajo. |
| NaN guard (poner a cero solo NaN/Inf) | 1 | Pasa las muestras bit exactas; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad del tono de modo digital; los flotantes fuera de rango llegan a la radio. |
| Measure only (bypass verdadero) | 2 | Nunca muta las muestras. Cuenta los picos para telemetría; la conversión a int16 aguas abajo aún recorta en la ruta DAX nativa de la radio. |

El valor predeterminado es **Clip** para que los usuarios existentes no vean cambios de comportamiento.

### Etiquetas de asignación de slices RX/TX

| Etiqueta | Descripción | Formato |
|----------|-------------|---------|
| **Estado RX1..RX4** | Muestra qué slice impulsa cada canal DAX de RX. Se muestra como "Slice <letra>" donde la letra puede aparecer como texto HTML enriquecido (p. ej., con tachado para slices deshabilitados). | `—` o etiqueta de slice HTML enriquecido |
| **Estado TX** | Muestra qué slice es el slice TX activo. Se muestra como "Slice <letra>" con el mismo formato HTML enriquecido que las etiquetas RX. | `—` o etiqueta de slice HTML enriquecido |

### Indicador de estado del servidor

| Estado | Significado |
|--------|-------------|
| `(detenido)` | El servidor no está en ejecución |
| `:<puerto> (N clientes)` | El servidor se está ejecutando en el puerto especificado con N clientes conectados |
| `(puerto en uso)` | Falló la vinculación — el puerto ya está en uso por otra aplicación |

## Consejos

- El servidor TCI admite sincronización de estado bidireccional: los cambios realizados localmente a través de los deslizadores del applet TCI también se envían de vuelta a los clientes externos que se suscriben a las actualizaciones de ganancia.
- El comando `rx_volume` acepta un número de canal (1–4). Los números de canal corresponden a los canales DAX que se muestran en las filas RX1–RX4 del applet TCI.
- El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (v0.9.5.1, #2276).
- Las etiquetas de asignación de slices ahora usan formato HTML enriquecido (v26.5.2.1, #2606), por lo que los slices deshabilitados o con estado especial pueden mostrar formato de texto (p. ej., tachado).
- Para obtener fidelidad de tono digital bit exacto, use el modo **NaN guard** o **Measure only** para evitar la distorsión armónica del limitador Clip.
- El contenedor del applet TCI ahora usa estilo temático (v26.6.1): los colores se adaptan al tema activo.
- Todos los medidores de ganancia tienen nombres accesibles explícitos establecidos para compatibilidad con lectores de pantalla (v26.6.3). "TCI RX 1 gain" hasta "TCI RX 4 gain" para los canales RX, y "TCI TX gain" para el canal TX.
- El texto del botón Habilitar cambia dinámicamente entre "Enabled" y "Disabled" para reflejar el estado del servidor (v26.7.4).
- El campo de texto Puerto tiene nombre accesible "TCI port" y descripción accesible "TCP port the TCI server listens on" (v26.7.4).

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia de RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia de TX de TCI](adjust-tci-tx-gain.md)
