# Descripción general de formas de onda

El diálogo de Formas de Onda refleja el panel SmartSDR Archivo > Formas de Onda, permitiéndole ver el estado del WFP (Procesador de Formas de Onda) y administrar las formas de onda instaladas en su radio FLEX-8600. Úselo para verificar si el procesador de formas de onda está encendido y listo, ver su dirección IP, y reiniciar o eliminar formas de onda individuales.

## Cómo funciona

El diálogo se conecta directamente al FlexWaveformModel del radio para obtener actualizaciones de estado en vivo. Muestra el estado de alimentación del WFP, su disponibilidad y dirección IP en la parte superior, seguido de una lista de formas de onda instaladas con controles por fila. Una etiqueta **Soporte WFP** indica si el radio conectado tiene hardware de Procesador de Formas de Onda. El diálogo también incluye controles de configuración de servicio de voz digital local (disponibles solo cuando `kShowLocalDigitalVoiceControls` está habilitado).

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Estado WFP** | Muestra el estado de alimentación del procesador de formas de onda, estado de disponibilidad y dirección IP. | Nuevo en v26.5.2.1. Muestra "WFP ENCENDIDO / LISTO", "WFP APAGADO / NO LISTO", etc. |
| **Soporte WFP** | Indica si el radio conectado tiene hardware de Procesador de Formas de Onda. Muestra "Compatible" (verde) o "No compatible" (gris). Muestra "Sin radio" cuando está desconectado y "Verificando" mientras espera la identificación del radio. | Basado en la capacidad real del hardware, no en la característica de licencia "wfp" (#4210). |
| **Formas de Onda Instaladas** | Lista las formas de onda instaladas con botones **Reiniciar** y **Eliminar/Desinstalar** por fila. | Se conecta a FlexWaveformModel para estado en vivo. |
| **Instalar** | Abre un diálogo de archivos para seleccionar una imagen Docker de forma de onda (archivo .tar o .tgz) para instalar en el radio. Bloqueado según el estado de conexión del radio y el estado de ejecución del WFP. | Deshabilitado cuando no hay radio conectado, la plataforma no admite implementación Docker, o el estado de ejecución del WFP es desconocido. |
| **Controles de Voz Digital Local** | Configura servicios de voz digital local (D-Star, etc.) para AetherModem. Solo se muestra cuando `kShowLocalDigitalVoiceControls` está habilitado en la configuración de compilación. | No visible por defecto. |

## Cómo abrir

**Archivo > Formas de Onda...**

## Requisitos

- Debe haber una conexión de radio activa (el diálogo requiere conectividad al radio) a menos que solo esté viendo información local de formas de onda.

## Instalación de forma de onda Docker

El botón **Instalar** está bloqueado por las siguientes condiciones (verificadas en orden):

1. **Radio conectado**: Debe estar conectado a un radio.
2. **Soporte de plataforma**: La plataforma del radio debe admitir implementación de formas de onda Docker en el radio (no una plataforma Microburst/DeepEddy de la serie 6000).
3. **Estado de ejecución del WFP**: El Procesador de Formas de Onda debe estar encendido y listo (WFP ENCENDIDO, LISTO).

Si alguna condición falla, el botón se deshabilita y una información sobre herramientas explica el motivo.

## Indicadores de estado de conexión

- **WFP Alimentado**: Muestra si la alimentación del Procesador de Formas de Onda está encendida.
- **WFP Listo**: Muestra si el Procesador de Formas de Onda está listo para aceptar imágenes de formas de onda.
- **Dirección IP del WFP**: Muestra la dirección IP del Procesador de Formas de Onda cuando está disponible.

## Consejos

- El diálogo es no modal, por lo que puede mantenerlo abierto mientras opera el radio.
- Use el botón **Reiniciar** para recargar una forma de onda sin eliminarla y reinstalarla.
- Use **Eliminar/Desinstalar** para borrar una forma de onda no deseada del radio.
- El diálogo aplica el estilo del tema actual para ventanas de formas de onda, asegurando consistencia visual con otros diálogos.
- El indicador **Soporte WFP** se actualiza automáticamente al conectarse o desconectarse de un radio. Si muestra "Verificando" por más de unos segundos, intente reconectar el radio.
- La política de bloqueo de instalación Docker (implementada en `WaveformInstallGate.h`) usa solo el estado de ejecución del WFP en vivo del radio y la capacidad de la plataforma — no la característica de licencia "wfp" — por lo que el estado habilitado del botón **Instalar** coincide con la preparación real del hardware.

## Relacionado

- Configuración del Radio... — Configure la conexión del radio, audio, antena y configuración de banda.
