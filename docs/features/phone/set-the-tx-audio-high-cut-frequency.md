# Establecer la frecuencia de corte alto del audio de TX

Utilice el applet Phone para subir o bajar el límite superior de la banda pasante de audio de TX. Reducir el corte alto disminuye el ancho de banda transmitido; aumentarlo permite pasar más contenido de audio de alta frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone requiere una conexión activa con la radio.
- La radio debe estar en un modo de telefonía (SSB, AM o similar) para que los cambios en el filtro de TX tengan efecto audible.

## Pasos

1. Si el applet Phone no está visible, haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para mostrarlo.
2. Localice la columna **High Cut** en el lado derecho de la sección de filtro de TX, debajo de la fila DEXP.
3. Haga clic en **>** para aumentar la frecuencia de corte alto al siguiente múltiplo de 50 Hz, o haga clic en **<** para disminuirla al múltiplo inferior de 50 Hz. También puede desplazar la rueda del ratón sobre el display de valor para avanzar en cualquier dirección.
4. Lea el valor actual en el display numérico entre los botones **<** y **>**.

## Función de cada control

| Control                | Descripción                                                                                      | Predeterminado |
|------------------------|--------------------------------------------------------------------------------------------------|----------------|
| **High Cut `<`**       | Disminuye la frecuencia de corte alto del filtro de TX al siguiente múltiplo inferior de 50 Hz. | —              |
| **High Cut `>`**       | Aumenta la frecuencia de corte alto del filtro de TX al siguiente múltiplo superior de 50 Hz.   | —              |
| Display de valor High Cut | Muestra la frecuencia de corte alto actual en Hz.                                              | 3300 Hz        |

La frecuencia de corte alto no puede establecerse por debajo de la frecuencia de corte bajo actual más 50 Hz. Por ejemplo, si el corte bajo está configurado a 100 Hz, el valor mínimo del corte alto es 150 Hz.

## Cómo funciona el avance

Los botones **<** y **>** ajustan el valor al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el corte alto actual es 3275 Hz, al hacer clic en **>** se establece en 3300 Hz y al hacer clic en **<** se establece en 3250 Hz. Este comportamiento se aplica igualmente a los controles **Low Cut**.

La radio acepta cualquier valor entero en Hz, por lo que si el valor actual ya es un múltiplo exacto de 50 Hz, el resultado es el mismo que un paso simple de 50 Hz.

## Consejos

- Para cambios más grandes, utilice la rueda de desplazamiento con movimiento rápido en lugar de clics repetidos en los botones.
- Una banda pasante típica de SSB utiliza un corte bajo de 50 Hz y un corte alto de 3300 Hz. Reducir el corte alto a alrededor de 2700-2800 Hz puede mejorar la inteligibilidad en condiciones ruidosas al eliminar el silbido de alta frecuencia.
- La configuración de corte alto no se conserva en los ajustes locales de AetherSDR: se envía directamente a la radio y se almacena en el perfil activo de la radio.

## Relacionado

- [Establecer la frecuencia de corte bajo del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Visión general de Phone](overview.md)

# Controles del applet Phone

El applet Phone proporciona controles de transmisión de voz para el nivel de portadora AM, ajustes de VOX, controles del expansor descendente (puerta de ruido) y configuradores de frecuencia de corte bajo/alto del filtro de TX.

## Transmisión activada por voz (VOX)

### Habilitar VOX

Haga clic en **VOX** para activar o desactivar la transmisión activada por voz. Cuando está habilitado, la radio comenzará a transmitir automáticamente cuando el audio del micrófono supere el umbral establecido por el deslizador **VOX level**.

### Nivel VOX

Establezca el umbral de activación de VOX arrastrando el deslizador **VOX level**. El rango del deslizador es de 0 a 100. Los valores más altos requieren un audio más fuerte para activar la transmisión. El deslizador muestra el valor como un porcentaje (por ejemplo, "48%") mientras se arrastra.

### Retardo

Establezca el tiempo de retención de VOX arrastrando el deslizador **Delay**. El rango del deslizador es de 0 a 100. Esto controla cuánto tiempo permanece la radio en modo de transmisión después de que el audio se detiene antes de volver a recepción.

## Nivel de portadora AM

Arrastre el deslizador **AM Carrier** para ajustar el nivel de potencia de la portadora AM. El rango del deslizador es de 0 a 100. El deslizador muestra el valor como un porcentaje (por ejemplo, "48%") mientras se arrastra. El valor actual se muestra como una etiqueta numérica junto al deslizador.

## Expansor descendente (DEXP)

### Habilitar DEXP

Haga clic en **DEXP** para activar o desactivar el expansor descendente (puerta de ruido). Nota: Este control no es funcional en la versión de firmware v1.4.0.0: la radio devuelve el error 0x5000002D.

### Umbral DEXP

Establezca el umbral de la puerta DEXP arrastrando el deslizador **DEXP threshold**. El rango del deslizador es de 0 a 100. El deslizador muestra el valor como un porcentaje mientras se arrastra. Esta configuración persiste en la clave de configuración `DexpLevel`. Nota: Misma limitación de firmware que el interruptor DEXP.

## Corte bajo del filtro de TX

Ajuste la frecuencia de corte bajo del filtro de TX usando el cuadro giratorio **Low Cut < / >**. El valor predeterminado es 50 Hz. El rango es de 0 a (high_cut - 50) Hz, con incrementos de 50 Hz. Haga clic en **<** para disminuir, en **>** para aumentar, o use la rueda del ratón sobre el display de valor.

## Corte alto del filtro de TX

Ajuste la frecuencia de corte alto del filtro de TX usando el cuadro giratorio **High Cut < / >**. El valor predeterminado es 3300 Hz. El rango es de (low_cut + 50) a 10000 Hz, con incrementos de 50 Hz. Haga clic en **<** para disminuir, en **>** para aumentar, o use la rueda del ratón sobre el display de valor.

## Función de cada control

| Control            | Descripción                                                                  | Predeterminado | Clave de configuración |
|--------------------|------------------------------------------------------------------------------|----------------|-------------------------|
| **AM Carrier**     | Establece el nivel de potencia de la portadora AM (0-100).                   | —              | None                    |
| **VOX**            | Activa/desactiva la transmisión activada por voz.                           | —              | None                    |
| **VOX level**      | Establece el umbral de activación de VOX (0-100).                            | —              | None                    |
| **Delay**          | Establece el tiempo de retención de VOX antes de volver a recepción (0-100). | —              | None                    |
| **DEXP**           | Activa/desactiva el expansor descendente (puerta de ruido). No funcional en fw v1.4.0.0 | —    | `DexpEnabled`           |
| **DEXP threshold** | Establece el umbral de la puerta DEXP (0-100). Misma limitación de firmware que el interruptor DEXP. | 0 | `DexpLevel`        |
| **Low Cut < / >**  | Ajusta la frecuencia de corte bajo del filtro de TX (0 a high_cut-50 Hz, paso 50 Hz). | 50 Hz | None                |
| **High Cut < / >** | Ajusta la frecuencia de corte alto del filtro de TX (low_cut+50 a 10000 Hz, paso 50 Hz). | 3300 Hz | None            |
