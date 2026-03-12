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
