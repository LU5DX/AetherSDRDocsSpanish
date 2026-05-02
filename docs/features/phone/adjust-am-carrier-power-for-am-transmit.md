# Ajustar la potencia de portadora AM para transmisión en AM

Use esta página para establecer el nivel de potencia de portadora AM al transmitir en modo AM. Ajustar el nivel de portadora controla cuánta potencia emite el radio como portadora AM antes de que se aplique la modulación de audio.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Configure el slice en modo AM antes de transmitir.

## Pasos

1. Abra el applet Phone haciendo clic en el botón de bandeja **PHNE** en la barra lateral derecha. Si el panel de applets no está visible, haga clic en **View > Applet Panel** para mostrarlo.
2. Localice la fila **AM Carrier** en la parte superior del applet Phone.
3. Arrastre el control deslizante **AM Carrier** hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia de portadora. La etiqueta numérica a la derecha del control deslizante se actualiza inmediatamente para mostrar el valor actual (por ejemplo, `48`).

## Qué hace cada control

| Control                        | Descripción                                                          | Rango válido              |
|-------------------------------|----------------------------------------------------------------------|---------------------------|
| Control deslizante **AM Carrier** | Establece el nivel de potencia de portadora AM enviado al radio.  | 0–100                     |
| Botón **VOX**                 | Activa o desactiva la transmisión controlada por voz.                | —                         |
| Control deslizante **VOX level** | Establece el umbral de activación del VOX.                        | 0–100                     |
| Control deslizante **Delay**  | Establece el tiempo de retardo del VOX antes de volver a recepción.  | 0–100                     |
| Botón **DEXP**                | Activa o desactiva el expansor descendente (puerta de ruido). Se almacena como `DexpEnabled`. Vea la nota a continuación. | — |
| Control deslizante **DEXP threshold** | Establece el umbral de la puerta DEXP. Se almacena como `DexpLevel`. Valor predeterminado: 0. Vea la nota a continuación. | 0–100 |
| **Low Cut < / >**             | Ajusta la frecuencia de corte inferior del filtro TX en pasos de 50 Hz, ajustándose al múltiplo de 50 Hz más cercano en la dirección elegida. Valor predeterminado: 50 Hz. | 0 hasta (corte superior − 50) |
| **High Cut < / >**            | Ajusta la frecuencia de corte superior del filtro TX en pasos de 50 Hz, ajustándose al múltiplo de 50 Hz más cercano en la dirección elegida. Valor predeterminado: 3300 Hz. | (corte inferior + 50) hasta 10000 |

> **Nota — Limitación de firmware en DEXP:** El botón **DEXP** y el control deslizante **DEXP threshold** no son funcionales en el firmware v1.4.0.0. El radio devuelve el error `0x5000002D` cuando se utilizan estos controles.

## Cómo funciona el avance en pasos de Low Cut y High Cut

A partir de la versión v0.9.5.1, los botones **Low Cut < / >** y **High Cut < / >** ajustan la frecuencia del filtro al siguiente múltiplo de 50 Hz en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el valor actual de corte inferior es 87 Hz, hacer clic en `>` lo establece en 100 Hz y hacer clic en `<` lo establece en 50 Hz. También puede ajustar cualquiera de los dos controles con la rueda del ratón. El radio acepta cualquier valor entero en Hz; el ajuste por pasos es únicamente una conveniencia de la interfaz.

## Consejos

- La etiqueta numérica junto al control deslizante **AM Carrier** muestra el valor actual en tiempo real. Úsela para establecer un nivel preciso sin tener que adivinar la posición del control deslizante.
- El control deslizante AM Carrier no tiene una clave de configuración persistente. Su valor se lee del radio al conectarse y se restablece si vuelve a conectarse.
- Dado que **Low Cut** y **High Cut** ahora se ajustan a múltiplos de 50 Hz, hacer clic una vez desde un valor fuera de la cuadrícula (por ejemplo, un valor no divisible entre 50) primero alineará al límite más cercano antes de continuar avanzando en la dirección esperada.

## Relacionados

- [Descripción general de Phone](overview.md)
- [Activar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Establecer la frecuencia de corte inferior del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte superior del audio TX](set-the-tx-audio-high-cut-frequency.md)
