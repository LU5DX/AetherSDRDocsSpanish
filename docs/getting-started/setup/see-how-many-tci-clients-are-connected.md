# Applet del Servidor TCI

El applet del Servidor TCI ejecuta un servidor WebSocket TCI de estilo Expert, permitiendo que software de registro, modos digitales y SDR de terceros (Log4OM, herramientas SunSDR, etc.) lean y controlen el radio mediante el protocolo TCI.

El audio TX de TCI se recibe a través del WebSocket y se introduce en una ranura de flujo dax_tx dedicada, independiente de la ruta de audio del dispositivo DAX2 de SmartSDR en Windows. De este modo, la transmisión por TCI funciona en todas las plataformas, incluyendo Windows y Linux, sin necesidad de PipeWire.

## Vea cuántos clientes TCI están conectados

El applet del Servidor TCI muestra un conteo de clientes en vivo en su indicador de estado. Úselo para confirmar que Log4OM, las herramientas SunSDR o cualquier otro cliente TCI se haya conectado correctamente.

## Antes de empezar

- AetherSDR debe estar conectado a un radio. El applet TCI requiere una conexión activa con el radio.
- El servidor TCI debe estar en ejecución (Habilitar activado). Si está detenido, el estado muestra `(detenido)` y no hay conteo de clientes disponible.

## Pasos

1. Haga clic en el botón **TCI** en la barra lateral derecha para abrir el applet del Servidor TCI.
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

## Descripción de cada control

| Control                         | Descripción                                                                                                                                                                                    | Notas                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Puerto                          | Puerto en el que escucha el servidor WebSocket TCI. Los valores fuera de rango se ajustan a `50001`.                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Habilitar                       | Inicia o detiene el servidor TCI.                                                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Estado del servidor             | Muestra `(detenido)`, `:<puerto> (N clientes)` o `(puerto en uso)`. Se vuelve rojo en caso de error de enlace.                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Medidor + deslizador RX1–RX4    | Medidor/deslizador combinado; al arrastrarlo se ajusta la ganancia RX de TCI para el canal y se emite `tciRxGainChanged`.                                                                      | Cada deslizador tiene un nombre accesible "TCI RX gain" seguido del número de canal (1–4) para compatibilidad con lectores de pantalla.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Medidor + deslizador TX         | Al arrastrarlo se ajusta la ganancia TX de TCI y se emite `tciTxGainChanged`. Al hacer clic derecho se abre el selector de modo de desbordamiento TX (Recortar / GuardarNaN / Medir).           | TciServer::setTxGain conserva TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú contextual permite elegir cómo se manejan las muestras fuera de rango (>1.0) provenientes de clientes de modos digitales: Recortar (saturación ±1.0, valor predeterminado heredado), GuardarNaN (pasante, solo pone a cero NaN/Inf) o Medir (bypass real con conteo de recortes). El valor predeterminado es Recortar para que los usuarios existentes no vean cambios de comportamiento (#3065). El deslizador tiene un nombre accesible "TCI TX gain" para compatibilidad con lectores de pantalla. |
| Modo de desbordamiento TX (clic derecho) | Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite `tciTxOverflowModeChanged`. El valor predeterminado es Recortar para que los usuarios existentes no vean cambios de comportamiento. |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Etiquetas de asignación de slice RX/TX | Muestran qué slice impulsa actualmente cada fila RX/TX. Muestra `—` cuando no hay ningún slice asignado o `Slice <letra>` cuando hay un slice mapeado.                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

## Detalles del modo de desbordamiento TX

Haga clic derecho en el medidor/deslizador de ganancia TX para abrir el menú de modo de manejo de desbordamiento TX. Esta configuración determina cómo se manejan las muestras fuera de rango (>1.0) de los clientes TCI antes de que lleguen al radio.

| Modo       | Valor | Descripción                                                                                                                                                                               |
|------------|-------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Recortar   | 0     | Limita bruscamente los picos a ±1.0. Valor defensivo predeterminado; introduce armónicos en los picos pero protege la conversión posterior a int16.                                       |
| GuardarNaN | 1     | Pasa las muestras sin cambios; solo pone a cero los valores NaN/Inf patológicos. Preserva la fidelidad del tono en modos digitales; los flotantes fuera de rango llegan al radio.         |
| Medir      | 2     | Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión posterior a int16 aún recorta en la ruta DAX nativa del radio.                                               |

Recortar es el valor predeterminado y conserva el limitador defensivo heredado. GuardarNaN y Medir son progresivamente menos destructivos para la fidelidad del tono en modos digitales. El modo se conserva como `TciTxOverflowMode` (0, 1 o 2).

## Consejos

- El conteo de clientes se actualiza automáticamente cuando un cliente se conecta o desconecta; no es necesario actualizar.
- Cuando hay un cliente conectado, el estado muestra `(1 cliente)` (singular); con dos o más muestra `(N clientes)` (plural).
- El texto de estado se vuelve azul cuando hay uno o más clientes conectados, lo que facilita su identificación de un vistazo.

## Solución de problemas

- **El estado muestra `(puerto en uso)`** — Otro proceso ya está usando el puerto configurado. Cambie el valor en el campo Puerto a un puerto no utilizado en el rango 1024–65535 y presione Enter. El servidor se reinicia automáticamente si Habilitar está activado.
- **El estado permanece en `(detenido)` después de hacer clic en Habilitar** — El enlace falló y Habilitar volvió a desactivarse. Verifique el valor del Puerto y confirme que ninguna otra aplicación esté usando ese puerto.
- **El conteo de clientes permanece en 0** — Confirme que la aplicación de terceros esté configurada para conectarse al host y puerto correctos. El puerto en uso se muestra en el indicador de estado.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Inicio automático de TCI al arrancar](../../features/tci/autostart-tci-on-launch.md)
- [Descripción general del Servidor TCI](../../features/tci/overview.md)
