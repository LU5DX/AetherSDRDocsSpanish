# Conectar a un clúster DX

El diálogo SpotHub de AetherSDR le permite conectarse a un clúster DX por telnet y mostrar los spots entrantes como superposiciones en el panadapter. Use esta página para realizar su primera conexión y, opcionalmente, volver a conectarse automáticamente en cada inicio.

## Antes de comenzar

- Conozca el nombre de host (o dirección IP) y el puerto telnet del clúster DX que eligió (por ejemplo, `dxc.k0xm.net` en el puerto `7373`).
- Conozca el indicativo con el que iniciará sesión en el clúster.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Cluster**.
3. En el campo **Server:**, escriba el nombre de host o la dirección IP del clúster. Esto se guarda en `ClusterHost`.
4. En el campo **Port:**, establezca el puerto telnet (1–65535). Esto se guarda en `ClusterPort`.
5. En el campo **Callsign:**, escriba su indicativo. Esto se guarda en `ClusterCallsign`.
6. Haga clic en **Connect**.
   - El indicador de estado cambia a **Connected** y la etiqueta del botón cambia a **Disconnect**.
   - El tráfico entrante del clúster aparece en la pantalla de solo lectura **Cluster Console**.
7. Para volver a conectarse automáticamente cada vez que AetherSDR inicia, active **Auto-connect on startup**. Esto se guarda en `ClusterAutoConnect`.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host o dirección IP del servidor telnet del clúster DX. | `ClusterHost` |
| **Port:** | Puerto telnet. Rango válido: 1–65535. | `ClusterPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado al clúster al conectarse. | `ClusterCallsign` |
| **Connect / Disconnect** | Activa o desactiva la conexión telnet. La etiqueta muestra la acción actual. | — |
| **Auto-connect on startup** | Conecta al clúster automáticamente cuando AetherSDR inicia. | `ClusterAutoConnect` |
| **Cluster Console** | Pantalla de solo lectura del tráfico telnet sin procesar del clúster. | — |
| **Send** (línea de comandos) | Envía un comando escrito al clúster mientras está conectado. | — |
| **Spot Color:** | Abre un selector de color para las superposiciones de spots del clúster en el panadapter. | `ClusterSpotColor` |

## Consejos

- Mientras está conectado, escriba un comando del clúster en el campo junto a **Send** y haga clic en **Send** para interactuar directamente con el clúster (por ejemplo, `set/dx` o `sh/dx 20`).
- Las superposiciones de spots aparecen en el panadapter solo cuando el interruptor principal **Spots:** en la pestaña **Display** está activado (predeterminado: activado, guardado en `IsSpotsEnabled`).
- Para revisar el tráfico reciente del clúster anterior a cuando abrió SpotHub, desplácese hacia arriba en la **Cluster Console** — AetherSDR carga hasta las últimas 500 líneas del archivo de registro del clúster cuando se abre el diálogo.

## Solución de problemas

- **El estado muestra "Error: ..."** — El nombre de host o el puerto es incorrecto, o el servidor del clúster no es accesible. Verifique la dirección y el puerto, luego haga clic en **Connect** nuevamente.
- **La Cluster Console está vacía después de conectarse** — Algunos clústeres requieren que envíe su indicativo como primer comando. Escriba su indicativo en el campo de comandos y haga clic en **Send**.
- **Los spots no aparecen en el panadapter** — Abra la pestaña **Display** y confirme que **Spots:** esté activado.

## Relacionado

- [Descripción general de SpotHub](../../features/dx-cluster/overview.md)
- [Conectar a la Red de Balizas Inversas (RBN)](connect-to-the-reverse-beacon-network.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](../../features/dx-cluster/tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spots](../../features/dx-cluster/pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](../../features/dx-cluster/tune-spot-density-position-font-size-and-lifetime.md)
- [Activar el coloreado DXCC desde un registro ADIF](../../features/dx-cluster/enable-dxcc-coloring-from-an-adif-log.md)
- [Borrar todos los spots del panadapter](../../features/dx-cluster/clear-all-spots-from-the-panadapter.md)
