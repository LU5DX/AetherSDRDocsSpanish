# Configurar el retardo de break-in de CW

El applet Phone/CW permite configurar cuánto tiempo espera el equipo después del último elemento CW antes de volver a recepción. Ajustar este retardo evita que el equipo cambie a RX entre caracteres a alta velocidad, o le permite regresar rápidamente para QSOs con respuesta inmediata.

## Antes de comenzar

- Conéctese a un equipo FLEX-8600. El applet Phone/CW requiere una conexión activa con el equipo.
- Configure el slice activo en un modo CW. El applet cambia automáticamente al subpanel de CW cuando el slice está en CW; el control Delay no es visible en modos de voz.

## Pasos

1. Localice el botón de bandeja **P/CW** en la barra lateral derecha y confirme que el applet está visible. Si el applet está oculto, haga clic en el botón de bandeja **P/CW** para mostrarlo.
2. Verifique que el applet muestre el subpanel de CW. Si el slice activo está en modo CW, los controles de CW aparecen automáticamente.
3. Localice el control deslizante **Delay (CW)**.
4. Arrastre el control deslizante **Delay (CW)** hasta el valor deseado. El retardo se aplica de inmediato.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Delay (CW)** | Establece el retardo de break-in: cuánto tiempo espera el equipo después del último elemento transmitido antes de volver a recepción. | — | 0–2000 ms, paso 10 | — |
| **Breakin** | Activa o desactiva el break-in completo (QSK). Cuando está habilitado, el equipo cambia a RX entre cada elemento. | — | On / Off | — |

## Consejos

- Configure **Delay (CW)** en 0 ms con **Breakin** activo para operación QSK completa.
- A velocidades más altas, aumente el retardo ligeramente para evitar conmutaciones RX/TX entre caracteres.

## Relacionado

- [Configurar la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Habilitar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar el monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
