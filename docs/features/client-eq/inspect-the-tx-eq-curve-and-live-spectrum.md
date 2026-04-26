# Inspeccionar la curva de EQ de TX y el espectro en tiempo real

El tile "Aetherial TX EQ" en el panel de applets muestra la curva de respuesta de EQ sumada y una superposición de analizador FFT en tiempo real para la ruta de audio de TX. Use esta vista para monitorear su ecualización de transmisión de un vistazo sin abrir el editor completo.

## Antes de comenzar

- El sub-contenedor "Aetherial TX EQ" permanece oculto hasta que la etapa de EQ de TX esté habilitada. Habilítela primero mediante el widget CHAIN o el editor flotante ("Aetherial Parametric EQ — TX").
- El tile "Aetherial TX EQ" se encuentra dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets. Confirme que ese contenedor esté visible antes de continuar.

## Pasos

1. Localice el contenedor principal **Aetherial Audio (TXDSP)** en el panel de applets.
2. Expándalo para revelar el sub-contenedor **Aetherial TX EQ**.
3. Observe el área del analizador / curva — la pantalla de 110 px de alto que muestra la cuadrícula de frecuencias, la curva de respuesta de EQ sumada y la superposición de analizador FFT en tiempo real para la ruta de TX.
4. Transmita audio (o active la radio) para llevar la superposición del analizador en tiempo real del estado inactivo al estado activo.
5. Observe la curva de respuesta de EQ sumada, que refleja la respuesta en frecuencia acumulada de todas las bandas de TX habilitadas (`ClientEqTxBands`).

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Área del analizador / curva | Muestra la cuadrícula de frecuencias, la curva de respuesta de EQ sumada y una superposición de analizador FFT en tiempo real bloqueada a la ruta de audio de TX. Solo lectura en este tile. | — |
| Respuesta de EQ sumada | Muestra la respuesta en frecuencia combinada de todas las bandas de TX habilitadas. Aparece plana cuando no hay bandas activas o todas están en bypass. | `ClientEqTxBands` |
| Superposición del analizador en tiempo real | FFT en tiempo real del audio que pasa por la ruta de TX. Se ejecuta mientras hay audio presente; inactiva cuando no fluye audio. | — |

El estado habilitado del EQ de TX se persiste en `ClientEqTxEnabled`.

## Consejos

- El tile es de solo lectura. Para agregar, eliminar o ajustar bandas, haga doble clic en la etapa de EQ de TX en el widget CHAIN para abrir el editor flotante titulado "Aetherial Parametric EQ — TX".
- Haga clic derecho en la barra de título del sub-contenedor "Aetherial TX EQ" para flotar, extraer u ocultar el tile de forma independiente al resto del panel de applets.
- Si el área de la curva aparece en blanco o el tile no es visible, es posible que la etapa de EQ de TX aún esté deshabilitada. Verifique `ClientEqTxEnabled` habilitando la etapa desde el widget CHAIN.

## Solución de problemas

- **El sub-contenedor "Aetherial TX EQ" no es visible** — El tile permanece oculto hasta que la etapa de EQ de TX esté habilitada. Habilite la etapa mediante el widget CHAIN o el editor flotante; luego el sub-contenedor aparecerá dentro de Aetherial Audio (TXDSP).
- **La superposición del analizador en tiempo real permanece inactiva durante la transmisión** — Confirme que el audio esté llegando realmente a la ruta del DSP de TX. Si no hay ningún motor de audio conectado al applet, el FFT no tiene muestras para mostrar.

## Relacionados

- [Descripción general de Aetherial Parametric EQ (TX / RX)](overview.md)
- [Inspeccionar la curva de EQ de RX y el espectro en tiempo real](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Poner en bypass la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Verificar que la curva sumada coincida con su objetivo mental](verify-the-summed-curve-matches-your-mental-target.md)
