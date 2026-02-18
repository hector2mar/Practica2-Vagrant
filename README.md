# 🚀 Infraestructura WordPress Multi-máquina
**Autor:** Héctor Martínez Márquez 
**Asignatura:** Virtualización y Cloud 2ºASIR

Este proyecto despliega una arquitectura de WordPress profesional separando el servidor web (Apache+PHP) del servidor de base de datos (MySQL) en dos máquinas virtuales distintas comunicadas por una red privada.

---

## 🏗️ Estructura del Proyecto
El repositorio está organizado de forma modular para cumplir con los estándares de infraestructura como código (IaC):

* **`Vagrantfile`**: Orquestación de las máquinas `web-server` y `db-server`.
* **`scripts/`**: Automatización del despliegue:
    * `common.sh`: Configuración base y resolución de nombres mediante `/etc/hosts`.
    * `install-db.sh`: Instalación de MySQL 8.0 y apertura de acceso remoto.
    * `install-web.sh`: Instalación de Apache, PHP y herramientas de cliente.
    * `configure-wordpress.sh`: Configuración dinámica de credenciales y llaves de seguridad.
* **`config/`**: Contiene el archivo `wordpress.conf` para la gestión del VirtualHost.

---

## 🛠️ Especificaciones Técnicas
| VM | Hostname | IP Privada | RAM | Software |
| :--- | :--- | :--- | :--- | :--- |
| **Web** | `web-server` | 192.168.56.10 | 1024 MB | Apache 2.4 + PHP 7.4 |
| **DB** | `db-server` | 192.168.56.20 | 2048 MB | MySQL 8.0 |

---
## 🚀 Pasos de Instalación
1. **Clonar el repositorio:** `git clone <tu-url>`
2. **Levantar la infraestructura:** `vagrant up`.
3. **Verificar estado:** `vagrant status`.

---

## 📸 Pruebas de Verificación realizadas
### 1. Conectividad entre máquinas
Desde el servidor web, hacemos ping a la base de datos:
`vagrant ssh web -c "ping -c 3 db-server"`.

### 2. Conexión remota a MySQL
Verificación de acceso desde la web a la DB con el cliente MySQL:
`vagrant ssh web -c "mysql -h 192.168.56.20 -u wp_user -pwp_secure_pass -e 'SHOW DATABASES;'"`.

### 3. Prueba de conexión PHP (PDO)
Comprobación de que PHP puede conectar a la base de datos:
`php -r "new PDO('mysql:host=192.168.56.20;dbname=wordpress_db', 'wp_user', 'wp_secure_pass');"`.

### 🌐 4. Interfaz de WordPress
Captura que muestra el acceso exitoso al asistente de configuración de WordPress a través del puerto mapeado (8080), confirmando que Apache, PHP y la conexión a MySQL funcionan en armonía.

![WordPress Funcionando](capturas/wordpress.admin.png)