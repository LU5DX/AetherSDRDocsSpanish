# Recuperar un marcador guardado con un solo clic

El panel Band Stack le permite saltar el panadapter a cualquier frecuencia guardada con un solo clic. Úselo cuando desee regresar rápidamente a una frecuencia que ya ha marcado sin tener que escribirla de nuevo.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El panel Band Stack solo es visible cuando hay un radio conectado.
- Al menos un marcador debe estar guardado previamente. Si el panel está vacío, consulte [Marcar la frecuencia actual](bookmark-the-current-frequency.md) primero.

## Pasos

1. Localice el panel Band Stack — la estrecha franja vertical de botones de colores ubicada junto al panadapter en la ventana principal.
2. Encuentre el botón de marcador que muestra la frecuencia deseada. Cada botón muestra la frecuencia en MHz (tres decimales). Pase el cursor sobre un botón para ver un tooltip con la frecuencia completa, el modo y la antena.
3. Haga clic en el botón de marcador. El panadapter sintoniza inmediatamente la frecuencia almacenada.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de marcador | Haga clic para sintonizar el panadapter en la frecuencia almacenada. Haga clic derecho para abrir un menú contextual con la opción **Remove**. | El color del botón refleja el segmento del plan de banda para esa frecuencia. |
| `+` | Agrega un nuevo marcador en la frecuencia actual del slice activo. | — |
| ⚙ (engranaje) | Abre el menú de opciones del Band Stack. Contiene el interruptor **Group by band** y la configuración **Auto-expiry** (Off, 5 min, 15 min, 30 min, 60 min). | — |
| × | Elimina todos los marcadores de una vez. El tooltip muestra "Clear all bookmarks". | — |

Los marcadores se guardan en `BandStack_<serial>`, donde `<serial>` es el número de serie de su radio.

## Consejos

- Si tiene muchos marcadores, desplace el panel verticalmente para encontrar el que desea. El panel cuenta con un área desplazable; el desplazamiento horizontal está desactivado.
- Active **Group by band** desde el menú ⚙ para ordenar los marcadores por banda en lugar de por orden de inserción. Esto facilita encontrar una frecuencia cuando tiene marcadores en múltiples bandas.

## Solución de problemas

- **El panel Band Stack no es visible** — El panel solo aparece cuando hay un radio conectado. Verifique su conexión mediante `Settings > Connect to Radio...`.
- **Hacer clic en un botón de marcador no hace nada** — Asegúrese de que el radio siga conectado. Si la conexión se interrumpió, reconéctese e intente nuevamente.

## Relacionados

- [Marcar la frecuencia actual](bookmark-the-current-frequency.md)
- [Eliminar un marcador que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
- [Explorar visualmente las frecuencias guardadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
- [Descripción general del Band Stack](overview.md)
