# Infraestructura de Almacenamiento TFG - CRIMSA
# 1. Configuración del Hardware y Montaje
El corazón físico es un NUC conectado a una caja RAID QNAP TR-002, tenemos 2 discos /dev/sdb de 4 TB y /dev/sdc de 4TB, donde usaremos el último como disco de respaldo en RAID 1
Pasos:
Identificar los discos mediante lsblk -f para obtener el UUID de los discos
(captura)
Editar el fichero del sistema /etc/fstab
(captura)
Implementar la línea de montaje persistente para aseguridad que el disco se monte siempre en el mismo sitio
(captura)
# 2. Estructura de Datos
Es indispensable un orden jerárquico para evitar la perdida de informacion y facilitar backups rapidos, donde hemos diseñado una estructura que separa el código de los datos
Organización de las carpetas
PROYECTO/-> Contiene la documentación completa y detallada junto a los scripts de automatización
DATOS/ Dividido entre los datos originales y los resultados de los scripts
ENTORNOS/ Exclusivo de contenedores Docker y entornos virtuales para las pruebas
SISTEMA/ Reservado para logs de acceso y los backups importantes
# 3. Sistema de Auditoría y Seguridad
La seguridad se basa en algo llamado "Privacidad por diseño", donde NO abrimos puertos hacia internet; en su lugar usamos una VPN Zero-Trust ''Tailscale'' y un sistema de logs que nos informa en tiempo real de quién entra al sevidor
Componentes de seguridad:
## Red: 
  Acceso cifrado WIREGUARD mediante Tailscale, donde el servidor escucha solo en la interfaz tailscale0
## Samba: 
  Configurado para requerir cifrado (smb encrypt = required) y restringido por IP para que solo tu portátil pueda mapear la unidad
## Scripts de Auditoría: 
  ## Automatización:
  Vinculado a /etc/profile para ejecutarse instantáneamente cada vez que alguien inicia sesión por SSH
  ## Funcionalidad: Genera un reporte dinámico que muestra:
    1. Usuarios SSH activos
    2. Sesiones de Samba abiertas
    3. Porcentaje de uso de los 3.4 TB


# Guía de Configuración: Del Hardware a la Nube Privada

# 1. Configuración de Discos y Creación del RAID
Para asegurar que los datos del TFG no se pierdan si un disco falla, hemos configurado un sistema de espejo (RAID 1).

### Paso A: Identificación de Hardware
Al conectar el gabinete QNAP TR-002, el sistema reconoce los discos físicos.
* **Comando:** `lsblk`
* **Resultado:** Identificamos `/dev/sdb` y `/dev/sdc` como los discos de 4TB.

### Paso B: Creación del RAID 1
Utilizamos el modo de hardware del QNAP (o herramientas de software como `mdadm` si fuera necesario) para que el sistema vea un único volumen lógico de **3.4 TB**.

### Paso C: Formateo y Montaje Persistente
## 1. **Formateo:** Se dio formato **EXT4** por su estabilidad en Linux.

sudo mkfs.ext4 /dev/sdb
## 2. Obtener UUID: Fundamental para que el montaje no falle nunca.
lsblk -f
## 3. Implementación de la línea de montaje persistente:
UUID=xxxx /mnt/TFG_CRIMSA ext4 defaults,nofail 0 2
# 2. Configuración de Red Segura (Tailscale)
Para evitar abrir puertos en el router y protegernos de ataques externos, usamos Tailscale.
    Consulta realizada correctamente

Gemini ha dicho

Aquí tienes el contenido en texto plano, respetando exactamente tu estructura y estilo para que solo tengas que copiarlo y pegarlo en tu archivo de GitHub (.md).
Markdown

# Guía de Configuración: Del Hardware a la Nube Privada

## 1. Configuración de Discos y Creación del RAID
Para asegurar que los datos del TFG no se pierdan si un disco falla, hemos configurado un sistema de espejo (RAID 1).

### Paso A: Identificación de Hardware
Al conectar el gabinete QNAP TR-002, el sistema reconoce los discos físicos.
* **Comando:** `lsblk`
* **Resultado:** Identificamos `/dev/sdb` y `/dev/sdc` como los discos de 4TB.

### Paso B: Creación del RAID 1
Utilizamos el modo de hardware del QNAP para que el sistema gestione los discos automáticamente.

### Paso C: Formateo y Montaje Persistente

### 1. Formateo
Se dio formato **EXT4** por su estabilidad en Linux

sudo mkfs.ext4 /dev/sdb1

## 2. Obtener UUID

Fundamental para que el montaje no falle nunca si cambian los identificadores de dispositivo.
Bash

lsblk -f

## 3. Implementación de la línea de montaje persistente

Editamos el archivo /etc/fstab añadiendo la siguiente configuración:
Plaintext

UUID=tu-uuid-aqui /mnt/TFG_CRIMSA ext4 defaults,nofail 0 2

## 2. Configuración de Red Segura (Tailscale)

Para evitar abrir puertos en el router y protegernos de ataques externos, usamos Tailscale.
Pasos:

    Instalación:

Bash

curl -fsSL [https://tailscale.com/install.sh](https://tailscale.com/install.sh) | sh

    Vinculación: Ejecutamos sudo tailscale up y autorizamos con nuestra cuenta.

    Verificación: El NUC recibe una IP privada (ej. 100.107.xx.xx) que solo es accesible desde mis dispositivos autorizados.

    Seguridad Extra: El tráfico viaja cifrado de punto a punto mediante el protocolo WireGuard.

## 3. Configuración de Samba sobre la VPN

Samba permite que el disco duro del NUC aparezca como una unidad de red local en Windows (Unidad Z:), pero configurado para ser invisible fuera de Tailscale.
Pasos en /etc/samba/smb.conf:

    Restringir interfaces: Obligamos a Samba a escuchar solo en Tailscale.

Ini, TOML

interfaces = lo tailscale0
bind interfaces only = yes

# 2. Seguridad y monitoreo
Decidimos crear un sistema de monitoreo en bash script para registrar cuando un dispositivo entra al servidor, guardando tanto la IP 
## 3.4. Sistema de Alerta y Auditoría en Tiempo Real (Bot de Telegram)

Para reforzar la seguridad, especialmente al trabajar desde equipos públicos en el centro educativo, se ha implementado un sistema de notificación reactiva. Cada vez que se establece una conexión SSH, el servidor ejecuta un script que informa al administrador a través de un Bot de Telegram y registra la actividad en un log persistent

### A. Configuración del Bot de Telegram (Crimsa_Sentinel_Bot)
Se utilizó la API de Telegram para crear un agente de monitorización. Este proceso permite recibir alertas instantáneas en dispositivos móviles sin necesidad de consultar manualmente los logs del sistema

1. **Creación:** Mediante `@BotFather`, se generó un token API único para la autenticación del servidor.
2. **Identificación:** Se obtuvo el `Chat ID` del administrador para asegurar que las alertas sean privadas y dirigidas

### B. Script de Automatización de Auditoría
El script se ubica en `/home/gerard/scripts/notificar_ssh.sh` y ha sido diseñado para ser ligero y no bloquear el inicio de sesión del usuario

#!/bin/bash

## Configuración de credenciales y rutas
TOKEN="xxxxxxxxxxxxxxxxxxx"
ID_CHAT="xxxxxxxxxx"
LOG_FILE="/mnt/TFG_CRIMSA/SISTEMA/LOGS/historial_conexiones.log"

## Recolección de variables de entorno y sistema
AHORA=$(date "+%Y-%m-%d %H:%M:%S")
USUARIO=$(whoami)
IP_REMOTA=$(echo $SSH_CONNECTION | awk '{print $1}')
[ -z "$IP_REMOTA" ] && IP_REMOTA="Local"

## Cálculo de estado del almacenamiento (DAS QNAP)
ESPACIO=$(df -h /mnt/TFG_CRIMSA | awk 'NR==2 {print $5}')

## 1. Registro en Log persistente (Una línea por acceso)
printf "%-20s | %-10s | %-15s | DAS: %-5s\n" "$AHORA" "$USUARIO" "$IP_REMOTA" "$ESPACIO" >> $LOG_FILE

## 2. Envío de notificación push vía Telegram
MENSAJE=" *Crimsa Sentinel: Acceso Detectado* 
------------------------------------
 *Usuario:* $USUARIO
 *Desde IP:* $IP_REMOTA
 *Storage DAS:* $ESPACIO
 *Fecha:* $AHORA"

curl -s -X POST "[https://api.telegram.org/bot$TOKEN/sendMessage](https://api.telegram.org/bot$TOKEN/sendMessage)" \
     -d "chat_id=$ID_CHAT" \
     -d "text=$MENSAJE" \
     -d "parse_mode=Markdown" > /dev/null

### C. Integración en el Sistema

Para que la auditoría sea ineludible, se vinculó la ejecución del script al entorno del usuario:

    Archivo de configuración: ~/.bashrc (o /etc/profile para todos los usuarios).

    Comando de activación: Se añadió la línea bash /home/gerard/scripts/notificar_ssh.sh & al final del fichero.

    Seguridad de Logs: Se aplicó el atributo de inmutabilidad chattr +a al archivo de log en el DAS, permitiendo únicamente añadir información y prohibiendo el borrado de registros previos.

### D. Verificación de Auditoría

El administrador puede consultar el historial de accesos de forma rápida mediante el alias verlogs, que muestra el contenido formateado del archivo alojado en el QNAP:
Bash

# Ejemplo de salida del log de auditoría
FECHA Y HORA         | USUARIO    | IP ORIGEN       | STORAGE
2026-03-16 16:45:02  | gerard     | 100.107.56.81   | DAS: 45%
2026-03-16 17:10:15  | david      | 100.107.56.81   | DAS: 45%
