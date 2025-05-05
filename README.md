# Stack de Monitoreo con Zabbix, Grafana y Portainer

Este repositorio contiene un archivo `docker-compose.yml` que despliega un stack completo de monitoreo con Zabbix, Grafana y Portainer, utilizando PostgreSQL como base de datos.

## Componentes

- PostgreSQL (base de datos)
- Zabbix Server
- Zabbix Web (interfaz web)
- Zabbix Agent
- Zabbix SNMP Traps
- Grafana (visualización de datos)
- Portainer (gestión de contenedores)

## Requisitos

- Docker + 19.03.0
- Docker Compose + 1.27.0

## Despliegue

Para desplegar todos los servicios:

```bash
docker compose up -d
```
Para comprobar todos los servicios:
```bash
docker compose ps
```

Para detener todos los servicios:

```bash
docker compose down
```

## URLs y Credenciales de Acceso

### PostgreSQL
- **Host**: localhost
- **Puerto**: 5432
- **Base de datos**: zabbix
- **Usuario**: zabbix
- **Contraseña**: zabbix
- **Conexión**: `psql -h localhost -U zabbix -d zabbix`

### Zabbix Web UI
- **URL**: [http://localhost:8085](http://localhost:8085)
- **Usuario**: Admin
- **Contraseña**: zabbix

### Portainer
- **URL**: [http://localhost:9000](http://localhost:9000)
- **Credenciales**: Se configuran en el primer acceso

### Grafana
- **URL**: [http://localhost:3000](http://localhost:3000)
- **Usuario**: admin
- **Contraseña**: admin

### Zabbix Server
- **Puerto**: 10051 (para comunicación con agentes)
- No tiene interfaz de usuario directa, se gestiona a través de Zabbix Web

### Zabbix Agent
- Se conecta automáticamente al servidor Zabbix
- Se configura a través de la interfaz web de Zabbix

### Zabbix SNMP Traps
- **Puerto**: 162/UDP
- Se configura a través de la interfaz web de Zabbix

## Verificación de Servicios

Para comprobar el estado de los servicios:

```bash
# Ver todos los contenedores en ejecución
docker ps

# Ver los servicios específicos del docker-compose
docker-compose ps

# Ver logs de un servicio específico
docker-compose logs -f nombre_servicio
```

## Volúmenes de Datos

Los datos se almacenan en volúmenes de Docker para persistencia:

- `postgres-data`: Datos de PostgreSQL
- `zabbix-server-data`: Datos del servidor Zabbix
- `portainer-data`: Datos de configuración de Portainer
- `grafana-data`: Datos y configuraciones de Grafana

## Red

Todos los servicios están conectados a una red Docker llamada `zabbix-net`, lo que permite la comunicación entre ellos usando sus nombres de servicio como nombres de host.

## Seguridad

**⚠️ Importante**: Las contraseñas incluidas en este archivo son predeterminadas y deben cambiarse antes de cualquier uso en producción.

Recomendaciones de seguridad:
- Cambiar todas las contraseñas predeterminadas
- Utilizar Docker secrets para credenciales en entornos de producción
- Configurar HTTPS para las interfaces web
- Limitar el acceso a los puertos mediante reglas de firewall
