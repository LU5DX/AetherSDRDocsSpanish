# Ajustar la ganancia RX de TCI por canal

El applet TCI Server proporciona cuatro controles deslizantes de ganancia RX independientes, uno por canal. Ajustarlos permite equilibrar el nivel de audio que los clientes TCI reciben de cada slice (receptor virtual) sin afectar la ganancia de recepción propia del equipo.

## Antes de comenzar

- El applet TCI debe estar visible. Si no lo está, haga clic en el botón **TCI** de la bandeja en la barra lateral derecha para mostrarlo.
- El servidor TCI debe estar en ejecución (el botón **Enable** debe estar activado). Los cambios de ganancia surten efecto de inmediato, pero debe haber un cliente conectado para recibir audio.
- El equipo debe estar conectado. El applet requiere una conexión de radio activa.

## Pasos

1. Abra el applet TCI haciendo clic en el botón **TCI** de la bandeja en la barra lateral derecha, si no está visible todavía.
2. Localice la fila **RX1**, **RX2**, **RX3** o **RX4** correspondiente al canal que desea ajustar. Cada fila muestra la etiqueta del canal, un indicador de asignación de slice y un medidor/control deslizante combinado.
3. Arrastre la parte deslizante del medidor/control hacia la izquierda para disminuir la ganancia o hacia la derecha para aumentarla. El valor se guarda de inmediato.
4. Repita el procedimiento para cualquier otro canal RX que requiera ajuste.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente |
|---|---|---|---|
| Ganancia+medidor RX1 | 0.5 | 0.0–1.0 | `TciRxGain1` |
| Ganancia+medidor RX2 | 0.5 | 0.0–1.0 | `TciRxGain2` |
| Ganancia+medidor RX3 | 0.5 | 0.0–1.0 | `TciRxGain3` |
| Ganancia+medidor RX4 | 0.5 | 0.0–1.0 | `TciRxGain4` |
| Etiquetas de asignación de slice RX/TX | — | — o Slice \<letter\> | *(ninguno)* |

El indicador de asignación de slice junto a cada fila RX muestra qué slice está conduciendo ese canal (por ejemplo, **Slice A**), según la asignación de canales DAX. Muestra **—** cuando no hay ningún slice asignado a ese canal.

La parte de medidor de cada control deslizante refleja el nivel de audio RX en tiempo real con suavizado exponencial: la visualización ataca rápidamente y decae lentamente, de modo que los picos breves son visibles sin parpadeo constante.

## Consejos

- Los cuatro valores de ganancia se guardan en cuanto suelta el control deslizante. Se restauran automáticamente la próxima vez que AetherSDR se inicia.
- Si el indicador de asignación de slice de un canal muestra **—**, no llegará audio a ese canal TCI RX independientemente del valor de ganancia. Asigne primero un canal DAX al slice correspondiente.
- Los valores de ganancia están en una escala lineal de 0.0 a 1.0, no en dB. Un valor de 0.5 (el predeterminado) equivale a la mitad del nivel de salida máximo presentado a los clientes TCI.

## Relacionados

- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Descripción general del TCI Server](overview.md)
