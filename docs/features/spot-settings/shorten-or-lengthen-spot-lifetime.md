# Acortar o alargar el tiempo de vida de los puntos

Use el control deslizante **Spot Lifetime:** en Spot Settings para controlar cuánto tiempo permanecen visibles los puntos de DX en el panadapter antes de que expiren.

## Antes de comenzar

- Los puntos deben mostrarse en el panadapter. Si no son visibles, confirme que el conmutador **Spots:** muestra "Enabled" en Spot Settings.
- Abra Spot Settings haciendo clic derecho en la superposición de puntos en el panadapter.

## Pasos

1. Haga clic derecho en la superposición de puntos en el panadapter para abrir el diálogo **Spot Settings**.
2. Localice la fila **Spot Lifetime:** .
3. Arrastre el control deslizante hacia la izquierda para acortar el tiempo de vida o hacia la derecha para alargarlo. La etiqueta a la derecha del control deslizante se actualiza de inmediato, mostrando el valor actual en segundos, minutos u horas (por ejemplo, `30 secs`, `15 mins`, `2 hrs`).
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente.

## Qué hace cada control

| Control                       | Comportamiento                                                                                                                                                                                                                                                                                                   | Valor predeterminado |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| Control deslizante **Spot Lifetime:** | Establece cuánto tiempo permanece un punto en el panadapter antes de desvanecerse. La escala no es lineal: la sección inferior tiene incrementos de 5 segundos (10 sec – 55 sec), la sección media tiene incrementos de 5 minutos (5 min – 55 min) y la sección superior tiene incrementos de 1 hora (1 hr – 24 hrs / 1 day). | 30 min               |
| Botón conmutador **Spot Lines:** | Dibuja líneas verticales desde la línea de base del espectro hasta cada etiqueta de punto. Haga clic para alternar entre Enabled y Disabled. Desactívelo durante concursos para reducir el desorden visual. Se guarda en `IsSpotsLinesEnabled`. Añadido en v0.9.7 (#2349).                                            | Enabled              |

## Consejos

- El control deslizante usa una escala no lineal. Los movimientos pequeños cerca del extremo izquierdo ajustan el tiempo de vida en segundos; los movimientos cerca del extremo derecho lo ajustan en horas. Posicione el control deslizante con cuidado al apuntar a un valor específico.
- La etiqueta mostrada se redondea al paso más cercano: los valores menores a 60 segundos se muestran como `sec`, los valores menores a 1 hora se muestran como `min` o `mins`, y los valores de 1 hora o más se muestran como `hr`, `hrs` o `1 day`.
- Si las líneas verticales hacen que el panadapter se sienta desordenado durante un concurso, haga clic en **Spot Lines:** para establecerlo en Disabled. El cambio surte efecto de inmediato y se guarda automáticamente.

## Solución de problemas

- **Aún aparecen puntos antiguos después de reducir el tiempo de vida** — Los puntos existentes que llegaron antes del cambio expirarán según la configuración anterior. Los puntos nuevos usarán el tiempo de vida actualizado. Haga clic en **Clear All Spots** para eliminar los puntos existentes de inmediato.

## Relacionado

- [Resumen de Spot Settings](overview.md)
- [Activar o desactivar los puntos](turn-spots-on-or-off.md)
- [Borrar todos los puntos del panadapter](clear-every-spot-from-the-panadapter.md)
