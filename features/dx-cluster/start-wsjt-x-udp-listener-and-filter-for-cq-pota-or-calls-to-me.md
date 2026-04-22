# Iniciar el oyente UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a usted

AetherSDR puede escuchar mensajes de decodificación de WSJT-X a través de UDP y colocar las estaciones coincidentes como spots en el panadapter. Use esta página para iniciar el oyente y restringir lo que aparece a llamadas CQ, activaciones POTA o decodificaciones dirigidas a su indicativo.

## Antes de comenzar

- WSJT-X debe estar en ejecución en la misma máquina o red, y configurado para enviar mensajes de estado UDP a la dirección y puerto que usted defina aquí.
- Conozca la dirección y el puerto UDP al que WSJT-X está enviando (verifique en WSJT-X bajo **File > Settings > Reporting**, campo UDP Server).
- La superposición de spots en el panadapter debe estar habilitada. Si los spots no son visibles, abra `Settings > SpotHub...`, vaya a la pestaña **Display** y confirme que **Spots:** esté establecido en Enabled.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. En **Address:**, ingrese la dirección de enlace UDP que coincida con la que WSJT-X está usando como destino (normalmente `127.0.0.1` para uso local). Se guarda como `WsjtxAddress`.
4. En **Port:**, establezca el puerto UDP para que coincida con el puerto UDP Server de WSJT-X. Rango válido: 1–65535. Se guarda como `WsjtxPort`.
5. Haga clic en **Start**. El indicador de estado cambia a **Listening**. La consola **WSJT-X Decodes** comienza a mostrar las transmisiones recibidas.
6. Habilite los filtros que desee:
   - Marque **CQ** para mostrar solo llamadas CQ. Se guarda como `WsjtxFilterCQ`.
   - Marque **CQ POTA** para mostrar llamadas CQ POTA. Se guarda como `WsjtxFilterPOTA`.
   - Marque **Calling Me** para mostrar solo las decodificaciones dirigidas a su indicativo. Se guarda como `WsjtxFilterCallingMe`.
7. Para iniciar el oyente automáticamente cada vez que AetherSDR se inicie, habilite **Auto-start on startup (WSJT-X)**. Se guarda como `WsjtxAutoStart`.

## Qué hace cada control

| Control | Función | Clave persistente |
|---|---|---|
| **Address:** | Dirección de enlace UDP para los mensajes entrantes de WSJT-X | `WsjtxAddress` |
| **Port:** | Puerto UDP en el que se escucha (1–65535) | `WsjtxPort` |
| **Start / Stop** | Inicia o detiene el oyente UDP | — |
| **Auto-start on startup (WSJT-X)** | Inicia el oyente automáticamente al arrancar | `WsjtxAutoStart` |
| **CQ** | Muestra solo llamadas CQ de las decodificaciones de WSJT-X | `WsjtxFilterCQ` |
| **CQ POTA** | Muestra llamadas CQ POTA | `WsjtxFilterPOTA` |
| **Calling Me** | Muestra solo decodificaciones dirigidas a su indicativo | `WsjtxFilterCallingMe` |
| **CQ color** | Color para los spots CQ en el panadapter | `WsjtxColorCQ` |
| **POTA color** | Color para los spots POTA en el panadapter | `WsjtxColorPOTA` |
| **Calling Me color** | Color para los spots que lo llaman a usted | `WsjtxColorCallingMe` |
| **Default color** | Color para todos los demás spots de WSJT-X | `WsjtxColorDefault` |
| **Spot Life:** | Segundos que un spot de WSJT-X permanece en el panadapter | `WsjtxSpotLife` |
| **WSJT-X Decodes** | Consola de solo lectura de las transmisiones decodificadas | — |

## Consejos

- Puede marcar cualquier combinación de **CQ**, **CQ POTA** y **Calling Me** simultáneamente. Un spot aparece si coincide con alguno de los filtros marcados. Si no hay ninguno marcado, todas las decodificaciones de WSJT-X aparecen como spots.
- Cada categoría de filtro tiene su propio selector de color. Asigne colores distintos para diferenciar de un vistazo las llamadas CQ, POTA y directas en el panadapter.
- Mantenga **Spot Life:** bajo (unos pocos segundos o un período FT8, 15 s) para evitar que decodificaciones obsoletas saturen el panadapter entre ciclos de decodificación de WSJT-X.
- La consola **WSJT-X Decodes** muestra todas las decodificaciones recibidas independientemente de los filtros activos, por lo que puede confirmar que el oyente funciona incluso antes de habilitar los filtros.

## Solución de problemas

- **El estado permanece en Stopped / no aparecen decodificaciones** — Confirme que el reporte UDP de WSJT-X esté habilitado y que su dirección y puerto UDP Server coincidan con **Address:** y **Port:** en AetherSDR. Verifique que ningún cortafuegos esté bloqueando el puerto.
- **Los spots aparecen en el panadapter pero los filtros parecen no tener efecto** — Verifique que las casillas correctas (**CQ**, **CQ POTA**, **Calling Me**) estén marcadas. Si ninguna está marcada, se muestran todas las decodificaciones.
- **El filtro Calling Me no muestra nada** — WSJT-X debe conocer su indicativo (configurado en WSJT-X bajo **File > Settings > General**) para que las decodificaciones dirigidas a usted se identifiquen correctamente.
- **La superposición de spots no es visible en absoluto** — Abra la pestaña **Display** en SpotHub y confirme que **Spots:** esté en Enabled.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
- [Consultar activaciones POTA](poll-pota-activations.md)
