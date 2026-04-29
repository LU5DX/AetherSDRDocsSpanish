# Escuchar el monitor de tono lateral de TX

AetherSDR proporciona un monitor del lado del radio (disponible en los modos Phone y CW) y un tono lateral CW de baja latencia del lado del cliente (aproximadamente 10 ms de latencia), controlados de forma sincronizada mediante el botón Sidetone y el control deslizante Sidetone volume. Esta página describe ambas rutas para que pueda escuchar su propio audio transmitido durante la operación.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone/CW requiere una conexión de radio activa.
- Abra el panel de applets. Si no está visible, haga clic en View > Applet Panel.

## Pasos

### Modo Phone: activar el monitor de banda lateral

1. Haga clic en el botón P/CW del panel lateral derecho para abrir el applet Phone/CW.
2. Confirme que el applet muestra el panel Phone (el slice activo debe estar en un modo de voz como SSB o AM).
3. Haga clic en MON para activar el monitor de banda lateral de TX. El botón se resalta cuando está activo.
4. Ajuste el control deslizante Monitor volume para establecer el nivel de reproducción (0–100).

### Modo CW: activar el monitor de tono lateral

1. Cambie el slice activo al modo CW. El applet muestra automáticamente el panel CW.
2. Haga clic en Sidetone para activar el monitor CW. El botón se resalta cuando está activo.
   - Este botón único controla de forma sincronizada tanto el monitor del radio alimentado por DAX como el generador de tono lateral de baja latencia del lado del cliente.
3. Ajuste el control deslizante Sidetone volume para establecer el nivel (0–100).
   - Este control deslizante único establece el volumen tanto para el monitor del lado del radio (`mon_gain_cw`) como para el generador de tono lateral local de forma simultánea.
4. El tono y el paneo estéreo se configuran automáticamente a partir de los ajustes `cw_pitch` y `mon_pan_cw` del radio. Para ajustar el paneo manualmente, use el control deslizante L / R pan (CW) (haga doble clic para centrarlo).

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| MON | Activa el monitor de banda lateral de TX (panel Phone). | — | On / Off | — |
| Monitor volume | Establece el nivel de reproducción del monitor de banda lateral. | — | 0–100 | — |
| Sidetone | Activa el monitor CW. Controla de forma sincronizada tanto el monitor del radio alimentado por DAX como el generador de tono lateral de baja latencia del lado del cliente. | — | On / Off | — |
| Sidetone volume | Establece el nivel de reproducción del monitor CW para el monitor del lado del radio y el generador de tono lateral local de forma simultánea. | — | 0–100 | — |
| L / R pan (CW) | Establece el paneo estéreo del monitor CW; se aplica tanto al monitor del radio como al generador de tono lateral local. Haga doble clic para centrar. | 50 | 0–100 | — |

## Consejos

- El botón Sidetone y el control deslizante Sidetone volume controlan ambas rutas de audio (monitor DAX del radio y generador del lado del cliente) de forma conjunta. No existe un control independiente para activar o ajustar el tono lateral local por separado.
- El tono siempre sigue automáticamente el ajuste de tono CW del radio. Use el selector Pitch < / > para cambiar el tono CW del radio; tanto el tono de decodificación como el tono lateral se actualizarán en consecuencia.
- El botón MON y el botón Sidetone son controles independientes en paneles separados. MON se aplica a los modos de voz; Sidetone se aplica al modo CW.

## Solución de problemas

- **El botón MON o Sidetone no tiene efecto** — Confirme que el radio está conectado y que el modo del slice activo corresponde al panel que se muestra (Phone o CW). El applet cambia de panel automáticamente según el modo del slice activo.
- **Sidetone no produce audio** — Verifique que la salida de audio del sistema esté configurada correctamente. El tono lateral del lado del cliente es generado localmente por AetherSDR; confirme que el botón Sidetone está activo.
- **El tono lateral es incorrecto** — El tono se deriva automáticamente del ajuste `cw_pitch` del radio. Ajuste el tono usando el selector Pitch < / > en el panel CW.

## Relacionados

- [Cambiar el tono CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
