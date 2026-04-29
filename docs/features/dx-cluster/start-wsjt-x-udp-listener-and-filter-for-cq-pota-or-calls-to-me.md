# Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí

Configure AetherSDR para recibir transmisiones decodificadas de WSJT-X por UDP y mostrar únicamente las categorías de spots que le interesan — llamadas CQ, activaciones POTA o estaciones que lo llamen a usted — como superposiciones en el panadapter.

## Antes de comenzar

- WSJT-X debe estar ejecutándose en la misma máquina o red, y configurado para enviar mensajes de estado UDP a la dirección y puerto que establecerá aquí.
- Conozca la dirección UDP y el puerto al que WSJT-X está transmitiendo (verifíquelo en WSJT-X en **File > Settings > Reporting**, sección UDP Server).
- Su indicativo debe estar configurado en WSJT-X para que el filtro "Calling Me" funcione.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. En **Address:**, ingrese la dirección de enlace UDP en la que AetherSDR debe escuchar (almacenada como `WsjtxAddress`). Use `127.0.0.1` si WSJT-X se ejecuta en la misma máquina, o `0.0.0.0` para escuchar en todas las interfaces.
4. En **Port:**, ingrese el número de puerto UDP que coincida con el puerto configurado en WSJT-X (almacenado como `WsjtxPort`; rango válido 1–65535).
5. Haga clic en **Start**. El indicador de estado cambia a **Listening**.
6. Para iniciar el receptor automáticamente cada vez que AetherSDR se inicie, habilite **Auto-start on startup (WSJT-X)** (almacenado como `WsjtxAutoStart`).
7. En las casillas de verificación de filtro, habilite una o más de las siguientes opciones para restringir qué decodificaciones aparecen como spots en el panadapter:
   - **CQ** — muestra estaciones que envían una llamada CQ general (almacenado como `WsjtxFilterCQ`).
   - **CQ POTA** — muestra estaciones que envían CQ POTA (almacenado como `WsjtxFilterPOTA`).
   - **Calling Me** — muestra decodificaciones dirigidas a su indicativo (almacenado como `WsjtxFilterCallingMe`).
8. Opcionalmente, asigne un color distintivo a cada categoría haciendo clic en el botón de color correspondiente:
   - **CQ color** (almacenado como `WsjtxColorCQ`)
   - **POTA color** (almacenado como `WsjtxColorPOTA`)
   - **Calling Me color** (almacenado como `WsjtxColorCallingMe`)
   - **Default color** para decodificaciones que no coincidan con ningún filtro activo (almacenado como `WsjtxColorDefault`)
9. Establezca **Spot Life:** con el número de segundos que un spot de WSJT-X debe permanecer visible en el panadapter (almacenado como `WsjtxSpotLife`).
10. Confirme que las transmisiones decodificadas están llegando en la consola **WSJT-X Decodes** en la parte inferior de la pestaña.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración | Valor predeterminado / Rango |
|---|---|---|---|
| **Address:** | Dirección de enlace UDP para mensajes entrantes de WSJT-X. | `WsjtxAddress` | — |
| **Port:** | Número de puerto UDP. Debe coincidir con el puerto de reporte de WSJT-X. | `WsjtxPort` | 1–65535 |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — | — |
| **Auto-start on startup (WSJT-X)** | Inicia el receptor automáticamente al arrancar. | `WsjtxAutoStart` | — |
| **CQ** | Pasa al panadapter solo transmisiones CQ. | `WsjtxFilterCQ` | — |
| **CQ POTA** | Pasa solo transmisiones CQ POTA. | `WsjtxFilterPOTA` | — |
| **Calling Me** | Pasa solo decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` | — |
| **CQ color** | Color para los spots CQ en el panadapter. | `WsjtxColorCQ` | — |
| **POTA color** | Color para los spots CQ POTA. | `WsjtxColorPOTA` | — |
| **Calling Me color** | Color para los spots que lo llaman a usted. | `WsjtxColorCallingMe` | — |
| **Default color** | Color para los spots que no coinciden con ningún filtro activo. | `WsjtxColorDefault` | — |
| **Spot Life:** | Segundos que un spot de WSJT-X permanece en el panadapter antes de desaparecer. | `WsjtxSpotLife` | — |
| **WSJT-X Decodes** | Consola de solo lectura que muestra las transmisiones decodificadas a medida que llegan. | — | — |

## Consejos

- Si ninguna de las tres casillas de filtro (**CQ**, **CQ POTA**, **Calling Me**) está marcada, todas las transmisiones decodificadas se muestran en el panadapter independientemente de su contenido.
- Los spots de WSJT-X aparecen en la pestaña unificada **Spot List** junto con spots de otras fuentes. Haga doble clic en cualquier fila para sintonizar directamente esa frecuencia.
- Los spots de WSJT-X solo aparecerán en el panadapter si el interruptor principal **Spots:** de la pestaña **Display** está habilitado (almacenado como `IsSpotsEnabled`; valor predeterminado: habilitado).
- FT8 opera en ciclos de 15 segundos. Mantenga **Spot Life:** en 15 segundos o un múltiplo de ese valor para que los spots expiren limpiamente entre ciclos.

## Solución de problemas

- **El estado permanece en Stopped / no aparecen decodificaciones en la consola** — Verifique que la dirección y el puerto en AetherSDR coincidan exactamente con los configurados en WSJT-X en **File > Settings > Reporting**. Confirme que ningún firewall esté bloqueando el puerto UDP. Haga clic en **Stop** y luego en **Start** después de corregir los valores.
- **Los spots aparecen en la pestaña Spot List pero no en el panadapter** — Abra `Settings > SpotHub...`, vaya a la pestaña **Display** y confirme que **Spots:** esté configurado como Enabled.
- **El filtro "Calling Me" no muestra ningún spot** — WSJT-X debe tener su indicativo ingresado en su configuración y debe estar decodificando activamente transmisiones dirigidas a ese indicativo. Verifique su indicativo en WSJT-X en **File > Settings > General**.

## Temas relacionados

- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Consultar activaciones POTA](poll-pota-activations.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
