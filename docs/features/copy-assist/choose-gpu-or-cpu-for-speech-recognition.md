# Asistente de copia — Voz a texto

Transcripción de voz en tiempo real para el segmento activo. Utiliza whisper.cpp para decodificar el audio de voz recibido en una transcripción desplazable con código de colores (verde = alta confianza, rojo = baja). Incluye selección de modelo, selector de dispositivo de cómputo y coloreado de texto basado en la confianza.

## Controles

### Habilitar / Deshabilitar

Inicia o detiene el motor de voz a texto whisper.cpp en el audio del segmento activo.

| Propiedad | Valor |
|---|---|
| Tipo | Botón de alternancia |
| Predeterminado | Deshabilitado |

### Transcripción

Transcripción desplazable y de solo lectura del habla decodificada. El texto se colorea según la confianza de whisper: verde (alta), amarillo (media), rojo (baja). El botón Borrar vacía el búfer.

| Propiedad | Valor |
|---|---|
| Tipo | Campo de texto |

### Nivel del modelo

Tamaño del modelo de Whisper. Los modelos más grandes son más precisos pero más lentos y usan más VRAM/RAM.

| Propiedad | Valor |
|---|---|
| Tipo | Cuadro combinado |
| Predeterminado | tiny |
| Rango válido | tiny / base / small / medium |

### Dispositivo de cómputo

Selecciona si whisper se ejecuta en GPU (más rápido, requiere VRAM) o CPU (más lento, funciona en cualquier lugar).

| Propiedad | Valor |
|---|---|
| Tipo | Cuadro combinado |
| Predeterminado | GPU (CUDA/Metal) |
| Rango válido | GPU / CPU |

### Indicador de acumulación

Segundos de audio recibido aún no transcrito. El color escala de ámbar a rojo a medida que la acumulación crece.

| Propiedad | Valor |
|---|---|
| Tipo | Indicador |
| Predeterminado | 0.0s |

### Botón de configuración

Abre el diálogo no modal de configuración de Asistente de copia para el nivel del modelo, el dispositivo de cómputo y la configuración del motor.

| Propiedad | Valor |
|---|---|
| Tipo | Botón pulsador |

### Borrar

Limpia el búfer de transcripción actual.

| Propiedad | Valor |
|---|---|
| Tipo | Botón pulsador |

## Indicadores

### Estado del motor

Estado actual del motor de voz a texto whisper.cpp.

| Estado | Significado |
|---|---|
| Idle | El motor no está en ejecución |
| Downloading model | El modelo se está descargando |
| Loading model | El modelo se está cargando en memoria |
| Listening | El motor está transcribiendo activamente |
| Error | El motor encontró un error |

### Acumulación

Segundos de audio no transcrito en el búfer de la canalización.
