# Applet del servidor TCI

El applet del servidor TCI ejecuta un servidor WebSocket de estilo Expert TCI para que software de registro, modos digitales y SDR de terceros (Log4OM, herramientas SunSDR, etc.) puedan leer y controlar el radio mediante el protocolo TCI.

El audio TX de TCI se recibe a través del WebSocket y se alimenta a un slot de flujo dax_tx dedicado, independiente de la ruta del dispositivo de audio DAX2 de Windows SmartSDR. Esto permite que la transmisión TCI funcione en todas las plataformas, incluyendo Windows y Linux, sin necesidad de PipeWire.

## Vea cuántos clientes TCI están conectados

El applet del servidor TCI muestra un contador de clientes en vivo en su indicador de estado. Utilícelo para confirmar que Log4OM, las herramientas SunSDR o cualquier otro cliente TCI se haya conectado exitosamente.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El applet TCI requiere una conexión activa al radio.
- El servidor TCI debe estar en ejecución (con la opción Habilitar activada). Si está detenido, el estado muestra `(detenido)` y no hay contador de clientes disponible.

## Pasos

1. Haga clic en el botón **TCI** de la bandeja en la barra lateral derecha para abrir el applet del servidor TCI.
2. Lea el indicador de estado junto al campo Puerto.

Cuando el servidor está en ejecución y al menos un cliente está conectado, el estado muestra:

```
:<puerto> (N clientes)
```

Por ejemplo, con dos clientes conectados en el puerto predeterminado:

```
:50001 (2 clientes)
```

Cuando el servidor está en ejecución pero no hay clientes conectados, el estado muestra el puerto y `(0 clientes)`. Cuando el servidor está detenido, el estado muestra `(detenido)`.

## Función de cada control

| Control                        | Descripción                                                                                                                                                                                                                             | Notas                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Puerto                         | Puerto en el que escucha el servidor WebSocket TCI. Los valores fuera de rango se ajustan a `50001`. Tiene el nombre accesible "Puerto TCI" y la descripción accesible "Puerto TCP en el que escucha el servidor TCI".                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Habilitar / Deshabilitado      | Inicia o detiene el servidor TCI. El texto del botón se actualiza dinámicamente a "Habilitado" cuando el servidor está en ejecución y a "Deshabilitado" cuando está detenido. Tiene el nombre accesible "Habilitar servidor TCI".       | El botón es verificable. Si la opción Inicio automático de TCI está habilitada en la configuración, el botón se inicializa como "Habilitado" y activado. Al alternar, el texto se actualiza inmediatamente. Si la vinculación falla, el botón vuelve a su estado desactivado y el texto regresa a "Deshabilitado".                                                                                                                                                                                                                                                            |
| Estado del servidor            | Muestra `(detenido)`, `:<puerto> (N clientes)` o `(puerto en uso)`. Se vuelve rojo si falla la vinculación.                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Ganancia+medidor RX1–RX4       | Combinación de medidor/deslizador; al arrastrar se establece la ganancia RX TCI para el canal y se emite `tciRxGainChanged`.                                                                                                            | Cada deslizador tiene un nombre accesible "Ganancia RX TCI" seguido del número de canal (1–4) para compatibilidad con lectores de pantalla.                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Ganancia+medidor TX            | Al arrastrar se establece la ganancia TX TCI y se emite `tciTxGainChanged`. El clic derecho abre el selector de modo de desbordamiento TX (Recortar / Protector NaN / Medir).                                                            | TciServer::setTxGain persiste TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú contextual permite al usuario elegir cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modos digitales: Recortar (saturación a ±1.0, predeterminado heredado), Protector NaN (paso directo, solo cero NaN/Inf), o Medir (bypass real con conteo de recortes). El valor predeterminado es Recortar para que los usuarios existentes no observen cambios de comportamiento (#3065). |
| Modo de desbordamiento TX (clic derecho) | Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite `tciTxOverflowModeChanged`. El valor predeterminado es Recortar para que los usuarios existentes no observen cambios de comportamiento. |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Etiquetas de asignación de segmento RX/TX | Muestran qué segmento impulsa cada fila RX/TX. Muestra `—` cuando no hay ningún segmento asignado o `Segmento <letra>` cuando hay un segmento mapeado.                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

## Detalles del modo de desbordamiento TX

Haga clic derecho en el medidor/deslizador de ganancia TX para abrir el menú del modo de manejo de desbordamiento TX. Esta configuración determina cómo se manejan las muestras fuera de rango (>1.0) de los clientes TCI antes de que el radio las vea.

| Modo          | Valor | Descripción                                                                                                                                                                                                                 |
|---------------|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Recortar      | 0     | Sujeta forzosamente los picos a ±1.0. Valor predeterminado defensivo; introduce armónicos en los picos pero protege la conversión ascendente a int16.                                                                       |
| Protector NaN | 1     | Pasa las muestras bit a bit; solo pone a cero valores patológicos NaN/Inf. Preserva la fidelidad tonal de los modos digitales; los flotantes fuera de rango llegan al radio.                                               |
| Medir         | 2     | Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión ascendente a int16 aún recorta en la ruta DAX nativa del radio.                                                                               |

Recortar es el valor predeterminado y preserva el limitador defensivo heredado. Protector NaN y Medir son progresivamente menos destructivos para la fidelidad tonal de los modos digitales. El modo se persiste como `TciTxOverflowMode` (0, 1 o 2).

## Consejos

- El contador de clientes se actualiza automáticamente cada vez que un cliente se conecta o desconecta: no es necesario actualizar.
- Cuando hay un cliente conectado, el estado muestra `(1 cliente)` (singular); dos o más muestran `(N clientes)` (plural).
- El texto de estado se vuelve azul cuando hay uno o más clientes conectados, lo que facilita su identificación de un vistazo.
- El texto del botón Habilitar cambia entre "Habilitado" y "Deshabilitado" para indicar claramente el estado actual del servidor.

## Solución de problemas

- **El estado muestra `(puerto en uso)`** — Otro proceso ya está vinculado al puerto configurado. Cambie el valor en el campo Puerto a un puerto no utilizado en el rango 1024–65535 y presione Enter. El servidor se reinicia automáticamente si la opción Habilitar está activada.
- **El estado permanece `(detenido)` después de hacer clic en Habilitar** — La vinculación falló y la opción Habilitar se desactivó. El texto del botón vuelve a "Deshabilitado". Verifique el valor del Puerto y confirme que ninguna otra aplicación esté usando ese puerto.
- **El contador de clientes permanece en 0** — Confirme que la aplicación de terceros esté configurada para conectarse al host y puerto correctos. El puerto en uso se muestra en el indicador de estado.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Inicio automático de TCI al iniciar](../../features/tci/autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](../../features/tci/overview.md)
