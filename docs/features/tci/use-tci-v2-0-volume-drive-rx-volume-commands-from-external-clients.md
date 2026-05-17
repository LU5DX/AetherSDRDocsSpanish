# Uso de los comandos `volume`, `drive` y `rx_volume` de TCI v2.0 desde clientes externos

Los clientes externos (software de registro, software de modo digital, programas SDR) pueden controlar AetherSDR mediante los comandos `volume`, `drive` y `rx_volume` de TCI v2.0 cuando el servidor TCI está habilitado y la radio está conectada.

## Antes de comenzar

- Habilite el servidor TCI (haga clic en el botón de la bandeja TCI en la barra lateral derecha y luego en **Enable**).
- Conéctese a una radio.
- Configure su cliente externo para que se conecte al servidor TCI de AetherSDR en el puerto que se muestra en el applet TCI (predeterminado: 50001).

## Pasos

1. En el applet TCI, observe el número de puerto o cámbielo editando el campo de texto y presionando Enter. Rango válido: 1024–65535.
2. Configure su cliente externo para que se conecte a la dirección IP de AetherSDR y a ese puerto.
3. Envíe comandos TCI v2.0 desde su cliente:

   - **`volume`** — Establece el volumen RX maestro. AetherSDR lo asigna a la ganancia RX para el slice activo actual.
   - **`drive`** — Establece el nivel de drive de TX. AetherSDR lo asigna a `TciTxGain`.
   - **`rx_volume <canal>`** — Establece la ganancia RX para un canal DAX específico (1–4). AetherSDR lo asigna a `TciRxGain1` hasta `TciRxGain4`.

4. El servidor TCI recibe estos comandos y actualiza los ajustes de ganancia correspondientes. Los cambios se reflejan en los controles de medidor/deslizador del applet TCI y se guardan en la configuración.

## Qué hace cada control

| Comando | Ajuste asignado | Valor predeterminado | Rango válido |
|---------|----------------|----------------------|--------------|
| `volume` | Ganancia RX del slice activo | 0.5 | 0.0–1.0 |
| `drive` | `TciTxGain` | 0.5 | 0.0–1.0 |
| `rx_volume <canal>` | `TciRxGain1`–`TciRxGain4` | 0.5 | 0.0–1.0 |

## Controles del applet TCI

El applet TCI muestra el estado actual y le permite ajustar los valores de ganancia:

| Control | Descripción | Clave de ajuste |
|---------|-------------|-----------------|
| **RX1 gain+meter** hasta **RX4 gain+meter** | Medidor/deslizador combinado para cada canal DAX. Arrastre para establecer la ganancia RX de TCI. Emite `tciRxGainChanged`. | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| **TX gain+meter** | Medidor/deslizador combinado para la ganancia TX. Arrastre para establecer la ganancia TX de TCI. Emite `tciTxGainChanged`. | `TciTxGain` |
| **Port** | Campo de texto para el puerto del servidor WebSocket. Cámbielo y presione Enter. Los valores fuera de rango se ajustan a 50001. | `TciPort` |
| **Enable** | Botón de alternancia para iniciar o detener el servidor TCI. Si el enlace falla, vuelve a apagado y el estado muestra "(port in use)". | Ninguno |

### Etiquetas de asignación de slices RX/TX

| Etiqueta | Descripción | Formato |
|----------|-------------|---------|
| Estado **RX1..RX4** | Muestra qué slice impulsa cada canal DAX de RX. Se muestra como "Slice <letra>" donde la letra puede aparecer como texto HTML enriquecido (por ejemplo, con tachado para slices deshabilitados). | `—` o etiqueta de slice HTML enriquecido |
| Estado **TX** | Muestra qué slice es el slice TX activo. Se muestra como "Slice <letra>" con el mismo formato HTML enriquecido que las etiquetas RX. | `—` o etiqueta de slice HTML enriquecido |

### Indicador de estado del servidor

| Estado | Significado |
|--------|-------------|
| `(stopped)` | El servidor no está en ejecución |
| `:<puerto> (N clientes)` | El servidor se está ejecutando en el puerto especificado con N clientes conectados |
| `(port in use)` | El enlace falló: el puerto ya está en uso por otra aplicación |

## Consejos

- El servidor TCI admite la sincronización de estado bidireccional: los cambios realizados localmente mediante los deslizadores del applet TCI también se envían de vuelta a los clientes externos que estén suscritos a las actualizaciones de ganancia.
- El comando `rx_volume` acepta un número de canal (1–4). Los números de canal corresponden a los canales DAX que se muestran en las filas RX1–RX4 del applet TCI.
- El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX hospedado (v0.9.5.1, #2276).
- Las etiquetas de asignación de slices ahora usan formato HTML enriquecido (v26.5.2.1, #2606), por lo que los slices deshabilitados o en estado especial pueden mostrarse con formato de texto (por ejemplo, tachado).

## Relacionado

- [Enable the TCI server for Log4OM / SunSDR clients](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Change the TCI port](change-the-tci-port.md)
- [Adjust TCI RX gain per channel](adjust-tci-rx-gain-per-channel.md)
- [Adjust TCI TX gain](adjust-tci-tx-gain.md)
