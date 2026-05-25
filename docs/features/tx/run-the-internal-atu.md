# Resumen de los controles de TX

*Introducido en v0.9.0. Actualizado para v26.5.3.*

El applet Controles de TX proporciona todos los controles relacionados con la transmisión: medidores de potencia directa y ROE, deslizadores de potencia RF/Tune, selector de perfil de TX y botones TUNE/MOX/ATU/MEM. También incluye la opción de APD (Predistorsión Adaptativa) con indicadores de estado Activo/Cal/Disponible.

## Cómo abrir el applet Controles de TX

1. Haga clic en el botón de la bandeja TX (icono TX) en la barra lateral derecha de la ventana principal.
2. El applet Controles de TX se abre como un panel flotante.

## Medidores de potencia directa y ROE

El medidor de potencia directa muestra la potencia de salida en el excitador. Una barra de retención de pico sigue la potencia envolvente de pico (PEP) en cada transmisión con una retención de 2 segundos y una caída gradual de regreso al nivel de potencia suavizado actual. La retención de pico se restablece a cero inmediatamente cuando el transmisor se desactiva.

El medidor de ROE muestra la relación de onda estacionaria en la salida del excitador.

El medidor de potencia directa se escala automáticamente según el modelo de radio conectado:
- FlexRadio sin amplificador: 0–120 W (zona roja por encima de 100 W)
- Con amplificador Aurora 500W: 0–600 W (zona roja por encima de 500 W)

## Deslizadores de RF Power y Tune Pwr

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| RF Power | 100 | 0–100 | Establece el nivel de potencia de RF de transmisión en vatios. Al arrastrar el control deslizante, aparece una información sobre herramientas que muestra el valor en vatios (p. ej., "75 W"). |
| Tune Pwr | 10 | 0–100 | Establece el nivel de potencia de la portadora de sintonía para operaciones de sintonización. Al arrastrar el control deslizante, aparece una información sobre herramientas que muestra el valor en vatios (p. ej., "25 W"). |

Ambos deslizadores ahora muestran una información sobre herramientas con el valor actual en vatios mientras arrastra el control. La información aparece junto al control deslizante y se actualiza en tiempo real a medida que ajusta el valor.

## Selector de perfil de TX

El cuadro combinado de perfil de TX lista todos los perfiles de TX almacenados en la radio. Seleccionar un perfil lo carga en el slice activo.

## Botones de control de transmisión

| Botón | Tipo | Comportamiento |
|---|---|---|
| TUNE | Botón pulsador | Inicia/detiene una portadora de sintonía. El texto del botón cambia a "SINTONIZANDO..." con fondo rojo mientras está activo. Haga clic derecho para seleccionar la forma de la portadora. |
| MOX | Botón de alternancia | Alterna la transmisión manual. El botón se vuelve rojo mientras transmite. Se enruta a través del coordinador de tonos Quindar cuando el chip QUIN está habilitado. |
| ATU | Botón pulsador | Inicia el ciclo de sintonización del ATU interno. Haga clic derecho para opciones de pre-sintonización y gestión de memoria. |
| MEM | Botón de alternancia | Alterna la activación/desactivación de la recuperación de la memoria del ATU. |

## Menú contextual del botón TUNE

Haga clic derecho en el botón TUNE para seleccionar la forma de la portadora para el próximo ciclo de sintonía. Esta es una configuración de un solo uso: la elección no se conserva al apagar el equipo.

Opciones disponibles:
- **Mono Tone** — Portadora de un solo tono
- **Two Tone** — Portadora de dos tonos para pruebas de distorsión por intermodulación

La selección actual muestra una marca de verificación junto a la opción activa.

## Menú contextual del botón ATU

Haga clic derecho en el botón ATU para acceder a funciones de sintonización adicionales. El menú aparece cuando MEM está habilitado.

Opciones disponibles:
- **Pre-tune bands…** — Abre el diálogo de barrido de pre-sintonización para ejecutar barridos de sintonía en múltiples bandas (requiere MEM habilitado)
- **Clear ATU memories…** — Borra todas las memorias del ATU almacenadas después de la confirmación

## Comportamiento del botón ATU

El botón ATU alterna entre iniciar un ciclo de sintonía y cambiar el sintonizador a derivación, según el estado actual del ATU y la frecuencia de transmisión.

| Situación | Lo que hace el clic en ATU |
|---|---|
| Sin sintonía previa en esta frecuencia, o el ATU no está en un estado Exitoso/OK | Inicia un ciclo de sintonía ATU fresco |
| El estado del ATU es Exitoso o OK, y la frecuencia de TX no ha cambiado desde la última sintonía | Cambia el ATU a derivación |
| El estado del ATU es Exitoso o OK, pero la frecuencia de TX ha cambiado desde la última sintonía | Inicia un ciclo de sintonía ATU fresco |

En la práctica:
- El primer clic en una frecuencia nueva siempre inicia un ciclo de sintonía.
- Después de una sintonía exitosa, al hacer clic en ATU nuevamente en la misma frecuencia, se deriva el sintonizador.
- Cambiar la frecuencia restablece la alternancia, por lo que el siguiente clic inicia un ciclo de sintonía fresco independientemente del estado anterior.
- Entrar en derivación borra la frecuencia sintonizada almacenada, por lo que el siguiente clic siempre inicia una sintonía fresca.

## Indicadores de estado del ATU

| Indicador | Color | Significado |
|---|---|---|
| Success | Verde | El resultado de la sintonía del ATU es exitoso o OK |
| Byp | Naranja | El ATU está en derivación o derivación manual |
| Mem | Verde | El ATU está usando una memoria almacenada |

## Controles APD (Predistorsión Adaptativa)

El botón de alternancia APD activa o desactiva la predistorsión adaptativa en la radio. Cuando está activado, tres indicadores de estado muestran el progreso de la calibración.

| Control/Indicador | Tipo | Comportamiento |
|---|---|---|
| APD | Botón de alternancia | Activa/desactiva la predistorsión adaptativa |
| Active | Indicador (verde) | Iluminado cuando APD está activado y el ecualizador se aplica activamente |
| Cal | Indicador (verde) | Iluminado cuando APD está activado y aún está calibrando |
| Avail | Indicador (verde) | Iluminado cuando APD está activado y hay una calibración disponible pero aún no aplicada |

Los indicadores de estado de APD siguen esta progresión: Cal (calibrando) → Avail (listo) → Active (aplicado).

## MOX y tonos Quindar

A partir de v0.9.7, al hacer clic en MOX se enruta a través del coordinador de tonos Quindar en lugar de activar la transmisión directamente. Cuando el chip QUIN está habilitado en la tira de canales de audio y el slice de TX activo está en un modo de teléfono, al hacer clic en MOX para iniciar la transmisión se reproduce el tono K, y al hacer clic nuevamente para finalizar, se reproduce el tono BK. Cuando Quindar está deshabilitado o el slice de TX activo no está en un modo de teléfono, MOX se comporta como antes y activa la transmisión directamente.

## Consejos

- La barra de retención de pico de potencia directa le ayuda a monitorear la PEP durante la transmisión de voz. La retención de 2 segundos le da tiempo para leer el valor, y la caída gradual evita saltos que distraigan.
- Use el menú contextual del botón TUNE para seleccionar una portadora de dos tonos para pruebas de distorsión por intermodulación cuando trabaje con amplificadores externos.
- El menú contextual del botón ATU proporciona acceso a la pre-sintonización de múltiples bandas a la vez, ahorrando tiempo durante los cambios de banda.
- Si Byp se ilumina después del ciclo de sintonía, el ATU no pudo encontrar una coincidencia y se ha derivado. Verifique su sistema de antena y la ROE antes de transmitir a máxima potencia.
- Si Mem se ilumina, el ATU aplicó una memoria de sintonía almacenada previamente en lugar de ejecutar una sintonía completa. Esto es normal cuando MEM está habilitado y existe una memoria válida para la frecuencia actual.
- Para forzar manualmente el sintonizador a derivación después de una sintonía exitosa, haga clic en ATU una segunda vez sin cambiar la frecuencia.
- Al ajustar los deslizadores de RF Power o Tune Pwr, la información sobre herramientas que aparece al arrastrar muestra el valor exacto en vatios, lo que facilita los ajustes finos.

## Solución de problemas

- **El botón ATU no responde** — El TGXL de la radio está en modo OPERATE. El ATU está deshabilitado en este modo. Cambie el TGXL fuera del modo OPERATE antes de intentar sintonizar.
- **El indicador Success no se enciende después de la sintonía** — Es posible que el ATU se haya derivado (verifique Byp) o que la potencia de la portadora de sintonía sea demasiado baja para que el ATU funcione con su antena. Aumente Tune Pwr e intente nuevamente.
- **Al hacer clic en ATU, se deriva en lugar de sintonizar** — El estado del ATU es Exitoso o OK y la frecuencia de TX no ha cambiado desde la última sintonía. Este es el comportamiento esperado de derivación en el segundo clic. Cambie la frecuencia para forzar un ciclo de sintonía fresco, o deje el sintonizador en su estado de adaptación actual.
- **Los tonos Quindar no se reproducen en MOX** — Confirme que el chip QUIN está habilitado en la tira de canales de audio y que el slice de TX activo está configurado en un modo de teléfono. Los tonos Quindar no se reproducen en modo CW o digital.
- **El menú contextual del botón TUNE no responde** — Es posible que la radio no esté conectada o que los controles de TX estén en un estado de transición. Asegúrese de que la radio esté conectada e intente nuevamente.

## Relacionados

- [Recall an ATU memory](recall-an-atu-memory.md)
- [Start a tune carrier to check SWR](start-a-tune-carrier-to-check-swr.md)
- [Set tune-carrier power](set-tune-carrier-power.md)
- Run a pre-tune sweep
- Clear ATU memories
