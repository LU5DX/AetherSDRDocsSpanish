# Diálogo SpotHub

El diálogo SpotHub es el centro principal para conectarse a fuentes de spots de DX y configurar cómo se muestran los spots en el panadapter.

## Abrir SpotHub

Seleccione `Settings > SpotHub...` desde el menú principal.

## Fuentes de Spots

SpotHub admite múltiples fuentes de spots, cada una en su propia pestaña:

- **Cluster** — Conexión telnet a cluster de DX
- **RBN** — Fuente telnet de Reverse Beacon Network con límite de velocidad
- **WSJT-X** — Escucha UDP para decodificaciones de WSJT-X
- **SpotCollector** — Escucha UDP para transmisiones de Ham Radio Deluxe SpotCollector
- **POTA** — Sondeo HTTP de api.pota.app para activaciones actuales
- **FreeDV** — Fuente WebSocket de spots de reportes QSO de FreeDV (limitado por compilación según soporte WebSocket)

### Pestaña Cluster

| Control | Descripción |
|---------|-------------|
| **Server:** | Nombre de host del cluster de DX al que conectarse |
| **Port:** | Puerto telnet del cluster de DX (1-65535) |
| **Callsign:** | Indicativo de inicio de sesión enviado al cluster |
| **Connect / Disconnect** | Alterna la conexión telnet al cluster |
| **Auto-connect on startup** | Conecta automáticamente el cluster al iniciar |
| **Cluster Console** | Consola telnet de solo lectura del tráfico crudo del cluster |
| **Send** | Envía un comando escrito al cluster |
| **Spot Color:** | Abre un selector de color para los spots del cluster |

### Pestaña RBN

| Control | Descripción |
|---------|-------------|
| **Server:** | Nombre de host telnet de RBN |
| **Port:** | Puerto telnet de RBN (1-65535) |
| **Callsign:** | Indicativo de inicio de sesión en RBN |
| **Rate Limit:** | Limita los spots de RBN por segundo |
| **Connect / Disconnect** | Alterna la conexión RBN |
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
| **Auto-start on startup** | Inicia automáticamente la escucha al lanzar |
| **CQ** | Muestra solo llamadas CQ de WSJT-X |
| **CQ POTA** | Muestra llamadas CQ POTA |
| **Calling Me** | Muestra solo decodificaciones dirigidas a su indicativo |
| **CQ color / POTA color / Calling Me color / Default color** | Selectores de color para cada categoría de spot de WSJT-X |
| **WSJT-X Decodes** | Consola de transmisiones decodificadas |
| **Spot Life:** | Segundos que los spots de WSJT-X permanecen en el panadapter |

### Pestaña SpotCollector

| Control | Descripción |
|---------|-------------|
| **UDP Port:** | Puerto UDP en el que transmite SpotCollector (1-65535) |
| **Start / Stop** | Inicia o detiene la escucha UDP |
| **Auto-start on startup** | Inicia automáticamente la escucha al lanzar |
| **SpotCollector Spots** | Consola de spots recibidos de SpotCollector |

### Pestaña POTA

| Control | Descripción |
|---------|-------------|
| **Server:** | Indicador fijo que muestra `api.pota.app (HTTP polling)` |
| **Poll Interval:** | Segundos entre sondeos de POTA |
| **Start / Stop** | Inicia o detiene el sondeo de POTA |
| **Auto-start on startup** | Inicia automáticamente POTA al lanzar |
| **POTA Activations** | Consola del flujo de activaciones |
| **Spot Color:** | Selector de color para spots de POTA |

### Pestaña FreeDV

| Control | Descripción |
|---------|-------------|
| **Server:** | Indicador fijo que muestra `qso.freedv.org (WebSocket)` |
| **Start / Stop** | Conecta o desconecta el WebSocket de FreeDV |
| **Auto-start on startup** | Inicia automáticamente FreeDV al lanzar |
| **FreeDV Spots** | Consola de actividad de FreeDV |
| **Spot Color:** | Selector de color para spots de FreeDV |

## Pestaña Lista de Spots

Muestra una tabla unificada y buscable de todos los spots activos de cada fuente conectada.

| Control | Descripción |
|---------|-------------|
| **Bands:** | Casillas de verificación por banda que alternan la visibilidad en la tabla. Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). Las casillas usan un diseño envolvente para que sigan siendo legibles incluso cuando el diálogo es estrecho. |
| **Clear** | Vacía la lista actual de spots |
| **Spot table** | Tabla ordenable de spots. Haga doble clic en una fila para sintonizar. Columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. Haga clic derecho en los encabezados de columna para mostrar u ocultar columnas individuales. Las columnas Time y Freq son ambas ordenables; haga clic en cualquiera de los encabezados para reordenar. |

### Cambiar columnas visibles

1. Haga clic derecho en cualquier encabezado de columna de la tabla de spots.
2. Aparece un menú con entradas marcables para cada columna.
3. Haga clic en una entrada marcable para alternar la visibilidad de esa columna. El menú permanece abierto para que pueda alternar varias columnas de una sola vez.
4. Haga clic fuera del menú o presione Escape para cerrarlo cuando haya terminado.

## Pestaña Display

Configura la visualización de spots en el panadapter, los ajustes de Signal History y el coloreado por DXCC.

### Fila de alternancia

| Control | Descripción |
|---------|-------------|
| **Spots:** | Interruptor principal para la superposición de spots de DX. Habilitado por defecto. |
| **Memories:** | Alterna la superposición de canales de memoria en el panadapter. Deshabilitado por defecto. |
| **Auto:** | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (p. ej., CW, FT8, RTTY). Habilitado por defecto. |
| **Signals** | Marcadores dorados para señales detectadas de ancho de voz en el panadapter. Deshabilitado por defecto. |
| **QRM** | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Deshabilitado por defecto. |
| **Clear All** | Borra todos los spots de DX, el flujo de memorias, los marcadores de Signal History y los marcadores QRM del espectro. |

### Controles deslizantes

| Control | Rango | Predeterminado | Descripción |
|---------|-------|---------|-------------|
| **Levels:** | 1-10 | 3 | Número de filas de apilamiento vertical para spots |
| **Position:** | 0-100 | 50 | Posición vertical en el panadapter |
| **Font Size:** | 8-32 | 16 | Tamaño del texto de los spots |
| **Spot Lifetime:** | 10 seg – 24 horas (pasos no lineales) | — | Segundos antes de que un spot se desvanezca |

### Colores de anulación

| Control | Descripción |
|---------|-------------|
| **Override Colors:** | Fuerza un único color de texto para todos los spots. Deshabilitado por defecto. |
| **Spot text color picker** | Abre un selector de color para el color del texto de los spots. Predeterminado: `#FFFF00` (amarillo). |
| **Override Background: Enabled** | Habilita un color de fondo personalizado para los spots. Habilitado por defecto. |
| **Override Background: Auto** | Selecciona automáticamente el color de fondo para contraste. Habilitado por defecto. |
| **Spot background color picker** | Abre un selector de color para el color de fondo de los spots. Predeterminado: `#000000` (negro). |
| **Background Opacity:** | Opacidad del color de fondo de los spots. Rango: 0-100. Predeterminado: 48. |
| **Spot Lines:** | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Deshabilítelas durante concursos para reducir el desorden visual. Habilitado por defecto. |

### Total Spots

Muestra el recuento en vivo de spots actualmente rastreados en todas las fuentes.

### Sección de coloreado DXCC

Controles en la columna izquierda debajo del divisor.

| Control | Descripción |
|---------|-------------|
| **DXCC Colors:** | Colorea los spots según el estado DXCC trabajado/confirmado/necesario. Deshabilitado por defecto. |
| **Log File (ADIF):** | Carga un archivo de registro ADIF para impulsar el coloreado DXCC. Vigila automáticamente el archivo para detectar cambios después de la selección. |
| **Imported:** | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`. |
| **DXCC Color swatches** | Selectores de color para cada categoría de estado DXCC: New DXCC, New Band, New Mode, Worked |

### Sección Signal History

Controles en la columna derecha debajo del divisor.

| Control | Rango | Predeterminado | Descripción |
|---------|-------|---------|-------------|
| **Marker Lifetime:** | 15-300 seg | 60 | Cuánto tiempo persiste un marcador de Signal History inactivo antes de eliminarse |
| **QRM Gate:** | 3-30 seg | 6 | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM |
| **Edge Threshold:** | 1.0-10.0 dB | 3.0 | Umbral por encima del piso de ruido para el recorrido de borde de pendiente que refina el borde lateral de la portadora de S-History |
| **Signal History color swatches** | — | #FFC800 / #FF0000 | Selectores de color para marcadores de señal de voz (dorado) y marcadores QRM (rojo) |
| **Snap to Step:** | — | Deshabilitado | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora |

## Indicadores de estado

| Indicador | Estados posibles | Significado |
|-----------|----------------|---------|
| Estado (cada fuente) | Disconnected, Connected, Stopped, Listening, Polling | Estado actual de conexión/escucha de cada fuente |
| Recuento total de spots | — | Total de spots actualmente rastreados en todas las fuentes |
| Estadísticas DXCC | — | Recuento importado de QSO y entidades del registro ADIF cuando el coloreado DXCC está habilitado. Formato: `<N> QSOs / <M> entities`. |

## Relacionado

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Toggle QRM markers to see persistent carriers and interference](toggle-qrm-markers-to-see-persistent-carriers-and-interference.md)
- [Tune spot density, position, font size and lifetime](tune-spot-density-position-font-size-and-lifetime.md)
- [Start WSJT-X UDP listener and filter for CQ, POTA or calls to me](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Connect to a DX cluster](../../getting-started/setup/connect-to-a-dx-cluster.md)
