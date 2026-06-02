# Configurar la frecuencia de corte alto del audio de TX

Use el applet Phone para subir o bajar el límite superior de la banda pasante de audio de TX. Reducir el corte alto disminuye el ancho de banda transmitido; aumentarlo pasa más contenido de audio de alta frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone requiere una conexión activa con la radio.
- La radio debe estar en un modo de telefonía (SSB, AM o similar) para que los cambios en el filtro de TX tengan efecto audible.

## Pasos

1. Si el applet Phone no está visible, haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para mostrarlo.
2. Localice la columna **High Cut** en el lado derecho de la sección del filtro de TX, debajo de la fila DEXP.
3. Haga clic en **>** para aumentar la frecuencia de corte alto al siguiente múltiplo de 50 Hz, o haga clic en **<** para disminuirla al siguiente múltiplo inferior de 50 Hz. También puede desplazar la rueda del ratón sobre la pantalla de valores para avanzar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los botones **<** y **>**.

## Qué hace cada control

| Control                | Descripción                                                                                      | Valor predeterminado |
|------------------------|--------------------------------------------------------------------------------------------------|----------------------|
| **High Cut `<`**       | Disminuye la frecuencia de corte alto del filtro de TX al siguiente múltiplo inferior de 50 Hz. | —                    |
| **High Cut `>`**       | Aumenta la frecuencia de corte alto del filtro de TX al siguiente múltiplo superior de 50 Hz.   | —                    |
| Pantalla de valor High Cut | Muestra la frecuencia de corte alto actual en Hz.                                           | 3300 Hz              |

La frecuencia de corte alto no se puede configurar por debajo de la frecuencia de corte bajo actual más 50 Hz. Por ejemplo, si el corte bajo está configurado a 100 Hz, el valor mínimo de corte alto es 150 Hz.

## Cómo funciona el avance incremental

Los botones **<** y **>** ajustan el valor al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el corte alto actual es 3275 Hz, hacer clic en **>** lo establece a 3300 Hz y hacer clic en **<** lo establece a 3250 Hz. Este comportamiento se aplica igualmente a los controles **Low Cut**.

La radio acepta cualquier valor entero en Hz, por lo que si el valor actual ya es un múltiplo exacto de 50 Hz, el resultado es el mismo que un incremento simple de 50 Hz.

## Consejos

- Para cambios más grandes, use la rueda de desplazamiento con movimiento rápido en lugar de clics repetidos en los botones.
- Una banda pasante SSB típica usa un corte bajo de 50 Hz y un corte alto de 3300 Hz. Reducir el corte alto a alrededor de 2700-2800 Hz puede mejorar la inteligibilidad en condiciones ruidosas al eliminar el siseo de alta frecuencia.
- La configuración de corte alto no es persistida por los ajustes locales de AetherSDR; se envía directamente a la radio y se almacena en el perfil activo de la radio.

## Relacionados

- [Configurar la frecuencia de corte bajo del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Descripción general de Phone](overview.md)

# Controles del applet Phone

El applet Phone proporciona controles de transmisión de voz para el nivel de portadora de AM, ajustes de VOX, controles del expansor descendente (puerta de ruido) y configuradores de frecuencia de corte bajo/alto del filtro de TX.

## Transmisión activada por voz (VOX)

### Habilitar VOX

Haga clic en **VOX** para activar o desactivar la transmisión activada por voz. Cuando está habilitado, la radio comenzará a transmitir automáticamente cuando el audio del micrófono supere el umbral establecido por el control deslizante **VOX level**.

### Nivel de VOX

Establezca el umbral de activación de VOX arrastrando el control deslizante **VOX level**. El rango del control deslizante es de 0 a 100. Los valores más altos requieren audio más fuerte para activar la transmisión. El control deslizante muestra el valor como un porcentaje (p. ej., "48%") mientras se arrastra.

### Retardo

Establezca el tiempo de retención de VOX arrastrando el control deslizante **Delay**. El rango del control deslizante es de 0 a 100. Esto controla cuánto tiempo permanece la radio en modo de transmisión después de que el audio se detiene antes de volver a recepción.

## Nivel de portadora AM

Arrastre el control deslizante **AM Carrier** para ajustar el nivel de potencia de la portadora AM. El rango del control deslizante es de 0 a 100. El control deslizante muestra el valor como un porcentaje (p. ej., "48%") mientras se arrastra. El valor actual se muestra como una etiqueta numérica junto al control deslizante.

## Expansor descendente (DEXP)

### Habilitar DEXP

Haga clic en **DEXP** para activar o desactivar el expansor descendente (puerta de ruido). Nota: Este control no es funcional en firmware v1.4.0.0 — la radio devuelve el error 0x5000002D.

### Umbral de DEXP

Establezca el umbral de la puerta de DEXP arrastrando el control deslizante **DEXP threshold**. El rango del control deslizante es de 0 a 100. El control deslizante muestra el valor como un porcentaje mientras se arrastra. Esta configuración persiste en la clave de configuración `DexpLevel`. Nota: Misma limitación de firmware que el conmutador de DEXP.

## Filtro de TX de corte bajo

Ajuste la frecuencia de corte bajo del filtro de TX usando la caja de incremento **Low Cut < / >**. El valor predeterminado es 50 Hz. El rango es de 0 a (high_cut − 50) Hz, incrementándose en pasos de 50 Hz. Haga clic en **<** para disminuir, en **>** para aumentar, o use la rueda del ratón sobre la pantalla de valores.

## Filtro de TX de corte alto

Ajuste la frecuencia de corte alto del filtro de TX usando la caja de incremento **High Cut < / >**. El valor predeterminado es 3300 Hz. El rango es de (low_cut + 50) a 10000 Hz, incrementándose en pasos de 50 Hz. Haga clic en **<** para disminuir, en **>** para aumentar, o use la rueda del ratón sobre la pantalla de valores.

## Qué hace cada control

| Control                | Descripción                                                                 | Valor predeterminado | Clave de configuración |
|------------------------|-----------------------------------------------------------------------------|----------------------|------------------------|
| **AM Carrier**         | Establece el nivel de potencia de portadora AM (0-100).                     | —                    | Ninguna                |
| **VOX**                | Activa/desactiva la transmisión activada por voz.                           | —                    | Ninguna                |
| **VOX level**          | Establece el umbral de activación de VOX (0-100).                           | —                    | Ninguna                |
| **Delay**              | Establece el tiempo de retención de VOX antes de volver a recepción (0-100).| —                    | Ninguna                |
| **DEXP**               | Activa/desactiva el expansor descendente (puerta de ruido). No funcional en fw v1.4.0.0 | —          | `DexpEnabled`          |
| **DEXP threshold**     | Establece el umbral de la puerta de DEXP (0-100). Misma limitación de firmware que el conmutador de DEXP. | 0   | `DexpLevel`            |
| **Low Cut < / >**      | Ajusta la frecuencia de corte bajo del filtro de TX (0 a high_cut-50 Hz, paso 50 Hz).       | 50 Hz     | Ninguna                |
| **High Cut < / >**     | Ajusta la frecuencia de corte alto del filtro de TX (low_cut+50 a 10000 Hz, paso 50 Hz). | 3300 Hz    | Ninguna                |

## Soporte de temas

El applet Phone ahora utiliza colores conscientes del tema para todos los elementos de la interfaz. Las etiquetas, controles deslizantes y botones se adaptan al tema activo. El contenedor del applet aplica el estilo de tema `applet/phone`, y todos los valores de color anteriormente codificados han sido reemplazados con equivalentes temáticos. Esto garantiza una apariencia consistente en temas claros y oscuros.
