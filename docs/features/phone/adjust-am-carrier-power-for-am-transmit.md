# Ajustar la potencia de portadora AM para transmisión en AM

Use esta página para establecer el nivel de potencia de la portadora AM al transmitir en modo AM. Ajustar el nivel de portadora controla cuánta potencia emite el radio como portadora AM antes de que se aplique la modulación de audio.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Configure el slice en modo AM antes de transmitir.

## Pasos

1. Abra el applet Phone haciendo clic en el botón de bandeja **PHNE** en la barra lateral derecha. Si el panel del applet no está visible, haga clic en **View > Applet Panel** para mostrarlo.
2. Ubique la fila **AM Carrier** en la parte superior del applet Phone.
3. Arrastre el control deslizante **AM Carrier** hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia de la portadora. La etiqueta numérica a la derecha del control deslizante se actualiza de inmediato para mostrar el valor actual (por ejemplo, `48`).

## Qué hace cada control

| Control | Descripción | Rango válido | Valor predeterminado |
|---|---|---|---|
| Control deslizante **AM Carrier** | Establece el nivel de potencia de la portadora AM enviado al radio. | 0–100 | Sin valor almacenado; refleja el estado del radio |

## Consejos

- La etiqueta numérica junto al control deslizante muestra el valor actual en tiempo real. Úsela para establecer un nivel preciso sin necesidad de adivinar la posición del control deslizante.
- El control deslizante AM Carrier no tiene una clave de configuración persistente. Su valor se lee del radio al conectarse y se restablece si vuelve a conectarse.

## Relacionado

- [Descripción general de Phone](overview.md)
- [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Establecer la frecuencia de corte inferior del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte superior del audio TX](set-the-tx-audio-high-cut-frequency.md)
