# Cómo leer el medidor de nivel de salida en el applet Tube

El medidor de nivel de salida del applet Tube muestra el nivel de pico post-saturación suavizado de su señal de audio. Úselo para confirmar que la etapa Tube no está recortando su salida y para evaluar cuánto margen dinámico queda después de aplicar la ganancia de drive y de salida.

## Antes de comenzar

- El applet Tube debe estar presente en el panel de applets.
- El editor Tube debe estar abierto. Si no lo está, haga doble clic en la etapa TUBE en el widget de cadena para abrirlo.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget de cadena para abrir el editor Tube.
2. Localice el medidor vertical en el lado derecho del editor, a la derecha de la curva de saturación. La etiqueta del encabezado dice **OUT**.
3. Haga pasar audio a través del equipo. La barra de nivel sube y baja a medida que la señal atraviesa la etapa Tube.
4. Observe el color del relleno para evaluar el margen dinámico de un vistazo (consulte los significados de los colores más abajo).
5. Lea el valor numérico en el indicador debajo de la barra para obtener una cifra precisa en dB con signo.

## Qué hace cada control

| Elemento | Qué muestra | Rango | Notas |
|---|---|---|---|
| Etiqueta de encabezado | Identifica el medidor | Dice **OUT** | Confirma que este medidor muestra el nivel de salida post-saturación. |
| Barra de nivel | Relleno de pico suavizado | −60 dB (abajo) a 0 dB (arriba) | Utiliza balística de ataque rápido (alpha = 0.6) / liberación lenta (alpha = 0.08). |
| Marcas de escala en dB | Cuadrícula de referencia estática | 0, −6, −12, −20, −40 dB etiquetados | Las líneas de marca se extienden sobre la barra para que el nivel absoluto sea legible de un vistazo. |
| Indicador numérico | Pico suavizado como valor en dB con signo | `-inf` o un valor con signo a un decimal, p. ej. `+0.0 dB` | Muestra `-inf` cuando la señal está por debajo de aproximadamente −59.5 dB. |

### Significado de los colores de la barra de nivel

| Color | Nivel aproximado | Significado |
|---|---|---|
| Verde | −60 dB a −12 dB | Abundante margen dinámico. |
| Verde lima | −12 dB a −6 dB | Nivel moderado; rango de operación normal para la mayoría de las señales. |
| Ámbar | −6 dB a −3 dB | Se acerca al recorte; considere reducir Drive o Output. |
| Rojo | Por encima de −3 dB | A 3 dB o menos del recorte. Reduzca Drive o Output para bajar el nivel. |

## Consejos

- La balística del medidor coincide con la del medidor del EQ Output Fader, por lo que la sensación visual es coherente si usa ambos applets uno al lado del otro.
- Si la barra permanece en rojo durante los picos normales de voz, reduzca el control **Output** (rango de −24 dB a +12 dB, valor predeterminado 0.0 dB) o el control **Drive** (rango de 0 dB a 24 dB, valor predeterminado 0.0 dB) hasta que el ámbar o un nivel inferior sea típico para los picos de su señal.
- La balística de liberación lenta (alpha = 0.08) hace que la barra descienda gradualmente después de un pico, lo que facilita detectar visualmente las sobrecargas transitorias.

## Relacionado

- [Descripción general del medidor de nivel de salida](overview.md)
