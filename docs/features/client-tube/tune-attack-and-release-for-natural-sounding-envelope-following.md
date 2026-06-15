# Ajuste de Ataque y Liberación para un seguimiento de envolvente de sonido natural

Ataque y Liberación determinan la rapidez con que el seguidor de envolvente rastrea los niveles de señal crecientes y decrecientes. Solo surten efecto cuando Envelope está ajustado a un valor distinto de cero. Ajustar estos dos mandos evita que el carácter de tubo se active y desactive de forma antinatural durante los transitorios del habla o del audio.

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- Envelope debe ajustarse a un valor distinto de cero. Ataque y Liberación no tienen efecto audible al 0 %. Consulte [Use Envelope to add dynamic drive on transients](use-envelope-to-add-dynamic-drive-on-transients.md).
- Abra el editor flotante del lado que desea ajustar: haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX. El editor se titula "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX.
2. Localice el mando Attack en la columna derecha del editor.
3. Ajuste Attack para definir la rapidez con que el seguidor de envolvente responde cuando los niveles de señal aumentan. Los valores más bajos hacen que el seguidor reaccione más rápido a los transitorios; los valores más altos suavizan los picos breves.
4. Localice el mando Release directamente debajo de Attack en la columna derecha.
5. Ajuste Release para definir la rapidez con que el seguidor se recupera después de que los niveles disminuyen. Los valores más bajos devuelven la excitación al reposo más rápido; los valores más altos prolongan el efecto después de un pico.
6. Supervise la curva de transferencia y la bola de entrada en vivo mientras transmite o recibe para confirmar que la modulación de la excitación parece natural.

## Edición inline de valores

En v26.5.2.1 y versiones posteriores, todos los mandos del editor Aetherial Tube admiten la entrada directa de texto. Haga clic en el valor numérico que se muestra debajo de cualquier mando para activar una superposición QLineEdit inline que reemplaza el texto del valor pintado. Escriba un número (con o sin unidades) y presione Enter, o haga clic en otro lugar, para confirmar. El valor se limita al rango válido del mando.

- Introduzca "12.5 ms", "−6 dB" o "0.75": el editor elimina automáticamente las etiquetas finales.
- En configuraciones regionales que usan coma como separador decimal, "12,5" se analiza correctamente.
- Presione Escape para cancelar la edición y revertir al valor anterior.
- Mientras el editor inline está enfocado, los eventos de rueda del ratón se reenvían al mando para un ajuste tradicional.
- La superposición utiliza un fondo oscuro sutil y un borde cian al enfocarse para mayor visibilidad.

## Qué hace cada control

| Control    | Valor predeterminado | Rango válido                                                               |
|------------|----------------------|----------------------------------------------------------------------------|
| Attack     | 5.00 ms              | 0.1 a 30.0 ms                                                              |
| Release    | 35.00 ms             | 10.0 a 500.0 ms                                                            |
| RN2        | Alternancia solo TX (oculta en modo RX). Habilita el eliminador de ruido neuronal RNNoise en la entrada de micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al gate/compresor/saturador. | Ubicado en el StripTubePanel flotante debajo del medidor de nivel de salida, solo lado TX. Solo modos de voz: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. Configuración persistida a través de AudioEngine. |

**Attack** — Utiliza mapeo exponencial en todo su rango. Define la rapidez con que el seguidor de envolvente responde a los niveles de señal crecientes cuando Envelope ≠ 0. La etiqueta se muestra como "X.XX ms" por debajo de 10 ms y "X.X ms" por encima de 10 ms. Clave de configuración: `ClientTubeTxAttackMs` / `ClientTubeRxAttackMs`.

**Release** — Utiliza mapeo exponencial en todo su rango. Define la rapidez con que el seguidor de envolvente se recupera después de que los niveles de señal caen cuando Envelope ≠ 0. La etiqueta se muestra como "X.XX ms" por debajo de 100 ms y "X.X ms" por encima de 100 ms. Clave de configuración: `ClientTubeTxReleaseMs` / `ClientTubeRxReleaseMs`.

**RN2** — Botón de alternancia solo TX ubicado en StripTubePanel debajo del medidor de nivel de salida. Usa la etiqueta `RN2`. Consulte [Reduce background noise with RN2](reduce-background-noise-with-rn2.md) para obtener todos los detalles.

## Consejos

- Attack y Release son independientes por lado. Los cambios realizados en el editor TX no afectan al editor RX y viceversa.
- Para un habla de sonido natural en TX, comience con los valores predeterminados (Attack 5.00 ms, Release 35.00 ms) y alargue Release primero. Valores de Release muy cortos pueden producir un carácter de bombeo o castañeteo.
- Para la conformación de tonos en RX, un Attack más largo (10 ms o más) permite que los picos transitorios pasen antes de que el seguidor de envolvente se active, preservando las consonantes iniciales en el audio recibido.
- La bola de entrada en vivo en la curva de transferencia se mueve en tiempo real. Con Envelope ajustado, puede ver el punto de operación cambiar a medida que los niveles cambian, lo que ayuda a confirmar que Attack y Release se sienten correctos antes de salir al aire.
- Cuando la etapa de tubo está puenteada, todo el mosaico acoplado del applet se atenúa aproximadamente al 55 % de opacidad. Esta señal visual se aplica tanto a los mosaicos TX como RX y facilita la confirmación de un vistazo de que la etapa no está procesando audio. El mosaico vuelve a la opacidad completa tan pronto como la etapa se vuelve a habilitar.
- Los colores visuales del mando (anillo de fondo, arco, puntero, etiqueta y texto del valor) están controlados por el tema en v26.6.1 y versiones posteriores. Respetan la anulación del contenedor por applet (por ejemplo, el color ámbar del primer plano del mando exclusivo del applet de compresión) recorriendo la jerarquía de widgets hasta `applet/tube`.

## Solución de problemas

- **Ajustar Attack o Release no tiene efecto audible**: es probable que Envelope esté ajustado al 0 %. Ajuste Envelope a un valor positivo o negativo primero; Attack y Release solo se aplican cuando el seguidor de envolvente está activo.
- **El efecto suena demasiado abrupto o castañeteante**: Release está ajustado demasiado bajo. Aumente Release hacia 100 ms o más para suavizar la recuperación.
- **Los picos fuertes hacen que la excitación se active bruscamente**: Attack está ajustado demasiado bajo. Aumente Attack a 10–20 ms para ralentizar la respuesta del seguidor a los transitorios.
- **El mosaico acoplado se ve atenuado y la etapa no está procesando**: la etapa de tubo está puenteada. El mosaico se atenúa al 55 % de opacidad cuando está puenteado. Vuelva a habilitar la etapa para restaurar la opacidad completa y reanudar el procesamiento. Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- **Escribir un valor en el editor inline no tiene efecto**: asegúrese de presionar Enter o hacer clic en otro lugar para confirmar. Presionar Escape cancela la edición y revierte al valor anterior.

## Relacionados

- [Use Envelope to add dynamic drive on transients](use-envelope-to-add-dynamic-drive-on-transients.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
- [Reduce background noise with RN2](reduce-background-noise-with-rn2.md)
