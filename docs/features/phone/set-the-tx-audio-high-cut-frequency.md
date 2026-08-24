# Controles del applet de Phone

El applet de Phone proporciona controles de transmisión de voz para el nivel de portadora de AM, ajustes de VOX, controles del expansor descendente (puerta de ruido) y ajustadores de frecuencia de corte bajo/alto del filtro de TX.

## Transmisión activada por voz (VOX)

### Habilitar VOX

Haga clic en **VOX** para activar o desactivar la transmisión activada por voz. Cuando está habilitado, la radio comenzará a transmitir automáticamente cuando el audio del micrófono supere el umbral establecido por el control deslizante **VOX level**.

### Nivel de VOX

Establezca el umbral de activación de VOX arrastrando el control deslizante **VOX level**. El rango del control es de 0 a 100. Los valores más altos requieren audio más fuerte para activar la transmisión. El control muestra el valor como porcentaje (p. ej., "48%") mientras se arrastra.

### Delay

Establezca el tiempo de retención de VOX arrastrando el control deslizante **Delay**. El rango del control es de 0 a 100. Esto controla cuánto tiempo permanece la radio en modo de transmisión después de que se detiene el audio antes de volver a recepción.

## Nivel de portadora de AM

Arrastre el control deslizante **AM Carrier** para ajustar el nivel de potencia de la portadora de AM. El rango del control es de 0 a 100. El control muestra el valor como porcentaje (p. ej., "48%") mientras se arrastra. El valor actual se muestra como una etiqueta numérica junto al control.

## Expansor descendente (DEXP)

### Habilitar DEXP

Haga clic en **DEXP** para activar o desactivar el expansor descendente (puerta de ruido).

**Nota:** Este control no es funcional en el firmware v1.4.0.0: la radio devuelve el error 0x5000002D.

### Umbral de DEXP

Establezca el umbral de la puerta de DEXP arrastrando el control deslizante **DEXP threshold**. El rango del control es de 0 a 100. El control muestra el valor como porcentaje mientras se arrastra. Esta configuración se guarda en la configuración local de AetherSDR bajo `DexpLevel`. El estado de activación de **DEXP** se guarda bajo `DexpEnabled`.

**Nota:** Este control tiene la misma limitación de firmware que la activación de DEXP en v1.4.0.0.

## Corte bajo del filtro de TX

Ajuste la frecuencia de corte bajo del filtro de TX usando el campo **Low Cut < / >**. El valor predeterminado es 50 Hz. El rango es de 0 a (high_cut − 50) Hz, en incrementos de 50 Hz.

## Corte alto del filtro de TX

Ajuste la frecuencia de corte alto del filtro de TX usando el campo **High Cut < / >**. El valor predeterminado es 3300 Hz. El rango es de (low_cut + 50) a 10000 Hz, en incrementos de 50 Hz.

## Ajuste de las frecuencias del filtro de TX

1. Haga clic en **<** para disminuir la frecuencia al siguiente múltiplo inferior de 50 Hz.
2. Haga clic en **>** para aumentar la frecuencia al siguiente múltiplo superior de 50 Hz.
3. Desplace la rueda del mouse sobre la pantalla de valor para avanzar en cualquier dirección.
4. Haga doble clic en la pantalla de valor para escribir un valor exacto en Hz. El valor escrito se acepta en radios que lo admiten, mientras que la lectura propia de la radio se conserva en otros lugares (problemas #3627, #5064).

### Comportamiento de los pasos y entrada directa

Los botones **<** y **>** ajustan el valor al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el corte alto actual es 3275 Hz, al hacer clic en **>** se establece en 3300 Hz y al hacer clic en **<** se establece en 3250 Hz. Este comportamiento se aplica igualmente a los controles de **Low Cut**.

Los valores escritos se manejan de manera diferente a los pasos:

- Un número **escrito** se trata como una solicitud de ese valor exacto. Los valores fuera de rango o los que no están en la cuadrícula de pasos admitida por la radio son **rechazados** y se restaura el valor anterior.
- Los **botones de paso** se ajustan al valor válido más cercano dentro del rango permitido, deteniéndose en el límite si se alcanza.

Al avanzar por pasos, si el backend de la radio publica un conjunto discreto de frecuencias admitidas (una lista de bordes), los botones avanzan al siguiente valor de esa lista en lugar de a un múltiplo de 50 Hz. De lo contrario, los pasos se ajustan a múltiplos de 50 Hz.

La tabla siguiente muestra la diferencia:

| Acción           | Comportamiento                                                                 |
|------------------|------------------------------------------------------------------------------|
| Hacer clic en **<**      | Se mueve a la siguiente frecuencia admitida inferior. Se limita al límite inferior. |
| Hacer clic en **>**      | Se mueve a la siguiente frecuencia admitida superior. Se limita al límite superior. |
| Escribir un valor     | Solicita esa frecuencia exacta. Rechaza valores fuera del rango válido o que no están en la cuadrícula admitida por la radio.         |

La frecuencia de corte alto no se puede establecer por debajo de la frecuencia de corte bajo actual más 50 Hz. Por ejemplo, si el corte bajo está establecido en 100 Hz, el valor mínimo de corte alto es 150 Hz. De manera similar, la frecuencia de corte bajo no se puede establecer por encima de la frecuencia de corte alto actual menos 50 Hz.

## Qué hace cada control

| Control                | Descripción                                                                      | Valor predeterminado | Clave de configuración |
|------------------------|----------------------------------------------------------------------------------|---------|-------------|
| **AM Carrier**         | Establece el nivel de potencia de la portadora de AM (0-100).                                             | —       | Ninguna        |
| **VOX**                | Activa o desactiva la transmisión activada por voz.                                          | —       | Ninguna        |
| **VOX level**          | Establece el umbral de activación de VOX (0-100).                                           | —       | Ninguna        |
| **Delay**              | Establece el tiempo de retención de VOX antes de volver a recepción (0-100).                          | —       | Ninguna        |
| **DEXP**               | Activa o desactiva el expansor descendente (puerta de ruido).                                   | —       | `DexpEnabled` |
| **DEXP threshold**     | Establece el umbral de la puerta de DEXP (0-100). Se guarda en `DexpLevel`.                      | 0       | `DexpLevel` |
| **Low Cut < / >**      | Ajusta la frecuencia de corte bajo del filtro de TX (0 a high_cut−50 Hz, paso de 50 Hz).           | 50 Hz   | Ninguna        |
| **High Cut < / >**     | Ajusta la frecuencia de corte alto del filtro de TX (low_cut+50 a 10000 Hz, paso de 50 Hz).       | 3300 Hz | Ninguna        |

## Soporte de temas

El applet de Phone utiliza colores adaptados al tema para todos los elementos de la interfaz. Las etiquetas, los controles deslizantes y los botones se adaptan al tema activo. El contenedor del applet aplica el estilo de tema `applet/phone`, y todos los valores de color previamente codificados se han reemplazado con equivalentes del tema. Esto garantiza una apariencia coherente en los temas claro y oscuro.

## Consejos

- Para cambios más grandes, use la rueda del mouse con movimiento rápido en lugar de hacer clic repetidamente en los botones.
- Una banda de paso de SSB típica usa un corte bajo de 50 Hz y un corte alto de 3300 Hz. Reducir el corte alto a unos 2700–2800 Hz puede mejorar la inteligibilidad en condiciones ruidosas al eliminar el silbido de alta frecuencia.
- Las configuraciones de corte bajo y corte alto no se guardan en la configuración local de AetherSDR: se envían directamente a la radio y se almacenan en el perfil activo de la radio.

## Relacionado

- [Establezca la frecuencia de corte alto del audio de TX](set-the-tx-audio-high-cut-frequency.md)
- [Resumen de Phone](overview.md)

---

# Establezca la frecuencia de corte alto del audio de TX

Use el applet de Phone para subir o bajar el límite superior de la banda de paso de audio de TX. Reducir el corte alto reduce el ancho de banda transmitido; subirlo permite pasar más contenido de audio de alta frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Phone requiere una conexión activa con la radio.
- La radio debe estar en un modo de telefonía (SSB, AM o similar) para que los cambios del filtro de TX tengan un efecto audible.

## Pasos

1. Si el applet de Phone no está visible, haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para mostrarlo.
2. Localice la columna **High Cut** en el lado derecho de la sección del filtro de TX, debajo de la fila de DEXP.
3. Haga una de las siguientes opciones:
   - Haga clic en **>** para aumentar la frecuencia de corte alto al siguiente valor admitido, o haga clic en **<** para disminuirla.
   - Desplace la rueda del mouse sobre la pantalla de valor para avanzar en cualquier dirección.
   - Haga doble clic en la pantalla de valor y escriba un valor exacto en Hz.
4. Lea el valor actual en la pantalla numérica entre los botones **<** y **>**.

## Qué hace cada control

| Control                | Descripción                                                                      | Valor predeterminado |
|------------------------|----------------------------------------------------------------------------------|---------|
| **High Cut `<`**       | Disminuye la frecuencia de corte alto del filtro de TX al siguiente valor admitido inferior.    | —       |
| **High Cut `>`**       | Aumenta la frecuencia de corte alto del filtro de TX al siguiente valor admitido superior.   | —       |
| Pantalla de valor de High Cut | Muestra la frecuencia de corte alto actual en Hz. Haga doble clic para escribir un valor exacto. | 3300 Hz |

La frecuencia de corte alto no se puede establecer por debajo de la frecuencia de corte bajo actual más 50 Hz. Por ejemplo, si el corte bajo está establecido en 100 Hz, el valor mínimo de corte alto es 150 Hz.

## Cómo funciona el avance por pasos

Los botones **<** y **>** ajustan el valor a la siguiente frecuencia admitida en la dirección elegida. En radios donde el backend publica una lista discreta de frecuencias admitidas, los botones avanzan a través de esa lista. De lo contrario, se ajustan al múltiplo de 50 Hz más cercano. Por ejemplo, en una radio continua con un corte alto actual de 3275 Hz, al hacer clic en **>** se establece en 3300 Hz y al hacer clic en **<** se establece en 3250 Hz. Este comportamiento se aplica igualmente a los controles de **Low Cut**.

Si el valor actual ya es un valor admitido exacto, el resultado es el mismo que un movimiento de un solo paso.

## Entrada numérica directa

Haga doble clic en la pantalla de valor para escribir un valor exacto en Hz.

- Los valores válidos son aquellos dentro del rango desde el corte bajo actual más 50 Hz hasta el corte alto máximo admitido por la radio, y en la cuadrícula de frecuencias admitida por la radio.
- Los valores fuera de rango o no admitidos son rechazados y se restaura el valor anterior.
- Un valor escrito se trata como una solicitud de esa frecuencia exacta, no como un paso, por lo que no se ajusta al valor admitido más cercano: se acepta tal cual o se rechaza.

## Consejos

- Para cambios más grandes, use la rueda del mouse con movimiento rápido en lugar de hacer clic repetidamente en los botones.
- Una banda de paso de SSB típica usa un corte bajo de 50 Hz y un corte alto de 3300 Hz. Reducir el corte alto a unos 2700–2800 Hz puede mejorar la inteligibilidad en condiciones ruidosas al eliminar el silbido de alta frecuencia.
- La configuración de corte alto no se guarda en la configuración local de AetherSDR: se envía directamente a la radio y se almacena en el perfil activo de la radio.

## Relacionado

- [Establezca la frecuencia de corte bajo del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Resumen de Phone](overview.md)

---

# Establezca la frecuencia de corte bajo del audio de TX

Use el applet de Phone para subir o bajar el límite inferior de la banda de paso de audio de TX. Subir el corte bajo elimina el retumbo de baja frecuencia y el contenido sub-audio de la señal transmitida; bajarlo permite pasar más audio de baja frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Phone requiere una conexión activa con la radio.
- La radio debe estar en un modo de telefonía (SSB, AM o similar) para que los cambios del filtro de TX tengan un efecto audible.

## Pasos

1. Si el applet de Phone no está visible, haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para mostrarlo.
2. Localice la columna **Low Cut** en el lado izquierdo de la sección del filtro de TX, debajo de la fila de DEXP.
3. Haga una de las siguientes opciones:
   - Haga clic en **>** para aumentar la frecuencia de corte bajo al siguiente valor admitido, o haga clic en **<** para disminuirla.
   - Desplace la rueda del mouse sobre la pantalla de valor para avanzar en cualquier dirección.
   - Haga doble clic en la pantalla de valor y escriba un valor exacto en Hz.
4. Lea el valor actual en la pantalla numérica entre los botones **<** y **>**.

## Qué hace cada control

| Control               | Descripción                                                                      | Valor predeterminado |
|-----------------------|----------------------------------------------------------------------------------|---------|
| **Low Cut `<`**       | Disminuye la frecuencia de corte bajo del filtro de TX al siguiente valor admitido inferior.     | —       |
| **Low Cut `>`**       | Aumenta la frecuencia de corte bajo del filtro de TX al siguiente valor admitido superior.    | —       |
| Pantalla de valor de Low Cut | Muestra la frecuencia de corte bajo actual en Hz. Haga doble clic para escribir un valor exacto.  | 50 Hz   |

La frecuencia de corte bajo no se puede establecer por encima de la frecuencia de corte alto actual menos 50 Hz. Por ejemplo, si el corte alto está establecido en 3300 Hz, el valor máximo de corte bajo es 3250 Hz.

## Cómo funciona el avance por pasos

Los botones **<** y **>** ajustan el valor a la siguiente frecuencia admitida en la dirección elegida. En radios donde el backend publica una lista discreta de frecuencias admitidas, los botones avanzan a través de esa lista. De lo contrario, se ajustan al múltiplo de 50 Hz más cercano. Por ejemplo, en una radio continua con un corte bajo actual de 87 Hz, al hacer clic en **>** se establece en 100 Hz y al hacer clic en **<** se establece en 50 Hz. Este comportamiento se aplica igualmente a los controles de **High Cut**.

Si el valor actual ya es un valor admitido exacto, el resultado es el mismo que un movimiento de un solo paso.

## Entrada numérica directa

Haga doble clic en la pantalla de valor para escribir un valor exacto en Hz.

- Los valores válidos son aquellos dentro del rango desde el corte bajo mínimo admitido por la radio hasta el corte alto actual menos 50 Hz, y en la cuadrícula de frecuencias admitida por la radio.
- Los valores fuera de rango o no admitidos son rechazados y se restaura el valor anterior.
- Un valor escrito se trata como una solicitud de esa frecuencia exacta, no como un paso, por lo que no se ajusta al valor admitido más cercano: se acepta tal cual o se rechaza.

Cuando escribe un valor de corte bajo que es muy alto, el corte alto de la radio **no** se arrastra hacia
