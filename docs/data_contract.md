# 📜 Data Contract — Predicciones de Demanda

## Esquema de salida esperado
Cada fila corresponde a una celda H3 y un intervalo de tiempo.

| Campo              | Tipo        | Descripción |
|--------------------|-------------|-------------|
| slot               | timestamp   | Inicio del intervalo (15 o 30 min). |
| h3_cell            | string      | ID de celda H3 (nivel 7–8). |
| demanda_esperada   | float       | Predicción puntual de número de pedidos. |
| p10                | float       | Cuantil 10 de predicción (intervalo bajo). |
| p90                | float       | Cuantil 90 de predicción (intervalo alto). |
| riders_sugeridos   | int         | Número recomendado de repartidores. |

---

## Notas importantes
- `slot` está en zona horaria **America/Bogota**.
- `demanda_esperada` es la salida principal del modelo.
- `p10` y `p90` ayudan a capturar incertidumbre.
- `riders_sugeridos` se calcula como:

```python
riders_sugeridos = ceil(demanda_esperada / capacidad_rider_slot)
