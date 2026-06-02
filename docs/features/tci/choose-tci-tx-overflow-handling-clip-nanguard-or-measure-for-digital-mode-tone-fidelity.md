# Elección del manejo de desbordamiento de TX por TCI (Clip, NaNGuard o Measure) para la fidelidad de tonos en modos digitales

El modo de manejo de desbordamiento de TX controla cómo AetherSDR procesa las muestras de audio provenientes del software cliente TCI que exceden el rango normal de ±1.0. Las aplicaciones de modos digitales (FT8, RTTY, etc.) pueden producir valores flotantes fuera de rango; elegir el modo correcto preserva la fidelidad de tonos bit-exacta o protege el hardware downstream según sea necesario.

## Antes de comenzar

- El servidor TCI debe estar en ejecución (el botón Enable está en verde, el estado muestra `:<puerto>`).
- Debe haber un cliente TCI (ej., WSJT-X, Log4OM) conectado y transmitiendo.

## Pasos

1. Haga clic derecho en el medidor/deslizador de ganancia de TX en el applet del servidor TCI.
2. En el menú contextual **TX overflow handling**, seleccione uno de los tres modos:
   - **Clip (saturating ±1.0)** — valor predeterminado heredado
   - **NaN guard (zero NaN/Inf only)**
   - **Measure only (true bypass)**

La selección se guarda como `TciTxOverflowMode` y tiene efecto inmediato para todo el audio nuevo proveniente de clientes TCI.

## Qué hace cada control

| Modo                           | Valor de enum                                                                                                                        | Comportamiento                                                                                                                                                                                                                                       |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Clip (saturating ±1.0)         | 0                                                                                                                                    | Limita forzosamente los picos a ±1.0. Introduce distorsión armónica en los picos, pero protege la conversión downstream a int16.                                                                                                                      |
| NaN guard (zero NaN/Inf only)  | 1                                                                                                                                    | Pasa las muestras bit-exactas; solo pone a cero valores patológicos NaN/Inf. Preserva la fidelidad de tonos en modos digitales; los flotantes fuera de rango llegan al equipo.                                                                        |
| Measure only (true bypass)     | 2                                                                                                                                    | Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión downstream a int16 aún limita en la ruta DAX nativa del equipo.                                                                                                           |
| TX overflow mode (clic derecho)| Haga clic derecho en el medidor/deslizador de ganancia de TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento de TX. Emite tciTxOverflowModeChanged. | Clip limita los picos a ±1.0 con distorsión armónica; NaNGuard preserva tonos digitales bit-exactos solo poniendo a cero NaN/Inf; Measure cuenta los picos para telemetría sin modificación. Se guarda como TciTxOverflowMode (0/1/2). |

## Consejos

- **El valor predeterminado es Clip (modo 0)** — los usuarios existentes no verán cambios de comportamiento tras la actualización.
- Los clientes de modos digitales suelen enviar audio exactamente a 0 dBFS; el redondeo de punto flotante puede empujar los valores ligeramente por encima de ±1.0. NaN guard preserva esos bordes de tono mientras sigue protegiendo contra tramas NaN/Inf corruptas.
- La conversión downstream a int16 en la ruta DAX nativa del equipo siempre limita independientemente de esta configuración al usar el modo Measure.

## Relacionado

- [Adjust TCI TX gain](adjust-tci-tx-gain.md)
- [Enable the TCI server for Log4OM / SunSDR clients](enable-the-tci-server-for-log4om-sunsdr-clients.md)
