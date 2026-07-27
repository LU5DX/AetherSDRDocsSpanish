# Descripción general de AetherClock

AetherClock es un applet de visualización de base de tiempo de precisión y diagnóstico de alineación de reloj para la aplicación AetherSDR. Muestra el estado de bloqueo GNSS (GPS) de la radio, mide la deriva del reloj entre la radio y su PC local en nanosegundos, y le permite alinear el reloj de su PC con la referencia disciplinada por GPS de la radio para un sellado de tiempo con precisión de muestra.

## Cómo funciona

El applet AetherClock se conecta a su radio FLEX-8600 y muestra tres piezas de información:

- **Indicador de estado de bloqueo GNSS** — Muestra si el receptor GPS de la radio tiene una fijación de tiempo válida. Los estados posibles son:
  - **Locked** — La radio tiene una referencia de tiempo GNSS válida.
  - **Unlocked** — No hay señal GNSS disponible.
  - **Acquiring** — La radio está buscando una fijación por satélite.

- **Indicador de deriva del reloj** — La diferencia medida entre el reloj disciplinado por GPS de la radio y el reloj de su PC local, mostrada en nanosegundos. Un valor pequeño (idealmente por debajo de 1000 ns) indica que los relojes están bien alineados.

- **Botón Align Clock** — Activa una alineación del reloj de su PC local con la referencia GPS de la radio. Esto sincroniza la base de tiempo local para que las marcas de tiempo aplicadas a los datos de IQ grabados o transmitidos en flujo tengan precisión de muestra.

El applet requiere una conexión activa a una radio FLEX-8600. No guarda ninguna configuración de usuario.

## Cómo abrir el applet

Abra el Applet Panel (generalmente acoplado en la parte inferior de la ventana principal) y haga clic en el mosaico **AetherClock** (etiquetado como **CLK**).

## Función de cada control

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Indicador de bloqueo GNSS | Indicador de estado | Muestra el estado de bloqueo GPS/GNSS de la radio (Locked, Unlocked, Acquiring). |
| Deriva del reloj | Pantalla numérica | Muestra la deriva medida entre el reloj GPS de la radio y el reloj del PC local en nanosegundos. |
| Align Clock | Botón pulsador | Activa la alineación del reloj del PC local con la referencia GPS de la radio. |

## Relacionados

- [Alinear el reloj local con la base de tiempo GPS de la radio](align-the-local-clock-to-the-radio-s-gps-timebase.md)
- [Verificar el estado de bloqueo GPS/GNSS de la radio](check-the-radio-s-gps-gnss-lock-status.md)
- [Monitorizar la deriva del reloj entre el PC y la radio](monitor-clock-drift-between-pc-and-radio.md)
