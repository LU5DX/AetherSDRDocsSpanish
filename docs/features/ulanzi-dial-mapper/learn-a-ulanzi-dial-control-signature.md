# Aprenda una firma de control del Ulanzi Dial

Aprenda qué evento físico de botón o perilla recibe AetherSDR de su Ulanzi Dial, para poder verificar que un control funciona o diagnosticar por qué una asignación no se activa.

## Antes de comenzar

- Un Ulanzi Dial conectado a su máquina (solo Linux).
- AetherSDR en ejecución y capaz de leer la entrada del dial. La etiqueta de estado en la parte inferior del diálogo muestra `Connected` o `Disconnected`.

## Pasos

1. Abra **Settings > Ulanzi Dial Mapping...**.
2. Observe la etiqueta **Last event:** en la parte inferior del diálogo: muestra la firma más reciente del evento del kernel que envió el dial.
3. Presione el botón físico o gire la perilla rotatoria cuya firma desea aprender.
4. Lea la firma en la etiqueta **Last event:**. Por ejemplo, al presionar el botón superior izquierdo se muestra `Last event: KEY_PREVIOUSSONG`.

## Qué hace cada control

| Control | Comportamiento |
| --- | --- |
| **Last event:** | Muestra la firma más reciente del evento del kernel recibida del dial (p. ej. `KEY_PLAYPAUSE`, `Ctrl+V`). La firma es un comportamiento inmutable del firmware, no configurable por el usuario. |
| **Etiqueta de estado** (abajo a la izquierda) | Muestra `Connected` o `Disconnected`, además del nombre del dispositivo cuando se detecta un dial. |
| **Grant access** | Aparece solo cuando se detecta un dial pero su nodo evdev no se puede abrir. Instala una regla de udev (con aprobación del administrador) para que AetherSDR pueda leer la entrada del dial. Se requiere una vez por máquina. |
| Píldoras de anotación | Mapa visual de los controles físicos del dial con sus asignaciones de acción actuales. Este diálogo no admite entrar en modo Learn mediante las píldoras: use **Last event:** para aprender una firma. |

## Consejos

- La asignación de firma a píldora es una propiedad del firmware del dial (v1.x), no configurable por el usuario. Cambiarla requiere re-flashear el dial.
- El evento de sintonización del control rotatorio es enrutado directamente por MainWindow y no aparece como firma de botón. Use el combo **Tuning:** en la parte inferior del diálogo para cambiar lo que hace la perilla.
- Si la etiqueta de estado indica `Disconnected`, verifique que el dial está enchufado antes de intentar aprender una firma.

## Solución de problemas

- **Last event:** permanece en `—` al presionar botones: el dial no está conectado o AetherSDR no puede leer su entrada. Verifique la etiqueta de estado de conexión; si aparece **Grant access**, haga clic en él para instalar la regla de udev y luego intente de nuevo.
- **La firma que veo no coincide con lo que espero** — Las firmas están fijadas por el firmware del dial. Consulte las píldoras de anotación para ver qué control físico se asigna a qué acción.

## Relacionado

- [Descripción general de la asignación del Ulanzi Dial](overview.md)
- [Asignar un botón del Ulanzi Dial a una acción de AetherSDR](map-a-ulanzi-dial-button-to-an-aethersdr-action.md)
