# Cómo funciona la sintonización: las cinco formas de cambiar la frecuencia

AetherSDR trata las diferentes acciones de sintonización de manera distinta, a propósito. Cuando desplaza el panadapter, hace clic en un punto, escribe una frecuencia en el VFO o recupera una memoria, cada acción produce un resultado sutilmente diferente. Esta página explica qué esperar de cada una.

## La versión rápida

| Acción | Qué sucede |
|---|---|
| Desplazamiento con rueda del ratón o trackpad, mando VFO, arrastre del VFO en el espectro, teclas de flecha, FlexControl, encoder USB, MIDI | La frecuencia cambia. El panadapter solo se mueve si el slice se acerca al borde del rango visible. |
| Clic en el espectro, clic en un punto DX común, selección de una entrada del band stack | La frecuencia salta al objetivo. El panadapter *revela* el objetivo si estaba fuera de la pantalla; de lo contrario, permanece inmóvil. |
| Escribir una frecuencia en el VFO, diálogo **Go To Frequency**, recuperar una memoria, clic en un punto de memoria | La frecuencia salta. El panadapter siempre se recentra en la nueva frecuencia. |
| Botones de zoom, pellizco para zoom, control deslizante de ancho de banda, atajo de zoom `+` / `-`, arrastre panorámico | El panadapter solo hace zoom o se desplaza. La frecuencia no cambia. |
| Cambio de slice activo que queda fuera de la pantalla | El panadapter trae el slice a la vista sin centrarlo forzosamente. |

## Sintonización incremental — ajustes pequeños

Cuando *ajusta* la frecuencia — desplazamiento con la rueda del ratón, mando VFO, arrastre del marcador VFO en el espectro, teclas de flecha, un FlexControl o encoder USB, controles relativos MIDI, la función Zero Beat — AetherSDR asume que está haciendo cambios pequeños y continuos. Sintoniza el radio pero no recentra el panadapter. Mientras el slice permanezca dentro de la región central del rango visible, la pantalla no se mueve.

Si el slice se desvía lo suficiente hacia el borde (aproximadamente un 12% desde cualquier lado), el panadapter se desplaza paso a paso para mantener el slice visible. No saltará al centro; simplemente se moverá silenciosamente detrás de usted. Esto hace que la sintonización con la rueda se sienta suave en lugar de entrecortada.

Si tiene desactivado **View > Pan Follows VFO**, el panadapter permanece completamente estático incluso cuando el slice se sale del borde. Útil cuando está sintonizando en un panadapter mientras observa otro.

## Saltos absolutos — sintonización basada en objetivos

Haga clic en una frecuencia en el espectro, en un punto de un clúster DX, seleccione una entrada del band stack — AetherSDR salta directamente a ese objetivo. Luego, el panadapter *revela* la nueva frecuencia si estaba fuera de la pantalla o cerca del borde (aproximadamente un 18%), pero si su objetivo ya era claramente visible, la pantalla no se mueve en absoluto.

Esto evita el comportamiento de "salta al centro cada vez que hago clic" que exhiben los clientes SDR más antiguos. Si desea echar un vistazo a un punto sin perder la vista de las señales que lo rodean, hacer clic en él sintoniza allí sin cambiar su contexto.

## Centro objetivo comandado — recuperaciones precisas

Cuando sabe exactamente dónde quiere estar — escribir una frecuencia en el VFO y presionar Enter, usar el diálogo **Go To Frequency**, recuperar una memoria, hacer clic en un punto de *memoria* (no en un punto de clúster común) — AetherSDR lo trata como un comando para aterrizar precisamente en esa frecuencia y centra forzosamente el panadapter en ella.

La distinción es importante: un punto común de un clúster DX podría estar cerca de donde ya está sintonizado, por lo que hacer clic en él solo desplaza ligeramente la vista. Pero recuperar una memoria es una acción explícita de "lléveme allí", por lo que la pantalla siempre salta al centro.

## Desplazamiento y zoom explícitos — sin sintonización

Los botones de zoom, el pellizco para zoom en un panel táctil o pantalla táctil, arrastrar el control deslizante de ancho de banda, el zoom con teclado `+` / `-`, o arrastrar el panadapter lateralmente — estos cambian solo la pantalla, no la frecuencia. El radio continúa recibiendo en el mismo slice; solo está cambiando cuánto espectro ve y dónde está centrado.

Los cambios de centro y ancho de banda se envían al radio como un solo comando combinado, por lo que el waterfall y el espectro se mantienen sincronizados mientras hace zoom. No verá la pérdida de borde del waterfall ni la deriva del zoom que podrían ocurrir en versiones anteriores.

## Revelar fuera de la pantalla — cambiar entre slices

Cuando activa un slice diferente y ese slice está fuera de la pantalla, AetherSDR lo trae a la vista sin centrarlo forzosamente. Desplaza el panadapter hasta que el slice sea visible — generalmente manteniendo el slice hacia el lado de la pantalla en lugar de saltar al centro. Esto preserva lo que estaba viendo mientras aún le muestra el slice activo.

Si desea el slice activo exactamente en el centro, use la acción explícita **Center Slice** (clic derecho en la letra del slice, o el atajo de teclado si ha configurado uno). Esto utiliza un centrado forzoso real.

## Acciones que siempre recentran

Algunas acciones siempre centran forzosamente independientemente de las reglas anteriores:

- **Botones de banda y el menú de bandas** — cambiar de banda recentra.
- **Restaurar el estado por banda** (cargar una configuración por banda guardada) — recentra.
- **La acción explícita Center Slice** — recentra bajo demanda.

Estas son acciones de tipo comando en las que solicita un reinicio limpio, por lo que son deliberadamente más asertivas que la sintonización contextual.

## Consejos

- **¿Se siente entrecortado al desplazarse?** Asegúrese de usar el desplazamiento con la rueda del ratón o trackpad, no clic para sintonizar. El desplazamiento es incremental; los clics son saltos.
- **¿Desea que la pantalla siga su VFO de forma ajustada?** Aumente el zoom del panadapter para que el slice toque la ventana de activación con más frecuencia. De esa manera, pequeños cambios en el VFO ya cruzan el umbral del 12% y mueven la pantalla.
- **¿Sintoniza de forma remota y no desea ningún movimiento automático de la pantalla?** Desactive `View > Pan Follows VFO`. Toda la entrada de la rueda y el encoder dejará el panadapter en paz.
- **¿La animación se siente extraña?** Los pequeños desplazamientos del centro se animan suavemente durante unos 110 ms. Los cambios grandes de centro o ancho de banda saltan instantáneamente (no tienen animación porque se vería lento).

## Solución de problemas

- **El panadapter sigue recentrándose después de escribir una frecuencia.** Eso es por diseño: la entrada del VFO es un objetivo comandado, por lo que la pantalla siempre se centra forzosamente. Use la rueda del ratón o el mando VFO si desea un comportamiento de solo deriva.
- **Al hacer clic en un punto, a veces recentra y otras no.** Los puntos de clúster comunes solo recentran si el objetivo estaba fuera de la pantalla. Los puntos de memoria siempre recentran. Si el comportamiento le sorprende, verifique si el punto es un punto de memoria o una entrada regular de clúster/band stack.
- **Mi slice activo fuera de la pantalla se muestra pero no está centrado.** Es la política de revelar fuera de la pantalla. Use **Center Slice** explícitamente para saltar a él.
- **Los clics entre panadapters se sienten entrecortados.** El cambio de slice activo se retrasa deliberadamente para evitar la agitación de la interfaz durante un gesto. Si desea trabajar en un panadapter específico, haga clic una vez para activar su slice y luego sintonice.

## Relacionado

- [Entendiendo los slices y VFOs](understanding-slices.md)
- [Entendiendo el panel de applets de AetherSDR](understanding-applets.md)
