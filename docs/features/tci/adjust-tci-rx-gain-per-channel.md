# Ajustar la ganancia RX del TCI por canal

El applet del Servidor TCI proporciona un control deslizante de ganancia para cada uno de sus cuatro canales RX. Ajustarlos permite igualar el nivel de audio que los clientes TCI (como Log4OM o herramientas SunSDR) reciben de cada segmento.

## Antes de comenzar

- La radio debe estar conectada. El applet TCI requiere una conexión de radio activa.
- El applet del Servidor TCI debe estar visible. Si el panel del applet no se muestra, haga clic en el botón **TCI** de la barra lateral derecha para revelarlo.

## Pasos

1. Haga clic en el botón **TCI** de la barra lateral derecha para abrir el applet del Servidor TCI.
2. Localice la fila **RX1**, **RX2**, **RX3** o **RX4** para el canal que desea ajustar. La etiqueta de asignación de segmento junto al nombre del canal (por ejemplo, `Slice A`) muestra qué segmento está impulsando ese canal. Un `—` significa que no hay ningún segmento asignado actualmente.
3. Arrastre el medidor/control deslizante de esa fila hacia la izquierda o derecha para ajustar la ganancia. El valor se guarda inmediatamente.
4. Repita para cualquier otro canal RX que desee ajustar.

## Habilitar el servidor TCI

El botón Habilitar inicia o detiene el servidor TCI.

1. En el applet del Servidor TCI, localice el botón **Enable**. Muestra **Disabled** cuando el servidor está apagado y **Enabled** cuando el servidor está en ejecución.
2. Haga clic en **Enable** para iniciar el servidor. El texto del botón cambia a **Enabled**.
3. Para detener el servidor, haga clic en **Enable** nuevamente. El texto del botón cambia a **Disabled**.
4. Si el servidor no puede vincularse al puerto especificado, el texto del botón vuelve a **Disabled** y el indicador de estado muestra **(port in use)** en rojo.

El estado del botón Enable se inicializa desde la configuración `AutoStartTCI`. Si `AutoStartTCI` está configurado en `True`, el botón comienza como **Enabled** y el servidor se inicia automáticamente cuando se carga el applet.

## Configurar el puerto TCI

El campo Puerto establece el puerto TCP en el que escucha el servidor TCI.

1. En el applet del Servidor TCI, localice el campo de texto **Port**.
2. Ingrese un número de puerto entre 1024 y 65535.
3. Si cambia el puerto mientras el servidor está en ejecución, el servidor se reinicia automáticamente en el nuevo puerto.
4. Los valores fuera de rango se ajustan a 50001.

El campo Port tiene un nombre accesible de "TCI port" con una descripción de "TCP port the TCI server listens on".

## Qué hace cada control

| Control                        | Valor predeterminado                                                                                                         | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Medidor/deslizador de ganancia RX1 | 0.5                                                                                                                         | 0.0 – 1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Medidor/deslizador de ganancia RX2 | 0.5                                                                                                                         | 0.0 – 1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Medidor/deslizador de ganancia RX3 | 0.5                                                                                                                         | 0.0 – 1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Medidor/deslizador de ganancia RX4 | 0.5                                                                                                                         | 0.0 – 1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Ganancia TX+medidor            | Arrastrar establece la ganancia TX del TCI y emite tciTxGainChanged. Clic derecho abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure). | TciServer::setTxGain persiste TciTxGain internamente; la UI refleja el valor almacenado. El audio TX del TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú de clic derecho permite al usuario elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes de modos digitales: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo pone a cero NaN/Inf) o Measure (bypass real con conteo de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Etiqueta de asignación de segmento | —                                                                                                                           | — o `Slice <letra>`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Modo de desbordamiento TX (clic derecho) | Clip                                                                                                                        | Clip, NaNGuard, Measure                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Botón Enable                  | Disabled (o Enabled si `AutoStartTCI` = True)                                                                                | Disabled o Enabled                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Campo Port                     | 50001                                                                                                                       | 1024 – 65535                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Indicador de estado del servidor | (stopped)                                                                                                                   | (stopped), `:<puerto> (N clients)` o (port in use)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

Cada medidor/deslizador también muestra un nivel RX o TX en vivo utilizando suavizado exponencial — ataque rápido, caída lenta — de modo que la barra refleje la actividad de la señal en ese canal mientras la posición de arrastre establece la ganancia.

Las etiquetas de asignación de segmento ahora renderizan las letras de los segmentos con formato de texto enriquecido (#2606). Esto permite que los indicadores de segmento externos (por ejemplo, un marcador de color o estilo en la letra del segmento) se muestren correctamente en la etiqueta de estado. El texto de la etiqueta se genera usando `SliceLabel::richText()` en lugar de una letra sin procesar, asegurando que cualquier formato HTML incrustado en la representación del segmento se conserve.

Cada medidor/deslizador tiene un nombre accesible configurado para compatibilidad con lectores de pantalla. Los deslizadores de ganancia RX se nombran "TCI RX 1 gain" a "TCI RX 4 gain", y el deslizador de ganancia TX se nombra "TCI TX gain". El botón Enable tiene un nombre accesible de "TCI server enable" con una descripción de "Start or stop the TCI server".

## Haga clic derecho en la ganancia TX para manejar desbordamientos

El medidor/deslizador de ganancia TX tiene un menú contextual de clic derecho que permite elegir cómo se manejan las muestras de audio fuera de rango (>1.0) de los clientes TCI antes de que lleguen a la radio.

1. Haga clic derecho en cualquier lugar del deslizador **TX gain+meter**.
2. Seleccione uno de los tres modos de manejo de desbordamiento:
   - **Clip (saturating ±1.0)** — Fija los excesos a ±1.0. Es el predeterminado heredado e introduce distorsión armónica en los excesos, pero protege la conversión a int16 aguas abajo.
   - **NaN guard (zero NaN/Inf only)** — Pasa las muestras sin cambios bit a bit; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad de tono de los modos digitales; los flotantes fuera de rango aún llegan a la radio.
   - **Measure only (true bypass)** — Nunca modifica las muestras. Cuenta los excesos para telemetría; la conversión a int16 aguas abajo aún recorta en la ruta DAX nativa de la radio.

El modo seleccionado se persiste como la configuración `TciTxOverflowMode` (valor 0, 1 o 2) y se restaura en el próximo inicio. El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065).

## Qué hace cada modo de desbordamiento TX

| Modo        | Valor | Comportamiento                                                               |
|-------------|-------|------------------------------------------------------------------------------|
| Clip        | 0     | Satura las muestras a ±1.0. Valor defensivo predeterminado; introduce armónicos. |
| NaNGuard    | 1     | Pasa las muestras sin cambios excepto poner a cero NaN/Inf. Bit exacto para tonos digitales. |
| Measure     | 2     | Bypass real: nunca modifica las muestras. Cuenta los excesos para telemetría. |

## Indicador de estado del servidor

El indicador de estado del servidor muestra el estado actual del servidor TCI:

- **(stopped)** — El servidor no está en ejecución.
- **:<puerto> (N clients)** — El servidor está en ejecución en el puerto especificado con N clientes conectados.
- **(port in use)** — El puerto seleccionado ya está siendo utilizado por otra aplicación. El texto de estado aparece en rojo.

## Consejos

- Las etiquetas de asignación de segmento (por ejemplo, `Slice A`) siguen la asignación del canal DAX. Si cambia la asignación del canal DAX de un segmento, la etiqueta se actualiza automáticamente.
- Los valores de ganancia se persisten como flotantes de dos decimales (por ejemplo, `0.75`). Se restauran la próxima vez que se inicie AetherSDR.
- El modo de desbordamiento TX es particularmente útil para modos digitales donde las muestras fuera de rango deben conservarse sin recorte para la fidelidad de tono bit exacto. Use **NaN guard** para operación en modo digital y **Measure** para telemetría de diagnóstico.

## Solución de problemas

- **Un canal muestra `—` y no pasa audio al cliente TCI** — No hay ningún segmento asignado a ese canal DAX. Asigne un segmento al canal DAX correspondiente en la configuración de su radio para que el audio RX del TCI se enrute a ese canal.
- **La selección del modo de desbordamiento TX no persiste** — Verifique que AetherSDR tenga permiso de escritura en su archivo de configuración. La configuración `TciTxOverflowMode` se almacena en la configuración de la aplicación.
- **El estado del servidor muestra (port in use)** — El puerto seleccionado está ocupado por otra aplicación. Elija un número de puerto diferente en el campo Port.
- **El botón Enable no inicia el servidor** — Verifique que el número de puerto sea válido (1024-65535). Si el puerto está en uso, el botón vuelve a **Disabled** y el estado muestra **(port in use)**.

## Relacionado

- [TCI Server overview](overview.md)
- [Adjust TCI TX gain](adjust-tci-tx-gain.md)
- [Enable the TCI server for Log4OM / SunSDR clients](enable-the-tci-server-for-log4om-sunsdr-clients.md)
