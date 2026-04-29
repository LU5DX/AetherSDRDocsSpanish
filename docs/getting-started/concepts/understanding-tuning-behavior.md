# Cómo funciona la sintonización: las cinco formas de cambiar de frecuencia

AetherSDR trata las distintas acciones de sintonización de manera diferente, y lo hace a propósito. Cuando desplaza el panadapter, hace clic en un spot, escribe una frecuencia en el VFO o recupera una memoria, cada acción produce un resultado sutilmente distinto. Esta página explica qué esperar de cada una.

## Resumen rápido

| Acción | Resultado |
|---|---|
| Rueda del ratón o desplazamiento en trackpad, mando VFO, arrastre del VFO en el espectro, teclas de flecha, FlexControl, codificador USB, MIDI | Cambia la frecuencia. El panadapter solo se desplaza ligeramente si el slice (rebanada de espectro activa) se acerca al borde del rango visible. |
| Clic en el espectro, clic en un spot de DX ordinario, selección de una entrada del band-stack | La frecuencia salta al objetivo. El panadapter *revela* el objetivo si estaba fuera de pantalla; de lo contrario, permanece en su lugar. |
| Escritura de una frecuencia en el VFO, diálogo **Go To Frequency**, recuperación de una memoria, clic en un spot de memoria | La frecuencia salta. El panadapter siempre se recentra en la nueva frecuencia. |
| Botones de zoom, pellizco para hacer zoom, control deslizante de ancho de banda, atajo de zoom `+` / `-`, arrastre del panadapter | Solo se aplica zoom o panorámica al panadapter. La frecuencia no cambia. |
| El slice activo queda fuera de pantalla al cambiar de slice | El panadapter trae el slice a la vista sin centrarlo de forma forzada. |

## Sintonización incremental — ajustes pequeños

Cuando *ajusta* la frecuencia mediante la rueda del ratón, el mando VFO, el arrastre del marcador VFO en el espectro, las teclas de flecha, un FlexControl o codificador USB, controles relativos de MIDI o la función Zero Beat, AetherSDR asume que está realizando cambios pequeños y continuos. Sintoniza la radio sin recentrar el panadapter. Mientras el slice permanezca dentro de la región central del rango visible, la pantalla no se mueve.

Si el slice se desplaza lo suficiente hacia el borde (aproximadamente un 12% desde cualquiera de los lados), el panadapter se mueve paso a paso para mantener el slice a la vista. No salta al centro; simplemente avanza discretamente detrás de usted. Esto es lo que hace que la sintonización con la rueda resulte fluida en lugar de brusca.

Si tiene **View > Pan Follows VFO** desactivado, el panadapter permanece completamente estático incluso cuando el slice se sale del borde. Esto resulta útil cuando sintoniza en un panadapter mientras observa otro.

## Saltos absolutos — sintonización por objetivo

Al hacer clic en una frecuencia del espectro, clic en un spot del cluster de DX o al seleccionar una entrada del band-stack, AetherSDR salta directamente a ese objetivo. El panadapter *revela* entonces la nueva frecuencia si estaba fuera de pantalla o cerca del borde (dentro de aproximadamente un 18%); pero si el objetivo ya era claramente visible, la pantalla no se mueve en absoluto.

Esto evita el comportamiento de "salta al centro cada vez que hago clic" que presentan los clientes SDR más antiguos. Si desea echar un vistazo a un spot sin perder la vista de las señales a su alrededor, al hacer clic se sintoniza allí sin alterar el contexto de pantalla.

## Centro por comando — recuperaciones precisas

Cuando sabe exactamente a dónde quiere ir —escribiendo una frecuencia en el VFO y presionando Enter, usando el diálogo **Go To Frequency**, recuperando una memoria o haciendo clic en un spot de *memoria* (no en un spot ordinario del cluster)— AetherSDR lo trata como una orden para posicionarse con precisión en esa frecuencia y centra el panadapter de forma forzada sobre ella.

La distinción es importante: un spot ordinario del cluster de DX puede estar cerca de donde ya está sintonizado, por lo que al hacer clic solo se desplaza ligeramente la vista. Pero recuperar una memoria es una acción explícita de "llévame allí", por lo que la pantalla siempre salta al centro.

## Panorámica y zoom explícitos — sin sintonización

Los botones de zoom, el pellizco para hacer zoom en un trackpad o pantalla táctil, el arrastre del control deslizante de ancho de banda, el zoom con teclado `+` / `-` o el arrastre lateral del panadapter cambian únicamente la visualización, no la frecuencia. La radio sigue recibiendo en el mismo slice; usted solo cambia cuánto espectro ve y dónde está centrado.

Los cambios de centro y ancho de banda se envían a la radio como un único comando combinado, por lo que el waterfall (cascada) y el espectro permanecen sincronizados durante el zoom. No aparecerán los artefactos de borde del waterfall ni la deriva de zoom que podían ocurrir en versiones anteriores.

## Revelar fuera de pantalla — cambio entre slices

Cuando activa un slice diferente que está fuera de pantalla, AetherSDR lo trae a la vista sin centrarlo de forma forzada. El panadapter se desplaza hasta que el slice es visible, generalmente manteniéndolo hacia un lado de la pantalla en lugar de saltar al centro. Esto preserva lo que estaba observando mientras le muestra el slice activo.

Si desea el slice activo exactamente en el centro, utilice la acción explícita **Center Slice** (clic derecho en la letra del slice, o el atajo de teclado si ha configurado uno). Esta acción sí aplica un centrado forzado real.

## Acciones que siempre recentran

Algunas acciones siempre recentran de forma forzada, independientemente de las reglas anteriores:

- **Botones de banda y el menú de banda** — el cambio de banda recentra.
- **Restauración del estado por banda** (cargar una configuración guardada por banda) — recentra.
- **La acción explícita Center Slice** — recentra bajo demanda.

Estas son acciones de tipo comando en las que se solicita un reinicio limpio, por lo que son deliberadamente más directas que la sintonización contextual.

## Consejos

- **¿La pantalla salta al desplazar la rueda?** Asegúrese de que está usando la rueda o el desplazamiento del trackpad, no el clic de sintonización. El desplazamiento es incremental; los clics son saltos.
- **¿Quiere que la pantalla siga el VFO de cerca?** Aumente el zoom del panadapter para que el slice choque con la ventana de activación con mayor frecuencia. Así, pequeños cambios del VFO ya superarán el umbral del 12% y desplazarán la pantalla.
- **¿Está sintonizando de forma remota y no desea ningún movimiento automático de pantalla?** Desactive `View > Pan Follows VFO`. Todo el movimiento de rueda o codificador dejará el panadapter completamente estático.
- **¿La animación se ve extraña?** Los desplazamientos de centro pequeños se animan suavemente en aproximadamente ~110 ms. Los desplazamientos grandes o los cambios de ancho de banda son instantáneos — no tienen animación porque resultaría lenta.

## Solución de problemas

- **El panadapter sigue recentrándose después de que escribo una frecuencia.** Así está diseñado: la entrada en el VFO es un objetivo por comando, por lo que la pantalla siempre se centra de forma forzada. Use la rueda del ratón o el mando VFO si prefiere un comportamiento de desplazamiento gradual.
- **Al hacer clic en un spot, a veces recentra y otras veces no.** Los spots ordinarios del cluster solo recentran si el objetivo estaba fuera de pantalla. Los spots de memoria siempre recentran. Si el comportamiento le sorprende, verifique si el spot es un spot de memoria o una entrada regular del cluster o band-stack.
- **Mi slice activo fuera de pantalla aparece pero no está centrado.** Esa es la política de revelar fuera de pantalla. Use **Center Slice** de forma explícita para saltar a él.
- **Los clics entre panadapters se sienten entrecortados.** El cambio de slice activo se difiere deliberadamente para evitar inestabilidad de la interfaz durante el gesto. Si desea trabajar en un panadapter específico, haga clic una vez para activar su slice y luego sintonice.

## Relacionados

- [Comprender los slices y los VFOs](understanding-slices.md)
- [Comprender el panel de applets de AetherSDR](understanding-applets.md)
