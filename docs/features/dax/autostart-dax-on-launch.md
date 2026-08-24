# Applet de audio DAX

## Nota sobre Windows

En Windows, AetherSDR no incluye un controlador de audio DAX integrado. El applet DAX muestra solo el siguiente mensaje informativo y no hay controles disponibles:

> No hay controlador DAX integrado en Windows. Use TCI o SmartSDR DAX.

El enrutamiento de audio DAX en Windows se admite mediante los controladores SmartSDR DAX propios de FlexRadio o mediante TCI. Consulte **Help > Configuring Data Modes** para obtener instrucciones de configuración.

En macOS y Linux, el applet DAX completo está disponible como se describe a continuación.

## Canales DAX y capacidad de slices de la radio

El applet DAX muestra filas de ganancia/medidor de RX para los canales DAX 1 a 8. Las filas por encima de la capacidad de slices de la radio conectada están ocultas, por lo que una radio con menos slices no muestra controles de ganancia muertos que no enrutan a ningún destino. Por ejemplo:

- FLEX-6300 / FLEX-6400 (2 slices): se muestran DAX 1-2, DAX 3-8 están ocultos.
- FLEX-6600 / FLEX-8600 (4 slices): se muestran DAX 1-4, DAX 5-8 están ocultos.
- FLEX-6700 (8 slices): se muestran todas las filas DAX 1-8.

Las filas ocultas no se destruyen, solo se ocultan, y sus valores de ganancia se conservan para que se restablezcan al conectar una radio más grande.

## Inicio automático de DAX al lanzar

Active el ajuste `AutoStartDAX` para que el puente de audio DAX se inicie automáticamente cada vez que AetherSDR se abra, sin necesidad de hacer clic manualmente en Enable en cada sesión.

### Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX requiere una conexión de radio activa.
- El applet DAX debe estar visible. Si no lo está, haga clic en el botón **DAX** de la barra lateral derecha para mostrarlo.

### Pasos

1. Abra el applet DAX haciendo clic en el botón **DAX** de la barra lateral derecha si aún no está visible.
2. Haga clic en **Settings > Autostart DAX with AetherSDR** para colocar una marca de verificación junto al elemento. Esto guarda `AutoStartDAX` como `True`.
3. Confirme que el botón **Enable** en el applet DAX muestra **Enabled** (iluminado en verde). Si muestra **Disabled**, haga clic en él para iniciar el puente en la sesión actual.

En el siguiente inicio, AetherSDR leerá `AutoStartDAX` y activará el puente automáticamente, reflejando el estado habilitado en el botón **Enable** (mostrando **Enabled**).

Para desactivar el inicio automático, haga clic nuevamente en **Settings > Autostart DAX with AetherSDR** para quitar la marca de verificación.

## Qué hace cada control

| Control                                     | Qué hace                                                                                                                                                   | Valor predeterminado                                                                                                                  |
|---------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| Botón **Enable** en el applet DAX           | Interruptor principal. Inicia o detiene el puente de audio DAX para la sesión actual y guarda el estado. Muestra **Enabled** cuando está activo y **Disabled** cuando está inactivo. | Deshabilitado                                                                                                                          |
| **Settings > Autostart DAX with AetherSDR** | Elemento de menú con casilla de verificación. Cuando está marcado, AetherSDR inicia el puente DAX en cada lanzamiento.                                      | Desactivado (sin marcar)                                                                                                               |
| DAX 1 ganancia+medidor                     | Medidor de nivel y control deslizante de ganancia combinados para el canal RX DAX 1. Arrastre para ajustar. Nombre accesible: "DAX RX 1 gain".               | 0.5                                                                                                                                   |
| DAX 2 ganancia+medidor                     | Medidor de nivel y control deslizante de ganancia combinados para el canal RX DAX 2. Arrastre para ajustar. Nombre accesible: "DAX RX 2 gain".               | 0.5                                                                                                                                   |
| DAX 3 ganancia+medidor                     | Medidor de nivel y control deslizante de ganancia combinados para el canal RX DAX 3. Arrastre para ajustar. Nombre accesible: "DAX RX 3 gain".               | 0.5                                                                                                                                   |
| DAX 4 ganancia+medidor                     | Medidor de nivel y control deslizante de ganancia combinados para el canal RX DAX 4. Arrastre para ajustar. Nombre accesible: "DAX RX 4 gain".               | 0.5                                                                                                                                   |
| DAX 5 ganancia+medidor                     | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 5.                                                              | Visible solo cuando la radio conectada admite al menos 5 slices.                                                                       |
| DAX 6 ganancia+medidor                     | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 6.                                                              | Visible solo cuando la radio conectada admite al menos 6 slices.                                                                       |
| DAX 7 ganancia+medidor                     | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 7.                                                              | Visible solo cuando la radio conectada admite al menos 7 slices.                                                                       |
| DAX 8 ganancia+medidor                     | Medidor/control deslizante combinado; arrastre para ajustar la ganancia de RX en el canal DAX 8.                                                              | Visible solo en una radio con capacidad de 8 slices.                                                                                   |
| TX ganancia+medidor                        | Medidor de nivel y control deslizante de ganancia combinados para el flujo TX de DAX. Arrastre para ajustar. Nombre accesible: "DAX TX gain".                 | 0.5                                                                                                                                   |
| Nota sobre Windows                         | En las versiones de Windows, el applet muestra solo la nota 'No hay controlador DAX integrado en Windows. Use TCI o SmartSDR DAX.' (#4112).                   | Windows no tiene puente DAX integrado (sin controlador de audio en modo kernel); todos los demás controles se omiten y sus definidores están protegidos contra valores nulos. |

## Significado de los indicadores

| Indicador               | Estados          | Significado                                                                                               |
|-------------------------|------------------|-----------------------------------------------------------------------------------------------------------|
| Asignación DAX 1..8     | — o Slice A..H   | El slice (si existe) asignado actualmente a este canal DAX. Muestra la letra del slice en el color del modelo de radio activo. |
| Asignación TX           | — o Slice A..H   | El slice que actualmente tiene privilegios de TX (impulsa DAX TX). Muestra la letra del slice en el color del modelo de radio activo. |

## Consejos

- El botón **Enable** y **Settings > Autostart DAX with AetherSDR** escriben ambos la misma clave `AutoStartDAX`. Al hacer clic en cualquiera de ellos se actualiza el ajuste compartido.
- Los valores de ganancia de todos los canales RX y del canal TX se guardan de forma independiente. Ajustarlos antes de activar el inicio automático significa que se restablecerán en los mismos niveles en el siguiente inicio.
- Los indicadores de asignación de slices muestran la letra del slice en el color del modelo de radio activo (formato de texto enriquecido) para una mejor visibilidad. Esto afecta tanto a las asignaciones de canales RX DAX como a los indicadores de asignación TX.
- En Linux, el audio DAX utiliza flujos nativos de PipeWire (`pw_stream`) para menor latencia, reduciendo la latencia de RX de aproximadamente 400 ms a aproximadamente 200 ms. Esto se aplica a todos los canales RX DAX.
- Cada control deslizante de ganancia tiene un nombre accesible configurado para compatibilidad con lectores de pantalla: "DAX RX N gain" para los canales 1-8 y "DAX TX gain" para el canal de transmisión.
- El botón **Enable** ahora actualiza dinámicamente su texto para mostrar **Enabled** o **Disabled** según el estado actual, proporcionando una retroalimentación visual más clara.
- Los niveles del medidor RX se suavizan exponencialmente con ataque rápido y decaimiento lento para una medición estable y legible.

## Solución de problemas

- **El applet DAX no está visible** — Haga clic en el botón **DAX** de la barra lateral derecha para mostrarlo.
- **Enable está marcado pero el puente no se inicia en el siguiente lanzamiento** — Verifique que **Settings > Autostart DAX with AetherSDR** tenga una marca de verificación. Hacer clic en **Enable** en el applet por sí solo establece el estado del puente para la sesión actual y guarda `AutoStartDAX`, pero confirmar que el elemento del menú está marcado garantiza que la ruta de inicio automático se ejecute al lanzar.
- **El botón Enable muestra Disabled después del inicio a pesar de que el inicio automático está activado** — Esto puede ocurrir si AetherSDR se lanza antes de que se establezca una conexión con la radio. El applet DAX requiere una radio conectada. Conéctese a la radio y haga clic en **Enable** manualmente, o permita que AetherSDR se conecte antes de verificar el estado del puente.
- **Faltan algunos controles deslizantes de ganancia DAX** — Esto es esperado cuando la radio conectada admite menos de 8 slices. Por ejemplo, una FLEX-6600 muestra solo DAX 1-4. Los controles deslizantes de ganancia reaparecen cuando se conecta a una radio con mayor capacidad de slices.
- **En Windows, el applet DAX muestra solo una nota** — Esto es esperado. AetherSDR no incluye un controlador de audio DAX integrado en Windows. Use los controladores SmartSDR DAX de FlexRadio o TCI en su lugar. Consulte **Help > Configuring Data Modes** para más detalles.

## Relacionados

- [Descripción general de audio DAX](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Configurar la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Configurar la ganancia TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
