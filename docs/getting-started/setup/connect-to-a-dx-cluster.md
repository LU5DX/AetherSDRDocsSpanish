# Conectarse a un clúster DX

El diálogo SpotHub de AetherSDR permite conectarse a un clúster DX mediante telnet y mostrar los spots entrantes en el panadapter. Use esta página para realizar esa primera conexión y, opcionalmente, reconectarse de forma automática en cada inicio.

## Antes de comenzar

- Tenga a mano el nombre de host y el puerto del clúster DX que desea usar (por ejemplo, `dxc.k0xm.net`, puerto `23`).
- Tenga su indicativo listo para usarlo como credencial de inicio de sesión.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Cluster**.
3. En el campo **Server:**, ingrese el nombre de host del clúster.
4. En el campo **Port:**, ingrese el puerto telnet (rango válido: 1–65535).
5. En el campo **Callsign:**, ingrese el indicativo con el que desea iniciar sesión.
6. Haga clic en **Connect**.
7. Observe el área **Cluster Console** para verificar el banner de inicio de sesión del clúster y el tráfico de spots, y confirme que la conexión está activa.
8. Para enviar un comando al clúster, escríbalo en el campo de línea de comandos ubicado debajo de la consola y haga clic en **Send**.

## Función de cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host del clúster DX al que conectarse. | `ClusterHost` |
| **Port:** | Puerto telnet del clúster DX. Rango válido: 1–65535. | `ClusterPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado al clúster en el momento de la conexión. | `ClusterCallsign` |
| **Connect / Disconnect** | Activa o desactiva la conexión telnet. La etiqueta cambia a "Disconnect" mientras está conectado. | — |
| **Auto-connect on startup** | Cuando está habilitado, AetherSDR se conecta al clúster automáticamente al iniciar. | `ClusterAutoConnect` |
| **Cluster Console** | Visualización de solo lectura del tráfico telnet sin procesar proveniente del clúster. | — |
| **Send** | Envía el comando escrito al clúster. Solo está activo mientras hay conexión. | — |
| **Spot Color:** | Abre un selector de color para definir el color usado para los spots del clúster en el panadapter. | `ClusterSpotColor` |

## Consejos

- Los spots del clúster aparecen en la pestaña unificada **Spot List** junto con spots de otras fuentes. La columna **Source** los identifica como "Cluster".
- Haga doble clic en cualquier fila de la tabla de spots para sintonizar la radio a esa frecuencia. Consulte [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md).
- La superposición maestra de spots en el panadapter debe estar habilitada. Vaya a la pestaña **Display** y confirme que **Spots:** esté configurado como Enabled (valor predeterminado). Si los spots no son visibles, revise ese control primero.
- Los colores de spots por fuente pueden modificarse en cualquier momento sin necesidad de desconectarse.

## Solución de problemas

- **El botón "Disconnect" aparece pero no llegan spots** — Es posible que el clúster requiera un comando de inicio de sesión específico tras el banner. Escriba el comando correspondiente (por ejemplo, `SET/SKIMMER` o `SET/DX`) en la línea de comandos y haga clic en **Send**.
- **El estado muestra un error en rojo** — El nombre de host o el puerto no son accesibles. Verifique los valores de **Server:** y **Port:** y confirme que su ruta de red hacia el host del clúster esté disponible.
- **Los spots aparecen en la Spot List pero no en el panadapter** — Abra la pestaña **Display** y confirme que **Spots:** esté como Enabled. Verifique también que la radio esté sintonizada en una banda con spots activos.

## Relacionados

- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
- [Conectarse a la Reverse Beacon Network](connect-to-the-reverse-beacon-network.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Seleccionar colores para cada fuente de spots](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y vida útil de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Habilitar coloración DXCC a partir de un registro ADIF](../../features/dx-cluster/enable-dxcc-coloring-from-an-adif-log.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](../../features/dx-cluster/start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
