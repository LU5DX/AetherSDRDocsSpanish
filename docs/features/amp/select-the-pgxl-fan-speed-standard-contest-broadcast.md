# Seleccione la velocidad del ventilador del PGXL (Standard, Contest, Broadcast)

Elija entre los tres perfiles de enfriamiento de un amplificador Power Genius XL conectado directamente desde el applet Amplifier, para que el ventilador funcione al nivel adecuado para su estilo de operación.

## Antes de comenzar

- Conéctese a una radio FLEX-8600 con firmware 4.1.5.
- El amplificador PGXL debe estar conectado físicamente de forma directa a la computadora, no mediante proxy a través de la radio.
- El applet Amplifier debe estar visible; actívelo con el botón de bandeja AMP en la barra lateral derecha.
- Espere el primer estado del modo de ventilador del amplificador; el selector de velocidad del ventilador está oculto hasta que llegue ese estado.

## Pasos

1. Haga clic en el botón de bandeja AMP en la barra lateral derecha para abrir el applet Amplifier.
2. Confirme que la etiqueta de fuente indique "● DIRECT" (la velocidad del ventilador solo está disponible en una conexión directa).
3. Haga clic en el selector de velocidad del ventilador (etiquetado "Fan: Std", "Fan: Contest" o "Fan: Bcast").
4. Seleccione **STANDARD**, **CONTEST** o **BROADCAST** en el menú desplegable.

El amplificador cambia al modo de ventilador elegido de inmediato. La etiqueta del selector se actualiza para reflejar el modo actual.

## Qué hace cada control

- **Selector de velocidad del ventilador** — Menú desplegable que lista los tres modos. Está oculto hasta que una conexión directa del PGXL entregue el primer estado del modo de ventilador. El selector ignora el desplazamiento de la rueda del ratón a menos que el menú esté abierto, lo que evita cambios accidentales al pasar el cursor sobre él.

## Consejos

- El selector de velocidad del ventilador solo aparece cuando la fuente de telemetría es DIRECT. Si ve "● RADIO", el amplificador está en proxy a través de la radio y el selector permanece oculto.
- Los tres modos se asignan a las etiquetas "Fan: Std", "Fan: Contest" y "Fan: Bcast" en el selector cerrado.

## Solución de problemas

- **Falta el selector de velocidad del ventilador** — El amplificador está conectado mediante el proxy de la radio, no directamente. Verifique la etiqueta de fuente; si indica "● RADIO", conecte el PGXL directamente a la computadora. El selector también necesita al menos un estado del modo de ventilador desde la conexión directa antes de aparecer.
- **El modo del ventilador cambió sin intención** — El selector ignora el desplazamiento de la rueda del ratón cuando el menú está cerrado. Si el modo cambia de todos modos, probablemente hizo clic en el selector y desplazó mientras el menú estaba abierto.

## Relacionados

- [Confirmar si la telemetría del PGXL es directa o mediante proxy a través de la radio](confirm-whether-pgxl-telemetry-is-direct-or-proxied-through-the-radio.md)
- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Poner el amplificador PGXL en STANDBY](put-the-pgxl-amplifier-in-standby.md)
