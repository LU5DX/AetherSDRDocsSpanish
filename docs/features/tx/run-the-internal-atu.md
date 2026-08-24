# Resumen de los controles TX

*Introducido en la versión v0.9.0. Actualizado para la v26.8.4.*

El applet Controles TX proporciona todos los controles relacionados con la transmisión: medidores de potencia directa y ROE, deslizadores de potencia RF/Tono, selector de perfil TX y botones TUNE/MOX/ATU/MEM. También incluye el conmutador APD (Predistorsión Adaptativa) con indicadores de estado Activo/Cal/Disponible.

## Apertura del applet Controles TX

1. Haga clic en el botón de la bandeja TX (icono TX) en la barra lateral derecha de la ventana principal.
2. El applet Controles TX se abre como un panel flotante.

## Medidores de potencia directa y ROE

El medidor de potencia directa muestra la potencia de salida en el excitador. Una barra de retención de pico sigue la potencia de envolvente de pico (PEP) en cada transmisión con una retención de 2 segundos y una caída gradual de vuelta al nivel de potencia suavizado actual. La retención de pico se restablece a cero inmediatamente cuando el transmisor se desactiva.

Pase el cursor del mouse sobre el medidor de potencia directa para mostrar el valor exacto en vatios (por ejemplo, "34 W"). Esta lectura es útil para leer niveles de potencia precisos entre las marcas de 40 W durante la transmisión.

El medidor de ROE muestra la relación de onda estacionaria en la salida del excitador.

Pase el cursor del mouse sobre el medidor de ROE para mostrar la relación exacta en la forma convencional N.N:1 (por ejemplo, "1.88:1").

El medidor de potencia directa se escala automáticamente según el modelo de radio conectado:
- FlexRadio sin amplificador: 0–120 W (zona roja por encima de 100 W)
- Con amplificador Aurora 500W: 0–600 W (zona roja por encima de 500 W)

Ambos medidores se limpian inmediatamente cuando el transmisor se desactiva: la aguja de potencia directa vuelve a cero y la aguja de ROE vuelve a su posición de reposo de 1.0. Esto evita que lecturas obsoletas permanezcan después de que termina una transmisión.

## Deslizadores de potencia RF y Tono

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| RF Power | 100 | 0–100 | Establece el nivel de potencia de RF de transmisión como porcentaje del máximo. Al arrastrar el control deslizante, una información sobre herramientas muestra el valor en porcentaje (por ejemplo, "75%"). Al soltar el control deslizante, se sincroniza el valor final desde el modelo. |
| Tune Pwr | 10 | 0–100 | Establece el nivel de potencia de la portadora de sintonía para operaciones de ajuste como porcentaje del máximo. Al arrastrar el control deslizante, una información sobre herramientas muestra el valor en porcentaje (por ejemplo, "25%"). Al soltar el control deslizante, se sincroniza el valor final desde el modelo. |

Ambos deslizadores muestran una información sobre herramientas con el valor actual en porcentaje mientras arrastra el control. La información aparece junto al control deslizante y se actualiza en tiempo real mientras ajusta el valor. El color de relleno del deslizador sigue el tema seleccionado.

Cuando suelta el control deslizante, el valor se sincroniza desde el modelo para garantizar la coherencia. Esto evita que el deslizador informe un valor diferente al que la radio está usando realmente.

## Selector de perfil TX

El cuadro combinado de perfil TX enumera todos los perfiles TX almacenados en la radio. Al seleccionar un perfil, este se carga en el slice activo.

## Botones de control de transmisión

| Botón | Tipo | Comportamiento |
|---|---|---|
| TUNE | Botón pulsador | Inicia/detiene una portadora de sintonía. El texto del botón cambia a "TUNING..." con fondo rojo mientras está activo. Haga clic derecho para seleccionar la forma de la portadora. |
| MOX | Botón de alternancia | Alterna la transmisión manual. El botón se pone rojo mientras transmite. Se enruta a través del coordinador de tonos Quindar cuando el chip QUIN está habilitado. En estado inactivo, MOX tiene un acento ámbar (borde y texto) para distinguirlo visualmente de los botones neutros TUNE/ATU/MEM. Este acento se puede editar en el Editor de temas usando los tokens `color.tx.mox.*`. |
| ATU | Botón pulsador | Inicia el ciclo de sintonía del ATU interno. Deshabilitado en radios sin sintonizador o cuando el TGXL está en modo OPERATE. Haga clic derecho para opciones de pre-sintonía y gestión de memoria. |
| MEM | Botón de alternancia | Alterna el uso de memoria del ATU. Deshabilitado en radios sin sintonizador o cuando el TGXL está en modo OPERATE. |

## Menú de clic derecho del botón TUNE

Haga clic derecho en el botón TUNE para seleccionar la forma de la portadora para el próximo ciclo de sintonía. Esta es una configuración de un solo uso: la elección no se conserva entre ciclos de encendido.

Opciones disponibles:
- **Mono Tone** — Portadora de tono único
- **Two Tone** — Portadora de dos tonos para pruebas de distorsión por intermodulación

La selección actual muestra una marca de verificación junto a la opción activa.

## Menú de clic derecho del botón ATU

Haga clic derecho en el botón ATU para acceder a funciones de sintonía adicionales. El menú aparece cuando MEM está habilitado.

Opciones disponibles:
- **Pre-tune bands…** — Abre el diálogo de barrido de pre-sintonía para ejecutar barridos de sintonía en múltiples bandas (requiere MEM habilitado)
- **Clear ATU memories…** — Borra todas las memorias ATU almacenadas después de la confirmación

## Comportamiento del botón ATU

El botón ATU alterna entre iniciar un ciclo de sintonía y cambiar el sintonizador a bypass, dependiendo del estado actual del ATU y la frecuencia de transmisión.

| Situación | Lo que hace el clic en ATU |
|---|---|
| Sin sintonía previa en esta frecuencia, o el ATU no está en estado Exitoso/OK | Inicia un nuevo ciclo de sintonía ATU |
| El estado del ATU es Exitoso u OK, y la frecuencia TX no ha cambiado desde la última sintonía | Cambia el ATU a bypass |
| El estado del ATU es Exitoso u OK, pero la frecuencia TX ha cambiado desde la última sintonía | Inicia un nuevo ciclo de sintonía ATU |

En la práctica:
- El primer clic en una frecuencia nueva siempre inicia un ciclo de sintonía.
- Después de una sintonía exitosa, hacer clic en ATU nuevamente en la misma frecuencia pone el sintonizador en bypass.
- Cambiar de frecuencia restablece la alternancia, por lo que el siguiente clic inicia un nuevo ciclo de sintonía independientemente del estado anterior.
- Activar el bypass borra la frecuencia sintonizada almacenada, por lo que el siguiente clic siempre inicia una sintonía nueva.

Cuando los botones ATU y MEM están deshabilitados, pasar el cursor sobre cualquiera de los botones muestra el motivo:
- **This radio has no antenna tuner** — El modelo de radio conectado no tiene hardware ATU.
- **Disabled — TGXL is in OPERATE mode** — El sintonizador externo TGXL está en modo OPERATE.

## Indicadores de estado del ATU

| Indicador | Color | Significado |
|---|---|---|
| Success | Verde | El resultado de sintonía del ATU es exitoso u OK |
| Byp | Naranja | El ATU está en Bypass o ManualBypass |
| Mem | Verde | El ATU está usando una memoria almacenada |

## Controles APD (Predistorsión Adaptativa)

El botón de alternancia APD habilita o deshabilita la predistorsión adaptativa en la radio. Cuando está habilitado, tres indicadores de estado muestran el progreso de la calibración.

| Control/Indicador | Tipo | Comportamiento |
|---|---|---|
| APD | Botón de alternancia | Alterna la predistorsión adaptativa activada/desactivada |
| Active | Indicador (verde) | Iluminado cuando APD está activado y el ecualizador se aplica activamente |
| Cal | Indicador (verde) | Iluminado cuando APD está activado y aún se está calibrando |
| Avail | Indicador (verde) | Iluminado cuando APD está activado y hay una calibración disponible pero aún no aplicada |

Los indicadores de estado APD siguen esta progresión: Cal (calibrando) → Avail (listo) → Active (aplicado).

La fila APD se oculta por completo cuando la radio conectada no admite predistorsión adaptativa, de modo que un botón APD con apariencia activa nunca aparezca sin función detrás.

## MOX y tonos Quindar

A partir de la v0.9.7, hacer clic en MOX se enruta a través del coordinador de tonos Quindar en lugar de alternar la transmisión directamente. Cuando el chip QUIN está habilitado en la tira de canales de audio y el slice TX activo está en un modo de fonía, hacer clic en MOX para activar la transmisión reproduce el tono K y hacer clic nuevamente para desactivarla reproduce el tono BK. Cuando Quindar está deshabilitado o el slice TX activo no está en un modo de fonía, MOX se comporta como antes y alterna la transmisión directamente.

## Consejos

- La barra de retención de pico de potencia directa le ayuda a monitorear la PEP durante la transmisión de voz. La retención de 2 segundos le da tiempo para leer el valor, y la caída gradual evita saltos distractores.
- Pase el cursor sobre el medidor de potencia directa para leer la potencia exacta en vatios, lo cual es especialmente útil al ajustar finamente entre las marcas de 40 W.
- Pase el cursor sobre el medidor de ROE para ver la relación exacta en la forma convencional N.N:1, lo que facilita ajustes precisos de ROE.
- Use el menú de clic derecho del botón TUNE para seleccionar una portadora de dos tonos para pruebas de distorsión por intermodulación cuando trabaje con amplificadores externos.
- El menú de clic derecho de ATU proporciona acceso a la pre-sintonía de múltiples bandas a la vez, ahorrando tiempo durante los cambios de banda.
- Si Byp se enciende después del ciclo de sintonía, el ATU no pudo encontrar una coincidencia y se ha puesto en bypass. Verifique su sistema de antena y la ROE antes de transmitir a plena potencia.
- Si Mem se enciende, el ATU aplicó una memoria de sintonía almacenada previamente en lugar de ejecutar una sintonía completa. Esto es normal cuando MEM está habilitado y existe una memoria válida para la frecuencia actual.
- Para forzar manualmente el sintonizador a bypass después de una sintonía exitosa, haga clic en ATU una segunda vez sin cambiar de frecuencia.
- Al ajustar los deslizadores RF Power o Tune Pwr, la información sobre herramientas que aparece mientras arrastra muestra el valor exacto en porcentaje, lo que facilita los ajustes finos. Suelte el control deslizante para sincronizar el valor final con la radio.
- El acento ámbar del botón MOX (borde y texto) cuando está inactivo lo distingue visualmente de los otros botones, confirmando que está a punto de activar la transmisión. Este acento se puede personalizar en el Editor de temas usando los tokens `color.tx.mox.*`.

## Solución de problemas

- **El botón ATU no responde** — El TGXL de la radio está en modo OPERATE, o la radio no tiene hardware ATU. Pase el cursor sobre el botón ATU para ver qué motivo corresponde. Cambie el TGXL fuera del modo OPERATE antes de intentar sintonizar, o use un sintonizador externo si la radio no tiene uno.
- **El indicador Success no se enciende después de sintonizar** — El ATU puede haberse puesto en bypass (verifique Byp) o la potencia de la portadora de sintonía puede ser demasiado baja para que el ATU funcione con su antena. Aumente Tune Pwr e intente nuevamente.
- **Al hacer clic en ATU se activa el bypass en lugar de sintonizar** — El estado del ATU es Exitoso u OK y la frecuencia TX no ha cambiado desde la última sintonía. Este es el comportamiento esperado del segundo clic. Cambie de frecuencia para forzar un nuevo ciclo de sintonía, o deje el sintonizador en su estado de adaptación actual.
- **Los tonos Quindar no se reproducen en MOX** — Confirme que el chip QUIN está habilitado en la tira de canales de audio y que el slice TX activo está configurado en un modo de fonía. Los tonos Quindar no se reproducen en modos CW o digitales.
- **El menú de clic derecho del botón TUNE no responde** — La radio puede no estar conectada o los controles TX pueden estar en un estado transitorio. Asegúrese de que la radio esté conectada e intente nuevamente.
- **El medidor de potencia o ROE muestra una lectura obsoleta después de desactivar la transmisión** — Los medidores están diseñados para limpiarse inmediatamente cuando el transmisor se desactiva. Si una lectura persiste, esto indica un problema de firmware o conexión. Vuelva a conectar la radio e intente nuevamente.

## Relacionados

- [Recall an ATU memory](recall-an-atu-memory.md)
- [Start a tune carrier to check SWR](start-a-tune-carrier-to-check-swr.md)
- [Set tune-carrier power](set-tune-carrier-power.md)
- Run a pre-tune sweep
- Clear ATU memories
