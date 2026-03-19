# Script de Notificación de Acceso y Estado vía Telegram

## Explicación

Este script integra una capa de seguridad activa al sistema, enviando una notificación instantánea a un bot de Telegram cada vez que se detecta un acceso o ejecución, informando sobre el usuario y el estado del almacenamiento.

### 1. Variables de configuración y API

El script define los parámetros necesarios para la comunicación externa:

- **TOKEN**: identificador único de seguridad para el bot de Telegram.
- **ID_CHAT**: dirección del chat o grupo específico donde se recibirán las alertas.
- **LOG_FILE**: ruta del archivo local donde se mantiene el histórico de eventos.

### 2. Captura y registro de datos

Al igual que el script de auditoría, recolecta información crítica del sistema:

- **Identificación**: obtiene la fecha (`date`), el nombre de usuario (`whoami`) y la dirección IP de origen (`$SSH_CONNECTION`).
- **Estado del DAS**: extrae el porcentaje de uso del disco mediante `df -h` y `awk`.
- **Persistencia local**: utiliza `printf` para guardar una copia formateada de estos datos en el log local del servidor.

### 3. Notificación remota (Telegram API)

Es la funcionalidad principal del script para la monitorización en tiempo real:

- **Construcción del mensaje**: crea una cadena de texto formateada en Markdown que incluye alertas visuales y los datos capturados.
- **Envío con `curl`**: realiza una petición `POST` a la API de Telegram para enviar el mensaje de forma silenciosa (`-s`).
- **Optimización**: el resultado de la petición se redirige a `/dev/null` para no generar salidas innecesarias en la terminal del usuario.

## Código base

```bash
TOKEN="TU_TOKEN"
ID_CHAT="TU_CHAT_ID"
LOG_FILE="/ruta/log.log"

printf "Registro de acceso" >> $LOG_FILE

curl -s -X POST https://api.telegram.org/bot$TOKEN/sendMessage \
-d chat_id=$ID_CHAT \
-d text="Mensaje" \
-d parse_mode="Markdown" > /dev/null
```

> Nota: Si algún día quieres editarlos, tendrás que quitar el atributo primero con `sudo chattr -i` (para los scripts) o `sudo chattr -a` (para el log).
