# Verificación del estado de bloqueo GPS/GNSS de la radio

Abra el applet AetherClock para ver si el receptor GPS de la radio tiene una fijación horaria válida para su base de tiempo de precisión.

## Antes de comenzar

- La radio debe estar conectada a AetherSDR.

## Pasos

1. Abra el **Applet panel** (haga clic en la barra de applets en la parte superior o inferior de la ventana principal).
2. Haga clic en el mosaico **AetherClock** (etiquetado como "CLK").
3. Observe el **GNSS lock indicator** — que muestra uno de tres estados:
   - **Locked** — el receptor GPS de la radio tiene una fijación horaria válida.
   - **Unlocked** — no hay fijación GPS disponible.
   - **Acquiring** — el receptor está buscando satélites.

## Qué hace cada control

| Control | Propósito |
|---------|-----------|
| GNSS lock indicator | Muestra el estado de bloqueo GPS/GNSS actual (Locked, Unlocked, Acquiring). |
| Clock drift | Muestra la deriva medida entre el reloj GPS de la radio y el reloj local de su PC, en nanosegundos. |
| Align Clock | Alinea el reloj local del PC con la referencia disciplinada por GPS de la radio para un sincronismo preciso de muestras. |

## Selección de canal DAX

El selector DAX en el applet AetherClock le permite enrutar el audio de la selección activa (slice) a un canal DAX para grabación o procesamiento. La longitud del selector coincide con la capacidad de slices de la radio: una 6300 expone dos receptores, una 6700 ocho. Las opciones disponibles son:

- **DAX Off** — desactiva el enrutamiento DAX para la selección activa seleccionada.
- **DAX 1** a **DAX N** — enruta el audio al canal DAX correspondiente, donde N es la capacidad de slices de la radio (1–8).

## Controles DAX en radios de alimentación nativa (seam-native)

En radios que utilizan una alimentación de audio nativa de seam en lugar de un plano DAX, el selector DAX y su banner de advertencia relacionado están ocultos. En estas radios:

- El audio fluye normalmente a través de la alimentación nativa de seam sin una asignación de canal DAX.
- Un canal DAX cero es el estado normal y correcto; no indica una ruta de audio faltante.
- El banner de advertencia ámbar "no DAX channel" no aparece, porque describiría una condición que no es la causa de ningún problema de audio.

## Qué significa el banner de advertencia DAX

Cuando los controles DAX están visibles (en radios que admiten un plano DAX), aparece un banner de advertencia si una selección activa en ejecución y vinculada no tiene un canal DAX seleccionado. Este banner indica que la selección activa está en ejecución, pero su audio no se está enrutando a ningún canal DAX.

Si el selector DAX está oculto (radio de alimentación nativa de seam), el banner no aparece porque el audio de la selección activa fluye a través de la alimentación nativa de la radio.

## Consejos

- Si el indicador muestra **Unlocked** durante más de unos minutos, verifique la conexión de antena de la radio y asegúrese de que tenga una vista despejada del cielo.
- El estado **Acquiring** es normal después de un arranque en frío; puede tomar varios minutos lograr una fijación.
- Si selecciona un canal DAX que está fuera de la capacidad de slices de la radio, AetherSDR configura automáticamente el selector en **DAX Off** en lugar de mostrar un valor no válido dentro del rango.

## Relacionados

- [Resumen de AetherClock](overview.md)
- [Alinear el reloj local con la base de tiempo GPS de la radio](align-the-local-clock-to-the-radio-s-gps-timebase.md)
- [Supervisar la deriva de reloj entre PC y radio](monitor-clock-drift-between-pc-and-radio.md)
