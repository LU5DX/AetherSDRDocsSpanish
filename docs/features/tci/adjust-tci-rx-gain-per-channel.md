# Ajustar la ganancia TCI de RX por canal

El applet TCI Server proporciona cuatro controles deslizantes de ganancia de RX independientes —uno por canal— que escalan el nivel de audio enviado a los clientes TCI conectados. Ajústelos cuando un cliente reciba audio demasiado alto o demasiado bajo en relación con su configuración operativa.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet TCI requiere una conexión de radio.
- El servidor TCI debe estar habilitado. Si no lo está, los valores de ganancia se guardan de todas formas, pero no se envía audio a los clientes. Consulte [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md).

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha para abrir el applet TCI Server.
2. Localice la fila **RX1**, **RX2**, **RX3** o **RX4** correspondiente al canal que desea ajustar. El slice asignado actualmente a cada canal se muestra en el indicador junto a la etiqueta de la fila (por ejemplo, `Slice A`); las filas sin slice asignado muestran `—`.
3. Arrastre el medidor/control deslizante de esa fila hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El valor se guarda de inmediato.
4. Repita el proceso para cualquier otro canal que necesite ajuste.

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Rango válido | Ajuste persistido |
|---|---|---|---|---|
| Ganancia+medidor RX1 | Medidor/control deslizante | 0.5 | 0.0–1.0 | `TciRxGain1` |
| Ganancia+medidor RX2 | Medidor/control deslizante | 0.5 | 0.0–1.0 | `TciRxGain2` |
| Ganancia+medidor RX3 | Medidor/control deslizante | 0.5 | 0.0–1.0 | `TciRxGain3` |
| Ganancia+medidor RX4 | Medidor/control deslizante | 0.5 | 0.0–1.0 | `TciRxGain4` |

Cada control deslizante también funciona como medidor en tiempo real, mostrando el nivel de audio de RX suavizado para el canal.

## Consejos

- La visualización del medidor utiliza suavizado de ataque rápido y decaimiento lento, por lo que los picos son visibles brevemente incluso durante los silencios en el audio.
- Los valores de ganancia se guardan en cuanto suelta el control deslizante. Se restauran automáticamente la próxima vez que AetherSDR inicia.
- Las asignaciones de canales de RX siguen el mapeo de canales DAX. Si un canal muestra `—`, no hay ningún slice asignado actualmente a ese canal DAX; asigne un canal DAX a un slice para activar esa fila de TCI RX.

## Solución de problemas

- **Todos los medidores de RX están apagados y no llega audio al cliente** — Es posible que el servidor TCI no esté en ejecución. Verifique que el estado del servidor muestre `:<puerto> (N clients)` y no `(stopped)`. Haga clic en **Enable** para iniciar el servidor si es necesario.
- **Los cambios de ganancia no tienen efecto en el cliente** — Confirme que el cliente está conectado al puerto correcto (`TciPort`, predeterminado `50001`). El estado del servidor muestra el puerto activo y el número de clientes.

## Relacionados

- [Ajustar la ganancia TCI de TX](adjust-tci-tx-gain.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Iniciar TCI automáticamente al arrancar](autostart-tci-on-launch.md)
