# Cambiar entre tres antenas en un TGXL 3x1

Esta página explica cómo seleccionar los puertos de antena 1, 2 o 3 en un 4O3A Tuner Genius XL con conmutador de antenas 3x1. Utilice esta función cuando tenga varias antenas conectadas al TGXL y necesite enrutar el radio hacia un puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El Tuner Genius XL debe estar detectado; el botón de bandeja TUN aparece en la barra lateral derecha únicamente cuando hay un TGXL presente.
- Debe haber una conexión directa al TGXL activa. La fila del conmutador de antenas permanece oculta a menos que haya una conexión directa activa y el TGXL informe que hay un conmutador de antenas instalado.

## Pasos

1. Haga clic en el botón de bandeja TUN en la barra lateral derecha para abrir el applet del sintonizador (Tuner).
2. Confirme que la fila del conmutador de antenas es visible en la parte inferior del applet. Si no es visible, el TGXL no tiene conexión directa o no tiene instalado un conmutador 3x1 — consulte la sección Antes de comenzar más arriba.
3. Haga clic en ANT 1, ANT 2 o ANT 3 para seleccionar el puerto de antena correspondiente.

## Qué hace cada control

| Botón | Comportamiento |
|-------|----------------|
| ANT 1 | Selecciona el puerto de antena 1 en el conmutador TGXL 3x1. |
| ANT 2 | Selecciona el puerto de antena 2 en el conmutador TGXL 3x1. |
| ANT 3 | Selecciona el puerto de antena 3 en el conmutador TGXL 3x1. |

Ninguno de estos botones tiene una clave de configuración persistente. La selección se envía directamente al TGXL.

## Solución de problemas

- **Los botones ANT 1 / ANT 2 / ANT 3 no son visibles** — La fila del conmutador de antenas permanece oculta a menos que haya una conexión directa al TGXL activa y el TGXL informe la presencia de un conmutador de antenas. Verifique su conexión al TGXL. Si el modelo de TGXL no incluye un conmutador 3x1, estos botones nunca aparecerán.

## Relacionado

- [Descripción general del sintonizador](overview.md)
- [Ejecutar un ajuste automático en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
