# Elegir el manejo de desbordamiento de TX por TCI (Clip, NaNGuard o Measure) para la fidelidad de tonos en modos digitales

El modo de manejo de desbordamiento de TX controla cómo AetherSDR procesa las muestras de audio provenientes del software cliente TCI que exceden el rango normal de ±1.0. Las aplicaciones de modos digitales (FT8, RTTY, etc.) pueden producir valores flotantes fuera de rango; elegir el modo correcto preserva la fidelidad de tonos bit-exacta o protege el hardware downstream según sea necesario.

## Antes de comenzar

- El servidor TCI debe estar en ejecución (el botón Enable muestra "Enabled", el estado muestra `:<port>`).
- Un cliente TCI (por ejemplo, WSJT-X, Log4OM) debe estar conectado y transmitiendo.

## Pasos

1. Haga clic derecho en el medidor/deslizador de ganancia de TX en el applet del Servidor TCI.
2. En el menú contextual **TX overflow handling**, seleccione uno de los tres modos:
   - **Clip (saturating ±1.0)** — predeterminado heredado
   - **NaN guard (zero NaN/Inf only)**
   - **Measure only (true bypass)**

La selección se conserva como `TciTxOverflowMode` y entra en vigor inmediatamente para todo el audio nuevo proveniente de clientes TCI.

## Qué hace cada control

| Modo                                | Valor de enumeración | Comportamiento                                                                                                                                                                                                                                                                                                                                                            |
|-------------------------------------|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Clip (saturating ±1.0)              | 0                    | Recorta los sobresaltos a ±1.0 de forma forzada. Introduce distorsión armónica en los sobresaltos pero protege la conversión downstream a int16.                                                                                                                                                                                                                           |
| NaN guard (zero NaN/Inf only)       | 1                    | Pasa las muestras bit-exactas; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad de tonos en modos digitales; los flotantes fuera de rango llegan al radio.                                                                                                                                                                                         |
| Measure only (true bypass)          | 2                    | Nunca modifica las muestras. Cuenta los sobresaltos para telemetría; la conversión downstream a int16 aún recorta en la ruta DAX nativa del radio.                                                                                                                                                                                                                        |
| TX overflow mode (clic derecho)     |                      | Haga clic derecho en el medidor/deslizador de ganancia de TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento de TX. Emite tciTxOverflowModeChanged. Clip recorta los sobresaltos a ±1.0 con distorsión armónica; NaNGuard preserva tonos digitales bit-exactos solo poniendo a cero NaN/Inf; Measure cuenta sobresaltos para telemetría sin modificación. Se conserva como TciTxOverflowMode (0/1/2). |

El botón Enable muestra "Enabled" cuando el servidor TCI está en ejecución y "Disabled" cuando está detenido.

## Consejos

- **El valor predeterminado es Clip (modo 0)** — los usuarios existentes no verán cambios de comportamiento después de la actualización.
- Los clientes de modos digitales suelen enviar audio exactamente a 0 dBFS; el redondeo de punto flotante puede hacer que los valores superen ligeramente ±1.0. NaN guard preserva esos bordes de tono mientras sigue protegiendo contra tramas NaN/Inf corruptas.
- La conversión downstream a int16 en la ruta DAX nativa del radio siempre recorta independientemente de esta configuración cuando se usa el modo Measure.

## Relacionado

- [Ajustar la ganancia de TX por TCI](adjust-tci-tx-gain.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
