# Ajustar la potencia de portadora AM para transmisión en AM

Use esta página para establecer el nivel de potencia de portadora AM al transmitir en modo AM. El nivel de portadora controla qué proporción de la potencia del transmisor se destina a la portadora sin modular.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- La radio debe estar configurada en modo AM antes de que el nivel de portadora AM tenga algún efecto en la transmisión.
- El applet Phone debe estar visible en el Panel de Applets.

## Pasos

1. Si el applet Phone no está visible, haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para mostrarlo.
2. Localice el control deslizante **AM Carrier** en el applet Phone.
3. Arrastre el control deslizante **AM Carrier** hacia la izquierda o la derecha para establecer el nivel de portadora deseado. El valor numérico (0–100) se actualiza junto al control deslizante mientras arrastra.

## Qué hace cada control

| Control | Tipo | Rango | Valor predeterminado | Clave persistente |
|---|---|---|---|---|
| AM Carrier | Deslizador | 0–100 | — | — |

La etiqueta numérica a la derecha del control deslizante **AM Carrier** muestra el valor actual (por ejemplo, `48`). Este valor se envía directamente a la radio y AetherSDR no lo guarda entre sesiones; la radio lo restaura desde su propio estado al reconectarse.

## Consejos

- El nivel de portadora AM se aplica únicamente mientras la radio está en modo AM. Ajustarlo en otros modos no produce ningún efecto audible, pero el valor se sigue enviando a la radio.
- Un nivel de portadora de 0 suprime la portadora por completo; un nivel de 100 establece la potencia de portadora máxima permitida por la configuración de banda TX de la radio.

## Relacionado

- [Descripción general de Phone](overview.md)
- [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Establecer la frecuencia de corte inferior del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte superior del audio TX](set-the-tx-audio-high-cut-frequency.md)
