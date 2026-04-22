# Ajustar la ganancia de RX por canal en TCI

El applet TCI Server proporciona cuatro controles deslizantes de ganancia de RX independientes, uno por canal. Ajustarlos permite igualar el nivel de audio que los clientes TCI (como Log4OM o las herramientas SunSDR) reciben de cada slice activo.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El applet TCI debe estar visible. Si no lo está, haga clic en el botón TCI del área de notificación en la barra lateral derecha para mostrarlo.
- El servidor TCI debe estar en ejecución (Enable activado) para poder ver la medición en tiempo real mientras realiza los ajustes.

## Pasos

1. Haga clic en el botón TCI del área de notificación en la barra lateral derecha para abrir el applet TCI Server.
2. Localice la fila RX1, RX2, RX3 o RX4 correspondiente al canal que desea ajustar. La etiqueta de slice a la derecha del nombre del canal (por ejemplo, `Slice A`) indica qué slice está controlando ese canal. Un `—` significa que no hay ningún slice asignado.
3. Arrastre el control deslizante/medidor combinado de esa fila hacia la izquierda para disminuir la ganancia, o hacia la derecha para aumentarla. El rango válido es de 0.0 a 1.0; el valor predeterminado es 0.5.
4. Repita el procedimiento para cualquier otro canal RX que desee ajustar.

El nuevo valor se guarda de inmediato. Persiste entre reinicios como `TciRxGain1`, `TciRxGain2`, `TciRxGain3` o `TciRxGain4`, según el canal.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Ganancia+medidor RX1 | 0.5 | 0.0 – 1.0 | `TciRxGain1` |
| Ganancia+medidor RX2 | 0.5 | 0.0 – 1.0 | `TciRxGain2` |
| Ganancia+medidor RX3 | 0.5 | 0.0 – 1.0 | `TciRxGain3` |
| Ganancia+medidor RX4 | 0.5 | 0.0 – 1.0 | `TciRxGain4` |
| Etiqueta de asignación de slice | — | — o `Slice <letter>` | (ninguna) |

La parte del medidor de cada control deslizante refleja el nivel de señal RX en tiempo real mediante suavizado exponencial: ataque rápido, decaimiento lento. Esto permite estimar un ajuste de ganancia adecuado mientras el audio está fluyendo.

## Consejos

- Si un canal muestra `—` en la etiqueta de slice, no hay ningún slice asignado a ese canal DAX. Los cambios de ganancia se guardan, pero no tendrán ningún efecto audible hasta que se asigne un slice a ese canal.
- Los cuatro valores de ganancia son independientes. Configurar RX1 no afecta a RX2–RX4.

## Solución de problemas

- **El medidor no muestra movimiento** — Es posible que el servidor TCI no esté en ejecución. Verifique que Enable esté activado y que el estado del servidor no indique `(stopped)` ni `(port in use)`. Consulte [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md).
- **La etiqueta de slice muestra `—` en todos los canales** — Ningún slice tiene asignado un canal DAX. Asigne un canal DAX a cada slice a través de la configuración de slice de la radio y, luego, vuelva aquí para ajustar la ganancia.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Ajustar la ganancia de TX en TCI](adjust-tci-tx-gain.md)
- [Descripción general del TCI Server](overview.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
