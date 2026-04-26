# Establecer la frecuencia de corte inferior del audio de TX

Use el applet Phone para subir o bajar el límite inferior del filtro de audio de TX. Reducir el extremo inferior elimina el ruido de baja frecuencia y los zumbidos en SSB y otros modos de voz.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Abra el Panel de Applets si no está visible. Si el panel está oculto, haga clic en el botón PHNE de la barra lateral derecha para mostrarlo.

## Pasos

1. Haga clic en el botón PHNE de la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **Low Cut** en la parte inferior del applet. Muestra un encabezado con la etiqueta "Low Cut" sobre una fila que contiene un indicador de valor y dos botones triangulares de paso.
3. Haga clic en `<` para disminuir la frecuencia de corte inferior en 50 Hz, o en `>` para aumentarla en 50 Hz. También puede colocar el puntero sobre el indicador de valor y desplazar la rueda del ratón para ajustar en los mismos incrementos.
4. Lea la frecuencia actual en Hz en el indicador de valor situado entre los dos botones.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| `<` (Low Cut) | — | — | Disminuye la frecuencia de corte inferior de TX en 50 Hz por clic. El mínimo es 0 Hz. |
| `>` (Low Cut) | — | — | Aumenta la frecuencia de corte inferior de TX en 50 Hz por clic. El máximo es (corte superior − 50) Hz. |
| Indicador de valor Low Cut | 50 Hz | 0 a (corte superior − 50), paso 50 Hz | Muestra la frecuencia de corte inferior actual. Admite ajuste con la rueda del ratón. |

El valor de corte inferior no se guarda en la configuración de AetherSDR; lo conserva la radio.

## Consejos

- La frecuencia de corte inferior no puede alcanzar ni superar la frecuencia de corte superior. El límite máximo siempre es 50 Hz por debajo del valor de corte superior actual. Si el botón `>` no tiene efecto, ha alcanzado ese límite.
- Un punto de partida típico para el corte inferior en SSB es 100–150 Hz, lo cual elimina el zumbido de baja frecuencia sin afectar notablemente la claridad de la voz.

## Temas relacionados

- [Establecer la frecuencia de corte superior del audio de TX](set-the-tx-audio-high-cut-frequency.md)
- [Descripción general de Phone](overview.md)
