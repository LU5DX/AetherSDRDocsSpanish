# Ajuste la potencia de portadora AM para transmisión en AM

Utilice esta página para establecer el nivel de potencia de portadora AM al transmitir en modo AM. El ajuste del nivel de portadora controla cuánta potencia emite la radio como portadora AM antes de que se aplique la modulación de audio.

## Antes de comenzar

- Conecte a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Establezca el slice en modo AM antes de transmitir.

## Pasos

1. Abra el applet Phone haciendo clic en el botón **PHNE** de la bandeja en la barra lateral derecha. Si el panel del applet no es visible, haga clic en **View > Applet Panel** para mostrarlo.
2. Localice la fila **AM Carrier** en la parte superior del applet Phone.
3. Arrastre el deslizador **AM Carrier** hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia de portadora. La etiqueta numérica a la derecha del deslizador se actualiza inmediatamente para mostrar el valor actual (por ejemplo, `48`).

## Qué hace cada control

| Control               | Descripción                                        | Rango válido |
|-----------------------|----------------------------------------------------|-------------|
| Deslizador **AM Carrier** | Establece el nivel de potencia de portadora AM enviado a la radio. | 0–100       |

## Consejos

- La etiqueta numérica junto al deslizador muestra el valor actual en tiempo real. Úsela para establecer un nivel preciso sin adivinar la posición del deslizador.
- El deslizador AM Carrier no tiene una clave de configuración persistente. Su valor se lee de la radio al conectar y se restablece si se reconecta.

## Relacionado

- [Descripción general de Phone](overview.md)
- [Habilitar VOX y establecer el umbral de disparo](enable-vox-and-set-trigger-threshold.md)
- [Establezca la frecuencia de corte bajo del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establezca la frecuencia de corte alto del audio TX](set-the-tx-audio-high-cut-frequency.md)
