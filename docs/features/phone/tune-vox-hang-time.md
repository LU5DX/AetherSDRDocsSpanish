# Ajustar el tiempo de mantenimiento de VOX

El tiempo de mantenimiento de VOX controla cuánto tiempo permanece la radio en transmisión después de que su voz cae por debajo del umbral de activación de VOX. Ajustarlo evita cortes de transmisión entrecortados al final de las palabras, evitando al mismo tiempo un silencio excesivo antes de volver a recepción.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone requiere una conexión de radio activa.
- VOX debe estar habilitado. Si VOX no está activado, actívelo primero; consulte [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md).

## Pasos

1. Abra el applet Phone haciendo clic en el botón de la bandeja **PHNE** en la barra lateral derecha. Si el panel del applet está oculto, haga clic en el borde del panel o use `View > Applet Panel` para mostrarlo.
2. Localice la fila **Delay:**, directamente debajo de la fila del nivel de VOX.
3. Arrastre el control deslizante **Delay** hacia la izquierda para acortar el tiempo de mantenimiento o hacia la derecha para alargarlo. El valor numérico a la derecha del control deslizante se actualiza mientras arrastra.

## Qué hace cada control

| Control            | Descripción                                                                                                    | Rango válido |
|--------------------|----------------------------------------------------------------------------------------------------------------|-------------|
| **AM Carrier**     | Establece el nivel de potencia de la portadora AM. Se muestra como porcentaje (p. ej., "48%") al arrastrarlo.  | 0–100       |
| **VOX**            | Activa o desactiva la transmisión controlada por voz.                                                          | —           |
| **VOX level**      | Establece el umbral de activación de VOX. Se muestra como porcentaje al arrastrarlo.                            | 0–100       |
| **Delay**          | Establece el tiempo de mantenimiento de VOX: cuánto tiempo permanece la radio en transmisión después de que termina el habla antes de volver a recepción. | 0–100       |
| **DEXP**           | Activa o desactiva el expansor descendente (puerta de ruido).                                                  | —           |
| **DEXP threshold** | Establece el umbral de la puerta de ruido DEXP.                                                               | 0–100       |
| **Low Cut < / >**  | Establece la frecuencia de corte baja del filtro de TX; se ajusta al siguiente múltiplo de 50 Hz.              | 50 Hz       |
| **High Cut < / >** | Establece la frecuencia de corte alta del filtro de TX; se ajusta al siguiente múltiplo de 50 Hz.              | 3300 Hz     |

## Persistencia de configuración

- El conmutador **DEXP** y los valores del control deslizante **DEXP threshold** se envían directamente a la radio. Ya no se conservan en la configuración de AetherSDR.
- Ningún otro control del applet Phone tiene una clave de configuración persistente; todos los valores se envían directamente a la radio.

## Consejos

- Un valor de Delay demasiado bajo hace que el transmisor entre y salga entre palabras. Aumente el valor hasta que cesen los cortes al final de las palabras.
- Un valor de Delay demasiado alto mantiene el transmisor activado mucho después de dejar de hablar, bloqueando a otras estaciones. Reduzca el valor hasta que el mantenimiento sea solo lo suficientemente largo para cubrir las pausas normales.
- El umbral de nivel de VOX y el Delay interactúan: un nivel de VOX más sensible (más bajo) puede requerir un Delay más corto, y viceversa.

## Comportamiento del escalonado de los puntos de corte del filtro de TX

A partir de v26.8.4, los botones **Low Cut < / >** y **High Cut < / >** ajustan la frecuencia del filtro al siguiente múltiplo de 50 Hz en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual.

Por ejemplo, si el corte bajo está actualmente en 87 Hz:

- Al presionar **>** (aumentar), se mueve a **100 Hz** (el siguiente múltiplo de 50 por encima de 87).
- Al presionar **<** (disminuir), se mueve a **50 Hz** (el siguiente múltiplo de 50 por debajo de 87).

Esto significa que una sola pulsación de botón siempre aterriza en un límite limpio de 50 Hz, independientemente del valor inicial. La rueda del ratón en cada cuadro de número sigue el mismo comportamiento de ajuste. Cuando el backend de la radio publica una lista discreta de frecuencias de borde permitidas, los botones recorren esa lista en su lugar. En radios que aceptan valores continuos de Hz enteros, el ajuste es solo una conveniencia de la interfaz y no restringe lo que la radio aceptará.

### Entrada numérica directa

A partir de v26.8.4, puede hacer doble clic en el valor de **Low Cut** o **High Cut** para escribir una frecuencia exacta en Hz en lugar de escalonarla de 50 Hz en 50 Hz. Presione Enter para confirmar el valor.

- Un valor escrito se trata como una solicitud de esa frecuencia exacta. En radios que admiten valores arbitrarios de Hz enteros, el valor exacto se envía a la radio.
- Los botones de escalonado aún se limitan a la cuadrícula de escalonado de la radio (múltiplos de 50 Hz o la lista de bordes discretos del backend). Esta asimetría es deliberada: un escalonado es una solicitud para moverse un incremento, mientras que un número escrito es una solicitud de un valor específico.
- Los valores fuera de rango se rechazan, no se limitan. El valor anterior se restaura si escribe una frecuencia no válida.
- Cuando el backend publica una lista de bordes discretos, los valores escritos que no estén presentes en esa lista se rechazan.

| Control            | Descripción                                                              | Predeterminado | Rango válido                          |
|--------------------|--------------------------------------------------------------------------|---------|--------------------------------------|
| **Low Cut < / >**  | Establece la frecuencia de corte baja del filtro de TX; se ajusta al siguiente múltiplo de 50 Hz. Haga doble clic para escribir un valor exacto en Hz. | 50 Hz   | 0 a (corte alto − 50), paso de 50 Hz |
| **High Cut < / >** | Establece la frecuencia de corte alta del filtro de TX; se ajusta al siguiente múltiplo de 50 Hz. Haga doble clic para escribir un valor exacto en Hz. | 3300 Hz | (corte bajo + 50) a 10000, paso de 50 Hz |

Ninguno de los dos controles tiene una clave de configuración persistente; los valores se envían directamente a la radio.

## Formato de valores de los controles deslizantes

A partir de v26.5.3, los controles deslizantes **AM Carrier**, **VOX level** y **DEXP threshold** muestran su valor como porcentaje (p. ej., "48%") al arrastrarlos. La etiqueta numérica junto al control deslizante continúa mostrando el valor bruto de 0–100 sin el signo de porcentaje.

## Soporte de temas

A partir de v26.6.1, el applet Phone utiliza colores basados en el tema activo en lugar de valores hexadecimales fijos. Los fondos de los controles deslizantes, los colores del controlador, los fondos de los botones y los colores del texto siguen el tema actualmente cargado. Los temas se administran mediante `View > Theme Manager`.

## Relacionados

- [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Descripción general del applet Phone](overview.md)
