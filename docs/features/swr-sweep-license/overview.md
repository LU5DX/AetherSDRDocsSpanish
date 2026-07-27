# Barrido de ROE de Antena — Confirmación de Licencia

La Confirmación de Licencia para Barrido de ROE de Antena es un diálogo modal que aparece antes del primer barrido de ROE de antena de cada sesión. Muestra un aviso de responsabilidad del operador y requiere que reconozca sus obligaciones de licencia antes de continuar. Una casilla "Recordar mi respuesta" le permite omitir el diálogo en futuros barridos dentro de la misma sesión.

## Cómo funciona

El diálogo se muestra automáticamente cuando inicia un Barrido de ROE de Antena (a través del menú contextual del panadapter o la acción de barrido de ROE en la Ventana Principal). Si previamente marcó la casilla "Recordar mi respuesta" y confirmó, el diálogo se omite por completo y el barrido comienza inmediatamente.

La función auxiliar estática `confirm()` maneja la lógica: verifica la configuración persistente, muestra el diálogo si es necesario, guarda su preferencia cuando la casilla está marcada y devuelve `true` (proceder con el barrido) o `false` (cancelar).

El diálogo usa una geometría única — no recuerda la posición de la ventana entre apariciones.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de configuración |
---|---|---|---|
| *Texto de aviso* | Indicador (QLabel con texto enriquecido) | Muestra la advertencia de responsabilidad del operador sobre no interferir con otro tráfico, cumplimiento de licencia y riesgos de barridos no supervisados. Tiene fondo naranja (`#2a1a10`). | Ninguna |
| Recordar mi respuesta | Casilla | Cuando está marcada, guarda su confirmación para que el diálogo se omita en barridos posteriores de esta sesión. | `SwrSweepLicenseConfirmed` |
| Tengo licencia para usar esta función | Botón pulsador | Acepta el aviso y procede al barrido de ROE. Estilizado como botón azul principal y configurado como botón predeterminado (tecla Enter). | Ninguna |
| Cancelar | Botón pulsador | Rechaza el aviso y cancela el barrido. | Ninguna |

## Relacionados

- [Confirmar responsabilidad del operador antes de ejecutar el barrido de ROE de antena](confirm-operator-responsibility-before-running-the-antenna-swr-sweep.md)
- [Recuerda la confirmación para que el diálogo no aparezca en barridos posteriores](remembers-confirmation-so-the-dialog-does-not-show-on-subsequent-sweeps.md)
