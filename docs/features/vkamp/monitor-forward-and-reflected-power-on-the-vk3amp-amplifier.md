# Monitoree la potencia directa y reflejada en el amplificador VK3AMP

Vea la potencia directa, la potencia reflejada y la ROE en tiempo real en el applet del amplificador VK3AMP, junto con la corriente de alimentación, para que pueda verificar el rendimiento de la antena y el funcionamiento del amplificador de un vistazo.

## Antes de comenzar

- La radio debe estar conectada.
- El amplificador VK3AMP debe estar encendido, conectado mediante TCP y reportando telemetría.

## Pasos

1. Abra el panel de applets.
2. Haga clic en el mosaico **VKAMP** para abrir el applet Amplificador VK3AMP.
3. Lea el indicador **Forward Power** para ver la potencia directa en tiempo real. El indicador se reescala según la salida nominal de la variante de hardware seleccionada.
4. Lea el indicador **Reflected Power** para ver la potencia reflejada en tiempo real.
5. Lea el indicador **SWR** para ver la relación de onda estacionaria.
6. Lea la lectura de texto **CURR** para ver la corriente de alimentación.

## Qué hace cada control

| Control | Qué muestra o hace |
|---|---|
| **Forward Power** | Potencia directa en tiempo real en un indicador. Se reescala según la salida nominal de la variante de hardware seleccionada (600 W / 1000 W / 2000 W). |
| **Reflected Power** | Potencia reflejada en tiempo real en un indicador. La escala completa es el 15 % de la salida nominal de la variante (p. ej., 300 W en la unidad de 2000 W). |
| **SWR** | Relación de onda estacionaria en un indicador con escala de 1:1 a 3:1. |
| **CURR** | Corriente de alimentación como lectura de texto. |
| **TEMP** | Temperatura del amplificador como lectura de texto. |
| **SUPPLY** | Tensión de alimentación como lectura de texto. La selección de riel bajo/alto está disponible mediante los botones **Voltage Low / High**. |
| **Fault** | Estado de falla reportado por el amplificador, mostrado como un código numérico sin procesar cuando está presente. |

## Consejos

- La escala completa del indicador **Forward Power** se adapta a la variante de hardware que haya seleccionado en la configuración: una unidad de 600 W mostrará un rango menor que una de 2000 W, de modo que la aguja siga siendo legible.
- El indicador **Reflected Power** también se escala según la variante, no es un valor fijo de 300 W: en una unidad de 600 W la escala completa es de 90 W, por lo que una potencia reflejada baja sigue siendo visible.

## Relacionados

- [Descripción general del amplificador VK3AMP](overview.md)
- [Bypass del amplificador VK3AMP](bypass-the-vk3amp-amplifier.md)
- [Seleccionar el puerto de antena del VK3AMP](select-the-vk3amp-antenna-port.md)
- [Restablecer el amplificador VK3AMP](reset-the-vk3amp-amplifier.md)
