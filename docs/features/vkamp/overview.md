# Resumen del amplificador VK3AMP

El applet del Amplificador VK3AMP supervisa y controla un amplificador de RF VK3AMP (600 W / 1000 W / 2000 W) conectado a su radio mediante TCP con telemetría UDP. Muestra la potencia directa, la potencia reflejada, la ROE y la corriente de alimentación, además de la selección de antena, bypass, refrigeración, reinicio e indicadores de falla.

## Antes de comenzar

- Se requiere una conexión de radio FLEX-8600.
- El amplificador debe ser accesible a través de su red (TCP con telemetría UDP).

## Cómo funciona

Abra el applet desde **Applet panel > VKAMP tile**. El applet se conecta al amplificador mediante TCP y recibe telemetría en tiempo real, que impulsa los indicadores y las lecturas de estado. Los controles envían comandos de vuelta a través de la misma conexión.

El applet reconoce la variante de hardware. Los indicadores de potencia directa y reflejada se reescalan a la salida nominal de la variante seleccionada, de modo que una unidad de 2000 W muestra un rango de escala completa diferente al de una unidad de 600 W.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Forward Power | Indicador | Potencia directa en tiempo real desde el amplificador. El indicador se reescala a la salida nominal de la variante de hardware seleccionada. |
| Reflected Power | Indicador | Potencia reflejada en tiempo real. El indicador se escala al 15 % de la salida nominal de la variante. |
| SWR | Indicador | Relación de onda estacionaria en tiempo real, escalada de 1,0 a 3,0. |
| Current | Indicador | Lectura de texto de la corriente de alimentación (etiquetada CURR). |
| Bypass | Botón pulsador (etiquetado BYPASS) | Alterna el amplificador entre bypass y en línea. La etiqueta muestra el estado actual, no la acción. |
| Cooling | Botón pulsador (etiquetado COOLING) | Alterna la anulación de refrigeración. |
| Antenna 1 / 2 / 3 | Botón pulsador | Selecciona el puerto de antena (1–3). La selección es una visualización de solo lectura hasta que el amplificador la confirma. La propia tabla del amplificador puede revertir una selección en unos ~50 ms. |
| Voltage Low / High | Botón pulsador | Selecciona qué carril de voltaje informa el estado en vivo. |
| Reset | Botón pulsador (mantener para confirmar) | Reinicia el amplificador. Mantenga pulsado para confirmar. |
| Fault | Indicador | Estado de falla reportado por el amplificador como un código numérico sin procesar. Se muestra solo cuando hay una falla activa. |

El applet también muestra temperatura (TEMP), voltaje de alimentación (SUPPLY), corriente (CURR), banda (BAND) y antena (ANT) en una cuadrícula de lecturas de texto.

## Consejos

- La etiqueta del botón de bypass refleja el estado actual, no la acción. Cuando el amplificador está en línea, muestra el estilo del estado activo; cuando está en bypass, muestra el estado de bypass.
- Los botones de antena no son optimistas: al hacer clic se solicita al amplificador que cambie, pero el resaltado solo se mueve después de que el estado en vivo lo confirma. Si la tabla interna del amplificador anula la selección, la visualización se revierte en unos 50 ms.

## Solución de problemas

- **Aparece el banner de falla** — El amplificador reporta una falla con un código numérico sin procesar. El applet muestra el código; no asigna nombres a los códigos. Consulte la documentación de su amplificador para conocer el significado del código.
- **La selección de antena se revierte** — La propia tabla de antenas del amplificador puede anular su selección en unos ~50 ms. Verifique la tabla configurada del amplificador para la banda actual.

## Relacionado

- [Monitor forward and reflected power on the VK3AMP amplifier](monitor-forward-and-reflected-power-on-the-vk3amp-amplifier.md)
- [Bypass the VK3AMP amplifier](bypass-the-vk3amp-amplifier.md)
- [Select the VK3AMP antenna port](select-the-vk3amp-antenna-port.md)
- [Reset the VK3AMP amplifier](reset-the-vk3amp-amplifier.md)
