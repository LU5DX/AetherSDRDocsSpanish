# Seleccionar el modo iambic A o B para el manipulador del radio

Elija entre el modo iambic Curtis A y el modo B para el manipulador integrado del FLEX-8600. La configuración se aplica tanto al manipulador de hardware del radio como al manipulador de software local de AetherSDR, que refleja el estado del radio para proporcionar sidetone de baja latencia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Phone/CW no está disponible cuando no hay ningún radio conectado.
- Un paddle debe estar cableado al conector de llave del radio para que el manipulador iambic funcione.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Phone/CW**.
3. Confirme que **Iambic:** esté configurado en **Enabled**. Si indica **Disabled**, haga clic una vez para habilitar el manipulador iambic.
4. Haga clic en **A** o **B** para seleccionar el modo iambic Curtis deseado.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Valores válidos | Comportamiento |
|---|---|---|---|---|
| **Iambic:** | Botón de alternancia | — | Enabled / Disabled | Habilita o deshabilita el manipulador iambic en el radio. Debe estar habilitado antes de que la selección de modo tenga efecto. |
| **Iambic Mode: A / B** | Botón de selección (par mutuamente excluyente) | A | A / B | Selecciona el modo iambic Curtis A o el modo B tanto para el manipulador del radio como para el manipulador de software local. |
| **Swap:** | Botón de alternancia | — | Enabled / Disabled | Intercambia las entradas de paddle de dit y dah. |

## Consejos

- El modo A (Curtis A) libera el último elemento cuando ambos paddles se sueltan en medio de una pulsación combinada. El modo B (Curtis B) completa el último elemento antes de detenerse. Elija según su estilo de envío.
- El manipulador de software local refleja el modo que seleccione aquí, proporcionando una respuesta de sidetone inferior a 5 ms independientemente de la latencia de red.

## Relacionados

- [Descripción general de Radio Setup](overview.md)
- [Configurar las funciones de los pines del puerto serie de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
