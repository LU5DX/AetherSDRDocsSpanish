# Ajustar la ganancia RX del TCI por canal

El applet del Servidor TCI proporciona un control deslizante de ganancia para cada uno de los hasta ocho canales RX. Ajustarlos le permite igualar el nivel de audio que los clientes TCI (como Log4OM o las herramientas SunSDR) reciben de cada slice. El número de filas RX visibles coincide con la capacidad de slices de la radio: una FLEX-6600 muestra cuatro, una FLEX-6700 muestra ocho.

## Antes de comenzar

- La radio debe estar conectada. El applet TCI requiere una conexión activa con la radio.
- El applet del Servidor TCI debe estar visible. Si el panel del applet no se muestra, haga clic en el botón **TCI** de la barra lateral derecha para revelarlo.

## Pasos

1. Haga clic en el botón **TCI** de la barra lateral derecha para abrir el applet del Servidor TCI.
2. Localice la fila **RX1** a **RX8** del canal que desea ajustar. Solo se muestran las filas dentro de la capacidad de slices de la radio. La etiqueta de asignación de slice junto al nombre del canal (por ejemplo, `Slice A`) indica qué slice está alimentando ese canal. Un `—` significa que no hay ningún slice asignado actualmente.
3. Arrastre el medidor/control deslizante de esa fila hacia la izquierda o la derecha para establecer la ganancia. El valor se guarda de inmediato.
4. Repita el procedimiento para cualquier otro canal RX que desee ajustar.

## Habilitar el servidor TCI

El botón Enable inicia o detiene el servidor TCI.

1. En el applet del Servidor TCI, localice el botón **Enable**. Muestra **Disabled** cuando el servidor está apagado y **Enabled** cuando el servidor está en ejecución.
2. Haga clic en **Enable** para iniciar el servidor. El texto del botón cambia a **Enabled**.
3. Para detener el servidor, haga clic en **Enable** nuevamente. El texto del botón cambia a **Disabled**.
4. Si el servidor no puede vincularse al puerto especificado, el texto del botón vuelve a **Disabled** y el indicador de estado muestra **(port in use)** en rojo.

El estado del botón Enable se inicializa desde la configuración `AutoStartTCI`. Si `AutoStartTCI` está establecido en `True`, el botón comienza como **Enabled** y el servidor se inicia automáticamente cuando se carga el applet.

## Establecer el puerto TCI

El campo Port establece el puerto TCP en el que escucha el servidor TCI.

1. En el applet del Servidor TCI, localice el campo de texto **Port**.
2. Ingrese un número de puerto entre 1024 y 65535.
3. Si cambia el puerto mientras el servidor está en ejecución, el servidor se reinicia automáticamente en el nuevo puerto.
4. Los valores fuera de rango se ajustan a 50001.

El campo Port tiene un nombre accesible de "TCI port" con una descripción de "TCP port the TCI server listens on".

## Qué hace cada control

| Control                        | Predeterminado                                                                                                             | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Medidor/control deslizante de ganancia RX1 | 0.5                                                                                                                         | 0.0 – 1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Medidor/control deslizante de ganancia RX2 | 0.5                                                                                                                         | 0.0 – 1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Medidor/control deslizante de ganancia RX3 | 0.5                                                                                                                         | 0.0 – 1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Medidor/control deslizante de ganancia RX4 | 0.5                                                                                                                         | 0.0 – 1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Medidor/control deslizante de ganancia RX5 | 0.5                                                                                                                         | 0.0 – 1.0 (visible solo en radios con 5 o más slices)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Medidor/control deslizante de ganancia RX6 | 0.5                                                                                                                         | 0.0 – 1.0 (visible solo en radios con 6 o más slices)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Medidor/control deslizante de ganancia RX7 | 0.5                                                                                                                         | 0.0 – 1.0 (visible solo en radios con 7 o más slices)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Medidor/control deslizante de ganancia RX8 | 0.5                                                                                                                         | 0.0 – 1.0 (visible solo en radios con 8 o más slices)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Ganancia+medidor TX                  | Arrastrar establece la ganancia TX del TCI y emite tciTxGainChanged. El clic derecho abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure). | TciServer::setTxGain persiste TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX del TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX hospedado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú de clic derecho permite al usuario elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes en modo digital: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo anula NaN/Inf), o Measure (bypass real con conteo de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Etiqueta de asignación de slice      | —                                                                                                                           | — o `Slice <letra>`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Modo de desbordamiento TX (clic derecho) | Clip                                                                                                                        | Clip, NaNGuard, Measure                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Botón Enable                  | Disabled (o Enabled si `AutoStartTCI` = True)                                                                              | Disabled o Enabled                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Campo Port                     | 50001                                                                                                                       | 1024 – 65535                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Indicador de estado del servidor        | (stopped)                                                                                                                   | (stopped), `:<puerto> (N clientes)`, o (port in use)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

Cada medidor/control deslizante también muestra un nivel RX o TX en vivo mediante suavizado exponencial — ataque rápido, caída lenta — de modo que la barra refleja la actividad de señal en ese canal mientras que la posición del arrastre establece la ganancia.

Las etiquetas de asignación de slice ahora muestran las letras de slice con formato de texto enriquecido (#2606). Esto permite que los indicadores externos de slice (por ejemplo, un marcador de color o con estilo en la letra del slice) se muestren correctamente en la etiqueta de estado. El texto de la etiqueta se genera mediante `SliceLabel::richText()` en lugar de una letra cruda, lo que garantiza que cualquier formato HTML incrustado en la representación del slice se conserve.

Cada medidor/control deslizante tiene un nombre accesible configurado para compatibilidad con lectores de pantalla. Los controles deslizantes de ganancia RX se denominan "TCI RX 1 gain" hasta "TCI RX 8 gain", y el control deslizante de ganancia TX se denomina "TCI TX gain". El botón Enable tiene un nombre accesible de "TCI server enable" con una descripción de "Start or stop the TCI server".

## Clic derecho en la ganancia TX para manejo de desbordamiento

El medidor/control deslizante de ganancia TX tiene un menú contextual de clic derecho que le permite elegir cómo se manejan las muestras de audio fuera de rango (>1.0) de los clientes TCI antes de que lleguen a la radio.

1. Haga clic derecho en cualquier parte del control deslizante **TX gain+meter**.
2. Seleccione uno de los tres modos de manejo de desbordamiento:
   - **Clip (saturación ±1.0)** — Limita con dureza los excesos a ±1.0. Este es el predeterminado heredado e introduce distorsión armónica en los excesos, pero protege la conversión int16 posterior.
   - **NaN guard (solo anula NaN/Inf)** — Pasa las muestras de forma bit-exacta; solo anula valores patológicos NaN/Inf. Preserva la fidelidad del tono en modos digitales; los valores de punto flotante fuera de rango aún llegan a la radio.
   - **Measure only (bypass real)** — Nunca modifica las muestras. Cuenta los excesos para telemetría; la conversión int16 posterior aún limita en la ruta DAX nativa de la radio.

El modo seleccionado se persiste como la configuración `TciTxOverflowMode` (valor 0, 1 o 2) y se restaura en el siguiente inicio. El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065).

## Qué hace cada modo de desbordamiento TX

| Modo        | Valor | Comportamiento                                                               |
|-------------|-------|------------------------------------------------------------------------------|
| Clip        | 0     | Satura las muestras en ±1.0. Predeterminado defensivo; introduce armónicos.   |
| NaNGuard    | 1     | Pasa las muestras sin cambios excepto anular NaN/Inf. Bit-exacto para tonos digitales. |
| Measure     | 2     | Bypass real — nunca modifica las muestras. Cuenta los excesos para telemetría. |

## Indicador de estado del servidor

El indicador de estado del servidor muestra el estado actual del servidor TCI:

- **(stopped)** — El servidor no está en ejecución.
- **:<puerto> (N clientes)** — El servidor se está ejecutando en el puerto especificado con N clientes conectados.
- **(port in use)** — El puerto seleccionado ya está en uso por otra aplicación. El texto de estado aparece en rojo.

## Consejos

- Las etiquetas de asignación de slice (por ejemplo, `Slice A`) siguen el mapeo de canales DAX. Si cambia la asignación del canal DAX de un slice, la etiqueta se actualiza automáticamente.
- El número de filas de ganancia RX visibles está limitado a la capacidad de slices de la radio (por ejemplo, cuatro en una FLEX-6600, ocho en una FLEX-6700). Las filas por encima de esa capacidad están ocultas; esto refleja el comportamiento del applet DAX (#4854).
- Los canales RX del TCI 1–8 transportan los mismos canales DAX que el applet DAX — `PanadapterStream::daxAudioReady` se distribuye tanto a DaxBridge como a TciServer, por lo que las letras de slice mostradas en el applet TCI coinciden con las asignaciones de canales DAX.
- Los valores de ganancia se persisten como flotantes de dos decimales (por ejemplo, `0.75`). Se restauran la próxima vez que se inicia AetherSDR.
- El modo de desbordamiento TX es particularmente útil para modos digitales donde las muestras fuera de rango deben conservarse sin recorte para una fidelidad de tono bit-exacta. Use **NaN guard** para operación en modo digital y **Measure** para telemetría de diagnóstico.

## Solución de problemas

- **Un canal muestra `—` y no pasa audio al cliente TCI** — No hay ningún slice asignado a ese canal DAX. Asigne un slice al canal DAX correspondiente en la configuración de su radio para que el audio RX del TCI se enrute a ese canal.
- **Falta una fila RX en el applet** — La radio a la que está conectado tiene menos slices de los que soporta el applet. Por ejemplo, una FLEX-6600 muestra cuatro filas RX; una FLEX-6700 muestra las ocho. Este es un comportamiento esperado y coincide con el applet DAX (#4854).
- **La selección del modo de desbordamiento TX no persiste** — Verifique que AetherSDR tenga permiso de escritura en su archivo de configuración. La configuración `TciTxOverflowMode` se almacena en la configuración de la aplicación.
- **El estado del servidor muestra (port in use)** — El puerto seleccionado está ocupado por otra aplicación. Elija un número de puerto diferente en el campo Port.
- **El botón Enable no inicia el servidor** — Verifique que el número de puerto sea válido (1024-65535). Si el puerto está en uso, el botón vuelve a **Disabled** y el estado muestra **(port in use)**.

## Relacionados

- [Descripción general del Servidor TCI](overview.md)
- [Ajustar la ganancia TX del TCI](adjust-tci-tx-gain.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
