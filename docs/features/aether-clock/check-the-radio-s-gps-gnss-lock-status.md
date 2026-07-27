# Verificar el estado de bloqueo GPS/GNSS de la radio

Abra el applet AetherClock para verificar si el receptor GPS de la radio tiene una sincronización horaria válida para su base de tiempo de precisión.

## Antes de comenzar

- La radio debe estar conectada a AetherSDR.

## Pasos

1. Abra el **panel de Applets** (haga clic en la barra de la bandeja de applets en la parte superior o inferior de la ventana principal).
2. Haga clic en el mosaico **AetherClock** (etiquetado como "CLK").
3. Observe el **indicador de bloqueo GNSS** — muestra uno de tres estados:
   - **Locked** — el receptor GPS de la radio tiene una sincronización horaria válida.
   - **Unlocked** — no hay sincronización GPS disponible.
   - **Acquiring** — el receptor está buscando satélites.

## Función de cada control

| Control | Propósito |
|---------|-----------|
| Indicador de bloqueo GNSS | Muestra el estado actual del bloqueo GPS/GNSS (Locked, Unlocked, Acquiring). |
| Deriva del reloj | Muestra la deriva medida entre el reloj GPS de la radio y el reloj de su PC local, en nanosegundos. |
| Align Clock | Alinea el reloj de la PC local con la referencia disciplinada por GPS de la radio para una sincronización precisa de las muestras. |

## Consejos

- Si el indicador muestra **Unlocked** durante más de unos minutos, verifique la conexión de la antena de la radio y asegúrese de que tenga una vista despejada del cielo.
- El estado **Acquiring** es normal después de un arranque en frío; puede tardar varios minutos en lograr un bloqueo.

## Relacionados

- [Descripción general de AetherClock](overview.md)
- [Alinear el reloj local con la base de tiempo GPS de la radio](align-the-local-clock-to-the-radio-s-gps-timebase.md)
- [Monitorear la deriva del reloj entre la PC y la radio](monitor-clock-drift-between-pc-and-radio.md)
