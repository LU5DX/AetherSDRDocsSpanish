# Cambiar entre tres antenas en un TGXL 3x1

Esta página explica cómo seleccionar uno de los tres puertos de antena en un 4O3A Tuner Genius XL con conmutador de antenas 3x1. Utilice esta función cuando tenga varias antenas conectadas al TGXL y desee cambiar entre ellas desde AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- El TGXL debe estar detectado; el botón TUN en la bandeja del panel lateral derecho aparece únicamente cuando hay un Tuner Genius XL presente.
- El TGXL debe estar conectado mediante una conexión directa TGXL. La fila del conmutador de antenas se oculta cuando solo hay activa una conexión a través del radio.
- El TGXL debe reportar un conmutador de antenas (los modelos sin conmutador 3x1 nunca exponen los puertos de antena).

## Pasos

1. Haga clic en el botón TUN de la bandeja en el panel lateral derecho para abrir el applet del sintonizador.
2. Confirme que la fila del conmutador de antenas es visible en la parte inferior del applet. Si no está visible, consulte "Antes de comenzar" más arriba.
3. Haga clic en `ANT 1`, `ANT 2` o `ANT 3` para seleccionar el puerto de antena correspondiente en el conmutador TGXL 3x1.

## Qué hace cada control

| Control | Comportamiento |
|---------|----------------|
| `ANT 1` | Selecciona el puerto de antena 1 en el conmutador TGXL 3x1. |
| `ANT 2` | Selecciona el puerto de antena 2 en el conmutador TGXL 3x1. |
| `ANT 3` | Selecciona el puerto de antena 3 en el conmutador TGXL 3x1. |

Ninguno de estos controles tiene una clave de configuración persistente. La selección se envía directamente al TGXL.

## Consejos

- La fila del conmutador de antenas se oculta automáticamente cuando la conexión directa TGXL no está activa o cuando el modelo de TGXL conectado no incluye el conmutador 3x1. Si no puede ver `ANT 1`, `ANT 2` o `ANT 3`, verifique su conexión directa al TGXL.
- El puerto de antena activo es rastreado por el TGXL. AetherSDR lee el valor reportado en el momento de la conexión y resalta la selección actual en consecuencia.

## Solución de problemas

- **Los botones ANT 1 / ANT 2 / ANT 3 no aparecen** — La fila del conmutador de antenas solo se muestra cuando hay una conexión directa TGXL activa y el TGXL reporta que hay un conmutador de antenas presente. Verifique que su TGXL esté conectado directamente (no solo a través del radio) y que su modelo de TGXL incluya la opción de conmutador 3x1.
- **Al hacer clic en un botón de antena no se produce ningún efecto** — El comando se envía únicamente cuando hay una conexión directa establecida. Si el applet TUN está abierto pero la fila apareció de forma inesperada, es posible que la conexión se haya interrumpido. Cierre y vuelva a abrir el applet para verificar el estado de la conexión.

## Relacionados

- [Descripción general del sintonizador](overview.md)
- [Ejecutar un autosintonizado en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
