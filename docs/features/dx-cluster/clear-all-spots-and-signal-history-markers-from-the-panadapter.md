# Cuadro de diálogo SpotHub

El cuadro de diálogo SpotHub es el centro central para conectarse a fuentes de spots DX y configurar cómo se muestran los spots en el panadapter.

## Abrir SpotHub

Seleccione `Settings > SpotHub...` desde el menú principal.

## Fuentes de spots

SpotHub admite múltiples fuentes de spots, cada una en su propia pestaña:

- **Cluster** — Conexión telnet a un clúster DX
- **RBN** — Fuente telnet de Reverse Beacon Network con limitación de velocidad
- **WSJT-X** — Escucha UDP para decodificaciones de WSJT-X
- **SpotCollector** — Escucha UDP para transmisiones de Ham Radio Deluxe SpotCollector
- **POTA** — Consulta HTTP de api.pota.app para activaciones actuales
- **FreeDV** — Fuente WebSocket de spots del reportador QSO de FreeDV (compilación condicionada al soporte WebSocket)

### Pestaña Cluster

| Control | Descripción |
|---------|-------------|
| **Server:** | Nombre de host del clúster DX al que conectarse |
| **Port:** | Puerto telnet en el clúster DX (1-65535) |
| **Callsign:** | Indicativo de inicio de sesión enviado al clúster |
| **Connect / Disconnect** | Activa/desactiva la conexión telnet al clúster |
| **Auto-connect on startup** | Conecta automáticamente al clúster al iniciar |
| **Cluster Console** | Consola telnet de solo lectura del tráfico bruto del clúster |
| **Send** | Envía un comando escrito al clúster |
| **Spot Color:** | Abre un selector de color para los spots del clúster |

### Pestaña RBN

| Control | Descripción |
|---------|-------------|
| **Server:** | Nombre de host telnet de RBN |
| **Port:** | Puerto telnet de RBN (1-65535) |
| **Callsign:** | Indicativo de inicio de sesión para RBN |
| **Rate Limit:** | Limita los spots de RBN por segundo |
| **Connect / Disconnect** | Activa/desactiva la conexión RBN |
| **Auto-connect on startup** | Inicia RBN automáticamente |
| **RBN Console** | Consola de solo lectura del tráfico de RBN |
| **Send** | Envía un comando a RBN |
| **Spot Color:** | Selector de color para spots de RBN |

### Pestaña WSJT-X

| Control | Descripción |
|---------|-------------|
| **Address:** | Dirección de enlace UDP para mensajes de WSJT-X |
| **Port:** | Puerto UDP para WSJT-X (1-65535) |
| **Start / Stop** | Inicia o detiene la escucha UDP |
| **Auto-start on startup** | Inicia la escucha automáticamente al arrancar |
| **CQ** | Muestra solo llamadas CQ de WSJT-X |
| **CQ POTA** | Muestra llamadas CQ POTA |
| **Calling Me** | Muestra solo decodificaciones dirigidas a su indicativo |
| **CQ color / POTA color / Calling Me color / Default color** | Selectores de color para cada categoría de spot de WSJT-X |
| **WSJT-X Decodes** | Consola de transmisiones decodificadas |
| **Spot Life:** | Segundos que los spots de WSJT-X permanecen en el panadapter |

### Pestaña SpotCollector

| Control | Descripción |
|---------|-------------|
| **UDP Port:** | Puerto UDP en el que SpotCollector transmite (1-65535) |
| **Start / Stop** | Inicia o detiene la escucha UDP |
| **Auto-start on startup** | Inicia la escucha automáticamente al arrancar |
| **SpotCollector Spots** | Consola de spots recibidos de SpotCollector |

### Pestaña POTA

| Control | Descripción |
|---------|-------------|
| **Server:** | Indicador fijo que muestra `api.pota.app (HTTP polling)` |
| **Poll Interval:** | Segundos entre consultas a POTA |
| **Start / Stop** | Inicia o detiene la consulta a POTA |
| **Auto-start on startup** | Inicia POTA automáticamente al arrancar |
| **POTA Activations** | Consola del feed de activaciones |
| **Spot Color:** | Selector de color para spots de POTA |

### Pestaña FreeDV

| Control | Descripción |
|---------|-------------|
| **Server:** | Indicador fijo que muestra `qso.freedv.org (WebSocket)` |
| **Start / Stop** | Conecta o desconecta el WebSocket de FreeDV |
| **Auto-start on startup** | Inicia FreeDV automáticamente al arrancar |
| **FreeDV Spots** | Consola de actividad de FreeDV |
| **Spot Color:** | Selector de color para spots de FreeDV |

## Pestaña Lista de Spots

Muestra una tabla unificada y buscable de todos los spots activos de cada fuente conectada.

| Control | Descripción |
|---------|-------------|
| **Bands:** | Casillas de verificación por banda que alternan la visibilidad en la tabla. Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). Las casillas usan un diseño de ajuste de línea para que sigan siendo legibles incluso cuando el diálogo es estrecho. |
| **Clear** | Vacía la lista actual de spots |
| **Spot table** | Tabla de spots ordenable. Haga doble clic en una fila para sintonizar. Columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. Haga clic derecho en los encabezados de columna para mostrar u ocultar columnas individuales. |

### Cambiar columnas visibles

1. Haga clic derecho en cualquier encabezado de columna en la tabla de spots.
2. Aparece un menú con entradas seleccionables para cada columna.
3. Haga clic en una entrada seleccionable para activar o desactivar la visibilidad de esa columna. El menú permanece abierto para que pueda activar o desactivar varias columnas de una sola vez.
4. Haga clic fuera del menú o presione Escape para cerrar el menú cuando haya terminado.

## Pestaña Pantalla

Configura la visualización de spots en el panadapter, los parámetros ajustables de Signal History y el coloreado por DXCC.

### Fila de alternancia

| Control | Descripción |
|---------|-------------|
| **Spots:** | Activación general para la superposición de spots DX. Activado por defecto. |
| **Memories:** | Activa la superposición de canales de memoria en el panadapter. Desactivado por defecto. |
| **Auto:** | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (p. ej., CW, FT8, RTTY). Activado por defecto. |
| **Signals** | Marcadores dorados para señales de ancho de voz detectadas en el panadapter. Desactivado por defecto. |
| **QRM** | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Desactivado por defecto. |
| **Clear All** | Borra todos los spots DX, el feed de memoria, los marcadores de Signal History y los marcadores de QRM del espectro. |

### Deslizadores

| Control | Rango | Valor predeterminado | Descripción |
|---------|-------|---------|-------------|
| **Levels:** | 1-10 | 3 | Número de filas de apilamiento vertical para spots |
| **Position:** | 0-100 | 50 | Posición vertical en el panadapter |
| **Font Size:** | 8-32 | 16 | Tamaño del texto del spot |
| **Spot Lifetime:** | 10 seg – 24 horas (pasos no lineales) | — | Segundos antes de que un spot se desvanezca |

### Colores de anulación

| Control | Descripción |
|---------|-------------|
| **Override Colors:** | Fuerza un solo color de texto para todos los spots. Desactivado por defecto. |
| **Spot text color picker** | Abre el selector de color para el color del texto del spot. Valor predeterminado: `#FFFF00` (amarillo). |
| **Override Background: Enabled** | Activa un color de fondo personalizado para los spots. Activado por defecto. |
| **Override Background: Auto** | Selecciona automáticamente el color de fondo para contraste. Activado por defecto. |
| **Spot background color picker** | Abre el selector de color para el color de fondo del spot. Valor predeterminado: `#000000` (negro). |
| **Background Opacity:** | Opacidad del color de fondo del spot. Rango: 0-100. Valor predeterminado: 48. |
| **Spot Lines:** | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir el desorden visual. Activado por defecto. |

### Total de Spots

Muestra el recuento en vivo de spots actualmente rastreados en todas las fuentes.

### Sección de coloreado DXCC

Controles en la columna izquierda debajo del divisor.

| Control | Descripción |
|---------|-------------|
| **DXCC Colors:** | Colorea los spots según el estado trabajado/confirmado/necesitado de DXCC. Desactivado por defecto. |
| **Log File (ADIF):** | Carga un archivo de registro ADIF para impulsar el coloreado DXCC. Vigila automáticamente el archivo en busca de cambios después de la selección. |
| **Imported:** | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`. |
| **DXCC Color swatches** | Selectores de color para cada categoría de estado DXCC: New DXCC, New Band, New Mode, Worked |

### Sección de Signal History

Controles en la columna derecha debajo del divisor.

| Control | Rango | Valor predeterminado | Descripción |
|---------|-------|---------|-------------|
| **Marker Lifetime:** | 15-300 seg | 60 | Cuánto tiempo persiste un marcador de Signal History inactivo antes de eliminarse |
| **QRM Gate:** | 3-30 seg | 6 | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM |
| **Edge Threshold:** | 1.0-10.0 dB | 3.0 | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde del lado de la portadora de S-History |
| **Signal History color swatches** | — | #FFC800 / #FF0000 | Selectores de color para marcadores de señal de voz (dorado) y marcadores QRM (rojo) |
| **Snap to Step:** | — | Desactivado | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora |

## Indicadores de estado

| Indicador | Estados posibles | Significado |
|-----------|----------------|---------|
| Estado (cada fuente) | Disconnected, Connected, Stopped, Listening, Polling | Estado actual de conexión/escucha para cada fuente |
| Recuento total de spots | — | Total de spots actualmente rastreados en todas las fuentes |
| Estadísticas DXCC | — | Recuento de QSO y entidades importados del registro ADIF cuando el coloreado DXCC está activado. Formato: `<N> QSOs / <M> entities`. |

## Relacionados

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Toggle QRM markers to see persistent carriers and interference](toggle-qrm-markers-to-see-persistent-carriers-and-interference.md)
- [Tune spot density, position, font size and lifetime](tune-spot-density-position-font-size-and-lifetime.md)
- [Start WSJT-X UDP listener and filter for CQ, POTA or calls to me](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Connect to a DX cluster](../../getting-started/setup/connect-to-a-dx-cluster.md)
