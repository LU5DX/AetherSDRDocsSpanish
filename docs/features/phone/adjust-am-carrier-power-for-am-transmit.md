# Ajustar la potencia de la portadora AM para transmisión AM

Utilice esta página para configurar el nivel de potencia de la portadora AM al transmitir en modo AM. Ajustar el nivel de la portadora controla cuánta potencia emite el radio como portadora AM antes de aplicar la modulación de audio.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone requiere una conexión activa con el radio.
- Configure el slice en modo AM antes de transmitir.

## Pasos

1. Abra el applet Phone haciendo clic en el botón de la bandeja **PHNE** en la barra lateral derecha. Si el panel del applet no está visible, haga clic en **View > Applet Panel** para mostrarlo.
2. Localice la fila **AM Carrier** en la parte superior del applet Phone.
3. Arrastre el control deslizante **AM Carrier** hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia de la portadora. La etiqueta numérica a la derecha del control deslizante se actualiza inmediatamente para mostrar el valor actual (por ejemplo, `48`). Mientras arrastra, la información sobre herramientas muestra el valor como un porcentaje (por ejemplo, `48%`).

## Qué hace cada control

| Control               | Descripción                                        | Rango válido |
|-----------------------|----------------------------------------------------|-------------|
| Control deslizante **AM Carrier** | Establece el nivel de potencia de la portadora AM enviado al radio. Arrastre para ajustar; la información sobre herramientas muestra el porcentaje. | 0–100       |
| Botón **VOX** | Activa o desactiva la transmisión por voz. | — |
| Control deslizante **VOX level** | Establece el umbral de activación de VOX. Arrastre para ajustar; la información sobre herramientas muestra el porcentaje. | 0–100 |
| Control deslizante **Delay** | Establece el tiempo de retención de VOX antes de volver a recepción. | 0–100 |
| Botón **DEXP** | Activa o desactiva el expansor descendente (puerta de ruido). Se almacena como `DexpEnabled`. Consulte la nota a continuación. | — |
| Control deslizante **DEXP threshold** | Establece el umbral de la puerta DEXP. Se almacena como `DexpLevel`. Valor predeterminado: 0. Arrastre para ajustar; la información sobre herramientas muestra el porcentaje. Consulte la nota a continuación. | 0–100 |
| **Low Cut < / >** | Ajusta la frecuencia de corte bajo del filtro TX en pasos de 50 Hz, fijándola al múltiplo de 50 Hz más cercano en la dirección elegida. Valor predeterminado: 50 Hz. | 0 a (corte alto − 50) |
| **High Cut < / >** | Ajusta la frecuencia de corte alto del filtro TX en pasos de 50 Hz, fijándola al múltiplo de 50 Hz más cercano en la dirección elegida. Valor predeterminado: 3300 Hz. | (corte bajo + 50) a 10000 |

> **Nota — Limitación de firmware DEXP:** La activación/desactivación de **DEXP** y el control deslizante **DEXP threshold** no funcionan en la versión de firmware v1.4.0.0. El radio devuelve el error `0x5000002D` cuando se utilizan estos controles.

## Cómo funciona el ajuste de Low Cut y High Cut

A partir de la versión v0.9.5.1, los botones **Low Cut < / >** y **High Cut < / >** fijan la frecuencia del filtro al siguiente múltiplo de 50 Hz en la dirección elegida, en lugar de sumar o restar 50 Hz fijos al valor actual. Por ejemplo, si el valor actual de corte bajo es 87 Hz, al hacer clic en `>` se establece en 100 Hz y al hacer clic en `<` se establece en 50 Hz. También puede ajustar cualquiera de los controles con la rueda del ratón. El radio acepta cualquier valor entero en Hz; el comportamiento de fijación es solo una comodidad de la interfaz.

## Consejos

- La etiqueta numérica junto al control deslizante **AM Carrier** muestra el valor actual en tiempo real. Úsela para establecer un nivel preciso sin adivinar la posición del control deslizante.
- El control deslizante AM Carrier no tiene una clave de configuración persistente. Su valor se lee del radio al conectarse y se restablece si se reconecta.
- Debido a que **Low Cut** y **High Cut** ahora se fijan a múltiplos de 50 Hz, al hacer clic una vez desde un valor fuera de la cuadrícula (por ejemplo, un valor no divisible por 50), primero se alineará con el límite más cercano antes de continuar avanzando en la dirección esperada.
- El applet Phone ahora es compatible con temas. Su apariencia se adapta automáticamente al tema seleccionado, afectando los colores de etiquetas, controles deslizantes y botones.

## Relacionados

- [Descripción general de Phone](overview.md)
- [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Establecer la frecuencia de corte bajo del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte alto del audio TX](set-the-tx-audio-high-cut-frequency.md)
