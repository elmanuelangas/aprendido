🚀 Prácticas de Laboratorio: Infraestructura, Servidores Web y Cloud Computing
Bienvenido/a a este repositorio. Aquí documento las prácticas realizadas en clase, enfocadas en la administración de redes locales, instalación de servicios web como Apache, y el despliegue de infraestructura en la nube con Microsoft Azure.

💻 Práctica 1: Entorno Local (Localhost) y Servidor Web Apache
📌 Descripción
En esta práctica se trabajó en la configuración de un entorno local y el despliegue de un servidor web utilizando Apache. El objetivo fue comprender el funcionamiento del protocolo HTTP, la resolución de bucles de retorno (loopback en 127.0.0.1), y cómo los servidores web procesan e interpretan archivos HTML para entregar contenido en el navegador.

🖥️ Comandos de Instalación y Gestión (Linux / WSL)# Actualizar el índice de paquetes del sistema
sudo apt update

# Instalación del servidor web Apache2
sudo apt install apache2 -y

# Verificar que el servicio de Apache esté activo y corriendo
sudo systemctl status apache2

# Comprobar la respuesta HTTP desde la terminal local
curl -I http://localhost🔑 Aprendizajes Clave
Instalación y gestión de servicios en segundo plano (daemons) con systemctl.

Verificación de la página por defecto de Apache (Apache2 Ubuntu Default Page) accediendo a http://localhost desde el navegador.

Entendimiento del directorio raíz del servidor (/var/www/html/) para el almacenamiento de sitios web.

☁️ Práctica 2: Máquina Virtual en Azure for Students
📌 Descripción
Aprovisionamiento de una máquina virtual (VM) en la nube mediante Azure for Students, configurando la red virtual (VNet), asignación de IP pública y reglas de seguridad en el Grupo de Seguridad de Red (NSG) para permitir acceso SSH y tráfico HTTP.

🖥️ Comandos de Conexión y Configuración Remota
# Conexión remota SSH a la máquina virtual en Azure
ssh usuario@ip_publica_de_tu_vm

# Instalación de Apache en la VM de Azure
sudo apt update && sudo apt install apache2 -y

# Verificación de conectividad remota HTTP
curl -I http://ip_publica_de_tu_vm
