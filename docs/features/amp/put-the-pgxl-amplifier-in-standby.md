# Poner el amplificador PGXL en STANDBY

Use esta página para cambiar un amplificador Power Genius XL conectado del modo OPERATE a STANDBY, deteniendo la amplificación de las señales transmitidas.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El botón de la bandeja AMP solo aparece después de detectar un Power Genius XL.
- El applet del amplificador debe estar abierto. Si no es visible, haga clic en el botón AMP de la barra lateral derecha para mostrarlo.
- El botón OPERATE está oculto hasta que llegue el primer mensaje de estado del amplificador. Confirme que sea visible antes de continuar.

## Pasos

1. Abra el applet del amplificador haciendo clic en el botón AMP de la barra lateral derecha si aún no es visible.
2. Confirme que el botón OPERATE muestre la etiqueta "OPERATE" en verde. Esto indica que el amplificador se encuentra actualmente en un estado operativo (IDLE, OPERATE o TRANSMIT).
3. Haga clic en OPERATE.

La etiqueta del botón cambia a "STANDBY" y el fondo verde se reemplaza con el estilo oscuro predeterminado, lo que confirma que el amplificador ha pasado a STANDBY.

## Qué hace cada control

| Control  | Comportamiento                                                              | Estados                                                                                                                                                                                                                                                       |
|----------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| OPERATE  | Conmuta el amplificador entre OPERATE y STANDBY; emite operateToggled.      | Oculto hasta que llegue setState. Muestra 'OPERATE' (verde) para estados IDLE/OPERATE/TRANSMIT_*, 'STANDBY' en caso contrario. En v0.9.8, setState se llama desde RadioModel::ampStateChanged (autoritativo), evitando que el botón se quede en la etiqueta anterior (#2437). |

## Solución de problemas

- **El botón de la bandeja AMP no es visible** — El applet está oculto hasta que la radio detecte un Power Genius XL. Confirme que el PGXL esté encendido y conectado a la radio Flex.
- **El botón OPERATE no es visible** — El botón está oculto hasta que llegue el primer mensaje de estado del amplificador. Espere un momento después de abrir el applet; si no aparece, verifique la conexión del amplificador.
- **Hacer clic en OPERATE no tiene efecto** — Confirme que AetherSDR aún esté conectado a la radio. Desconecte y vuelva a conectar si es necesario.

## Relacionado

- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Monitorear la potencia directa y la ROE en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Observar la temperatura, la corriente de drenaje y el voltaje de red del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
- [Resumen del amplificador](overview.md)
