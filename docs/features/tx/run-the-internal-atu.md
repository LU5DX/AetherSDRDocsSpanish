# Resumen de Controles de TX

*Introducido en v0.9.0. Actualizado para v26.5.2.1.*

El applet Controles de TX proporciona todos los controles relacionados con la transmisión: medidores de potencia directa y ROE, controles deslizantes de potencia de RF/Sintonía, selector de perfil de TX y botones TUNE/MOX/ATU/MEM. También incluye el conmutador APD (Predistorsión Adaptativa) con indicadores de estado Activo/Cal/Disponible.

## Abrir el applet Controles de TX

1. Haga clic en el botón de la bandeja TX (icono de TX) en la barra lateral derecha de la ventana principal.
2. El applet Controles de TX se abre como un panel flotante.

## Medidores de potencia directa y ROE

El medidor de potencia directa muestra la potencia de salida en el excitador. Una barra de retención de pico rastrea la potencia de pico envolvente (PEP) en cada transmisión con una retención de 2 segundos y una disminución gradual hasta el nivel de potencia suavizado actual. La retención de pico se restablece a cero inmediatamente cuando se desactiva el transmisor.

El medidor de ROE muestra la relación de onda estacionaria en la salida del excitador.

El medidor de potencia directa se escala automáticamente según el modelo de radio conectado:
- FlexRadio sin amplificador: 0–120 W (zona roja por encima de 100 W)
- Con amplificador Aurora 500W: 0–600 W (zona roja por encima de 500 W)

## Controles deslizantes de Potencia de RF y Potencia de Sintonía

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| Potencia de RF | 100 | 0–100 | Establece el nivel de potencia de RF de transmisión en vatios |
| Potencia de Sintonía | 10 | 0–100 | Establece el nivel de potencia de la portadora de sintonía para operaciones de ajuste |

## Selector de perfil de TX

El cuadro combinado de Perfil de TX enumera todos los perfiles de TX almacenados en la radio. Al seleccionar un perfil, se carga en la slice activa.

## Botones de control de transmisión

| Botón | Tipo | Comportamiento |
|---|---|---|
| TUNE | Botón pulsador | Inicia/detiene una portadora de sintonía. El texto del botón cambia a "SINTONIZANDO..." con fondo rojo mientras está activo. Haga clic derecho para seleccionar la forma de la portadora. |
| MOX | Botón conmutador | Conmuta la transmisión manual. El botón se vuelve rojo mientras transmite. Se enruta a través del coordinador de tonos Quindar cuando el chip QUIN está habilitado. |
| ATU | Botón pulsador | Inicia el ciclo de sintonía del ATU interno. Haga clic derecho para opciones de pre-sintonía y gestión de memoria. |
| MEM | Botón conmutador | Activa/desactiva la recuperación de memoria del ATU. |

## Menú contextual del botón TUNE

Haga clic derecho en el botón TUNE para seleccionar la forma de la portadora para el próximo ciclo de sintonía. Esta es una configuración de un solo uso; la elección no se conserva entre ciclos de alimentación.

Opciones disponibles:
- **Tono único** — Portadora de un solo tono
- **Dos tonos** — Portadora de dos tonos para pruebas de distorsión por intermodulación

La selección actual muestra una marca de verificación junto a la opción activa.

## Menú contextual del botón ATU

Haga clic derecho en el botón ATU para acceder a funciones de sintonía adicionales. El menú aparece cuando MEM está habilitado.

Opciones disponibles:
- **Pre-sintonizar bandas…** — Abre el diálogo de barrido de pre-sintonía para ejecutar barridos de sintonía en múltiples bandas (requiere MEM habilitado)
- **Borrar memorias del ATU…** — Borra todas las memorias del ATU almacenadas después de la confirmación

## Comportamiento del botón ATU

El botón ATU conmuta entre iniciar un ciclo de sintonía y cambiar el sintonizador a derivación, dependiendo del estado actual del ATU y la frecuencia de transmisión.

| Situación | Lo que hace al hacer clic en ATU |
|---|---|
| Sin sintonía previa en esta frecuencia, o el ATU no está en estado Exitoso/OK | Inicia un nuevo ciclo de sintonía del ATU |
| El estado del ATU es Exitoso u OK, y la frecuencia de TX no ha cambiado desde la última sintonía | Cambia el ATU a derivación |
| El estado del ATU es Exitoso u OK, pero la frecuencia de TX ha cambiado desde la última sintonía | Inicia un nuevo ciclo de sintonía del ATU |

En la práctica:
- El primer clic en una nueva frecuencia siempre inicia un ciclo de sintonía.
- Después de una sintonía exitosa, al hacer clic nuevamente en ATU en la misma frecuencia se deriva el sintonizador.
- Cambiar la frecuencia restablece el conmutador, por lo que el siguiente clic inicia un nuevo ciclo de sintonía independientemente del estado anterior.
- Al entrar en derivación se borra la frecuencia sintonizada almacenada, por lo que el siguiente clic siempre inicia una nueva sintonía.

## Indicadores de estado del ATU

| Indicador | Color | Significado |
|---|---|---|
| Éxito | Verde | El resultado de la sintonía del ATU es exitoso u OK |
| Deriv | Naranja | El ATU está en Derivación o DerivaciónManual |
| Mem | Verde | El ATU está usando una memoria almacenada |

## Controles APD (Predistorsión Adaptativa)

El botón conmutador APD activa o desactiva la predistorsión adaptativa en la radio. Cuando está activado, tres indicadores de estado muestran el progreso de la calibración.

| Control/Indicador | Tipo | Comportamiento |
|---|---|---|
| APD | Botón conmutador | Activa/desactiva la predistorsión adaptativa |
| Activo | Indicador (verde) | Se enciende cuando APD está activado y el ecualizador se aplica activamente |
| Cal | Indicador (verde) | Se enciende cuando APD está activado y aún se está calibrando |
| Disponible | Indicador (verde) | Se enciende cuando APD está activado y hay una calibración disponible pero aún no se ha aplicado |

Los indicadores de estado de APD siguen esta progresión: Cal (calibrando) → Disponible (listo) → Activo (aplicado).

## MOX y tonos Quindar

A partir de v0.9.7, al hacer clic en MOX se enruta a través del coordinador de tonos Quindar en lugar de activar la transmisión directamente. Cuando el chip QUIN está habilitado en la Tira de Canal de Audio y la slice de TX activa está en un modo de telefonía, al hacer clic en MOX para iniciar la transmisión se reproduce el tono K y al hacer clic nuevamente para finalizar se reproduce el tono BK. Cuando Quindar está deshabilitado o la slice de TX activa no está en un modo de telefonía, MOX se comporta como antes y conmuta la transmisión directamente.

## Consejos

- La barra de retención de pico de potencia directa le ayuda a monitorear la PEP durante la transmisión de voz. La retención de 2 segundos le da tiempo para leer el valor, y la disminución gradual evita saltos que distraigan.
- Use el menú contextual del botón TUNE para seleccionar una portadora de dos tonos para pruebas de distorsión por intermodulación cuando trabaje con amplificadores externos.
- El menú contextual del ATU proporciona acceso a la pre-sintonía de múltiples bandas a la vez, ahorrando tiempo durante los cambios de banda.
- Si se enciende Deriv después del ciclo de sintonía, el ATU no pudo encontrar una coincidencia y se ha derivado. Verifique su sistema de antena y ROE antes de transmitir a máxima potencia.
- Si se enciende Mem, el ATU aplicó una memoria de sintonía almacenada previamente en lugar de ejecutar una sintonía completa. Esto es normal cuando MEM está habilitado y existe una memoria válida para la frecuencia actual.
- Para forzar manualmente el sintonizador a derivación después de una sintonía exitosa, haga clic en ATU una segunda vez sin cambiar la frecuencia.

## Solución de problemas

- **El botón ATU no responde** — El TGXL de la radio está en modo OPERAR. El ATU está deshabilitado en este modo. Saque el TGXL del modo OPERAR antes de intentar sintonizar.
- **El indicador de Éxito no se enciende después de la sintonía** — Es posible que el ATU se haya derivado (verifique Deriv) o que la potencia de la portadora de sintonía sea demasiado baja para que el ATU funcione con su antena. Aumente la Potencia de Sintonía e intente nuevamente.
- **Al hacer clic en ATU se deriva en lugar de sintonizar** — El estado del ATU es Exitoso u OK y la frecuencia de TX no ha cambiado desde la última sintonía. Este es el comportamiento esperado de derivación en el segundo clic. Cambie la frecuencia para forzar un nuevo ciclo de sintonía, o deje el sintonizador en su estado de adaptación actual.
- **Los tonos Quindar no se reproducen en MOX** — Confirme que el chip QUIN está habilitado en la Tira de Canal de Audio y que la slice de TX activa está configurada en un modo de telefonía. Los tonos Quindar no se reproducen en modos CW o digitales.
- **El menú contextual del botón TUNE no responde** — Es posible que la radio no esté conectada o que los controles de TX estén en un estado transitorio. Asegúrese de que la radio esté conectada e intente nuevamente.

## Relacionados

- [Recall an ATU memory](recall-an-atu-memory.md)
- [Start a tune carrier to check SWR](start-a-tune-carrier-to-check-swr.md)
- [Set tune-carrier power](set-tune-carrier-power.md)
- [Run a pre-tune sweep](run-a-pre-tune-sweep.md)
- [Clear ATU memories](clear-atu-memories.md)
