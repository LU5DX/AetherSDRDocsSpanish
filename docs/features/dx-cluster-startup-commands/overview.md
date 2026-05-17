# Resumen de comandos de inicio del DX Cluster

Defina comandos personalizados que AetherSDR envía a un DX cluster o Reverse Beacon Network (RBN) inmediatamente después de cada inicio de sesión y reconexión automática. Esto le permite aplicar su filtro, anuncios o configuraciones operativas preferidas (por ejemplo, `set/dx` o `set/wwv`) sin tener que escribirlos manualmente cada vez.

## Cómo funciona

Cuando AetherSDR se conecta (o reconecta) a un DX cluster o nodo RBN, envía cada línea de la lista de comandos correspondiente, una por línea, inmediatamente después de que se completa el protocolo de inicio de sesión. Los mismos comandos se reenvían después de cada reconexión automática provocada por una caída de red.

Se almacenan y gestionan dos conjuntos de comandos independientes:

- **DX Cluster** — comandos enviados al cluster configurado en la pestaña DX Cluster de SpotHub (clave AppSettings `DxClusterStartupCommands`).
- **RBN** — comandos enviados a la pestaña Reverse Beacon Network de SpotHub (clave AppSettings `RbnStartupCommands`).

## Función de cada control

| Control | Predeterminado | Rango válido / Notas | Clave AppSettings |
|---|---|---|---|
| **Editor de comandos** (editor de texto plano multilínea) | *(vacío)* | Un comando por línea. Las líneas en blanco se ignoran. Sin límite en el número de líneas. | `DxClusterStartupCommands` (pestaña principal) / `RbnStartupCommands` (pestaña RBN) |

## Cómo abrir el cuadro de diálogo

Abra `Settings > SpotHub...`, luego haga clic en **Edit Startup Commands** en cualquiera de las siguientes pestañas:

- La pestaña **DX Cluster** — para editar el conjunto de comandos del cluster principal.
- La pestaña **RBN** — para editar el conjunto de comandos del RBN.

## Consejos

- Los comandos se envían en el orden en que aparecen en el editor, de arriba a abajo.
- Los comandos de inicio típicos incluyen `set/dx` (habilitar spots DX), `set/announce` (habilitar anuncios) o `set/filter` para limitar los tipos de spots. Consulte la ayuda de su cluster (`help`) para conocer los comandos disponibles.
- Si un comando requiere una respuesta del cluster (por ejemplo, una confirmación de estado), AetherSDR no espera; envía todas las líneas inmediatamente. Para secuencias en las que el tiempo sea importante, manténgalas cortas.
- Los cambios surten efecto en la próxima conexión o reconexión; no se envían a una sesión ya conectada.

## Véase también

- [Configuración de DX Cluster y RBN](dx-cluster-rbn-configuration.md)
