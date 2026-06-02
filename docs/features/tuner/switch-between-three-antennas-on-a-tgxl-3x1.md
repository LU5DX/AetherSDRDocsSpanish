# Conmutar entre tres antenas en un TGXL 3×1

Esta página explica cómo seleccionar los puertos de antena 1, 2 o 3 en un 4O3A Tuner Genius XL con un conmutador de antena de 3×1. Úselo cuando tenga varias antenas conectadas al TGXL y necesite enrutar la radio a un puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Debe detectarse un Tuner Genius XL; el botón TUN de la bandeja aparece en la barra lateral derecha solo cuando hay un TGXL presente.
- Debe haber una conexión directa activa con el TGXL. La fila del conmutador de antena está oculta a menos que haya una conexión directa activa y el TGXL informe que hay un conmutador de antena presente.

## Pasos

1. Haga clic en el botón TUN de la bandeja en la barra lateral derecha para abrir el applet del sintonizador.
2. Confirme que la fila del conmutador de antena sea visible en la parte inferior del applet. Si no es visible, el TGXL no tiene conexión directa o no tiene instalado un conmutador 3×1; consulte Antes de comenzar más arriba.
3. Haga clic en ANT 1, ANT 2 o ANT 3 para seleccionar el puerto de antena correspondiente.

## Funciones de cada control

| Botón | Comportamiento |
|-------|----------------|
| ANT 1 | Selecciona el puerto de antena 1 en el conmutador TGXL 3×1. |
| ANT 2 | Selecciona el puerto de antena 2 en el conmutador TGXL 3×1. |
| ANT 3 | Selecciona el puerto de antena 3 en el conmutador TGXL 3×1. |

Ninguno de estos botones tiene una clave de ajuste persistente. La selección se envía directamente al TGXL.

## Solución de problemas

- **Los botones ANT 1 / ANT 2 / ANT 3 no son visibles** — La fila del conmutador de antena está oculta a menos que haya una conexión directa activa con el TGXL y el TGXL informe que hay un conmutador de antena. Verifique su conexión con el TGXL. Si el modelo de TGXL no incluye un conmutador 3×1, estos botones nunca aparecerán.

## Relacionado

- [Resumen del sintonizador](overview.md)
- [Ejecutar un autoajuste en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
