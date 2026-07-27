# Descripción general de los controles de TX

*Introducido en v0.9.0. Actualizado para v26.7.4.*

El applet de controles de TX proporciona todos los controles relacionados con la transmisión: medidores de potencia directa y ROE, controles deslizantes de potencia RF/Tune, selector de perfil de TX y botones TUNE/MOX/ATU/MEM. También incluye el conmutador APD (predistorsión adaptativa) con indicadores de estado Activo/Cal/Disponible.

## Cómo abrir el applet de controles de TX

1. Haga clic en el botón de la bandeja TX (icono TX) en la barra lateral derecha de la ventana principal.
2. El applet de controles de TX se abre como un panel flotante.

## Medidores de potencia directa y ROE

El medidor de potencia directa muestra la potencia de salida en el excitador. Una barra de retención de pico sigue la potencia de pilo envolvente (PEP) en cada transmisión con una retención de 2 segundos y una caída gradual de vuelta al nivel de potencia suavizado actual. La retención de pico se restablece a cero inmediatamente cuando el transmisor se desactiva.

Coloque el cursor del ratón sobre el medidor de potencia directa para mostrar el valor exacto en vatios (p. ej., "34 W"). Esta lectura es útil para leer niveles de potencia precisos entre las marcas de 40 W durante la transmisión.

El medidor de ROE muestra la relación de onda estacionaria en la salida del excitador.

Coloque el cursor del ratón sobre el medidor de ROE para mostrar la relación exacta en la forma convencional N.N:1 (p. ej., "1.88:1").

El medidor de potencia directa se escala automáticamente según el modelo de radio conectado:
- FlexRadio sin amplificador: 0–120 W (zona roja por encima de 100 W)
- Con amplificador Aurora 500W: 0–600 W (zona roja por encima de 500 W)

## Controles deslizantes de RF Power y Tune Pwr

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| RF Power | 100 | 0–100 | Establece el nivel de potencia de RF de transmisión como porcentaje del máximo. Al arrastrar el control deslizante, aparece un tooltip con el valor en porcentaje (p. ej., "75%"). Al soltar el control deslizante, se sincroniza el valor final desde el modelo. |
| Tune Pwr | 10 | 0–100 | Establece el nivel de potencia de la portadora de sintonía para operaciones de ajuste como porcentaje del máximo. Al arrastrar el control deslizante, aparece un tooltip con el valor en porcentaje (p. ej., "25%"). Al soltar el control deslizante, se sincroniza el valor final desde el modelo. |

Ambos controles deslizantes muestran un tooltip con el valor actual en porcentaje mientras arrastra el control. El tooltip aparece junto al control deslizante y se actualiza en tiempo real mientras ajusta el valor. El color de relleno del control deslizante sigue el tema seleccionado.

Cuando suelta el control deslizante, el valor se sincroniza desde el modelo para garantizar la coherencia. Esto evita que el control deslizante muestre un valor diferente al que la radio está usando realmente.

## Selector de perfil de TX

El cuadro combinado de perfil de TX enumera todos los perfiles de TX almacenados en la radio. Seleccionar un perfil lo carga en el slice activo.

## Botones de control de transmisión

| Botón | Tipo | Comportamiento |
|---|---|---|
| TUNE | Botón pulsador | Inicia/detiene una portadora de sintonía. El texto del botón cambia a "TUNING..." con fondo rojo mientras está activo. Haga clic derecho para seleccionar la forma de la portadora. |
| MOX | Botón conmutador | Conmuta la transmisión manual. El botón se vuelve rojo mientras transmite. Se enruta a través del coordinador de tonos Quindar cuando el chip QUIN está habilitado. En estado inactivo, MOX tiene un acento ámbar (borde y texto) para distinguirlo visualmente de los botones neutros TUNE/ATU/MEM. Este acento se puede editar en el Editor de temas usando los tokens `color.tx.mox.*`. |
| ATU | Botón pulsador | Inicia el ciclo de sintonización del ATU interno. Haga clic derecho para acceder a opciones de pre-sintonía y gestión de memoria. |
| MEM | Botón conmutador | Activa/desactiva la memoria de recall del ATU. |

## Menú contextual del botón TUNE

Haga clic derecho en el botón TUNE para seleccionar la forma de la portadora para el próximo ciclo de sintonía. Esta es una configuración de un solo uso: la elección no se conserva entre ciclos de alimentación.

Opciones disponibles:
- **Mono Tone** — Portadora de tono único
- **Two Tone** — Portadora de dos tonos para pruebas de distorsión por intermodulación

La selección actual muestra una marca de verificación junto a la opción activa.

## Menú contextual del botón ATU

Haga clic derecho en el botón ATU para acceder a funciones de sintonía adicionales. El menú aparece cuando MEM está habilitado.

Opciones disponibles:
- **Pre-tune bands…** — Abre el diálogo de barrido de pre-sintonía para ejecutar barridos de sintonía en múltiples bandas (requiere MEM habilitado)
- **Clear ATU memories…** — Borra todas las memorias del ATU almacenadas después de la confirmación

## Comportamiento del botón ATU

El botón ATU conmuta entre iniciar un ciclo de sintonía y cambiar el sintonizador a bypass, según el estado actual del ATU y la frecuencia de transmisión.

| Situación | Qué hace un clic en ATU |
|---|---|
| No hay sintonía previa en esta frecuencia, o el ATU no está en estado Correcto/OK | Inicia un nuevo ciclo de sintonía del ATU |
| El estado del ATU es Correcto o OK, y la frecuencia de TX no ha cambiado desde la última sintonía | Cambia el ATU a bypass |
| El estado del ATU es Correcto o OK, pero la frecuencia de TX ha cambiado desde la última sintonía | Inicia un nuevo ciclo de sintonía del ATU |

En la práctica:
- El primer clic en una frecuencia nueva siempre inicia un ciclo de sintonía.
- Después de una sintonía exitosa, hacer clic en ATU nuevamente en la misma frecuencia pone el sintonizador en bypass.
- Cambiar la frecuencia restablece el conmutador, por lo que el siguiente clic inicia un nuevo ciclo de sintonía independientemente del estado anterior.
- Entrar en bypass borra la frecuencia sintonizada almacenada, por lo que el siguiente clic siempre inicia una nueva sintonía.

## Indicadores de estado del ATU

| Indicador | Color | Significado |
|---|---|---|
| Success | Verde | El resultado de la sintonía del ATU es exitoso u OK |
| Byp | Naranja | El ATU está en Bypass o ManualBypass |
| Mem | Verde | El ATU está usando una memoria almacenada |

## Controles APD (Predistorsión adaptativa)

El botón conmutador APD activa o desactiva la predistorsión adaptativa en la radio. Cuando está activado, tres indicadores de estado muestran el progreso de la calibración.

| Control/Indicador | Tipo | Comportamiento |
|---|---|---|
| APD | Botón conmutador | Activa/desactiva la predistorsión adaptativa |
| Active | Indicador (verde) | Se enciende cuando APD está activado y el ecualizador se aplica activamente |
| Cal | Indicador (verde) | Se enciende cuando APD está activado y aún está calibrando |
| Avail | Indicador (verde) | Se enciende cuando APD está activado y hay una calibración disponible pero aún no aplicada |

Los indicadores de estado de APD siguen esta progresión: Cal (calibrando) → Avail (listo) → Active (aplicado).

## MOX y tonos Quindar

A partir de v0.9.7, hacer clic en MOX se enruta a través del coordinador de tonos Quindar en lugar de conmutar la transmisión directamente. Cuando el chip QUIN está habilitado en la tira de canales de audio y el slice TX activo está en un modo de voz, hacer clic en MOX para activar la transmisión reproduce el tono K y hacer clic nuevamente para desactivarla reproduce el tono BK. Cuando Quindar está desactivado o el slice TX activo no está en un modo de voz, MOX se comporta como antes y conmuta la transmisión directamente.

## Consejos

- La barra de retención de pico de potencia directa le ayuda a monitorear la PEP durante la transmisión de voz. La retención de 2 segundos le da tiempo para leer el valor, y la caída gradual evita saltos molestos.
- Coloque el cursor sobre el medidor de potencia directa para leer la potencia exacta en vatios, lo cual es especialmente útil al ajustar entre las marcas de 40 W.
- Coloque el cursor sobre el medidor de ROE para ver la relación exacta en la forma convencional N.N:1, lo que facilita ajustes precisos de ROE.
- Use el menú contextual del botón TUNE para seleccionar una portadora de dos tonos para pruebas de distorsión por intermodulación cuando trabaje con amplificadores externos.
- El menú contextual del botón ATU proporciona acceso a la pre-sintonía de múltiples bandas a la vez, ahorrando tiempo durante los cambios de banda.
- Si Byp se enciende después del ciclo de sintonía, el ATU no pudo encontrar una coincidencia y se ha puesto en bypass. Verifique su sistema de antena y la ROE antes de transmitir a máxima potencia.
- Si Mem se enciende, el ATU aplicó una memoria de sintonía almacenada previamente en lugar de ejecutar una sintonía completa. Esto es normal cuando MEM está habilitado y existe una memoria válida para la frecuencia actual.
- Para forzar manualmente el sintonizador a bypass después de una sintonía exitosa, haga clic en ATU una segunda vez sin cambiar la frecuencia.
- Al ajustar los controles deslizantes de RF Power o Tune Pwr, el tooltip que aparece mientras arrastra muestra el valor exacto en porcentaje, lo que facilita los ajustes finos. Suelte el control deslizante para sincronizar el valor final con la radio.
- El acento ámbar del botón MOX (borde y texto) cuando está inactivo lo distingue visualmente de los otros botones, confirmando que está a punto de activar el transmisor. Este acento se puede personalizar en el Editor de temas usando los tokens `color.tx.mox.*`.

## Solución de problemas

- **El botón ATU no responde** — El TGXL de la radio está en modo OPERATE. El ATU está desactivado en este modo. Saque el TGXL del modo OPERATE antes de intentar sintonizar.
- **El indicador Success no se enciende después de la sintonía** — El ATU puede haberse puesto en bypass (verifique Byp) o la potencia de la portadora de sintonía puede ser demasiado baja para que el ATU funcione con su antena. Aumente Tune Pwr e intente nuevamente.
- **Al hacer clic en ATU se pone en bypass en lugar de sintonizar** — El estado del ATU es Correcto u OK y la frecuencia de TX no ha cambiado desde la última sintonía. Este es el comportamiento de bypass esperado al segundo clic. Cambie la frecuencia para forzar un nuevo ciclo de sintonía, o deje el sintonizador en su estado de coincidencia actual.
- **Los tonos Quindar no se reproducen en MOX** — Confirme que el chip QUIN está habilitado en la tira de canales de audio y que el slice TX activo está configurado en un modo de voz. Los tonos Quindar no se reproducen en modos CW o digitales.
- **El menú contextual del botón TUNE no responde** — Es posible que la radio no esté conectada o que los controles de TX estén en un estado de transición. Asegúrese de que la radio esté conectada e intente nuevamente.

## Relacionados

- [Recall an ATU memory](recall-an-atu-memory.md)
- [Start a tune carrier to check SWR](start-a-tune-carrier-to-check-swr.md)
- [Set tune-carrier power](set-tune-carrier-power.md)
- Ejecutar un barrido de pre-sintonía
- Borrar memorias del ATU
