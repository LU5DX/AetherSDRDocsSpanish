# Ajustar la potencia de portadora AM para transmitir en AM

Use esta página para configurar el nivel de potencia de portadora AM al transmitir en modo AM. Ajustar el nivel de portadora controla cuánta potencia emite el radio como portadora AM antes de que se aplique la modulación de audio.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone requiere una conexión activa al radio.
- Configure el slice en modo AM antes de transmitir.

## Pasos

1. Abra el applet Phone haciendo clic en el botón **PHNE** de la bandeja en la barra lateral derecha. Si el panel del applet no está visible, haga clic en **View > Applet Panel** para mostrarlo.
2. Ubique la fila **AM Carrier** en la parte superior del applet Phone.
3. Arrastre el control deslizante **AM Carrier** hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia de portadora. La etiqueta numérica a la derecha del control se actualiza inmediatamente para mostrar el valor actual (por ejemplo, `48`). Mientras arrastra, la información sobre herramientas muestra el valor como porcentaje (por ejemplo, `48%`).

## Qué hace cada control

| Control                        | Descripción                                                                                                                                   | Rango válido                    |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------|
| Control deslizante **AM Carrier** | Establece el nivel de potencia de portadora AM enviado al radio. Arrastre para ajustar; la información sobre herramientas muestra el porcentaje. | 0–100                           |
| Botón **VOX**                  | Activa o desactiva la transmisión activada por voz.                                                                                           | —                               |
| Control deslizante **VOX level** | Establece el umbral de activación de VOX. Arrastre para ajustar; la información sobre herramientas muestra el porcentaje.                     | 0–100                           |
| Control deslizante **Delay**   | Establece el tiempo de retención de VOX antes de volver a recepción.                                                                           | 0–100                           |
| Botón **DEXP**                 | Activa o desactiva el expansor descendente (puerta de ruido). Se almacena como `DexpEnabled`.                                                 | —                               |
| Control deslizante **DEXP threshold** | Establece el umbral de puerta de DEXP. Se almacena como `DexpLevel`. Valor predeterminado: 0. Arrastre para ajustar; la información sobre herramientas muestra el porcentaje. | 0–100                           |
| **Low Cut < / >**              | Ajusta la frecuencia de corte bajo del filtro de TX. Los botones de paso se mueven en incrementos de 50 Hz usando el rango informado por el modelo; doble clic para escribir un valor exacto. Valor predeterminado: 50 Hz. | 0 a (corte alto − 50), paso de 50 Hz |
| **High Cut < / >**             | Ajusta la frecuencia de corte alto del filtro de TX. Los botones de paso se mueven en incrementos de 50 Hz usando el rango informado por el modelo; doble clic para escribir un valor exacto. Valor predeterminado: 3300 Hz. | (corte bajo + 50) a 10000, paso de 50 Hz |

## Cómo funciona el paso de Low Cut y High Cut

Los botones **Low Cut < / >** y **High Cut < / >** ajustan la frecuencia del filtro al siguiente múltiplo de 50 Hz en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el valor actual de corte bajo es 87 Hz en un radio que acepta valores continuos, hacer clic en `>` lo establece en 100 Hz y hacer clic en `<` lo establece en 50 Hz. También puede ajustar cualquiera de los controles con la rueda del mouse.

Algunos radios publican una lista discreta de frecuencias de borde válidas. Cuando el radio proporciona dicha lista, los botones de paso se mueven al valor válido más cercano en la dirección elegida en lugar de a un múltiplo de 50 Hz. El comportamiento de paso es una conveniencia de la interfaz; el radio es quien finalmente aplica los límites reales.

## Entrada numérica directa para Low Cut y High Cut

A partir de la v26.8.4, puede hacer doble clic en la etiqueta de valor de **Low Cut** o **High Cut** para escribir una frecuencia exacta en Hz en lugar de ajustarla de 50 Hz en 50 Hz:

1. Haga doble clic en la etiqueta de valor de **Low Cut** o **High Cut**.
2. Escriba la frecuencia deseada en Hz.
3. Presione Enter para aplicar el valor.

Los valores escritos se validan contra el rango actual del modelo y se **rechazan** (no se limitan) si están fuera de rango. Por ejemplo, escribir un valor de corte bajo igual o superior al corte alto actual menos el ancho mínimo del filtro se ignora y se restaura el valor anterior. En radios que publican una lista discreta de bordes, los valores escritos deben estar presentes en dicha lista para ser aceptados.

Este comportamiento difiere deliberadamente de los botones de paso: un paso es una solicitud para moverse un incremento, por lo que detenerse en un límite es razonable; un número escrito es una solicitud de ese valor exacto, por lo que se acepta o se rechaza por completo.

## Consejos

- La etiqueta numérica junto al control deslizante **AM Carrier** muestra el valor actual en tiempo real. Úsela para configurar un nivel preciso sin adivinar la posición del control.
- El control deslizante **AM Carrier** no tiene una clave de configuración persistente. Su valor se lee del radio al conectar y se restablece si se vuelve a conectar.
- Debido a que **Low Cut** y **High Cut** se ajustan a límites válidos, hacer clic una vez desde un valor fuera de la cuadrícula (por ejemplo, un valor no divisible por 50) primero alineará el valor al límite más cercano antes de continuar con el paso en la dirección esperada.
- El applet Phone ahora admite temas. Su apariencia se adapta automáticamente al tema seleccionado, lo que afecta los colores de etiquetas, controles deslizantes y botones.
- Los controles **DEXP** ya no guardan configuraciones en el disco. Su estado se comunica directamente al radio y se restablece al reconectar.

## Relacionado

- [Phone overview](overview.md)
- [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md)
- [Set the TX audio low-cut frequency](set-the-tx-audio-low-cut-frequency.md)
- [Set the TX audio high-cut frequency](set-the-tx-audio-high-cut-frequency.md)
