# 🚀 Infraestructura WordPress Multi-máquina
**Autor:** Héctor Martínez Márquez
**Asignatura:** Virtualización y Cloud 2ºASIR

[cite_start]Este proyecto despliega una arquitectura de WordPress profesional separando el servidor web (Apache+PHP) del servidor de base de datos (MySQL) en dos máquinas virtuales distintas [cite: 8-10].

---

## 🏗️ Estructura del Proyecto
* [cite_start]**`Vagrantfile`**: Orquestación de las dos VMs (`web-server` y `db-server`)[cite: 87].
* [cite_start]**`scripts/`**: Automatización del despliegue[cite: 89]:
    * [cite_start]`common.sh`: Configuración base y resolución de nombres (`/etc/hosts`) [cite: 90, 158-172].
    * [cite_start]`install-db.sh`: Instalación de MySQL 8.0 y configuración de acceso remoto [cite: 92, 176-198].
    * [cite_start]`install-web.sh`: Instalación de Apache, PHP y cliente de MySQL [cite: 91, 200-234].
    * [cite_start]`configure-wordpress.sh`: Configuración automática de `wp-config.php` y salts [cite: 93, 236-296].
* [cite_start]**`config/wordpress.conf`**: Archivo de VirtualHost para Apache [cite: 94-95].

---

## 🛠️ Especificaciones Técnicas
| VM | Hostname | IP Privada | RAM | Software |
| :--- | :--- | :--- | :--- | :--- |
| **Web** | `web-server` | 192.168.56.10 | 1024MB | [cite_start]Apache 2.4, PHP 7.4 [cite: 64-67] |
| **DB** | `db-server` | 192.168.56.20 | 2048MB | [cite_start]MySQL 8.0 [cite: 74-76] |

---

## 🚀 Pasos de Instalación
1. **Clonar el repositorio:** `git clone <tu-url>`
2. [cite_start]**Levantar la infraestructura:** `vagrant up`[cite: 302].
3. [cite_start]**Verificar estado:** `vagrant status`[cite: 303].

---

## 📸 Pruebas de Verificación realizadas
### 1. Conectividad entre máquinas
Desde el servidor web, hacemos ping a la base de datos:
[cite_start]`vagrant ssh web -c "ping -c 3 db-server"`[cite: 306].

### 2. Conexión remota a MySQL
Verificación de acceso desde la web a la DB con el cliente MySQL:
[cite_start]`vagrant ssh web -c "mysql -h 192.168.56.20 -u wp_user -pwp_secure_pass -e 'SHOW DATABASES;'"`[cite: 308].

### 3. Prueba de conexión PHP (PDO)
Comprobación de que PHP puede conectar a la base de datos:
[cite_start]`php -r "new PDO('mysql:host=192.168.56.20;dbname=wordpress_db', 'wp_user', 'wp_secure_pass');"` [cite: 285-290].