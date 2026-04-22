# Cambiar entre tres antenas en un TGXL 3x1

Seleccione cuál de los tres puertos de antena del conmutador 4O3A Tuner Genius XL 3x1 está activo. Esto le permite cambiar de antena sin tocar ningún conmutador físico.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Se debe detectar un Tuner Genius XL; el botón TUN en la bandeja del panel lateral derecho aparece únicamente cuando hay uno presente.
- Debe haber una conexión directa con el TGXL activa. La fila del conmutador de antenas se oculta si el TGXL no está conectado directamente o no reporta un conmutador de antenas.

## Pasos

1. Haga clic en el botón TUN de la bandeja del panel lateral derecho para abrir el applet del sintonizador.
2. Confirme que la fila de antenas es visible en la parte inferior del applet. Si la fila no aparece, la conexión directa con el TGXL no está activa o este TGXL no tiene un conmutador 3x1 — consulte la sección Antes de comenzar más arriba.
3. Haga clic en `ANT 1`, `ANT 2` o `ANT 3` para seleccionar el puerto de antena correspondiente.

## Qué hace cada control

| Etiqueta | Comportamiento |
|----------|----------------|
| `ANT 1` | Cambia el TGXL 3x1 al puerto de antena 1. |
| `ANT 2` | Cambia el TGXL 3x1 al puerto de antena 2. |
| `ANT 3` | Cambia el TGXL 3x1 al puerto de antena 3. |

La fila de antenas completa se oculta a menos que la conexión directa con el TGXL esté activa y el TGXL reporte que hay un conmutador de antenas presente.

Ninguno de estos controles tiene claves de configuración persistente; el puerto seleccionado lo mantiene el hardware del TGXL.

## Solución de problemas

- **Los botones ANT 1 / ANT 2 / ANT 3 no son visibles** — La conexión directa con el TGXL no está activa, o esta unidad TGXL no tiene instalado un conmutador 3x1. Verifique la conexión directa en la configuración de hardware de su TGXL. La fila aparece automáticamente una vez que la conexión directa está activa y el TGXL reporta un conmutador de antenas.

## Relacionados

- [Descripción general del sintonizador](overview.md)
- [Ejecutar un autosintonizado en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
