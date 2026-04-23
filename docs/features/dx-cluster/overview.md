# Descripción general de SpotHub

SpotHub es el concentrador central de gestión de spots de AetherSDR. Agrega spots de DX provenientes de hasta seis fuentes independientes — clúster DX, Reverse Beacon Network (RBN), WSJT-X, SpotCollector, POTA y FreeDV — y los superpone sobre el panadapter. Use SpotHub para configurar cada fuente, controlar la apariencia de los spots y sintonizar cualquier spot con un solo clic.

## Antes de comenzar

- Abra SpotHub desde `Settings > SpotHub...`. No se requiere conexión con el radio.
- Cada pestaña de fuente es independiente. Puede ejecutar cualquier combinación de fuentes simultáneamente.

## Cómo funciona

SpotHub recopila spots de múltiples fuentes y los combina en un único grupo activo. Cada spot contiene frecuencia, indicativo, comentario, spotter, banda, modo y etiqueta de fuente. Los spots se muestran como superposiciones en todos los panadapters. La pestaña unificada Spot List permite ordenar y filtrar entre todas las fuentes activas; al hacer doble clic en cualquier fila se sintoniza el VFO activo a esa frecuencia.

Las seis pestañas de fuente gestionan cada una un flujo de datos. La pestaña Display controla cómo se representa el grupo combinado. La coloración DXCC — basada en su propio registro ADIF — puede codificar con colores los spots según el estado: trabajado, confirmado o necesario.

## Qué hace cada control

### Pestaña Cluster

Controla la conexión telnet a un nodo de clúster DX tradicional.

| Control | Descripción | Clave de configuración |
|---|---|---|
| Server: | Nombre de host del clúster DX al que conectarse. | `ClusterHost` |
| Port: | Puerto telnet. Rango válido: 1–65535. | `ClusterPort` |
| Callsign: | Indicativo de inicio de sesión enviado al clúster al conectarse. | `ClusterCallsign` |
| Connect / Disconnect | Activa o desactiva la conexión telnet. Etiqueta predeterminada: Connect. | — |
| Auto-connect on startup | Cuando está habilitado, se conecta automáticamente al iniciar. | `ClusterAutoConnect` |
| Cluster Console | Visualización de solo lectura del tráfico telnet sin procesar del clúster. | — |
| Send | Envía un comando escrito al clúster. | — |
| Spot Color: | Abre un selector de color para los spots del clúster en el panadapter. | `ClusterSpotColor` |

### Pestaña RBN

Controla la conexión telnet a la Reverse Beacon Network, con limitación de velocidad para gestionar un volumen alto de spots.

| Control | Descripción | Clave de configuración |
|---|---|---|
| Server: | Nombre de host telnet de RBN. | `RbnHost` |
| Port: | Puerto telnet de RBN. Rango válido: 1–65535. | `RbnPort` |
| Callsign: | Indicativo de inicio de sesión enviado a RBN. | `RbnCallsign` |
| Rate Limit: | Máximo de spots de RBN aceptados por segundo. | `RbnRateLimit` |
| Connect / Disconnect | Activa o desactiva la conexión telnet de RBN. Etiqueta predeterminada: Connect. | — |
| Auto-connect on startup | Se conecta a RBN automáticamente al iniciar. | `RbnAutoConnect` |
| RBN Console | Visualización de solo lectura del tráfico telnet sin procesar de RBN. | — |
| Send | Envía un comando a la conexión RBN. | — |
| Spot Color: | Abre un selector de color para los spots provenientes de RBN. | `RbnSpotColor` |

### Pestaña WSJT-X

Escucha en un puerto UDP las transmisiones decodificadas de una instancia de WSJT-X en ejecución. Los filtros limitan lo que aparece en el panadapter.

| Control | Descripción | Clave de configuración |
|---|---|---|
| Address: | Dirección de enlace UDP para los mensajes de WSJT-X. | `WsjtxAddress` |
| Port: | Puerto UDP. Rango válido: 1–65535. | `WsjtxPort` |
| Start / Stop | Inicia o detiene el receptor UDP. | — |
| Auto-start on startup | Inicia el receptor automáticamente al arrancar. | `WsjtxAutoStart` |
| CQ | Cuando está marcado, muestra solo llamadas CQ. | `WsjtxFilterCQ` |
| CQ POTA | Cuando está marcado, muestra llamadas CQ POTA. | `WsjtxFilterPOTA` |
| Calling Me | Cuando está marcado, muestra solo decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` |
| CQ color / POTA color / Calling Me color / Default color | Selectores de color para cada categoría de spot de WSJT-X. | `WsjtxColorCQ` / `WsjtxColorPOTA` / `WsjtxColorCallingMe` / `WsjtxColorDefault` |
| WSJT-X Decodes | Consola de solo lectura de transmisiones decodificadas. | — |
| Spot Life: | Segundos que los spots de WSJT-X permanecen en el panadapter antes de expirar. | `WsjtxSpotLife` |

### Pestaña SpotCollector

Recibe spots transmitidos por UDP por Ham Radio Deluxe SpotCollector.

| Control | Descripción | Clave de configuración |
|---|---|---|
| UDP Port: | Puerto UDP por el que SpotCollector transmite. Rango válido: 1–65535. | `SpotCollectorPort` |
| Start / Stop | Inicia o detiene el receptor UDP. | — |
| Auto-start on startup | Inicia el receptor automáticamente al arrancar. | `SpotCollectorAutoStart` |
| SpotCollector Spots | Consola de solo lectura de los spots recibidos de SpotCollector. | — |

### Pestaña POTA

Consulta `api.pota.app` mediante HTTP para obtener las activaciones actuales de Parks on the Air.

| Control | Descripción | Clave de configuración |
|---|---|---|
| Server: | Indicador de punto de acceso fijo: `api.pota.app` (consulta HTTP). No editable. | — |
| Poll Interval: | Segundos entre consultas. | `PotaPollInterval` |
| Start / Stop | Inicia o detiene las consultas a POTA. | — |
| Auto-start on startup | Inicia las consultas automáticamente al arrancar. | `PotaAutoStart` |
| POTA Activations | Consola de solo lectura del flujo de activaciones. | — |
| Spot Color: | Abre un selector de color para los spots provenientes de POTA. | `PotaSpotColor` |

### Pestaña FreeDV

Se conecta al reportador de QSO de FreeDV mediante WebSocket para mostrar spots de actividad FreeDV. Esta pestaña solo está presente en compilaciones con soporte WebSocket.

| Control | Descripción | Clave de configuración |
|---|---|---|
| Server: | Indicador de punto de acceso fijo: `qso.freedv.org` (WebSocket). No editable. | — |
| Start / Stop | Conecta o desconecta el WebSocket de FreeDV. | — |
| Auto-start on startup | Se conecta automáticamente al arrancar. | `FreeDvAutoStart` |
| FreeDV Spots | Consola de solo lectura de la actividad FreeDV. | — |
| Spot Color: | Abre un selector de color para los spots provenientes de FreeDV. | `FreeDvSpotColor` |

### Pestaña Spot List

Tabla unificada y ordenable de todos los spots activos de cada fuente habilitada.

| Control | Descripción | Clave de configuración |
|---|---|---|
| Bands: | Casillas de verificación por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m y otras). Desmarque una banda para ocultarla de la tabla. | — |
| Clear | Elimina todos los spots de la lista actual. | — |
| Spot table | Tabla ordenable con las columnas: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source. Haga doble clic en una fila para sintonizar esa frecuencia. | — |

### Pestaña Display

Controla cómo se representan los spots en el panadapter y habilita la coloración basada en el registro DXCC.

| Control | Valor predeterminado | Descripción | Clave de configuración |
|---|---|---|---|
| Spots: | Habilitado | Interruptor principal de la superposición de spots. Deshabilítelo para ocultar todos los spots sin desconectar las fuentes. | `IsSpotsEnabled` |
| Memories: | Deshabilitado | Activa o desactiva la superposición de canales de memoria en el panadapter. | `IsMemoriesShownOnPanadapter` |
| Auto Mode: | — | Ajusta automáticamente la densidad de spots según el nivel de zoom actual. | `SpotsAutoMode` |
| Levels: | — | Número de filas de apilamiento vertical usadas cuando los spots se superponen. | `SpotsStackLevels` |
| Position: | — | Posición vertical de la superposición de spots en el panadapter. | `SpotsPosition` |
| Font Size: | — | Tamaño del texto de las etiquetas de spots. | `SpotsFontSize` |
| Spot Lifetime: | — | Segundos antes de que un spot desaparezca del panadapter. | `SpotsLifetime` |
| Override Colors: | — | Fuerza un único color de texto para todos los spots, reemplazando los colores por fuente. | `IsSpotsOverrideColorsEnabled` |
| Override Background: Enabled / Auto | — | Habilita un color de fondo personalizado para los spots. Auto aplica contraste automático. | `IsSpotsOverrideBackgroundColorsEnabled` / `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Background Opacity: | 48 | Opacidad del color de fondo de los spots. | `SpotsOverrideBgOpacity` |
| DXCC Coloring | — | Colorea los spots según el estado DXCC (trabajado, confirmado o necesario) a partir de su registro ADIF. | `DxccColoringEnabled` |
| Log File (ADIF): | — | Abre un selector de archivos para cargar un registro ADIF que controla la coloración DXCC. | `DxccAdifPath` |
| Auto-Reload Log: | — | Vuelve a leer el archivo ADIF automáticamente cada vez que cambia en el disco. | `DxccAutoReload` |
| Clear All Spots | — | Elimina todos los spots que se siguen actualmente en todas las fuentes. | — |

## Consejos

- El indicador de estado de cada fuente muestra el estado actual: Disconnected, Connected, Stopped, Listening o Polling. Verifique el indicador de estado en cada pestaña antes de solucionar problemas.
- El indicador del total de spots muestra cuántos spots se están siguiendo actualmente en todas las fuentes combinadas.
- RBN puede generar tasas de spots muy elevadas. Configure Rate Limit: en la pestaña RBN para evitar que el grupo de spots se sature.
- Los spots de WSJT-X son efímeros por naturaleza. Use Spot Life: para ajustar la duración a
