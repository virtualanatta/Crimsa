# Script de Backup con rsync

## Explicación

El script de backup en Bash utiliza `rsync` para realizar una copia.

### 1. Variables y rutas

Define:

- **ORIGEN**: directorios a respaldar.
- **DESTINO**: ruta con carpeta de fecha, por ejemplo `semanal_20260318`.
- **LOG**: archivo de historial.

### 2. Preparación

Crea el directorio de destino y sus carpetas superiores si no existen:

```bash
mkdir -p "$DESTINO"
```

### 3. Respaldo (`rsync -az`)

```bash
rsync -az "$ORIGEN" "$DESTINO"
```

Opciones usadas:

- **`-a` (archive)**: mantiene permisos, propietarios y fechas.
- **`-z` (compress)**: comprime los datos para acelerar la transferencia.

Se omite el modo verbose (`-v`) para facilitar la automatización.

### 4. Logging y control de errores (`$?`)

- **0 (éxito)**: registra `"COPIA CORRECTA"` en el log.
- **Otro valor (fallo)**: registra `"ERROR EN LA COPIA"` para revisión.

## Código base

```bash
mkdir -p "$DESTINO"

rsync -az "$ORIGEN" "$DESTINO"

if [ $? -eq 0 ]; then
    echo "COPIA CORRECTA" >> $LOG
else
    echo "ERROR EN LA COPIA" >> $LOG
fi
```
