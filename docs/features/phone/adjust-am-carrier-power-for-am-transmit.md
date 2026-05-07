# Ajustar la potencia de portadora AM para transmisión en AM

Use esta página para configurar el nivel de potencia de portadora AM al transmitir en modo AM. Ajustar el nivel de portadora controla cuánta potencia emite el radio como portadora AM antes de que se aplique la modulación de audio.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone requiere una conexión activa al radio.
- Configure el slice en modo AM antes de transmitir.

## Pasos

1. Abra el applet Phone haciendo clic en el botón de la bandeja **PHNE** en la barra lateral derecha. Si el panel del applet no está visible, haga clic en **View > Applet Panel** para mostrarlo.
2. Localice la fila **AM Carrier** en la parte superior del applet Phone.
3. Arrastre el deslizador **AM Carrier** hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia de portadora. La etiqueta numérica a la derecha del deslizador se actualiza inmediatamente para mostrar el valor actual (por ejemplo, `48`).

## Función de cada control

| Control               | Descripción                                        | Rango válido |
|-----------------------|----------------------------------------------------|--------------|
| Deslizador **AM Carrier** | Establece el nivel de potencia de portadora AM enviado al radio. | 0–100 |
| Botón **VOX** | Activa o desactiva la transmisión por voz. | — |
| Deslizador **VOX level** | Establece el umbral de activación de VOX. | 0–100 |
| Deslizador **Delay** | Establece el tiempo de retención de VOX antes de volver a recepción. | 0–100 |
| Botón **DEXP** | Activa o desactiva el expansor descendente (puerta de ruido). Se almacena como `DexpEnabled`. Consulte la nota a continuación. | — |
| Deslizador **DEXP threshold** | Establece el umbral de la puerta DEXP. Se almacena como `DexpLevel`. Valor predeterminado: 0. Consulte la nota a continuación. | 0–100 |
| **Low Cut < / >** | Ajusta la frecuencia de corte bajo del filtro TX en pasos de 50 Hz, fijándose al múltiplo de 50 Hz más cercano en la dirección elegida. Valor predeterminado: 50 Hz. | 0 a (corte alto − 50) |
| **High Cut < / >** | Ajusta la frecuencia de corte alto del filtro TX en pasos de 50 Hz, fijándose al múltiplo de 50 Hz más cercano en la dirección elegida. Valor predeterminado: 3300 Hz. | (corte bajo + 50) a 10000 |

> **Nota — Limitación de firmware DEXP:** El conmutador **DEXP** y el deslizador **DEXP threshold** no son funcionales en la versión de firmware v1.4.0.0. El radio devuelve el error `0x5000002D` cuando se utilizan estos controles.

## Cómo funciona el ajuste de Low Cut y High Cut

A partir de la versión v0.9.5.1, los botones **Low Cut < / >** y **High Cut < / >** fijan la frecuencia del filtro al siguiente múltiplo de 50 Hz en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el valor actual de corte bajo es 87 Hz, hacer clic en `>` lo establece en 100 Hz y hacer clic en `<` lo establece en 50 Hz. También puede ajustar cualquiera de los controles con la rueda del ratón. El radio acepta cualquier valor entero en Hz; el comportamiento de fijación es solo una conveniencia de la interfaz de usuario.

## Consejos

- La etiqueta numérica junto al deslizador **AM Carrier** muestra el valor actual en tiempo real. Úsela para establecer un nivel preciso sin adivinar la posición del deslizador.
- El deslizador **AM Carrier** no tiene una clave de configuración persistente. Su valor se lee del radio al conectarse y se restablece si se vuelve a conectar.
- Debido a que **Low Cut** y **High Cut** ahora se fijan a múltiplos de 50 Hz, al hacer clic una vez desde un valor fuera de la cuadrícula (por ejemplo, un valor no divisible por 50), primero se alineará al límite más cercano antes de continuar avanzando en la dirección esperada.

## Relacionado

- [Phone overview](overview.md)
- [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md)
- [Set the TX audio low-cut frequency](set-the-tx-audio-low-cut-frequency.md)
- [Set the TX audio high-cut frequency](set-the-tx-audio-high-cut-frequency.md)
