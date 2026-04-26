# Activar el ATU interno

Use el sintonizador de antena automático (ATU) interno para encontrar la mejor adaptación de impedancia para su antena en la frecuencia actual. Esto reduce el ROE y protege los transistores finales antes de operar.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet TX Controls requiere una conexión de radio activa.
- Su radio debe tener un ATU interno instalado y habilitado. Los controles ATU y MEM se deshabilitan cuando un amplificador TGXL está en modo OPERATE.
- Configure el nivel de potencia de la portadora de sintonía antes de comenzar. Se recomienda un nivel de potencia bajo (valor predeterminado 10) para el ciclo de sintonía.

## Pasos

1. Haga clic en el botón TX del área de notificación en la barra lateral derecha para abrir el applet TX Controls si no está visible.
2. Verifique el control deslizante **Tune Pwr**. El valor predeterminado es 10. Ajústelo si es necesario antes de sintonizar.
3. Haga clic en **ATU**.

La radio inicia inmediatamente su ciclo de sintonía ATU. Observe los tres indicadores de estado del ATU:

- **Success** se ilumina en verde cuando el sintonizador encuentra una adaptación aceptable.
- **Byp** se ilumina en naranja si el ATU entra en modo bypass o bypass manual.
- **Mem** se ilumina en verde si el sintonizador aplicó una memoria almacenada en lugar de realizar un barrido completo.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| ATU | Botón | — | Inicia el ciclo de sintonía del ATU interno. Deshabilitado cuando el TGXL está en modo OPERATE. |
| MEM | Botón alternante | — | Activa o desactiva la recuperación de memoria del ATU. Deshabilitado cuando el TGXL está en modo OPERATE. |
| Tune Pwr | Control deslizante | 10 | Establece el nivel de potencia de la portadora de sintonía durante la sintonización. Rango 0–100. |
| Success | Indicador | apagado | Se ilumina en verde cuando el estado del ATU es Successful u OK. |
| Byp | Indicador | apagado | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass. |
| Mem | Indicador | apagado | Se ilumina en verde cuando el ATU utiliza una memoria almacenada. |

## Sugerencias

- Si cambia de banda o se desplaza significativamente en frecuencia, haga clic en **ATU** nuevamente para re-sintonizar. Una adaptación almacenada de una frecuencia distante puede no ser óptima.
- Para permitir que la radio reutilice adaptaciones almacenadas previamente sin ejecutar un barrido de sintonía completo cada vez, habilite **MEM** antes de hacer clic en **ATU**.

## Solución de problemas

- **Los botones ATU y MEM aparecen atenuados** — Un amplificador TGXL está conectado y se encuentra en modo OPERATE. Saque el TGXL del modo OPERATE antes de usar el ATU.
- **Byp se ilumina en naranja después de sintonizar** — El ATU no pudo encontrar una adaptación dentro de su rango y se ha puesto en bypass. Revise el sistema de antena y el cable coaxial en busca de fallas y vuelva a intentarlo.

## Relacionados

- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Configurar la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Iniciar una portadora de sintonía para verificar el ROE](start-a-tune-carrier-to-check-swr.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
