# Cómo funciona el sintonizado: las cinco formas de cambiar la frecuencia

AetherSDR trata las diferentes acciones de sintonizado de forma distinta, y esto es intencional. Cuando desplaza el panadapter, hace clic en un spot, escribe una frecuencia en el VFO o recupera una memoria, cada acción produce un resultado sutilmente diferente. Esta página explica qué esperar de cada una.

## Resumen rápido

| Acción | Qué ocurre |
|---|---|
| Rueda del ratón o desplazamiento del trackpad, mando del VFO, arrastre del VFO en el espectro, teclas de flecha, FlexControl, encoder USB, MIDI | La frecuencia cambia. El panadapter solo se desplaza ligeramente si el slice (segmento de recepción) se acerca al borde del rango visible. |
| Clic en el espectro, clic en un spot DX ordinario, selección de una entrada del band-stack | La frecuencia salta al objetivo. El panadapter *revela* el objetivo si estaba fuera de pantalla; de lo contrario, permanece en su lugar. |
| Escribir una frecuencia en el VFO, diálogo **Go To Frequency**, recuperar una memoria, hacer clic en un spot de memoria | La frecuencia salta. El panadapter siempre se recentra en la nueva frecuencia. |
| Botones de zoom, pellizco para hacer zoom, control deslizante de ancho de banda, atajo de zoom `+` / `-`, arrastre panorámico | El panadapter solo hace zoom o desplazamiento panorámico. La frecuencia no cambia. |
| El cambio de slice activo queda fuera de pantalla | El panadapter acerca el slice a la vista sin centrarlo de forma forzada. |

## Sintonizado incremental — ajustes pequeños

Cuando *ajusta* la frecuencia —con la rueda del ratón, el mando del VFO, arrastrando el marcador del VFO en el espectro, las teclas de flecha, un FlexControl o encoder USB, controles MIDI relativos, o la función Zero Beat— AetherSDR asume que está realizando cambios pequeños y continuos. Sintoniza la radio pero no recentra el panadapter. Mientras el slice permanezca dentro de la región central del rango visible, la visualización no se mueve.

Si el slice se desplaza lo suficiente hacia el borde (aproximadamente el 12% desde cualquiera de los lados), el panadapter se mueve paso a paso para mantener el slice a la vista. No salta al centro; simplemente se desliza discretamente detrás de usted. Esto es lo que hace que el sintonizado con la rueda sea fluido en lugar de brusco.

Si tiene la opción **View > Pan Follows VFO** desactivada, el panadapter permanece completamente estático incluso cuando el slice se desplaza fuera del borde. Esto resulta útil cuando está sintonizando en un panadapter mientras observa otro.

## Saltos absolutos — sintonizado basado en objetivo

Al hacer clic en una frecuencia del espectro, en un spot del cluster DX o al seleccionar una entrada del band-stack, AetherSDR salta directamente a ese objetivo. El panadapter entonces *revela* la nueva frecuencia si estaba fuera de pantalla o cerca del borde (dentro de aproximadamente el 18%); pero si el objetivo ya estaba cómodamente visible, la visualización no se mueve en absoluto.

Esto evita el comportamiento de "salta al centro cada vez que hago clic" que muestran los clientes SDR más antiguos. Si quiere echar un vistazo a un spot sin perder la vista de las señales a su alrededor, hacer clic en él sintoniza ahí sin reorganizar su contexto.

## Centro de objetivo comandado — recuperaciones precisas

Cuando sabe exactamente adónde quiere ir —escribiendo una frecuencia en el VFO y presionando Enter, usando el diálogo **Go To Frequency**, recuperando una memoria o haciendo clic en un spot de *memoria* (no en un spot ordinario del cluster)— AetherSDR lo trata como una orden de aterrizar precisamente en esa frecuencia y centra el panadapter de forma forzada sobre ella.

La distinción es importante: un spot ordinario del cluster DX puede estar cerca de donde ya está sintonizado, por lo que hacer clic en él simplemente desplaza la vista ligeramente. Pero recuperar una memoria es una acción explícita de "llévame ahí", por lo que la visualización siempre se centra de forma forzada.

## Desplazamiento panorámico y zoom explícitos — sin sintonizado

Los botones de zoom, el pellizco para hacer zoom en un touchpad o pantalla táctil, el arrastre del control deslizante de ancho de banda, el zoom con teclado `+` / `-`, o el arrastre lateral del panadapter — estos cambios afectan únicamente la visualización, no la frecuencia. La radio sigue recibiendo en el mismo slice; usted solo cambia cuánto espectro ve y dónde está centrado.

Los cambios de centro y ancho de banda se envían a la radio como un único comando combinado, de modo que el waterfall (cascada) y el espectro permanecen sincronizados durante el zoom. No verá la pérdida de bordes en el waterfall ni la deriva del zoom que podía ocurrir en versiones anteriores.

## Revelar fuera de pantalla — cambio entre slices

Cuando activa un slice diferente y ese slice está fuera de pantalla, AetherSDR lo acerca a la vista sin centrarlo de forma forzada. Desliza el panadapter hasta que el slice sea visible, generalmente manteniéndolo hacia un lado de la pantalla en lugar de centrarlo. Esto preserva lo que estaba observando mientras le muestra el slice activo.

Si desea que el slice activo quede exactamente en el centro, use la acción explícita **Center Slice** (haga clic derecho en la letra del slice, o use el atajo de teclado si ha configurado uno). Esa opción aplica un centrado forzado real.

## Acciones que siempre recentran

Algunas acciones siempre recentran de forma forzada, independientemente de las reglas anteriores:

- **Botones de banda y el menú de bandas** — cambiar de banda recentra la visualización.
- **Restaurar el estado por banda** (cargar una configuración guardada por banda) — recentra.
- **La acción explícita Center Slice** — recentra a demanda.

Estas son acciones de tipo comando en las que se solicita un reinicio limpio, por lo que son deliberadamente más contundentes que el sintonizado contextual.

## Consejos

- **¿La visualización parece brusca al desplazar?** Asegúrese de usar la rueda del ratón o el desplazamiento del trackpad, no el clic para sintonizar. El desplazamiento es incremental; los clics son saltos.
- **¿Quiere que la visualización siga de cerca su VFO?** Aumente el zoom del panadapter para que el slice llegue al umbral de activación con más frecuencia. Así, los cambios pequeños del VFO ya cruzarán el umbral del 12% y desplazarán la visualización.
- **¿Sintoniza de forma remota y no quiere ningún movimiento automático de la visualización?** Desactive `View > Pan Follows VFO`. Toda la entrada de la rueda y el encoder dejará el panadapter sin modificar.
- **¿La animación se siente mal?** Los desplazamientos pequeños del centro se animan suavemente durante aproximadamente 110 ms. Los desplazamientos grandes o los cambios de ancho de banda se aplican de forma instantánea — no hay animación para ellos porque resultaría lenta visualmente.

## Solución de problemas

- **El panadapter sigue recentrándose después de que escribo una frecuencia.** Esto es intencional — la entrada en el VFO es un objetivo comandado, por lo que la visualización siempre se centra de forma forzada. Use la rueda del ratón o el mando del VFO si prefiere un comportamiento de solo desplazamiento.
- **Hacer clic en un spot a veces recentra y a veces no.** Los spots ordinarios del cluster solo recentran si el objetivo estaba fuera de pantalla. Los spots de memoria siempre recentran. Si el comportamiento le sorprende, verifique si el spot es un spot de memoria o una entrada ordinaria del cluster o band-stack.
- **Mi slice activo fuera de pantalla se muestra pero no está centrado.** Esa es la política de revelar fuera de pantalla. Use **Center Slice** de forma explícita para centrarlo.
- **Los clics entre panadapters se sienten entrecortados.** El cambio de slice activo se difiere deliberadamente para evitar cambios bruscos en la interfaz durante un gesto. Si quiere trabajar en un panadapter específico, haga clic una vez para activar su slice y luego sintonice.

## Relacionado

- [Entender los slices y los VFOs](understanding-slices.md)
- [Entender el panel de applets de AetherSDR](understanding-applets.md)
