# Cambiar entre tres antenas en un TGXL 3x1

Esta página explica cómo seleccionar los puertos de antena 1, 2 o 3 en un 4O3A Tuner Genius XL con un conmutador de antenas 3x1. Utilice esto cuando tenga varias antenas conectadas al TGXL y necesite enrutar la radio a un puerto específico.

## Antes de empezar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Se debe detectar un Tuner Genius XL; el botón de la bandeja TUN aparece en la barra lateral derecha solo cuando hay un TGXL presente.
- Debe haber una conexión directa activa al TGXL. La fila del conmutador de antenas está oculta a menos que haya una conexión directa activa y el TGXL informe que hay un conmutador de antenas presente.

## Pasos

1. Haga clic en el botón de la bandeja TUN en la barra lateral derecha para abrir el applet del sintonizador.
2. Confirme que la fila del conmutador de antenas es visible en la parte inferior del applet. Si no es visible, el TGXL no tiene una conexión directa o no tiene un conmutador 3x1 instalado; consulte Antes de empezar arriba.
3. Haga clic en ANT 1, ANT 2 o ANT 3 para seleccionar el puerto de antena correspondiente.

## Qué hace cada control

| Botón | Comportamiento |
|--------|----------|
| ANT 1 | Selecciona el puerto de antena 1 en el conmutador 3x1 del TGXL. |
| ANT 2 | Selecciona el puerto de antena 2 en el conmutador 3x1 del TGXL. |
| ANT 3 | Selecciona el puerto de antena 3 en el conmutador 3x1 del TGXL. |

Ninguno de estos botones tiene una clave de configuración persistida. La selección se envía directamente al TGXL.

## Solución de problemas

- **Los botones ANT 1 / ANT 2 / ANT 3 no son visibles** — La fila del conmutador de antenas está oculta a menos que haya una conexión directa activa al TGXL y el TGXL informe que hay un conmutador de antenas. Verifique su conexión al TGXL. Si el modelo del TGXL no incluye un conmutador 3x1, estos botones nunca aparecerán.

## Relacionado

- [Resumen del sintonizador](overview.md)
- [Ejecutar un autoajuste en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
