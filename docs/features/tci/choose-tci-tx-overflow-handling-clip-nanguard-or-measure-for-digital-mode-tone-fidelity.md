# Cómo elegir el manejo de desbordamiento TX de TCI (Clip, NaNGuard o Measure) para la fidelidad de tonos en modos digitales

El modo de manejo de desbordamiento TX controla cómo procesa AetherSDR las muestras de audio provenientes del software cliente TCI que superan el rango normal de ±1.0. Las aplicaciones de modos digitales (FT8, RTTY, etc.) pueden producir valores de punto flotante fuera de rango; elegir el modo correcto preserva la fidelidad de tonos bit exacta o protege el hardware aguas abajo según sea necesario.

## Antes de comenzar

- El servidor TCI debe estar en ejecución (el botón Enable muestra "Enabled" y el estado muestra `:<port>`).
- Un cliente TCI (por ejemplo, WSJT-X, Log4OM) debe estar conectado y transmitiendo.

## Pasos

1. Haga clic derecho en el medidor/control deslizante de ganancia TX en el applet del servidor TCI.
2. En el menú contextual **TX overflow handling**, seleccione uno de los tres modos:
   - **Clip (saturating ±1.0)** — predeterminado heredado
   - **NaN guard (zero NaN/Inf only)**
   - **Measure only (true bypass)**

La selección se guarda como `TciTxOverflowMode` y se aplica inmediatamente a todo el audio nuevo proveniente de clientes TCI.

## Qué hace cada control

| Modo                             | Valor de enumeración | Comportamiento                                                                                                                                                                                                                                                                                                                                                                      |
|----------------------------------|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Clip (saturating ±1.0)           | 0                    | Limita de forma forzada los excesos a ±1.0. Introduce distorsión armónica en los excesos, pero protege la conversión int16 aguas abajo.                                                                                                                                                                                                                                              |
| NaN guard (zero NaN/Inf only)    | 1                    | Pasa las muestras de forma bit exacta; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad de tonos en modos digitales; los valores de punto flotante fuera de rango llegan al radio.                                                                                                                                                                          |
| Measure only (true bypass)       | 2                    | Nunca modifica las muestras. Cuenta los excesos para telemetría; la conversión int16 aguas abajo aún limita en la ruta DAX nativa del radio.                                                                                                                                                                                                                                        |
| TX overflow mode (right-click)   |                      | Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir un menú contextual que permite seleccionar el modo de manejo de desbordamiento TX. Emite tciTxOverflowModeChanged. Clip limita los excesos a ±1.0 con distorsión armónica; NaNGuard preserva los tonos digitales bit exactos al poner a cero solo NaN/Inf; Measure cuenta los excesos para telemetría sin modificación. Se guarda como TciTxOverflowMode (0/1/2). |

El botón Enable muestra "Enabled" cuando el servidor TCI está en ejecución y "Disabled" cuando está detenido.

## Consejos

- **El valor predeterminado es Clip (modo 0)** — los usuarios existentes no verán cambios de comportamiento tras actualizar.
- Los clientes de modos digitales suelen enviar audio a exactamente 0 dBFS; el redondeo de punto flotante puede empujar los valores ligeramente por encima de ±1.0. NaN guard preserva esos bordes de tono mientras sigue protegiendo contra tramas NaN/Inf corruptas.
- La conversión int16 aguas abajo en la ruta DAX nativa del radio siempre limita, independientemente de esta configuración, cuando se usa el modo Measure.

## Relacionado

- [Adjust TCI TX gain](adjust-tci-tx-gain.md)
- [Enable the TCI server for Log4OM / SunSDR clients](enable-the-tci-server-for-log4om-sunsdr-clients.md)
