# Elección del manejo de desbordamiento de TX en TCI (Clip, NaNGuard o Measure) para la fidelidad de tonos en modos digitales

El modo de manejo de desbordamiento de TX controla cómo AetherSDR procesa las muestras de audio provenientes del software cliente TCI que exceden el rango normal de ±1.0. Las aplicaciones de modos digitales (FT8, RTTY, etc.) pueden producir valores flotantes fuera de rango; elegir el modo correcto preserva la fidelidad bit-exacta de los tonos o protege el hardware aguas abajo según sea necesario.

## Antes de comenzar

- El servidor TCI debe estar en ejecución (el botón Enable está en verde, el estado muestra `:<port>`).
- Un cliente TCI (por ejemplo, WSJT-X, Log4OM) debe estar conectado y transmitiendo.

## Pasos

1. Haga clic derecho en el medidor/control deslizante de ganancia de TX en el applet del Servidor TCI.
2. En el menú contextual **TX overflow handling**, seleccione uno de los tres modos:
   - **Clip (saturating ±1.0)** — predeterminado heredado
   - **NaN guard (zero NaN/Inf only)**
   - **Measure only (true bypass)**

La selección se conserva como `TciTxOverflowMode` y tiene efecto inmediato para todo el audio nuevo proveniente de los clientes TCI.

## Qué hace cada control

| Modo | Valor de enum | Comportamiento | Mejor para |
|------|---------------|----------------|------------|
| Clip (saturating ±1.0) | 0 | Limita forzosamente los picos a ±1.0. Introduce distorsión armónica en los picos, pero protege la conversión a int16 aguas abajo. | Configuraciones heredadas, uso general, protección de la radio contra picos inesperados |
| NaN guard (zero NaN/Inf only) | 1 | Pasa las muestras bit-exactas; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad de los tonos en modos digitales; los valores flotantes fuera de rango llegan a la radio. | FT8, RTTY y otros modos digitales que requieren formas de onda bit-exactas |
| Measure only (true bypass) | 2 | Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión a int16 aguas abajo aún limita en la ruta DAX nativa de la radio. | Depuración, recopilación de telemetría, cuando desea ver con qué frecuencia ocurren los picos |

## Consejos

- **El valor predeterminado es Clip (modo 0)** — los usuarios existentes no verán cambios de comportamiento después de actualizar.
- Los clientes de modos digitales comúnmente envían audio exactamente a 0 dBFS; el redondeo en coma flotante puede empujar los valores ligeramente por encima de ±1.0. NaN guard preserva esos bordes de tono mientras aún protege contra tramas NaN/Inf corruptas.
- La conversión a int16 aguas abajo en la ruta DAX nativa de la radio siempre limita, independientemente de esta configuración, cuando se usa el modo Measure.

## Relacionados

- [Ajustar la ganancia de TX de TCI](adjust-tci-tx-gain.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
