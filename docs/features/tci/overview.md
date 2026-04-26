# Descripción general del servidor TCI

El applet TCI Server ejecuta un servidor WebSocket que implementa el protocolo TCI de Expert Electronics, lo que permite que aplicaciones de terceros —como Log4OM, las herramientas de SunSDR y otras aplicaciones compatibles con TCI— lean y controlen el radio. Abra este applet para iniciar el servidor, configurar su puerto y ajustar la ganancia de audio de cada canal RX y TX.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TCI requiere una conexión de radio activa.
- La función TCI Server solo está presente en las compilaciones que incluyen soporte WebSocket. Si el botón TCI en la bandeja de iconos no aparece, su compilación no lo incluye.

## Cómo funciona

El applet TCI Server está oculto de forma predeterminada. Haga clic en el botón **TCI** de la barra lateral derecha para mostrarlo.

Al hacer clic en **Enable**, AetherSDR vincula un servidor WebSocket al puerto configurado (valor predeterminado: `50001`). Cualquier cliente compatible con TCI en la red puede entonces conectarse a ese puerto. El indicador de estado del servidor muestra el estado actual: `(stopped)` cuando el servidor está detenido, `:<port> (<N> clients)` cuando está en ejecución, o `(port in use)` en rojo si el enlace falló.

Cada uno de los cuatro canales RX se asigna a un canal DAX. El indicador de asignación de slice (ranura de frecuencia) junto a cada fila muestra qué slice está alimentando ese canal (por ejemplo, `Slice A`), o `—` si no hay ningún slice asignado. La fila TX funciona de la misma manera y muestra el slice TX activo.

Los niveles de audio de todos los canales se muestran en tiempo real en los controles combinados de medidor/deslizador. Arrastrar la parte deslizadora establece la ganancia de ese canal, que se almacena de inmediato.

El inicio automático se configura por separado mediante `Settings > Autostart TCI with AetherSDR`. Cuando está habilitado, AetherSDR inicia el servidor TCI cada vez que se lanza, sin necesidad de hacer clic en **Enable** manualmente.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Ganancia+medidor RX1–RX4 | Establece la ganancia de audio TCI RX para cada canal. El medidor muestra el nivel de señal en tiempo real; arrastre para ajustar la ganancia. | 0.5 | 0.0–1.0 | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| Ganancia+medidor TX | Establece la ganancia de audio TCI TX. El medidor muestra el nivel TX en tiempo real; arrastre para ajustar la ganancia. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Puerto | El puerto WebSocket al que se vincula el servidor. Si se cambia el valor mientras el servidor está en ejecución, este se reinicia automáticamente. Los valores fuera del rango 1024–65535 se ajustan a `50001`. | `50001` | 1024–65535 | `TciPort` |
| Enable | Inicia o detiene el servidor TCI. Si el enlace falla, el interruptor vuelve a la posición de desactivado y el estado muestra `(port in use)` en rojo. | Off | On / Off | — |
| Etiquetas de asignación de slice RX/TX | Indicadores de solo lectura que muestran qué slice controla cada fila RX o TX. Muestra `Slice <letra>` o `—`. | `—` | — | — |
| Estado del servidor | Muestra `(stopped)`, `:<port> (<N> clients)` o `(port in use)`. Se pone en rojo cuando el enlace falla. | `(stopped)` | — | — |

## Consejos

- Si desea que el servidor se inicie cada vez que AetherSDR se lance, use `Settings > Autostart TCI with AetherSDR` en lugar de hacer clic en **Enable** en cada sesión. Consulte [Inicio automático de TCI al lanzar](autostart-tci-on-launch.md).
- La ganancia del canal RX y la asignación de slice siguen la asignación de canales DAX. Si un canal muestra `—`, asigne primero un canal DAX al slice correspondiente.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable vuelve a desactivado** — Otra aplicación ya está vinculada a ese puerto. Cambie el puerto en el campo Port a un valor no utilizado entre 1024 y 65535 y haga clic en **Enable** nuevamente. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El botón TCI de la bandeja no es visible** — Esta compilación de AetherSDR fue compilada sin soporte WebSocket. La función TCI Server no está disponible.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia TCI RX por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TCI TX](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al lanzar](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
