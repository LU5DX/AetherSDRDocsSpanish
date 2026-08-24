# Uso de los comandos TCI v2.0 `volume`/`drive`/`rx_volume` desde clientes externos

Los clientes externos (software de registro, software de modos digitales, programas SDR) pueden controlar AetherSDR mediante los comandos TCI v2.0 `volume`, `drive` y `rx_volume` cuando el servidor TCI está habilitado y la radio está conectada.

## Antes de comenzar

- Habilite el servidor TCI (haga clic en el botón de la bandeja TCI en la barra lateral derecha y luego en Enable).
- Conéctese a una radio.
- Configure su cliente externo para conectarse al servidor TCI de AetherSDR en el puerto que se muestra en el applet TCI (predeterminado: 50001).

## Pasos

1. En el applet TCI, anote el número de puerto o cámbielo editando el campo de texto y presionando Enter. Rango válido: 1024–65535.
2. Configure su cliente externo para conectarse a la dirección IP de AetherSDR y a ese puerto.
3. Envíe comandos TCI v2.0 desde su cliente:

   - **`volume`** — Establece el volumen maestro de RX. AetherSDR lo asigna a la ganancia de RX del slice activo.
   - **`drive`** — Establece el nivel de excitación de TX. AetherSDR lo asigna a `TciTxGain`.
   - **`rx_volume <canal>`** — Establece la ganancia de RX para un canal DAX específico (1–8). AetherSDR lo asigna a `TciRxGain1` hasta `TciRxGain8`.

4. El servidor TCI recibe estos comandos y actualiza los ajustes de ganancia correspondientes. Los cambios se reflejan en los controles de medidor/deslizador del applet TCI y se guardan en la configuración.

## Qué hace cada control

| Comando                        | Ajuste asignado                                                                                                                       | Predeterminado                                                                                                                                                                                                                                        |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `volume`                       | Ganancia de RX del slice activo                                                                                                                 | 0.5                                                                                                                                                                                                                                            |
| `drive`                        | `TciTxGain`                                                                                                                          | 0.5                                                                                                                                                                                                                                            |
| `rx_volume <canal>`          | `TciRxGain1`–`TciRxGain8`                                                                                                            | 0.5                                                                                                                                                                                                                                            |
| Modo de desbordamiento de TX (clic derecho) | Haga clic derecho en el medidor/deslizador de ganancia de TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento de TX. Emite `tciTxOverflowModeChanged`. | Nuevo en v26.5.3. Clip limita los excesos a ±1.0 con distorsión armónica; NaNGuard preserva los tonos digitales bit-exactos al poner solo a cero los valores NaN/Inf; Measure cuenta los excesos para telemetría sin modificación. Se guarda como `TciTxOverflowMode` (0/1/2). |

## Controles del applet TCI

El applet TCI muestra el estado actual y le permite ajustar los valores de ganancia:

| Control | Descripción | Clave de ajuste |
|---------|-------------|-------------|
| **Ganancia+medidor RX1** hasta **ganancia+medidor RX8** | Medidor/deslizador combinado para cada canal DAX. Arrastre para establecer la ganancia de RX de TCI. Emite `tciRxGainChanged`. Cada control tiene un nombre accesible "TCI RX _N_ gain" para los lectores de pantalla. Las filas más allá de la capacidad de slices de la radio se ocultan automáticamente. | `TciRxGain1` hasta `TciRxGain8` |
| **Ganancia+medidor TX** | Medidor/deslizador combinado para la ganancia de TX. Arrastre para establecer la ganancia de TX de TCI. Emite `tciTxGainChanged`. Haga clic derecho para abrir el selector de modo de desbordamiento de TX. Tiene nombre accesible "TCI TX gain" para los lectores de pantalla. | `TciTxGain` |
| **Port** | Campo de texto para el puerto del servidor WebSocket. Cámbielo y presione Enter. Los valores fuera de rango se ajustan a 50001. Tiene nombre accesible "TCI port". | `TciPort` |
| **Enable** | Botón de alternancia para iniciar o detener el servidor TCI. El texto muestra "Enabled" cuando el servidor está en ejecución o se iniciará automáticamente, y "Disabled" en caso contrario. Si el enlace falla, vuelve a apagado, el texto cambia a "Disabled" y el estado muestra "(port in use)". | Ninguno |

### Modo de desbordamiento de TX (clic derecho)

Haga clic derecho en el control **ganancia+medidor TX** para abrir un menú contextual que selecciona cómo se manejan las muestras fuera de rango (>1.0) de los clientes TCI antes de llegar a la radio. Emite `tciTxOverflowModeChanged`. El modo seleccionado se guarda como `TciTxOverflowMode` (0/1/2).

| Modo | Valor | Descripción |
|------|-------|-------------|
| Clip (saturación ±1.0) | 0 | Limita rígidamente los excesos a ±1.0. Predeterminado defensivo; introduce armónicos en los excesos pero protege la conversión posterior a int16. |
| NaN guard (solo cero para NaN/Inf) | 1 | Pasa las muestras bit-exactas; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad de los tonos en modos digitales; los flotantes fuera de rango llegan a la radio. |
| Measure only (derivación real) | 2 | Nunca modifica las muestras. Cuenta los excesos para telemetría; la conversión posterior a int16 aún limita en la ruta DAX nativa de la radio. |

El predeterminado es **Clip** para que los usuarios existentes no vean cambios de comportamiento.

### Etiquetas de asignación de slices RX/TX

| Etiqueta | Descripción | Formato |
|-------|-------------|--------|
| **Estado RX1..RX8** | Muestra qué slice impulsa cada canal DAX de RX. Se muestra como "Slice <letra>" donde la letra puede aparecer como texto HTML enriquecido (p. ej., con tachado para slices deshabilitados). | `—` o etiqueta de slice HTML enriquecido |
| **Estado TX** | Muestra qué slice es el slice TX activo. Se muestra como "Slice <letra>" con el mismo formato HTML enriquecido que las etiquetas RX. | `—` o etiqueta de slice HTML enriquecido |

### Indicador de estado del servidor

| Estado | Significado |
|-------|---------|
| `(stopped)` | El servidor no está en ejecución |
| `:<puerto> (N clients)` | El servidor está en ejecución en el puerto especificado con N clientes conectados |
| `(port in use)` | El enlace falló: el puerto ya está en uso por otra aplicación |

## Consejos

- El servidor TCI admite sincronización de estado bidireccional: los cambios realizados localmente mediante los deslizadores del applet TCI también se envían a los clientes externos que se suscriben a las actualizaciones de ganancia.
- El comando `rx_volume` acepta un número de canal (1–8). Los números de canal corresponden a los canales DAX que se muestran en las filas RX1–RX8 del applet TCI.
- El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (v0.9.5.1, #2276).
- Las etiquetas de asignación de slices ahora usan formato HTML enriquecido (v26.5.2.1, #2606), por lo que los slices deshabilitados o en estado especial pueden mostrarse con formato de texto (p. ej., tachado).
- Para la fidelidad bit-exacta de los tonos en modos digitales, use el modo **NaN guard** o **Measure only** para evitar la distorsión armónica del limitador Clip.
- El contenedor del applet TCI ahora usa estilo temático (v26.6.1): los colores se adaptan al tema activo.
- Todos los medidores de ganancia tienen nombres accesibles explícitos para la compatibilidad con lectores de pantalla (v26.6.3). "TCI RX 1 gain" hasta "TCI RX 8 gain" para los canales RX y "TCI TX gain" para el canal TX.
- El texto del botón Enable cambia dinámicamente entre "Enabled" y "Disabled" para reflejar el estado del servidor (v26.7.4).
- El campo de texto Port tiene nombre accesible "TCI port" y descripción accesible "TCP port the TCI server listens on" (v26.7.4).
- Las filas RX más allá de la capacidad de slices de la radio se ocultan automáticamente (v26.8.4, #4854). Por ejemplo, una radio con 4 slices muestra solo las filas RX1–RX4, mientras que una radio de 8 slices muestra todas las filas RX1–RX8.

## Relacionado

- [Enable the TCI server for Log4OM / SunSDR clients](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Change the TCI port](change-the-tci-port.md)
- [Adjust TCI RX gain per channel](adjust-tci-rx-gain-per-channel.md)
- [Adjust TCI TX gain](adjust-tci-tx-gain.md)
