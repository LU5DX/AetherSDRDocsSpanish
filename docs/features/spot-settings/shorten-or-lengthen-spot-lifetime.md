# Acortar o alargar el tiempo de vida de un spot

Use el control deslizante **Spot Lifetime:** en Spot Settings para controlar cuánto tiempo permanecen visibles los spots de DX en el panadapter antes de que expiren.

## Antes de comenzar

- Los spots deben estar visibles en el panadapter. Si no se muestran, confirme que el interruptor **Spots:** indique "Enabled" en Spot Settings.
- Abra Spot Settings haciendo clic derecho sobre la capa de spots en el panadapter.

## Pasos

1. Haga clic derecho sobre la capa de spots en el panadapter para abrir el diálogo **Spot Settings**.
2. Localice la fila **Spot Lifetime:**.
3. Arrastre el control deslizante hacia la izquierda para acortar el tiempo de vida o hacia la derecha para alargarlo. La etiqueta a la derecha del control se actualiza de inmediato y muestra el valor actual en segundos, minutos u horas (por ejemplo, `30 secs`, `15 mins`, `2 hrs`).
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Control deslizante **Spot Lifetime:** | Define cuánto tiempo permanece un spot en el panadapter antes de desvanecerse. La escala es no lineal: la parte inferior avanza en incrementos de 5 segundos (10 sec – 55 sec), la parte media en incrementos de 5 minutos (5 min – 55 min) y la parte superior en incrementos de 1 hora (1 hr – 24 hrs / 1 day). | 30 min | 10 sec – 24 hrs | `SpotsLifetime` |

## Consejos

- El control deslizante utiliza una escala no lineal. Los movimientos pequeños cerca del extremo izquierdo ajustan el tiempo de vida en segundos; los movimientos cerca del extremo derecho lo ajustan en horas. Posicione el control con cuidado cuando busque un valor específico.
- La etiqueta mostrada se redondea al paso más cercano: los valores por debajo de 60 segundos se muestran como `sec`, los valores por debajo de 1 hora se muestran como `min` o `mins`, y los valores de 1 hora o más se muestran como `hr`, `hrs` o `1 day`.

## Solución de problemas

- **Los spots antiguos siguen apareciendo después de reducir el tiempo de vida** — Los spots existentes que llegaron antes del cambio expirarán según la configuración anterior. Los spots nuevos utilizarán el tiempo de vida actualizado. Haga clic en **Clear All Spots** para eliminar los spots existentes de inmediato.

## Relacionados

- [Descripción general de Spot Settings](overview.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
