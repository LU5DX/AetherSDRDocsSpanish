# Descripción general de AetherClock

AetherClock es un applet de visualización de base de tiempo de precisión y diagnóstico de alineación de reloj para la aplicación AetherSDR. Muestra el estado de bloqueo GNSS (GPS) de la radio, mide la deriva del reloj entre la radio y su PC local en nanosegundos, y le permite alinear el reloj de su PC con la referencia disciplinada por GPS de la radio para obtener marcas de tiempo con precisión de muestra.

## Cómo funciona

El applet AetherClock se conecta a su radio FLEX-8600 y muestra tres elementos de información:

- **Indicador de estado de bloqueo GNSS** — Muestra si el receptor GPS de la radio tiene una fijación de tiempo válida. Los estados posibles son:
  - **Locked** — La radio tiene una referencia de tiempo GNSS válida.
  - **Unlocked** — No hay señal GNSS disponible.
  - **Acquiring** — La radio está buscando una fijación satelital.

- **Indicador de deriva del reloj** — La diferencia medida entre el reloj disciplinado por GPS de la radio y el reloj de su PC local, mostrada en nanosegundos. Un valor pequeño (idealmente inferior a 1000 ns) indica que los relojes están bien alineados.

- **Botón Align Clock** — Activa la alineación del reloj de su PC local con la referencia GPS de la radio. Esto sincroniza la base de tiempo local para que las marcas de tiempo aplicadas a los datos IQ grabados o transmitidos en streaming tengan precisión de muestra.

El applet requiere una conexión activa a una radio FLEX-8600. No conserva ninguna configuración de usuario.

## Selección de canal DAX

El selector de DAX en el applet AetherClock le permite asignar un canal DAX al slice seleccionado actualmente. El número de canales DAX disponibles coincide con la capacidad de slices de su radio:

- Las radios que admiten menos slices (por ejemplo, una FLEX-6300 con 2 receptores) muestran una lista de canales DAX más corta.
- Las radios que admiten más slices (por ejemplo, una FLEX-6700 con 8 receptores) muestran canales DAX hasta ese límite.

Si la radio no expone ningún plano DAX, el selector de DAX y el banner de advertencia asociado de "sin canal DAX" se ocultan. En dichas radios, el audio fluye a través de la alimentación nativa seam y un canal DAX cero es el estado normal y correcto.

## Cómo abrir el applet

Abra el Applet Panel (normalmente acoplado en la parte inferior de la ventana principal) y haga clic en el mosaico **AetherClock** (etiquetado como **CLK**).

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| Indicador de bloqueo GNSS | Indicador de estado | Muestra el estado de bloqueo GPS/GNSS de la radio (Locked, Unlocked, Acquiring). |
| Deriva del reloj | Pantalla numérica | Muestra la deriva medida entre el reloj GPS de la radio y el reloj del PC local en nanosegundos. |
| Align Clock | Botón pulsador | Activa la alineación del reloj del PC local con la referencia GPS de la radio. |
| Selector de canal DAX | Lista desplegable | Asigna un canal DAX (DAX 1 hasta DAX N, donde N coincide con la capacidad de slices de la radio) al slice seleccionado, o desactiva DAX. Se oculta en radios que no exponen un plano DAX. |

## Relacionados

- [Alinear el reloj local con la base de tiempo GPS de la radio](align-the-local-clock-to-the-radio-s-gps-timebase.md)
- [Verificar el estado de bloqueo GPS/GNSS de la radio](check-the-radio-s-gps-gnss-lock-status.md)
- [Supervisar la deriva del reloj entre el PC y la radio](monitor-clock-drift-between-pc-and-radio.md)
