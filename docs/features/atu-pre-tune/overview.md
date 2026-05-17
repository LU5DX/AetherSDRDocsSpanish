# Descripción general del preajuste del ATU

Realiza un barrido automático a través de las bandas de HF y 6m seleccionadas, activando el ATU (Unidad de Sintonización de Antena) interno del radio en cada frecuencia central. Esto garantiza que su sintonizador tenga una solución de sintonización válida almacenada para cada banda que planee usar, reduciendo la posibilidad de una ROE alta cuando cambie de frecuencia durante una sesión de operación.

## Cómo funciona

La función de preajuste del ATU desplaza el slice activo de TX a través de un conjunto calculado de frecuencias centrales en las bandas que seleccione. En cada frecuencia, AetherSDR envía un comando `atu start` al radio y espera a que el radio informe la finalización (mediante `atuStateChanged`) antes de pasar al siguiente punto. Los bordes de banda se toman del plan de banda de la región activa, por lo que el barrido se mantiene dentro de los límites de frecuencia legales y prácticos.

## Antes de comenzar

- Debe haber un radio conectado. El diálogo de preajuste requiere una conexión activa con el radio para enviar comandos ATU.
- El radio debe tener un ATU interno o externo disponible y funcional.

## Cómo abrir el diálogo

- **Ruta de menú:** `Settings > TX Band Settings...` luego seleccione la pestaña **ATU Pre-Tune**.
- **Alternativa:** Haga clic derecho en el applet del sintonizador en el Panel de applets y elija **ATU Pre-Tune** en el menú contextual.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Band selection** | Cuadro combinado | Selecciona qué bandas de HF/6m incluir en el barrido de preajuste. Los bordes de banda siguen el plan de banda de la región activa. |
| **Start Sweep** | Botón pulsador | Inicia el barrido de preajuste del ATU. Recorre las frecuencias centrales de cada banda seleccionada y activa la sintonización del ATU en cada punto. |

## Solución de problemas

- **El barrido no comienza** — Asegúrese de que haya un radio conectado y de que exista un slice activo de TX. El diálogo requiere una conexión activa con el radio.
- **El ATU falla en algunas frecuencias** — El ATU del radio puede no encontrar una coincidencia en ciertas bandas o configuraciones de antena. Verifique que su antena resuene razonablemente en las bandas elegidas.

## Relacionados

- [Radio Setup](Radio Setup)
- [TX Band Settings](TX Band Settings)
