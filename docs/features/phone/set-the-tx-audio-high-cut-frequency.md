# Configurar la frecuencia de corte alto del audio de TX

Utilice el applet Phone para aumentar o disminuir el límite superior de la banda de paso del audio de TX. Reducir el corte alto reduce el ancho de banda transmitido; aumentarlo permite pasar más contenido de audio de alta frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone requiere una conexión activa con la radio.
- La radio debe estar en un modo de telefonía (SSB, AM o similar) para que los cambios en el filtro de TX tengan efecto audible.

## Pasos

1. Si el applet Phone no está visible, haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para mostrarlo.
2. Localice la columna **High Cut** en el lado derecho de la sección del filtro de TX, debajo de la fila DEXP.
3. Haga clic en **>** para aumentar la frecuencia de corte alto al siguiente múltiplo de 50 Hz, o haga clic en **<** para disminuirla al siguiente múltiplo inferior de 50 Hz. También puede usar la rueda del ratón sobre la pantalla de valor para avanzar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los botones **<** y **>**.

## Qué hace cada control

| Control                | Descripción                                                                                      | Valor por defecto |
|------------------------|--------------------------------------------------------------------------------------------------|-------------------|
| **High Cut `<`**       | Disminuye la frecuencia de corte alto del filtro de TX al siguiente múltiplo inferior de 50 Hz. | —                 |
| **High Cut `>`**       | Aumenta la frecuencia de corte alto del filtro de TX al siguiente múltiplo superior de 50 Hz.  | —                 |
| Pantalla de valor High Cut | Muestra la frecuencia de corte alto actual en Hz.                                            | 3300 Hz           |

La frecuencia de corte alto no puede establecerse por debajo de la frecuencia de corte bajo actual más 50 Hz. Por ejemplo, si el corte bajo está configurado a 100 Hz, el valor mínimo del corte alto es 150 Hz.

## Cómo funciona el ajuste paso a paso

Los botones **<** y **>** ajustan el valor al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el corte alto actual es 3275 Hz, al hacer clic en **>** se establece en 3300 Hz y al hacer clic en **<** se establece en 3250 Hz. Este comportamiento se aplica igualmente a los controles **Low Cut**.

La radio acepta cualquier valor entero en Hz, por lo que si el valor actual ya es un múltiplo exacto de 50 Hz, el resultado es el mismo que un paso simple de 50 Hz.

## Consejos

- Para cambios más grandes, use la rueda del ratón con movimiento rápido en lugar de hacer clics repetidos en los botones.
- Una banda de paso típica de SSB utiliza un corte bajo de 50 Hz y un corte alto de 3300 Hz. Reducir el corte alto a alrededor de 2700–2800 Hz puede mejorar la inteligibilidad en condiciones ruidosas al eliminar el silbido de alta frecuencia.
- La configuración de corte alto no es persistida por la configuración local de AetherSDR; se envía directamente a la radio y se almacena en el perfil activo de la radio.

## Relacionado

- [Configurar la frecuencia de corte bajo del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Descripción general de Phone](overview.md)

# Controles del applet Phone

El applet Phone proporciona controles de transmisión de voz para el nivel de portadora de AM, configuración de VOX, controles del expansor descendente (puerta de ruido) y ajustadores de frecuencia de corte bajo/alto del filtro de TX.

## Transmisión activada por voz (VOX)

### Habilitar VOX

Haga clic en **VOX** para activar o desactivar la transmisión activada por voz. Cuando está habilitado, la radio comenzará a transmitir automáticamente cuando el audio del micrófono supere el umbral establecido por el control deslizante **VOX level**.

### Nivel de VOX

Configure el umbral de activación de VOX arrastrando el control deslizante **VOX level**. El rango del control deslizante es de 0 a 100. Los valores más altos requieren un audio más fuerte para activar la transmisión. El control deslizante muestra el valor como un porcentaje (por ejemplo, "48 %") mientras se arrastra.

### Retardo

Configure el tiempo de retención de VOX arrastrando el control deslizante **Delay**. El rango del control deslizante es de 0 a 100. Esto controla cuánto tiempo permanece la radio en modo de transmisión después de que el audio se detiene antes de volver a recepción.

## Nivel de portadora de AM

Arrastre el control deslizante **AM Carrier** para ajustar el nivel de potencia de la portadora de AM. El rango del control deslizante es de 0 a 100. El control deslizante muestra el valor como un porcentaje (por ejemplo, "48 %") mientras se arrastra. El valor actual se muestra como una etiqueta numérica junto al control deslizante.

## Expansor descendente (DEXP)

### Habilitar DEXP

Haga clic en **DEXP** para activar o desactivar el expansor descendente (puerta de ruido).

### Umbral de DEXP

Configure el umbral de la puerta de DEXP arrastrando el control deslizante **DEXP threshold**. El rango del control deslizante es de 0 a 100. El control deslizante muestra el valor como un porcentaje mientras se arrastra. Esta configuración no es persistida localmente por AetherSDR; se envía directamente a la radio.

## Corte bajo del filtro de TX

Ajuste la frecuencia de corte bajo del filtro de TX usando el cuadro de incremento **Low Cut < / >**. El valor predeterminado es 50 Hz. El rango es de 0 a (high_cut − 50) Hz, con incrementos de 50 Hz. Haga clic en **<** para disminuir, en **>** para aumentar, o use la rueda del ratón sobre la pantalla de valor.

## Corte alto del filtro de TX

Ajuste la frecuencia de corte alto del filtro de TX usando el cuadro de incremento **High Cut < / >**. El valor predeterminado es 3300 Hz. El rango es de (low_cut + 50) a 10000 Hz, con incrementos de 50 Hz. Haga clic en **<** para disminuir, en **>** para aumentar, o use la rueda del ratón sobre la pantalla de valor.

## Qué hace cada control

| Control            | Descripción                                                         | Valor por defecto | Clave de configuración |
|--------------------|---------------------------------------------------------------------|-------------------|------------------------|
| **AM Carrier**     | Establece el nivel de potencia de la portadora de AM (0-100).       | —                 | None                   |
| **VOX**            | Activa/desactiva la transmisión activada por voz.                   | —                 | None                   |
| **VOX level**      | Establece el umbral de activación de VOX (0-100).                   | —                 | None                   |
| **Delay**          | Establece el tiempo de retención de VOX antes de volver a recepción (0-100). | —                 | None                   |
| **DEXP**           | Activa/desactiva el expansor descendente (puerta de ruido).         | —                 | None                   |
| **DEXP threshold** | Establece el umbral de la puerta de DEXP (0-100). No se persiste localmente. | 0                 | None                   |
| **Low Cut < / >**  | Ajusta la frecuencia de corte bajo del filtro de TX (0 a high_cut-50 Hz, paso 50 Hz). | 50 Hz  | None                   |
| **High Cut < / >** | Ajusta la frecuencia de corte alto del filtro de TX (low_cut+50 a 10000 Hz, paso 50 Hz). | 3300 Hz | None |

## Compatibilidad con temas

El applet Phone ahora utiliza colores adaptables al tema para todos los elementos de la interfaz. Las etiquetas, los controles deslizantes y los botones se adaptan al tema activo. El contenedor del applet aplica el estilo de tema `applet/phone`, y todos los valores de color previamente codificados han sido reemplazados por equivalentes temáticos. Esto garantiza una apariencia coherente en temas claros y oscuros.
