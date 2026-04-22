# Guardar la frecuencia actual como marcador

Guarde la frecuencia, el modo y los ajustes de filtro del slice activo como un marcador en el panel Band Stack para poder volver a esa configuración con un solo clic.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El panel Band Stack solo es visible cuando hay un radio conectado.
- Sintonice el slice activo en la frecuencia que desea guardar como marcador.

## Pasos

1. Localice el panel Band Stack — la franja vertical estrecha de botones de colores ubicada al costado del panadapter.
2. Haga clic en `+` en la parte inferior del panel Band Stack.

Aparece un nuevo botón de marcador en el panel que muestra la frecuencia en MHz. Su color refleja el segmento del plan de banda correspondiente a esa frecuencia.

## Función de cada control

| Control | Comportamiento | Ajuste persistido |
|---|---|---|
| `+` | Agrega un marcador en la frecuencia actual del slice activo. | `BandStack_<serial>` |
| Botones de marcador | Haga clic para recuperar la frecuencia almacenada. Haga clic derecho para eliminar. El color refleja el segmento del plan de banda para esa frecuencia. | `BandStack_<serial>` |

## Consejos

- Los marcadores se guardan por número de serie del radio. Si conecta un radio diferente, su lista de marcadores es independiente.
- Al pasar el cursor sobre un botón de marcador, se muestra la frecuencia completa en MHz, el modo y la antena RX almacenados con él.
- Si tiene muchos marcadores, el panel se desplaza verticalmente. El botón `+` permanece fijo en la parte inferior.

## Solución de problemas

- **El botón `+` no es visible** — El panel Band Stack solo aparece cuando hay un radio conectado. Verifique su conexión a través de `Settings > Connect to Radio...`.
- **El nuevo marcador aparece en color gris** — El gris indica que la frecuencia no coincide con ningún segmento del plan de banda activo. Verifique la región de su plan de banda en `View > Band Plan`.

## Temas relacionados

- [Descripción general del Band Stack](overview.md)
- [Recuperar un marcador almacenado con un solo clic](recall-a-stored-bookmark-with-one-click.md)
- [Eliminar un marcador que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
- [Explorar visualmente las frecuencias almacenadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
