# Asignar un botón del Ulanzi Dial a una acción de AetherSDR

Esta página le muestra cómo asignar funciones a los botones físicos y al control giratorio del Ulanzi Dial. Cada botón y la perilla giratoria pueden activar una acción diferente de AetherSDR, lo que le permite controlar su radio sin tocar el software.

## Antes de comenzar

- El Ulanzi Dial debe estar conectado y detectado por AetherSDR.
- AetherSDR debe estar ejecutándose en Linux (la función Ulanzi Dial solo está disponible en Linux).

## Pasos

1. Abra **Settings > Ulanzi Dial Mapping...**.
2. Espere a que la etiqueta de estado en la parte inferior del diálogo muestre **Connected** (en lugar de **Disconnected**).
3. Busque la píldora correspondiente al control físico que desea asignar. Las píldoras están etiquetadas como **Top Left**, **Top Middle**, **Top Right**, **Left Top**, **Left Bottom**, **Right Top**, **Right Bot** y **Dial Press**.
4. Haga clic en el cuadro combinado junto a esa píldora.
5. Seleccione la acción que desea asignar en la lista desplegable.
6. Repita el proceso para cualquier otro botón o para el control giratorio.

## Qué hace cada control

| Control | Predeterminado | Descripción |
| --- | --- | --- |
| **Top Left** | MOX toggle | Acción de acceso directo vinculada al botón físico superior izquierdo. |
| **Top Middle** | RIT toggle | Acción de acceso directo vinculada al botón físico superior central. |
| **Top Right** | Tune toggle | Acción de acceso directo vinculada al botón físico superior derecho. |
| **Left Top** | None | Acción de acceso directo vinculada al botón lateral superior izquierdo. |
| **Left Bottom** | None | Acción de acceso directo vinculada al botón lateral inferior izquierdo. |
| **Right Top** | Next slice | Acción de acceso directo vinculada al botón lateral superior derecho. |
| **Right Bot** | None | Acción de acceso directo vinculada al botón lateral inferior derecho. |
| **Dial Press** | Mute toggle | Acción de acceso directo vinculada a la presión de la perilla giratoria. |
| **Tuning:** | WheelFrequency | Lista desplegable para elegir qué controla la perilla giratoria. Las opciones incluyen frecuencia de sintonía, ancho de banda del filtro, volumen de slice/maestro/auriculares, zoom del panadapter, RIT/XIT, AGC-T, ganancia de RF, APF, velocidad de CW y potencia de RF. |
| **Reset to Defaults** | — | Restaura todas las asignaciones de botones y de la perilla giratoria a sus acciones predeterminadas. |
| **Close** | — | Cierra el diálogo. |
| **Grant access** | Oculto | Se muestra solo cuando se detecta un dial pero su dispositivo de entrada no puede abrirse en Linux. Instala una regla udev para que AetherSDR pueda leer la entrada del dial. |
| **Last event:** | — | Muestra el evento de control físico más reciente recibido del dial. |

## Consejos

- La asignación física de botón a señal está fijada por el firmware del dial. Puede cambiar qué acción de AetherSDR activa cada botón, pero no puede reasignar qué botón físico envía qué señal.
- Use **Last event:** para verificar que un botón está siendo detectado antes de asignarle una acción.

## Solución de problemas

- **El estado muestra "Disconnected"** — El dial no está siendo detectado. Verifique la conexión USB y asegúrese de que el dial esté encendido.
- **El estado muestra "Disconnected" pero aparece un botón "Grant access"** — AetherSDR no puede abrir el dispositivo de entrada del dial. Haga clic en **Grant access** y siga las instrucciones para instalar la regla udev requerida. Necesitará aprobación de administrador una vez por máquina.
- **La perilla giratoria no funciona después de asignar un botón** — La perilla giratoria se configura por separado con la lista desplegable **Tuning:**. Las asignaciones de botones y de la perilla giratoria son independientes.

## Relacionados

- [Ulanzi Dial Mapping overview](overview.md)
- [Learn a Ulanzi Dial control signature](learn-a-ulanzi-dial-control-signature.md)
