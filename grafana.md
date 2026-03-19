#  Explicación Técnica de las Queries (PromQL)

Lo que ves en la imagen son consultas en lenguaje **PromQL (Prometheus Query Language)**. Estas consultas piden datos al **Node Exporter**, que es el servicio que lee directamente el hardware del NUC y el DAS.

---

## 1. La métrica base: `node_filesystem_*`

Todas tus consultas empiezan con este prefijo. Es la forma en que Prometheus identifica las métricas relacionadas con los discos y particiones del sistema Linux.

---

## 2. Query A: La Capacidad Total

```promql
node_filesystem_size_bytes{mountpoint="/mnt/TFG_CRIMSA"}
```

### ¿Qué hace?
Le pregunta al sistema:

> ¿Cuál es el tamaño total (en bytes) de la unidad montada en `/mnt/TFG_CRIMSA`?

### Filtro `{mountpoint="..."}`

Este filtro es fundamental:

- Sin él → Grafana sumaría todos los discos (SSD, RAM, etc.)
- Con él → solo analiza el DAS (QNAP)

Esto permite obtener correctamente la capacidad total (por ejemplo, 3.58 TiB).

---

## 3. Query B: Espacio Ocupado (Cálculo Matemático)

```promql
node_filesystem_size_bytes{mountpoint="/mnt/TFG_CRIMSA"} 
- 
node_filesystem_avail_bytes{mountpoint="/mnt/TFG_CRIMSA"}
```

### ¿Qué hace?

Prometheus no tiene una métrica directa llamada *espacio ocupado*, así que se calcula manualmente:

- Tamaño total (`size_bytes`)
- menos espacio disponible (`avail_bytes`)

### Resultado

Obtienes exactamente:

> La cantidad de datos escritos actualmente en el disco

---

##  Resumen

| Métrica | Descripción |
|--------|------------|
| `node_filesystem_size_bytes` | Tamaño total del disco |
| `node_filesystem_avail_bytes` | Espacio disponible |
| `size - avail` | Espacio usado |

---

##  Uso en Grafana

Estas queries se usan en paneles de Grafana para:

- Monitorizar almacenamiento en tiempo real
- Detectar saturación del disco
- Visualizar uso del DAS
