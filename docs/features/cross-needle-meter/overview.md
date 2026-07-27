# Resumen del Medidor de Agujas Cruzadas

El Medidor de Agujas Cruzadas muestra la potencia de RF directa y reflejada como dos agujas que se cruzan en una cara de medidor de estilo analógico clásico, con una lectura de ROE calculada. Le ayuda a monitorear la adaptación de la antena y la potencia de salida de un vistazo, como un medidor de ROE de agujas cruzadas de escritorio tradicional.

## Antes de comenzar

- Una radio debe estar conectada a AetherSDR.
- El Medidor de Agujas Cruzadas requiere una conexión de radio activa para recibir datos de potencia y ROE.

## Cómo funciona

El medidor muestra la potencia directa (aguja derecha) y la potencia reflejada (aguja izquierda) en la misma cara de medidor calibrada. El punto donde se cruzan las dos agujas indica la ROE. El medidor se actualiza continuamente en tiempo real.

Abra el medidor desde **Applet panel > Cross-Needle tile**.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| Agujas de potencia directa/reflejada | indicador | — | Visualización analógica de dos agujas: potencia directa (aguja derecha) y potencia reflejada (aguja izquierda) que se cruzan para indicar la ROE. |
| Peak hold | botón de alternancia | Apagado | Mantiene la posición máxima de la aguja para una lectura más fácil durante los picos de voz en SSB. |
| Lectura digital | indicador | — | Valores numéricos de potencia directa, potencia reflejada y ROE mostrados debajo del medidor. |
| Tema de la cara del medidor | cuadro combinado | — | Seleccione entre estilos predefinidos de cara de medidor (negro clásico, blanco, militar, etc.). |

## Consejos

- Use Peak hold al operar en SSB para capturar picos de voz que son demasiado breves para leer en el medidor analógico.
- La lectura digital debajo del medidor proporciona valores numéricos exactos de potencia directa, potencia reflejada y ROE, útil cuando la posición de la aguja analógica es ambigua.

## Relacionados

- [Leer la potencia directa y reflejada en el medidor de agujas cruzadas](read-forward-and-reflected-power-on-the-cross-needle-meter.md)
- [Activar la retención de pico para picos de voz SSB](enable-peak-hold-for-ssb-voice-peaks.md)
- [Cambiar el tema de la cara del medidor](change-the-meter-face-theme.md)
