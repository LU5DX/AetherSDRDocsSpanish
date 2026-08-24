# Habilitar DAX para enrutar el audio de un slice a WSJT-X / FLDigi / otro software digital

DAX (Digital Audio eXchange) crea flujos de audio virtuales entre AetherSDR y otro software que se ejecuta en la misma máquina. Habilítelo cuando quiera que WSJT-X, FLDigi o cualquier otro programa de modo digital reciba audio de un slice de la radio o envíe audio de vuelta a la radio. El applet muestra medidores de RX por canal y controles deslizantes de ganancia para los canales DAX 1-8, además de un medidor de TX único.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. DAX requiere una conexión de radio activa.
- Cada slice que quiera enrutar debe tener asignado un canal DAX en la configuración de slices de la radio. El applet DAX muestra qué slices ya están asignados.
- En Linux, PipeWire debe estar en ejecución. En macOS, el subsistema de audio del sistema gestiona el enrutamiento automáticamente.
- En Windows, AetherSDR no incluye un controlador de audio DAX incorporado. El audio DAX en Windows requiere los controladores SmartSDR DAX de FlexRadio o TCI.
- El applet DAX muestra solo tantas filas de canales RX como slices admita la radio conectada. Una 6300 muestra 2 canales; una 6600 muestra 4; una 6700 muestra los 8 (#4854).

## Pasos

1. Haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para abrir el applet de Audio DAX. El applet está oculto por defecto.
2. En macOS y Linux, haga clic en **Enable** (etiquetado **Disabled** cuando está apagado). El botón cambia a **Enabled** y se pone verde cuando DAX está activo. AetherSDR guarda este estado como `AutoStartDAX`.
3. En Windows, el applet DAX muestra una nota "No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX." El botón Enable y todos los medidores no están disponibles. Continúe con sus controladores SmartSDR DAX existentes.
4. Verifique los indicadores de asignación de slices junto a cada etiqueta de canal DAX (por ejemplo, **DAX 1:**, **DAX 2:**). Cada indicador muestra `—` (sin slice asignado) o `Slice A` hasta `Slice H`. Confirme que el canal que desea esté mostrando el slice correcto.
5. En su software de modo digital (WSJT-X, FLDigi, etc.), seleccione el dispositivo de audio virtual DAX correspondiente como dispositivo de entrada (y salida para TX) de audio. Consulte [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md) para los pasos específicos de cada aplicación.
6. Transmita un tono de audio de prueba desde su software digital y observe el medidor **TX** en el applet. Ajuste el control deslizante **TX gain+meter** para que el nivel se mantenga por debajo del punto de recorte.
7. Reciba una señal y observe el control deslizante **DAX 1–8 gain+meter** para el canal que asignó. Ajuste el control para establecer un nivel cómodo para la entrada de audio de su software.

## Qué hace cada control

| Control                    | Descripción                                                                                                                                            | Valor predeterminado                                                                                                                              |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| Enable                     | Interruptor principal. Inicia o detiene todos los flujos de audio DAX. Solo en macOS/Linux. En Windows, el botón no está disponible.                   | Deshabilitado                                                                                                                             |
| DAX 1 gain+meter           | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX 1. Arrastre para ajustar la ganancia de RX enviada al software en ese canal. Utiliza el nombre accesible "DAX RX 1 gain". | 0.5                                                                                                                                  |
| DAX 2 gain+meter           | Igual que DAX 1, para el canal 2. Utiliza el nombre accesible "DAX RX 2 gain".                                                                                    | 0.5                                                                                                                                  |
| DAX 3 gain+meter           | Igual que DAX 1, para el canal 3. Utiliza el nombre accesible "DAX RX 3 gain".                                                                                    | 0.5                                                                                                                                  |
| DAX 4 gain+meter           | Igual que DAX 1, para el canal 4. Utiliza el nombre accesible "DAX RX 4 gain".                                                                                    | 0.5                                                                                                                                  |
| DAX 5 gain+meter           | Igual que DAX 1, para el canal 5. Utiliza el nombre accesible "DAX RX 5 gain". Visible solo cuando la radio conectada admite al menos 5 slices.                  | 0.5                                                                                                                                  |
| DAX 6 gain+meter           | Igual que DAX 1, para el canal 6. Utiliza el nombre accesible "DAX RX 6 gain". Visible solo cuando la radio conectada admite al menos 6 slices.                  | 0.5                                                                                                                                  |
| DAX 7 gain+meter           | Igual que DAX 1, para el canal 7. Utiliza el nombre accesible "DAX RX 7 gain". Visible solo cuando la radio conectada admite al menos 7 slices.                  | 0.5                                                                                                                                  |
| DAX 8 gain+meter           | Igual que DAX 1, para el canal 8. Utiliza el nombre accesible "DAX RX 8 gain". Visible solo en una radio con capacidad de 8 slices.                    | 0.5                                                                                                                                  |
| TX gain+meter              | Medidor de nivel y control deslizante de ganancia combinados para el flujo de TX de DAX (audio de su software digital a la radio). Utiliza el nombre accesible "DAX TX gain".        | 0.5                                                                                                                                  |
| Indicador de asignación de slice (por canal) | Solo lectura. Muestra qué slice (A–H) está enrutado a cada canal DAX, o `—` si ninguno. Las letras de slice se muestran en texto enriquecido para mejorar la legibilidad.          | `—`                                                                                                                                  |
| Nota de Windows               | En las compilaciones de Windows, el applet muestra solo la nota 'No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX.' (#4112).                               | Windows no tiene puente DAX incorporado (sin controlador de audio en modo kernel); todos los demás controles se omiten y sus setters están protegidos contra null. |

## Consejos

- Para iniciar DAX automáticamente cada vez que se lance AetherSDR, marque `Settings > Autostart DAX with AetherSDR` en el menú. Esto escribe la misma configuración `AutoStartDAX` que controla el botón **Enable**.
- El indicador TX junto a la etiqueta **TX** muestra qué slice tiene actualmente los privilegios de TX. Si muestra `—`, ningún slice está configurado como slice de TX y el audio de TX de DAX no llegará a la radio. Las letras de slice se muestran en texto enriquecido para mejorar la legibilidad.
- Los controles deslizantes de ganancia son post-fader: la barra del medidor refleja el nivel después de su ajuste de ganancia, por lo que lo que ve es lo que recibe la aplicación receptora.
- Los niveles del medidor de RX se suavizan exponencialmente con ataque rápido y caída lenta, de modo que los picos son visibles pero se reduce la fluctuación de la aguja.
- Las filas por encima de la capacidad de slices de la radio conectada están ocultas, por lo que una radio pequeña no muestra controles de ganancia inactivos.
- En Linux (v26.6.1+), la latencia de RX de DAX es de aproximadamente 200 ms, reducida desde aproximadamente 400 ms en versiones anteriores, mediante transmisión nativa por PipeWire.
- En Windows, consulte `Help > Configuring Data Modes` para obtener detalles sobre la configuración del enrutamiento de audio con controladores DAX externos.

## Solución de problemas

- **Los canales DAX muestran `—` y no pasa audio** — Ningún slice tiene asignado un canal DAX. Asigne un canal DAX al slice usando los controles de slice en el panadapter y luego confirme que el indicador en el applet se actualice a `Slice A` (o la letra correspondiente).
- **El botón Enable no permanece marcado después de reiniciar AetherSDR** — `AutoStartDAX` no se guardó. Habilite la configuración mediante `Settings > Autostart DAX with AetherSDR` para que se aplique al inicio.
- **El software digital no recibe audio a pesar de que DAX está habilitado** — Confirme que el dispositivo virtual DAX correcto esté seleccionado como entrada de audio en su software de modo digital. El nombre del dispositivo depende de su sistema operativo y subsistema de audio. En Windows, asegúrese de que los controladores SmartSDR DAX estén instalados.
- **El medidor TX está activo pero la radio no está transmitiendo** — Confirme que el indicador del slice de TX muestre un slice válido. Si muestra `—`, ningún slice tiene privilegios de TX. Consulte [Identificar qué slice es el slice de TX](identify-which-slice-is-the-tx-slice.md).
- **El botón Enable de DAX y los medidores no son visibles en Windows** — Esto es un comportamiento esperado. AetherSDR no incluye controladores de audio DAX incorporados para Windows. Use los controladores SmartSDR DAX de FlexRadio o TCI para el audio DAX en Windows. Consulte `Help > Configuring Data Modes`.
- **Aparecen menos filas de DAX de las esperadas** — El applet oculta las filas por encima de la capacidad de slices de la radio conectada. Una 6300 muestra 2 canales, una 6600 muestra 4 y una 6700 muestra los 8.

## Relacionado

- [Resumen de Audio DAX](overview.md)
- [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md)
- [Establecer la ganancia de RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Establecer la ganancia de TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar qué slice es el slice de TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
