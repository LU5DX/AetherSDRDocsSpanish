# Seleccione la frecuencia de muestreo IQ (24k/48k/96k/192k)

Seleccione la frecuencia de muestreo para cada canal DAX IQ para que coincida con los requisitos de su software SDR externo. Las frecuencias más altas proporcionan más ancho de banda; las frecuencias más bajas reducen la carga de CPU y red.

## Antes de empezar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El applet DAX IQ debe estar visible. Si no lo está, haga clic en el botón **IQ** de la bandeja en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice la fila del canal que desea configurar: **IQ 1**, **IQ 2**, **IQ 3** o **IQ 4**.
2. Haga clic en el cuadro combinado de frecuencia en esa fila. Muestra la frecuencia actual (por defecto **48k**).
3. Seleccione una de las cuatro opciones: **24k**, **48k**, **96k** o **192k**.

AetherSDR envía inmediatamente la nueva frecuencia al radio y guarda su selección. La configuración persiste entre reinicios como `DaxIqRate1` a `DaxIqRate4`.

Si el flujo ya está activo, el cuadro combinado se sincroniza con la frecuencia informada por el radio cuando el flujo existe y no está en un estado de ajuste de frecuencia. Esto evita que el cuadro combinado muestre brevemente 48k mientras el radio aplica una frecuencia no predeterminada que seleccionó mientras el flujo estaba apagado.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave de configuración persistente |
|---|---|---|---|
| Cuadro combinado de frecuencia (por canal) | 48k | 24k (24000 Hz), 48k (48000 Hz), 96k (96000 Hz), 192k (192000 Hz) | `DaxIqRate1` … `DaxIqRate4` |
| Interruptor de encendido/apagado (por canal) | Apagado | Apagado, Encendido | `DaxIqEnabled1` … `DaxIqEnabled4` |
| Medidor de nivel (por canal) | 0 | 0–100 (escalado desde RMS × 200) | — |

## Detalles del comportamiento

- **Selección de frecuencia mientras el flujo está apagado**: Seleccione una frecuencia mientras el flujo está apagado, luego actívelo. La frecuencia que eligió se aplica al flujo recién creado, no al valor predeterminado de 48k del radio.
- **Sincronización de frecuencia mientras el flujo está activo**: El cuadro combinado se actualiza para coincidir con la frecuencia informada por el radio solo cuando el flujo existe y no está en un estado transitorio de ajuste de frecuencia. Durante el breve período de ajuste después de activar una frecuencia no predeterminada, el cuadro combinado mantiene su selección.
- **Desactivación del flujo**: Cuando desactiva un flujo, el cuadro combinado conserva su última frecuencia seleccionada. El radio restablece internamente la frecuencia de muestreo del flujo a 48k, pero el cuadro combinado no se sincroniza con ese valor restablecido.
- **Comportamiento del medidor**: El medidor de nivel se restablece a 0 cuando el canal está apagado o cuando está activado pero no vinculado a un pan (por ejemplo, si el `daxiq_channel` del pan se movió a otro canal IQ). En ninguno de los casos fluyen datos IQ.
- **Restauración de canales activados al conectar**: Después de conectar o reconectar al radio, AetherSDR espera 1.5 segundos para que la configuración de la sesión se estabilice, luego reactiva cualquier canal que estuviera activado antes de la desconexión. Si ocurren dos eventos de conexión dentro de la ventana de estabilización, el segundo se ignora para evitar la doble activación.

## Consejos

- Puede cambiar la frecuencia tanto si el flujo está apagado como si está encendido. Si el flujo ya está activado, el radio aplica la nueva frecuencia al flujo activo.
- Al reconectar, el cuadro combinado se restablece brevemente antes de que el radio confirme el estado del flujo. La frecuencia mostrada se sincroniza automáticamente una vez que el flujo se restablece y finaliza el período de ajuste.
- Los eventos de la rueda de desplazamiento en el cuadro combinado se suprimen cuando el bloqueo de desplazamiento del panel del applet está activo. Si el cuadro combinado no responde a la rueda de desplazamiento, desplace el panel a la posición deseada y luego haga clic directamente en el cuadro combinado.
- El medidor de nivel utiliza el color de acento y la paleta de fondo del tema actual.

## Solución de problemas

- **El cuadro combinado de frecuencia muestra un valor diferente al que seleccionó**: El radio ha informado una frecuencia diferente para el flujo activo después del período de ajuste, y el cuadro combinado se ha sincronizado para coincidir. Esto es normal. Desactive el flujo, cambie la frecuencia y luego vuelva a activarlo.
- **El cuadro combinado de frecuencia no responde a la rueda de desplazamiento**: El bloqueo de desplazamiento del panel del applet está activo. Haga clic en el cuadro combinado para abrir el menú desplegable.
- **Los colores del medidor de nivel se ven diferentes de lo esperado**: El medidor sigue el tema activo. Cambie el tema en **Settings > Appearance > Theme** para ajustar los colores del medidor.
- **Los canales no se reactivan después de la reconexión**: Si el temporizador de estabilización de 1.5 segundos ha transcurrido antes de que el applet termine de cargarse, es posible que los canales no se restauren automáticamente. Desconéctese y reconéctese para activar la restauración nuevamente.
- **El cuadro combinado de frecuencia muestra brevemente 48k después de la activación**: Este es el período de ajuste de frecuencia. El cuadro combinado se actualizará a la frecuencia que seleccionó una vez que el radio confirme la nueva frecuencia.

## Relacionado

- [Descripción general de DAX IQ](overview.md)
- [Activar un flujo IQ para software SDR externo](enable-an-iq-stream-for-external-sdr-software.md)
- [Desactivar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
