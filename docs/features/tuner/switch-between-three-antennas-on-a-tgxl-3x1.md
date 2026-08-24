# Cambiar entre tres antenas en un TGXL 3x1

Esta página explica cómo seleccionar los puertos de antena 1, 2 o 3 en un 4O3A Tuner Genius XL con un conmutador de antenas 3x1. Úsela cuando tenga varias antenas conectadas al TGXL y necesite enrutar la radio a un puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Debe detectarse un Tuner Genius XL; el botón TUN de la bandeja aparece en la barra lateral derecha solo cuando hay un TGXL presente.
- Debe haber una conexión directa activa al TGXL. La fila del conmutador de antenas está oculta a menos que haya una conexión directa activa y el TGXL informe que hay un conmutador de antenas instalado.

## Pasos

1. Haga clic en el botón TUN de la bandeja en la barra lateral derecha para abrir el applet del sintonizador.
2. Confirme que la fila del conmutador de antenas sea visible en la parte inferior del applet. Si no es visible, el TGXL no tiene conexión directa o no tiene instalado un conmutador 3x1; consulte "Antes de comenzar" arriba.
3. Haga clic en ANT 1, ANT 2 o ANT 3 para seleccionar el puerto de antena correspondiente.

## Qué hace cada control

| Botón | Comportamiento |
|--------|----------|
| ANT 1 | Selecciona el puerto de antena 1 en el conmutador 3x1 del TGXL. |
| ANT 2 | Selecciona el puerto de antena 2 en el conmutador 3x1 del TGXL. |
| ANT 3 | Selecciona el puerto de antena 3 en el conmutador 3x1 del TGXL. |

Ninguno de estos botones tiene una clave de ajuste persistente. La selección se envía directamente al TGXL.

## Solución de problemas

- **Los botones ANT 1 / ANT 2 / ANT 3 no son visibles** — La fila del conmutador de antenas está oculta a menos que haya una conexión directa activa al TGXL y el TGXL informe que hay un conmutador de antenas. Verifique su conexión al TGXL. Si el modelo de TGXL no incluye un conmutador 3x1, estos botones nunca aparecerán.

## Relacionado

- [Descripción general del sintonizador](overview.md)
- [Ejecutar un autosintonizado en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
