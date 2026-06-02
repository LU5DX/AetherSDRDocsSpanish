# Resumen de comandos de inicio de DX Cluster

Defina comandos personalizados que AetherSDR envía a un clúster DX o a la Red de Balizas Inversa (Reverse Beacon Network, RBN) inmediatamente después de cada inicio de sesión y reconexión automática. Esto le permite aplicar su filtro, avisos o ajustes operativos preferidos (por ejemplo, `set/dx` o `set/wwv`) sin tener que escribirlos manualmente cada vez.

## Cómo funciona

Cuando AetherSDR se conecta (o reconecta) a un clúster DX o a un nodo RBN, envía cada línea de la lista de comandos correspondiente, una por línea, inmediatamente después de que se complete el protocolo de inicio de sesión. Los mismos comandos se reenvían después de cada reconexión automática provocada por una caída de red.

Se almacenan y gestionan dos conjuntos de comandos independientes:

- **DX Cluster** — comandos enviados al clúster configurado en la pestaña DX Cluster de SpotHub (clave `DxClusterStartupCommands` en AppSettings).
- **RBN** — comandos enviados a la pestaña Reverse Beacon Network de SpotHub (clave `RbnStartupCommands` en AppSettings).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido / Notas | Clave AppSettings |
|---|---|---|---|
| **Editor de comandos** (editor de texto plano multilínea) | *(vacío)* | Un comando por línea. Las líneas en blanco se ignoran. Sin límite en el número de líneas. | `DxClusterStartupCommands` (pestaña principal) / `RbnStartupCommands` (pestaña RBN) |

## Cómo abrir el diálogo

Abra `Settings > SpotHub...`, luego haga clic en **Edit Startup Commands** en cualquiera de las siguientes pestañas:

- La pestaña **DX Cluster** — para editar el conjunto de comandos del clúster principal.
- La pestaña **RBN** — para editar el conjunto de comandos RBN.

## Consejos

- Los comandos se envían en el orden en que aparecen en el editor, de arriba abajo.
- Los comandos de inicio típicos incluyen `set/dx` (habilitar spots DX), `set/announce` (habilitar avisos) o `set/filter` para limitar los tipos de spots. Consulte la ayuda de su clúster (`help`) para conocer los comandos disponibles.
- Si un comando requiere una respuesta del clúster (por ejemplo, una confirmación de estado), AetherSDR no espera: envía todas las líneas inmediatamente. Para secuencias de tiempo crítico, manténgalas cortas.
- Los cambios surten efecto en la siguiente conexión o reconexión; no se envían a una sesión ya conectada.
- El diálogo ahora utiliza la paleta de colores del tema activo. Los fondos, colores de texto y colores de acento se adaptan automáticamente a la selección del tema de interfaz de usuario actual.

## Véase también

- Configuración de DX Cluster y RBN
