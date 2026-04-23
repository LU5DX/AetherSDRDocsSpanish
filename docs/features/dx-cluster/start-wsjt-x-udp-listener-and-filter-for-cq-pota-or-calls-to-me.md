# Iniciar el oyente UDP de WSJT-X y filtrar por CQ, POTA o llamadas a su indicativo

AetherSDR puede escuchar en un puerto UDP los mensajes de decodificación de WSJT-X y representar los spots resultantes en el panadapter. Use los filtros para limitar lo que aparece a llamadas CQ, activaciones POTA o estaciones que llaman a su indicativo.

## Antes de comenzar

- WSJT-X debe estar configurado para enviar mensajes UDP a la dirección y el puerto que usted defina aquí. En WSJT-X, abra **File > Settings > Reporting** y confirme que la dirección y el puerto del servidor UDP coincidan con los valores que ingrese a continuación.
- AetherSDR no necesita estar conectado a un radio para que el oyente funcione, pero los spots solo aparecen en el panadapter cuando hay un radio conectado.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. En **Address:**, ingrese la dirección UDP de enlace donde AetherSDR debe escuchar (almacenada como `WsjtxAddress`). Use `127.0.0.1` si WSJT-X se ejecuta en el mismo equipo.
4. En **Port:**, establezca el puerto UDP para que coincida con la configuración de reporte de WSJT-X (almacenado como `WsjtxPort`; rango válido: 1–65535).
5. Haga clic en **Start**. El indicador de estado cambia a **Listening**.
6. Para iniciar el oyente automáticamente al arrancar, haga clic en **Auto-start on startup** (almacenado como `WsjtxAutoStart`).
7. Active uno o más filtros:
   - Marque **CQ** para mostrar solo llamadas CQ (almacenado como `WsjtxFilterCQ`).
   - Marque **CQ POTA** para mostrar llamadas CQ POTA (almacenado como `WsjtxFilterPOTA`).
   - Marque **Calling Me** para mostrar solo decodificaciones dirigidas a su indicativo (almacenado como `WsjtxFilterCallingMe`).
8. Opcionalmente, ajuste **Spot Life:** para controlar cuántos segundos permanecen los spots de WSJT-X en el panadapter (almacenado como `WsjtxSpotLife`).
9. Confirme que las transmisiones decodificadas aparecen en la consola **WSJT-X Decodes**.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración | Valor predeterminado | Rango válido |
|---|---|---|---|---|
| **Address:** | Dirección UDP de enlace para los mensajes de WSJT-X | `WsjtxAddress` | — | — |
| **Port:** | Puerto UDP para WSJT-X | `WsjtxPort` | — | 1–65535 |
| **Start / Stop** | Inicia o detiene el oyente UDP | — | — | — |
| **Auto-start on startup** | Inicia el oyente automáticamente al arrancar | `WsjtxAutoStart` | — | — |
| **CQ** | Mostrar solo llamadas CQ | `WsjtxFilterCQ` | — | — |
| **CQ POTA** | Mostrar llamadas CQ POTA | `WsjtxFilterPOTA` | — | — |
| **Calling Me** | Mostrar solo decodificaciones dirigidas a su indicativo | `WsjtxFilterCallingMe` | — | — |
| **CQ color** | Selector de color para spots CQ | `WsjtxColorCQ` | — | — |
| **POTA color** | Selector de color para spots POTA | `WsjtxColorPOTA` | — | — |
| **Calling Me color** | Selector de color para estaciones que le llaman | `WsjtxColorCallingMe` | — | — |
| **Default color** | Selector de color para todos los demás spots de WSJT-X | `WsjtxColorDefault` | — | — |
| **Spot Life:** | Segundos que los spots de WSJT-X permanecen en el panadapter | `WsjtxSpotLife` | — | — |
| **WSJT-X Decodes** | Consola de solo lectura de transmisiones decodificadas | — | — | — |

## Consejos

- Si ninguno de los tres filtros (**CQ**, **CQ POTA**, **Calling Me**) está marcado, todos los spots decodificados pasan al panadapter.
- El filtro **Calling Me** compara contra el indicativo que AetherSDR recibe de WSJT-X en cada mensaje de decodificación, por lo que asegúrese de que su indicativo esté correctamente configurado en WSJT-X.
- Puede asignar colores distintos a cada categoría de filtro para que las llamadas CQ, las activaciones POTA y las estaciones que le llaman sean visualmente distinguibles en el panadapter. Use los selectores **CQ color**, **POTA color**, **Calling Me color** y **Default color** en la misma pestaña.
- Los spots decodificados se integran en la pestaña unificada **Spot List** junto con los spots de otras fuentes. Use las casillas de banda disponibles allí para acotar la vista.

## Solución de problemas

- **No aparecen spots en WSJT-X Decodes** — Verifique que la dirección y el puerto en AetherSDR coincidan con la dirección y el puerto del servidor UDP configurados en WSJT-X en **File > Settings > Reporting**. Confirme que el estado del oyente muestre **Listening** y no **Stopped**. Compruebe que su cortafuegos no esté bloqueando el puerto UDP.
- **Los spots aparecen en la consola pero no en el panadapter** — Confirme que la superposición principal de spots esté habilitada. Abra la pestaña **Display** en SpotHub y verifique que **Spots:** esté establecido en **Enabled** (`IsSpotsEnabled`). Confirme también que hay un radio conectado, ya que la superposición en el panadapter requiere una conexión de radio activa.
- **Solo aparecen algunos spots** — Uno o más filtros están activos. Si desea ver todas las decodificaciones, desmarque **CQ**, **CQ POTA** y **Calling Me**.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Consultar activaciones POTA](poll-pota-activations.md)
