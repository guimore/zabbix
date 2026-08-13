# 🐳 Zabbix Stack - Monitoreo en Contenedores

## 📌 Descripción del Proyecto
Este repositorio contiene la configuración para desplegar un sistema de monitoreo completo con **Zabbix 7.0** utilizando Docker Compose. El stack incluye:

- **Zabbix Server** (motor principal)
- **Zabbix Web** (interfaz gráfica Nginx + PHP)
- **MySQL 8.0** (base de datos persistente)
- **Zabbix Agent** (monitoreo del propio host)

Todo el sistema está orquestado con un solo archivo `docker-compose.yaml`, diseñado para ser **rápido de desplegar, escalable y fácil de mantener**.

---

## 🧩 Componentes

| Servicio | Imagen | Puerto | Descripción |
|----------|--------|--------|-------------|
| **MySQL** | `mysql:8.0` | `3306` | Base de datos relacional para Zabbix |
| **Zabbix Server** | `zabbix/zabbix-server-mysql:alpine-7.0-latest` | `10051` | Motor principal de monitoreo |
| **Zabbix Web** | `zabbix/zabbix-web-nginx-mysql:alpine-7.0-latest` | `80` | Interfaz web de administración |
| **Zabbix Agent** | `zabbix/zabbix-agent:alpine-7.0-latest` | `10050` | Agente para monitoreo local |

---

## ⚙️ Configuración Destacada

- **Persistencia de Datos:** Los volúmenes `/mnt/mis_datos/zabbix/mysql` y `/mnt/mis_datos/zabbix/data` garantizan que la configuración y los datos históricos sobrevivan a reinicios.
- **Alta Disponibilidad:** Todos los servicios usan `restart: unless-stopped` para auto-recuperarse ante fallos.
- **Seguridad:** La base de datos se inicializa con la variable `log_bin_trust_function_creators=1` para evitar errores comunes de permisos al crear funciones.
- **Zona Horaria:** La interfaz web está configurada para `America/Argentina/Buenos_Aires`.

---

## 🚀 Cómo Levantarlo

```bash
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/zabbix-docker.git
cd zabbix-docker

# 2. Levantar el stack
docker compose up -d

# 3. Acceder a la interfaz web
http://localhost
Usuario: Admin
Contraseña: zabbix
