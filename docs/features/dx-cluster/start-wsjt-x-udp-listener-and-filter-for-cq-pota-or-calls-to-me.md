# Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a usted

AetherSDR puede escuchar paquetes de decodificación de WSJT-X a través de UDP y mostrar las transmisiones coincidentes como spots en el panadapter. Use los filtros para limitar lo que aparece a llamadas CQ, activaciones POTA o estaciones que lo llaman a usted.

## Antes de comenzar

- WSJT-X debe estar ejecutándose en la misma computadora o en una computadora accesible a través de la red.
- En WSJT-X, confirme que los mensajes UDP están habilitados y que la dirección de destino y el puerto coinciden con los que configurará en AetherSDR. El puerto UDP predeterminado de WSJT-X es 2237.
- Conozca su propio indicativo si tiene intención de usar el filtro "Calling Me".

## Pasos

1. Vaya a `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. En **Address:**, ingrese la dirección de enlace UDP en la que AetherSDR debe escuchar. Para aceptar paquetes desde cualquier interfaz, use `0.0.0.0`. Este valor se almacena como `WsjtxAddress`.
4. En **Port:**, establezca el puerto UDP para que coincida con el puerto de destino configurado en WSJT-X. Rango válido: 1–65535. Este valor se almacena como `WsjtxPort`.
5. Haga clic en **Start**. El indicador de estado cambia a **Listening**.
6. Para mostrar solo llamadas CQ, marque **CQ**. Este valor se almacena como `WsjtxFilterCQ`.
7. Para mostrar solo activaciones POTA, marque **CQ POTA**. Este valor se almacena como `WsjtxFilterPOTA`.
8. Para mostrar solo decodificaciones dirigidas a su indicativo, marque **Calling Me**. Este valor se almacena como `WsjtxFilterCallingMe`.
9. Para que AetherSDR inicie el receptor automáticamente cada vez que se lanza, habilite **Auto-start on startup (WSJT-X)**. Este valor se almacena como `WsjtxAutoStart`.

## Qué hace cada control

| Control | Función | Clave de configuración |
|---|---|---|
| **Address:** | Dirección de enlace UDP para los mensajes entrantes de WSJT-X. | `WsjtxAddress` |
| **Port:** | Número de puerto UDP. Rango válido: 1–65535. | `WsjtxPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. El estado muestra **Listening** cuando está activo. | — |
| **Auto-start on startup (WSJT-X)** | Inicia el receptor automáticamente cuando AetherSDR se lanza. | `WsjtxAutoStart` |
| **CQ** | Pasa al overlay de spots solo las llamadas CQ de las decodificaciones de WSJT-X. | `WsjtxFilterCQ` |
| **CQ POTA** | Pasa solo las llamadas CQ POTA. | `WsjtxFilterPOTA` |
| **Calling Me** | Pasa solo las decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` |
| **CQ color** | Selector de color para los spots CQ en el panadapter. | `WsjtxColorCQ` |
| **POTA color** | Selector de color para los spots POTA. | `WsjtxColorPOTA` |
| **Calling Me color** | Selector de color para los spots que lo llaman a usted. | `WsjtxColorCallingMe` |
| **Default color** | Selector de color para todos los demás spots de WSJT-X. | `WsjtxColorDefault` |
| **Spot Life:** | Segundos que un spot de WSJT-X permanece visible en el panadapter. | `WsjtxSpotLife` |
| **WSJT-X Decodes** | Consola de solo lectura que muestra las transmisiones decodificadas a medida que llegan. | — |

## Consejos

- Puede habilitar más de un filtro al mismo tiempo. Por ejemplo, marcar tanto **CQ** como **Calling Me** muestra las llamadas CQ y cualquier estación que lo llame a usted.
- Si no hay ningún filtro marcado, todas las decodificaciones de WSJT-X aparecen como spots.
- La consola **WSJT-X Decodes** muestra las líneas de decodificación sin procesar independientemente de los filtros activos, lo cual es útil para verificar que los paquetes están llegando.
- El tiempo de vida del spot configurado con **Spot Life:** se aplica únicamente a los spots de WSJT-X. El tiempo de vida global de los spots en el panadapter se controla por separado en la pestaña **Display**, en **Spot Lifetime:**.

## Solución de problemas

- **El estado permanece en Stopped después de hacer clic en Start** — Compruebe que ninguna otra aplicación esté enlazada al mismo puerto. Cambie **Port:** si hay un conflicto.
- **Las decodificaciones aparecen en la consola pero no en el panadapter** — Confirme que los spots estén habilitados globalmente. Vaya a `Settings > SpotHub...`, abra la pestaña **Display** y verifique que **Spots:** esté configurado como **Enabled**.
- **El filtro "Calling Me" no muestra nada** — WSJT-X debe estar configurado con su indicativo para que lo incluya en los mensajes de decodificación UDP. Verifique que el indicativo en WSJT-X coincida con el que espera que AetherSDR detecte.
- **Los paquetes no llegan desde una computadora remota** — Asegúrese de que ningún firewall esté bloqueando el UDP en el puerto configurado, y que la dirección de destino UDP de WSJT-X esté configurada con la dirección IP de la computadora con AetherSDR, no con `127.0.0.1`.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Seleccionar colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Consultar activaciones POTA](poll-pota-activations.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Configurar modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
