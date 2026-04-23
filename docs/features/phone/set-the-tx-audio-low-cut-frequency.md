# Configurar la frecuencia de corte inferior del audio TX

Use esta página para subir o bajar el límite de corte inferior del filtro de audio TX en el applet Phone. Ajustar el corte inferior elimina ruido de vibración, ruido de respiración o interferencias de baja frecuencia del audio transmitido.

## Antes de comenzar

- Conéctese a una radio Flex. El applet Phone requiere una conexión de radio activa.
- Confirme que el applet Phone sea visible en el Panel de Applets. Si no lo está, haga clic en el botón PHNE de la barra lateral derecha.

## Pasos

1. Localice el spinbox **Low Cut** en el applet Phone. Aparece como un encabezado con la etiqueta "Low Cut" sobre una fila de controles que muestra un botón `<`, un valor de frecuencia y un botón `>`.
2. Haga clic en `<` para disminuir la frecuencia de corte inferior en 50 Hz, o haga clic en `>` para aumentarla en 50 Hz.
3. Alternativamente, coloque el puntero del mouse sobre la etiqueta del valor de frecuencia y gire la rueda del mouse para incrementar o decrementar el valor en 50 Hz.
4. Confirme que el valor mostrado refleje la frecuencia deseada.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| `<` (Low Cut) | — | — | Disminuye el corte inferior del filtro TX en 50 Hz por clic. |
| `>` (Low Cut) | — | — | Aumenta el corte inferior del filtro TX en 50 Hz por clic. |
| Indicador del valor de corte inferior | 50 Hz | 0 Hz hasta (corte superior − 50 Hz), paso de 50 Hz | Muestra la frecuencia de corte inferior actual del filtro TX en Hz. También responde a la rueda del mouse. |

## Consejos

- El valor de corte inferior no puede igualar ni superar el valor de corte superior actual. El límite máximo es siempre el ajuste de corte superior actual menos 50 Hz.
- Para eliminar más contenido de baja frecuencia — por ejemplo, para reducir las vibraciones del soporte del micrófono en SSB — aumente el valor de corte inferior hacia 200–300 Hz.

## Relacionados

- [Configurar la frecuencia de corte superior del audio TX](set-the-tx-audio-high-cut-frequency.md)
- [Descripción general del applet Phone](overview.md)
